---
nav_sort: 3
src: /Tutorials/Database Access and Cloud Storage/Saving and Loading Player Inventory Data.md
---

# Saving and Loading Data - Player Inventory and Item Management


## Introduction

This tutorial covers the basics of saving and loading data to and from your game using GameSparks custom [LogEventRequests](/API Documentation/Request API/Player/LogEventRequest.md). We'll start off with the basics of how to set up a simple player-inventory system in Cloud Code, and later we'll look at how to create a management screen for your items on GameSparks using dynamic forms.

## Inventory Items

To begin with, we're going to create a collection for all items in the game. This is where we'll keep the list of all items a player can get in the game. These items will have a simple-structure. All we need is an ID, a name (or Short Code), display name and a description.

There's plenty of other attributes these items can have. For example:
* We can use a *type* field to filter specific items for specific areas or stores in your game.
* Or, we can use the *type* field to filter only specific inventory items to be displayed in a store-front - that is weapons, potions, or armour.
* We could add another field which would similarly denote the level of the item, and could be used to only show the user items at their level.

There are plenty of attributes we can add here that could be hooked into your game in various ways.

### Creating a Collection from Scratch

We can create a collection from scratch through the NoSQL explorer. Later on, in another tutorial, we'll go through how to create items using a CMS screen, but let’s save that for when we have everything working.

To do this:

*1.* Go to the NoSQL tab on the portal and click on the plus [+] button on the *Collections* panel.

*2.* We'll create a new *Metadata* collection called *items*:

![](img/PlayerInvent/1.png)

#### Why Metadata Collection?

The reason we want this to be a meta-collection as opposed to a runtime collection is because meta-collections don’t get reset when you publish your game. Runtime-collections, such as the player collection or player inventory are only specific to the game.

The difference is that meta-collections can be moved from preview to live without being reset. That makes them very useful for persistent data like items.
It is also important to note that meta-collections are not editable while the game is live, so they are much safer to use for game-configuration information.

### Inserting New Items

The next thing we are going to do is to create a new item and insert it into our collection. We'll also do this through the NoSQL explorer. The item will have the following structure (below) and you can add or remove fields if you want.

To insert the new item, simply paste the following JSON structure into the text-field on the *Insert* tab for the new *items* collection:

```
{  "shortCode" : "hearthstone",  "name" : "Hearth Stone",  "description" : "Transports the user to their home", "type" : "item" }

```

![](img/PlayerInvent/2.png)

You can add multiple items at once by using a comma between each item-definition and by wrapping them in bracket to create a JSON-array.

![](img/PlayerInvent/3.png)


Now that we have some items defined we can start on our inventory system.

## Get Items

The first thing we are going to is create a new Event, which we'll use for getting a list of our items. We’ll need this first in order to know what items we actually can add to our inventory.

Create a new Event called *getItems* and give it one field - a string called type. We'll use this to filter for items of a specific type.

![](img/PlayerInvent/4.png)

Next, we'll open up the Cloud Code for this Event and start writing some code. What we want this script to do is return all items of the specific *type* we requested. This also means we want to return all items if no *type* was requested. So we'll first check if the *type* was an empty string, and if so, we return everything in that collection:

```
var type = Spark.getData().type; // get the type we passed in
if(type != ""){
    // if the type wasnt an empty string, then we can use the type in our query
    Spark.setScriptData('items', Spark.metaCollection('items').find({ "type" : type })
}else{
    // if the type was an empty string, we can forget the query as we just want to return everything
    Spark.setScriptData('items', Spark.metaCollection('items').find());
}


```

![](img/PlayerInvent/5.png)


Note that you can also exclude certain fields from the response. In this example, we've excluded the ID of the item which we don’t need because it's not useful information for the client and leaving it out reduces the size of the data being sent back.

### Testing

Let’s test this script out in the [Test Harness](/Documentation/Test Harness/README.md). If we call this Event with no *type* set, we should get a full-list of items:

![](img/PlayerInvent/6.png)

But if we only ask for the weapons, we should only get items with the weapon-type:

![](img/PlayerInvent/7.png)

## Add Item

So now that we have a list of item-data being returned from our game, we can give our player the ability to add items to their inventory.

We're going to create a new Event called *addItem*, which will take the item’s Short Code. We'll check to see if that ShortCode exists, and if so, we'll add it to the player’s inventory:

![](img/PlayerInvent/8.png)


There are several ways to create the inventory structure. The way we are going to do this for our example will involve a separate document for each item in the player’s inventory. This method carries several advantages:

