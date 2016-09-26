---
nav_sort: 6
src: /Getting Started/Creating a Virtual Good/README.md
---

# Creating a Virtual Good

## Introduction

In the context of the GameSparks platform, a Virtual Good is any in-game asset that can be awarded, accumulated, or bought. This would cover XP points and in-game currencies as well as specific goods that deliver benefits in-game (such as convenience, customization, competitive advantage, and so on). These can be used and consumed cross-platform:
* You can set up Virtual Goods to be bought as In-App Purchases (IAPs). This is when you associate the Virtual Goods with the Product IDs of the corresponding items on the stores and when a good is purchased we can reconcile the store receipts with the items.
* You can define relationships between your Virtual Goods so they can be traded or converted.

There are many ways of awarding Virtual Goods. In this tutorial, we'll award the player with a Virtual Good by "purchasing" it, this is done via [BuyVirtualGoodsRequest](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md).

## Setting Up a Virtual Good

*1.* First, navigate to *Configurator > Virtual Goods*.

*2.* Click the plus ![](/img/fa/plus.png) icon. The *Create Virtual Good* dialog appears:

![](img/Create/5.png)

*3.* Next, add the details of the new Virtual Good:

  * *Short Code* - This mandatory field is the reference by which we'll award the Virtual Good. *Short Codes* are always unique.
  * *Name* - This mandatory field is used when listing Virtual Goods in all of the Returns.
  * *Description* - This mandatory field is used to display what the Virtual Good is used for - use it for your own benefit to keep track of the Virtual Goods in a game.
  * *Currency 1* - This is the amount of Currency 1 that is required to "purchase" this Virtual Good.

You can leave the other configuration options as default.

<q>**Other Configuration Options?** For more details on the configuration options for Virtual Goods, click [here](/Documentation/Configurator/Virtual Goods.md).</q>


## Purchasing the Virtual Good in the Test Harness

Now everything is set up, you'll need to navigate to the Test Harness and authenticate with one of the players you have [registered](/Getting Started/Using Authentication/README.md) previously. The [previous](/Getting Started/Creating an Achievement/README.md) tutorial showed you how to award your player with some currency via an Achievement. Now you are ready to purchase your first Virtual Good.

*1.* To start, and just to be sure, let's validate that the player has enough of Currency *1* to purchase the Virtual Good using the [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md).

![](img/Create/7.png)


*2.* To get the Virtual Good, navigate to the Store and then submit a [BuyVirtualGoodsRequest](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md). To do this you will have to fill in JSON builder with the following values and click the Play ![](/img/fa/play.png) icon:

  * *currencyType* - This is the currency you're "paying" with, here it's *1*.
  * *quantity* - This is the quantity of the given Virtual Good that you wish to purchase, here it's *1*.
  * *shortCode* - The Short Code of your Virtual Good you'll be using in this request, here it's *"Gold_Coin"*.

Receiving a successful *BuyVirtualGoodsResponse* is a good indication everything has succeeded. However, you should still validate this by doing an [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md). You should see that the Currency 1 has decreased by 1 and that you've been awarded with 1 Gold Coin.

![](img/Create/8.png)

![](img/Create/9.png)
 

## SDK Instructions

* [Unity](/Getting Started/Creating a Virtual Good/Unity Virtual Goods.md)
* [Unreal](/Getting Started/Creating a Virtual Good/Unreal Virtual Goods.md)
* [ActionScript](/Getting Started/Creating a Virtual Good/ActionScript Virtual Goods.md)
