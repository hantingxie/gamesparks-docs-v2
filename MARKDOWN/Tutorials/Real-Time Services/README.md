---
nav_sort: 9
no_toc: true
no_comment: true
src: /Tutorials/Real-Time Services/README.md
---

# Real-Time Services

## Introduction

Welcome to our series of tutorials on GameSparks Real-Time services SDK. These tutorials give you an introduction to our Real-Time SDK, how it works, and provide an example on how our Real-Time might be implemented in a multiplayer game.


## What Are Real-Time Services?

Our real-time services provide a network communication layer which has the ability to send and receive data in real-time:

* **Designed for Multiplayer Contexts.** Our real-time services are intended for use in multiplayer networked games where player and game-data should be sent and received as quickly as possible.

* **Host Server Support for Player vs. Player (PvP) Model.** We use a PvP model for our network programming. However, we use a host server to relay communications between players. This brings significant benefits:
  * Allows our services to support a higher number of players than traditional PvP models.
  * Gives you the option to host games in the regions of your choice to reduce latency issues.

* **Lightweight and Flexible SDK.** Our real-time SDK is very lightweight, giving the developer tight control over what is sent and received:
  * You have wide flexibility on what data you send and how you wish to send the data.
  * You can keep the packets as small as possible making transmission much more efficient.

## Tutorials

* [Understanding GameSparks Real-Time](/Tutorials/Real-Time Services/Understanding GameSparks Real-Time.md) - Introductory overview of working with GameSparks Real-Time.
* [Creating and Using Real-Time Scripts](/Tutorials/Real-Time Services/Creating and Using Real-Time Scripts.md) - Setting up a real-time script and understanding the functions available through the RTSession API.

* [Setting Up Real-Time Matchmaking](/Tutorials/Real-Time Services/Setting Up Real-Time Matchmaking.md) - Integrating the real-time SDK into an existing GameSparks project in Unity3D and setting up a new real-time match through your game’s portal.

* [Real-Time Matchmaking & Player Lobby](/Tutorials/Real-Time Services/Real-Time Matchmaking.md) - Using the GameSparks matchmaking services to match players of a certain skill level.

* [Real-Time Chat Services](/Tutorials/Real-Time Services/Implementing Real-Time Chat Services.md) - Once a real-time session has started from the match set up in the lobby, how to start sending and receiving packets to build a real-time chat service.

* [Multiplayer Game Example](/Tutorials/Real-Time Services/Real-Time Game Example.md) - To demonstrate the real-time services, this tutorial shows you how to create a very simple multiplayer game. This example will have networked objects moving around, firing projectiles, and sending and receiving information between each player to update each other’s game-objects.

* [Clock Synchronization and Network Programming](/Tutorials/Real-Time Services/Clock Synchronization and Network Programming.md) - This tutorial explores further key concepts in multiplayer network programming, such as clock-synchronization and packet analytics.

* [Calling Log Event Requests in RT Scripts](/Tutorials/Real-Time Services/Calling Log Event Requests in RT Scripts.md) - This tutorial explains how to call Log Event Requests in your Real-Time scripts.

* [Unreal Real-Time Guide](/Tutorials/Real-Time Services/Unreal Real-Time Guide.md) - This tutorial is written for game developers working in Unreal and explains how to get the most out of GameSparks Real-Time services.