* The inventory is easier to query and modify, because we can let MongoDB do what it's designed for.
* Since we are using individual documents instead of an array, we don't have to write code to search, update, and remove items ourselves.
* All of this means that operations on the inventory are more efficient.

The disadvantage of this way of setting up the inventory structure is that there are multiple documents for each player instead of one document per player, so the collection is potentially much larger.

The Cloud Code script for this Event will have the following steps:
1.	Check that the Short Code entered corresponds to a valid item in our items collection.
2.	Construct a player inventory document from that item and the player’s ID (so we can check it later).
3.	Insert the doc into the *player_inventory* runtime collection.

Note that we don’t have to create the *player_inventory* collection as we did with the items collection. It will be created for us as soon as we run our code:

```
var shortCode = Spark.getData().shortCode; // get the shortcode passed into this event
// check that the shortcode is a valid item //
var item = Spark.metaCollection('items').findOne({ "shortCode" : shortCode }, { "_id" : 0 }); // we dont want the _id to be returned so we will exclude it from the returned fields
if(item){
    // item shortcode is valid lets make doc for our player's inventory//
    var newInvItem = { // new inventory item
        "player_id" : Spark.getPlayer().getPlayerId(), // we need the player id to be able to get the player's full inventory later on
        "item" : item
    }
    Spark.runtimeCollection('player_inventory').insert(newInvItem); // insert the new doc
    Spark.setScriptData('item-added', shortCode);

}else{
    // we want to return an error if the wrong code was submitted //
    // so here, we log that an incorrect code was submitted and return an error //
    Spark.getLog().debug("Add Item| Invalid Item ShortCode - "+shortCode);
    Spark.setScriptError('item', 'invalid-item-id');
}


```

![](img/PlayerInvent/9.png)

### Testing

We can test this Event through the [Test Harness](/Documentation/Test Harness/README.md). If we enter a *shortCode* for the [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md), we know that in the response, the *scriptData* field should return the item-added message:

![](img/PlayerInvent/10.png)


We can check to see if our item actually was added by checking to see if our player has a new entry in the *player_inventory* collection through [NoSQL Explorer](/Documentation/NoSQL Explorer.md):

![](img/PlayerInvent/11.png)

Something to note here is that this code does not check if the player already has an item before granting it. This is not difficult to implement, it just means that before we grant the item we query the collection for the *shortCode* and *playerID* and see if there are any records before inserting the new document into the collection.

However, for this tutorial we aren’t worried about that because there's no limit to the number of items a player can have.

## Removing Items

The next thing we want to do is to be able to remove items from our inventory. Our *removeItem* Event is pretty straightforward:
* It will take an item *shortCode* string data type.
* It will also take a number, in case we want to drop more than one of an item (like dumping items from our inventory in bulk).

We're also going to use a default value for the *count* Attribute:
* By setting the default value of *count* to *1* we'll save ourselves having to write an extra piece of code to ensure this field is filled-out.
* Secondly, by setting it to *1* by default, it will always remove 1 item unless otherwise specified:

![](img/PlayerInvent/12.png)

The *removeItem* Cloud Code script will have the following steps:
1.	We'll query the *player_inventory* collection for the number of items requested and we'll use the *player_id* field to make sure we get the items for our player only.
2.	We'll then loop through those items and remove them from the collection. For this we'll use the *\_id* field for each item to remove it.
3.	If there are no items to remove, we'll return a message.

So our first step will take care of validating the *shortCode*, because if the *shortCode* is wrong, we won’t get any items to remove. Therefore, we avoid crashes or removing unwanted items if the *shortCode* were invalid.

```
var shortCode = Spark.getData().shortCode; // get the shortcode passed into this event
var count = Spark.getData().count; // get the amount we want to remove
// we are going to use the limit function to get only the number of items we requested //
// we only care about the _id.$oid so thats all we need to return. We will use that later to remove items //
var itemsToRemove =  Spark.runtimeCollection('player_inventory').find({ 'player_id' : Spark.getPlayer().getPlayerId(), 'item.shortCode' : shortCode }, { "_id": 1 }).limit(count);
var itemsCount = itemsToRemove.count();

if(itemsToRemove.count() > 0){ // check that we actually have items to remove
   while(itemsToRemove.hasNext()){
       // loop through all items and remove them using the remove() function
       Spark.runtimeCollection('player_inventory').remove({ "_id"  : {  "$oid" : itemsToRemove.next()._id.$oid }});
   }
   Spark.setScriptData('items-removed', itemsCount);
   Spark.setScriptData('items-shortCode', shortCode);
}else{
    // we want to log the error and return a message to the player //
    Spark.getLog().debug("Remove Item| Player Has No Items With ShortCode - "+shortCode);
    Spark.setScriptError('no-item-to-remove', shortCode);
}


```

