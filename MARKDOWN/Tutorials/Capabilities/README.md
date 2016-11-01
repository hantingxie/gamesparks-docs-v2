---
nav_sort: 3
src: /Tutorials/Capabilities/README.md
---

# Capabilities and User Permissions

As a game Owner or Admin, you may wish to set specific read/write permissions for a particular user for different areas of the Portal. You might want a user of your game:
* To be able to edit and make changes to Events and Leaderboards configurations.
* To able to view the configuration of Virtual Goods and Achievements but not be able to edit them.
* To be prevented from either editing or viewing the Integrations and Downloadables sections.

You can quickly set up this sort of mixed permissions for users as a specific set of capabilities.

## Collaborators and Group Permissions

Previously, when adding Collaborators to a game, we had just 2 types of permissions available - an Administrator and a Read-Only user, which are called *gameAdmin* and *readOnly* permissions respectively. These were not configurable to the finer granularity that we allow today.

<q>**Don't Modify!** We recommend that *you don't modify* the permissions on the *gameAdmin* and *readOnly* default Groups (which can now be found in *Groups*), because their visibility should serve only as an intuitive template for how to configure your own Group permissions.</q>

You can now set up the read/write permissions for Collaborators on your game with a high degree of precision:
* Create a Collaborator Group.
* Edit the Group to define the read/write permissions for the Group.
* Assign Collaborators to that permissions Group.

## Creating Group Permissions and Assigning to Collaborators

By default on any game, the *gameAdmin* and *readOnly* Groups are displayed. The game author and owner will always have full read/write access to everything in the Portal, regardless of how the settings are changed for other game Admins. You can modify the *gameAdmin* and *readOnly* permissions Groups, but we strongly recommend that *you do not change* these default Groups. Instead, create your own custom Groups to impose the required access permissions on your Collaborators.

*1.* To create a new Group, go to your *Game Overview* page.

*2.* Under *User Management* select the *Groups* tab and click *Add Group*:

![](img/12.png)

The *Add Group* page appears.

*3.* Enter a *Name* and *Description* for the new Group and enable *Read* and *Write* permissions for each capability in the portal, as required:

![](img/13.png)

You can expand headings in the *Permission* list to achieve precisely the granularity of *Read/Write* access you want for *Collaborators* that are assigned to this new *Group*:
* Here, for example, although users will have *Read* access for all functions under *Configurator*, they are restricted to only five areas where they will have *Write* access: *Events*, *Leaderboards*, *Running Totals*, *Cloud Code*, and *Teams*.

*4.* Click to *Save* the new *Group*. It is added in the list on the *Groups* tab:

![](img/14.png)

*5.* Select the *Collaborators* tab and click to *Add Collaborator*:

![](img/15.png)

The *Add Collaborator* page appears.

*6.* Enter an *Email* for the new Collaborator.

<q>**Email is Unique Identifier!** Note that this will be used in the platform as the unique identifier for the Collaborator. This means that if you want to add a Collaborator who will acquire the permissions you have configured under more than one *Group*, you must add them once and assign them to those multiple *Groups*. You can't add them more than once using the same Email and each time add them to a different Group.</q>

*7.* To assign the new Collaborator to one or more permission Groups, select these from the *Groups* drop-down and click to *Save* the new Collaborator:

![](img/16.png)

In this example, the new *Collaborator* is assigned the newly-configured *Restricted* Group permissions.

*8.* Click to *Save* the new Collaborator. The new Collaborator is added under *User Management* on the *Game Overview* page:

![](img/17.png)

<q>**Editing a Collaborator?** If you click to edit the details of a Collaborator after you have added them to your game, you'll be able to change the permission Groups to which they are assigned but you won't be able to edit their Email. This is because the Email is used as the *unique identifier* for the Collaborator and therefore the field is protected and is read-only. To change a Collaborator's Email, you must delete the Collaborator and add them again.</q>

*9.* Log in as the *Collaborator* and navigate to the game. Based on the Capabilities set which is defined by the *Restricted* Group permissions, a Collaborator will be able to view certain things but not edit them. Given the Read/Write permissions configured for this Group, the Collaborator will be able to both view and edit game *Team Types*:

![](img/18.png)

But the Collaborator will only be able to view and not edit the game's *Virtual Goods*:
* Fields will be grayed-out.
* If a *Save* is attempted, it will be blocked.

![](img/19.png)