![](img/PlayerInvent/13.png)

### Testing

Before testing this code, you should make sure you have added a bunch of items to your player’s inventory. We need to test two things:
* First, that we can remove multiple items.
* Second, what happens when no items were found:

You can see that the way the code is written that even if I try to remove 3 items, having only two in my inventory, it will not fail, it will only remove the items it can and return the number of items that were removed:

![](img/PlayerInvent/14.png)

However, if I then attempt to remove items, with none left in my inventory, it will get an error. This behavior can be modified if you like, but the basic idea is to catch invalid behaviors the client might cause.

![](img/PlayerInvent/15.png)

### Get Player Inventory

The next thing we need to do is to be able to get the player’s entire inventory.

We'll create a new Event for this called *getPlayerInventory*. This Event will take one field, a string called *type* and, just like the *getItems* Event, *getPlayerInventory* will have the ability to check only specific types of player items:

![](img/PlayerInvent/16.png)

In this example, we’ve used a default value of *all*:
* We did this just to show you how we can use different word to denote these query-fields instead of an empty string.

The *getPlayerInventory* Event is very simple. All we need is to request the *type* of item we want to return and if the player has some of those items in their inventory, then they will be returned. There is no need for any error checks because if they have no items of that type, then an empty array will be returned automatically:

```
var type = Spark.getData().type; // get the type we passed in
if(type != "all"){
    Spark.setScriptData('items', Spark.runtimeCollection('player_inventory').find({ 'player_id' : Spark.getPlayer().getPlayerId(),
                                                                                    'item.type' : type }, { "_id" : 0 }));
}else{
    Spark.setScriptData('items', Spark.runtimeCollection('player_inventory').find({ 'player_id' : Spark.getPlayer().getPlayerId()}, { "_id" : 0 })
}


```

![](img/PlayerInvent/17.png)


### Testing

We can again test this through our [Test Harness](/Documentation/Test Harness/README.md). The player-ID is taken from the logged-in player, so we don’t have to worry about passing this into the Event:

![](img/PlayerInvent/18.png)

## Editing Item Details Using Dynamic Forms

In this section of the tutorial we'll create a management screen where you can list items, update them, and create new ones.

We can do this using Dynamic Forms. Dynamic Forms are very useful in GameSparks for creating your own management screens and they can be used for a variety of things. Dynamic Forms can be a bit complicated so we advise you take a look over how they work. There are tutorials [here](/Tutorials/Analytics. Segmentation and Game Management/README.md) and there is a list of tags you can use through the Dynamic Forms API [here](/API Documentation/Dynamic Forms API.md).

### Creating a Management Screen

The first thing we need is to create a new management screen. To do this:

*1.* Go to the *Manage* tab of your GameSparks portal and click the *Add* button:

![](img/PlayerInvent/19.png)

*2.* In this screen all you need to do is:
* Enter a *Name* and *Short Code*.
* Add a little HTML to set up a placeholder, which will run a Snippet called *items_view* - this is the first Snippet we'll be working on:

![](img/PlayerInvent/20.png)

### Creating Snippets

Next we are going to create the Snippets we need for our *Item Manager* screen. To do this we select the *Snippets* tab and click to *Add* the new Snippets. We'll create three Snippets called: *items_view*, *items_edit*, and *items_delete*:
* There are only two sections we need to worry about in these Snippets, the *JavaScript* window and the *Handlebars* window.


#### Item List

The first Snippet we're going to look at is the *items_view* Snippet. This will list details about the items currently in the collection and will allow us to delete, edit, and add new items.

##### JavaScript Window

In the *JavaScript* window, all we need to do is create a function that will return the list of items in the *items* meta-collection:

```
Spark.setScriptData("form", SnippetProcessor());

function SnippetProcessor(){

    var form = {};
    return view();

    function view(){

        form.itemList = Spark.metaCollection("items").find({}).sort({ "_id" : -1 });
        return form;
    }
}


```

##### Handlebars Window

In the Handlebars window, we'll add some HTML for drawing the list. This HTML will also include:
* A button which will run the *items_edit* Snippet (where we can edit item details).
* For each item there will be an icon which will allow you to edit an item (using the *items_edit* Snippet again) or delete an item using the *items_delete* Snippet.

```
<gs-title-block title="Manage Items" padding="10" margin="0">
    <gs-row>
        <gs-col width="10"><h4>Here you can View, Create, Edit or Delete Items.</h4></gs-col>
        <gs-col width="2">
            <gs-link snippet="items_edit?action=view" target="modal"><button>Create New</button></gs-link>
        </gs-col>
    </gs-row><hr/>
    <gs-row>
            <gs-col width="2"><h5>Item Name</h5></gs-col>
            <gs-col width="2"><h5>ShortCode</h5></gs-col>
            <gs-col width="4"><h5>Description</h5></gs-col>
            <gs-col width="2"><h5>Type</h5></gs-col>
            <gs-col width="1"><h5>[Edit]</h5></gs-col>
            <gs-col width="1"><h5>[Delete]</h5></gs-col>
    </gs-row><hr/>
    <gs-row>
        {{#each form.itemList}}
        <gs-row>
            <gs-col width="2">{{name}}</gs-col>
            <gs-col width="2">{{shortCode}}</gs-col>
            <gs-col width="4">{{description}}</gs-col>
            <gs-col width="2">{{type}}</gs-col>
            <gs-col width="1"><gs-link snippet="items_edit?action=view&itemId={{_id.$oid}}" target="modal-wide"><i data-toggle="tooltip" data-placement="top" title="Edit Item" class="icon-edit"/></gs-link></gs-col>
            <gs-col width="1"><gs-link snippet="items_delete?action=view&itemId={{_id.$oid}}" target="modal-small"><i data-toggle="tooltip" data-placement="top" title="Delete Item" class="icon-trash"/></gs-link></gs-col>
        </gs-row>
        {{/each}}
    </gs-row>
</gs-title-block>


```

![](img/PlayerInvent/21.png)

Now, if you save this Snippet, you'll be able to go back to your *Item Manager* Screen and see the list of items we’ve already created.

![](img/PlayerInvent/22.png)


#### Editing Items

For editing items, we are going to use the *items_edit* Snippet. When we start to get this Snippet working, we'll need to pass some sample data into the Snippet so that we know it's all working correctly.

In the *items_view* Snippet, when we wanted to have this Snippet run, we passed two fields into the Snippet:
* The first was { “action” : “view” }, which is used to tell the Snippet which action we want (later we will pass in { “action” : “save” },  for when we are saving the Snippet).
* However, when we want to edit the Snippet we also want to pass in the ID for the item we want to edit.

So, in order to test this, we want to get the ID for an item that already exists. So you will need to go to the [NoSQL Explorer](/Documentation/NoSQL Explorer.md) and look up an object-ID for one of your existing items.

##### JavaScript Window

This section will have two functions - one for saving and one for drawing the Event data. The way this is set up we won't need any extra code for a new Event or an Event we want to edit. When we are creating a new Event, there'll be no data to display, so the HTML will automatically draw placeholder text instead. We'll then use a MongoDB update method to edit or insert a document automatically if one doesn’t exist.

```
Spark.setScriptData("form", SnippetProcessor(Spark.getData().scriptData))

function SnippetProcessor(data){

    var form = {};

    var action = data.action;

    switch(data.action){
        case "view":
            return view(data);
        case "save":
            return save(data);
    }

    function view(data){

        if(data.itemId != undefined){
            form.item = Spark.metaCollection('items').findOne({  "_id" : { "$oid" : data.itemId } });
        }
        return form;    
    }

    function save(data){

        Spark.metaCollection('items').update(
            {"name" :  data.name }
            {
                $set : { // all the fields we want to update go here
,
                    "shortCode" : data.shortCode,
                    "description" : data.description,
                    "type" : data.type
                }
            },
            true,
            false
            );        
        form.updated = true;

        return form;    
    }
}


```

An important part of the code above is the *form.updated* field in the *save* function. This is going to be used in the HTML code to tell the Snippet that it should close the window when the user has hit the *Save* button.

##### Handlebars Window

This part is pretty straightforward. It has 3 parts:
1.	Check if the *updated* field is present and if so, we close the window
2.	The main body of the window will contain fields we can edit. These will be wrapped in a form so that when we click on the *Save* button at the bottom, it saves all fields back to the Snippet, but this time with the ‘view’ action.
3.	The last part is the body of the form which in this case is just text fields for Name, Short Code, Description, and Type.

```
{{#if form.updated}}
    <gs-modal-close></gs-modal-close>
    <gs-snippet snippet="items_view"></gs-snippet>  
{{else}}
<gs-row>
    <gs-title-block title={{#if form.items}}"Edit Item"{{else}}"Create New Item"{{/if}} padding="10" margin="0">
<input type="hidden" name='itemId' value="{{form.item._id.$oid}}"/>
            <gs-row>
                <gs-col width="6"><h5>Name</h5></gs-col>
                <gs-col width="6"><h5>Short Code</h5></gs-col>
            </gs-row>
            <gs-row>
                <gs-col width="6"><input type='text' placeholder="Item Name..." name='name' value="{{form.item.name}}"/></gs-col>
                <gs-col width="6"><input type='text' placeholder="Item ShortCode..." name='shortCode' value="{{form.item.shortCode}}"/></gs-col>
            </gs-row>
            <gs-row>
                <gs-col width="12">Description<br/>
                    <input type="text" name="description" value="{{form.item.description}}" required />
                </gs-col>
            </gs-row>
            <gs-row>
                <gs-col width="3"></gs-col>
                    <gs-col width="6">Type<br/>
                        <input type="text" name="type" value="{{form.item.type}}" required />
                    </gs-col>
                <gs-col width="3"></gs-col>
            </gs-row>
            <gs-row>
                <gs-col><gs-submit>Save</gs-submit></gs-col>
            </gs-row>
        </gs-form>
    </gs-title-block>
</gs-row>
{{/if}}


```

![](img/PlayerInvent/23.png)

When you save this, you should be able to go back to your *Item Manager* Screen (make sure to reload the page so the new code is updated) and you should be able to create new items and edit old ones:

![](img/PlayerInvent/24.png)

#### Deleting Items

Deleting items works in a similar way to how we edited items. This Snippet will:
* First draw a simple window showing the ID of the item you want to delete and it will include a button to delete it.
* When the user presses the button, we'll send the ID back to the Snippet but this time it will remove the item from the collection and return the *updated* bool so we know to close the window.

##### JavaScript Section


The two functions we have here will be *view* and *deletion*. We'll use the MongoDB *findAndRemove* function to delete the item.

```
Spark.setScriptData("form", SnippetProcessor(Spark.getData().scriptData))

function SnippetProcessor(data){

    var form = {};

    switch(data.action){
        case "view":
            return view(data);
        case "delete":
            deletion(data);
            return view(data);
    }

    function view(data){

        form.itemId = data.itemId;
        return form;
    }

    function deletion(data){

        Spark.metaCollection('items').findAndRemove({"_id" : {"$oid" : data.itemId }});
        form.updated = true;
    }
}    


```

##### Handlebars Section

This code is also very simple - we just want to draw a title for the window containing the item’s ID and we'll have a button which will send the item’s ID back to the Snippet when clicked:

```
{{#if form.updated}}
    <gs-modal-close></gs-modal-close>
    <gs-snippet snippet="items_view"></gs-snippet>
{{else}}
    <gs-row>
        <gs-title-block title="Delete Items - {{form.itemId}}" padding="5" margin="0">
            <gs-row>
                <gs-col>
                    <h4>Delete Items with the ID: {{form.itemId}}?</h4>
                </gs-col>
            </gs-row>
            <gs-row>
                <gs-col><gs-link snippet="items_delete?action=delete&itemId={{form.itemId}}" target="items_ph"><button>Delete</button></gs-link></gs-col>
            </gs-row>
        </gs-title-block>
    </gs-row>
{{/if}}


```

![](img/PlayerInvent/25.png)


## Summary

By following this tutorial you'll be able to create requests for updating and removing player inventory items as well as getting a list of available items and the player’s current inventory. We also covered building a simple Item Manager screen where you can create and edit items available to your player.

This was a very simple example. There is much more you could add for your own games - for example:
* Adding new fields to the Item Manager screen would allow you to define statistics for your items such as health, damage, and so on.
* You could also incorporate item-uses into your request so that items can be used and exhausted as players use them.
* Another option could be to add prices to the items so that players could purchase items before they are added to their inventory. In this case, you could use [SparkPlayer.debit](API Documentation/Cloud Code API/Player/SparkPlayer.md) to debit the player the price of the item you have set instead of using the built-in Virtual Goods.

There are many ways to customize this sort of Player Inventory use case to suit your own needs so please let us know if we can help!
