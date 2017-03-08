---
nav_sort: 2
src: /Tutorials/Real-Time Services/Real-Time Best Practices.md
---
# Real-Time Best Practices

## Limitations

On  | Limit
-----  | -----------
Packet Size    | 1400 bytes

## Recommended Bandwidth Usage and Maximum Players

For optimal performance and best player experience, we recommend the following standard-level usage of the platform for bandwidth and maximum player numbers in your networked games:

Device Type | Bandwidth (kilobytes per second) | Maximum Players per Match
-----  | ----------- | -----------
Console or Desktop | 19 kbps | Approximately 60
Mobile | 2 kbps | 15 to 20

### Balancing Frequency of Updates against Available Bandwidth

When implementing Real-Time games it's important to balance game-state updates per second against available bandwidth - although frequent updates will give your players a smoother gaming experience, this can quickly eat into available bandwidth. This issue is especially relevant for Real-Time games played on mobile devices, where around 4 to 6 updates per second is a safe baseline frequency to work with.

## Performance Tips

There are several important factors that affect the performance of networked multiplayer games. Some of these you don’t have a lot of control over, such as latency and quality of service your player’s ISP delivers. However, there are plenty of ways to incorporate network design principles to improve performance and keep your network design simple.

### Tick Rate

With GameSparks you can implement Real-Time scripts which allows the server to control the flow of packets in your game and to run code on data contained in those packets. Doing this allows you to control when the server broadcasts updates to players. This is an example of a *server-authoritative model* where each client sends updates to the server. The server then sends back details of the entire game-state at scheduled regular intervals. This interval is called the tick-rate.

Tick-rate reduces the traffic from the server to the client by not requiring the server to immediately respond to each packet from each client. It also reduces the processing done by the server because processing can be done in a regular loop instead of having to process each packet as it arrives.

Typically, the tick-rate is kept as low as possible while delivering the best networking experience to your players (around 10 times per second or every 100ms).

### Client-Side Prediction

It's not efficient to send updates about object positions each frame because you would update your game on the client. Therefore, in order to show objects moving smoothly and regularly throughout in each player’s game, you instead broadcast position updates at regular intervals.

As the client waits for the next position update from the server it is moving the object to the last known position it got from the server. This way you can overcome jitter or warping due to loss of data packets or low bandwidth.

### Packet Size, Packet Frequency, and when to Send Packets

The golden rule for creating the best networking experience for your players is to send the minimal amount of data as infrequently as possible!

#### Packet Size

You are limited to 1400 bytes per packet, which is a typical maximum transmission unit (MTU) size for most networks. It's generally advisable to keep your packets as small as possible because small packets have a faster transmission time. However, there is some trade-off to consider when thinking about the frequency you are sending your packets.

#### Packet Frequency

Sending packets comes with an overhead for processing and sending each packet. Therefore, keeping your packets small is not a cure-all if it means you need to send packets more frequently. There's also an issue of packets being dropped and the game needing to wait for the next frame in order to catch up:

* Although larger packets take longer to transmit, there is more data included and therefore they can be a more efficient way of sending data because the overhead is reduced.

* One approach is to buffer the data you want to send instead of sending it each time an Event takes place. This will lower the bandwidth demand for your game.

#### To Send or not to Send

Another thing to consider is what you actually need to send in each packet:
* A position update for example generally has no need to send regular updates or updates every frame. Very often during gameplay objects are not moving or are moving to a predictable position or in a specific direction. Consider this when designing your network code to make sure data is only sent when necessary.

* Similarly, if you want to send Event-based packets such as on button-presses, there is no need to send updates while the button is pressed but only when the button is first pressed and then again when released - let your client-side code figure out what is happening in-between.

* Another example is if you are firing a gun and need to update shells or bullets, you don’t need to send an update for each bullet. Instead, send a message to say a bullet should be created, and then predict the trajectory. Each time the bullet hits an object or needs to change direction, send an update to all players.

<q>**Important!** You should never attempt to send packets every frame of your update loop!</q>

### Protocol Choice - UDP vs. TCP

GameSparks allows you to choose how you want to send packets via the network. You can choose either TCP (reliable) or UDP (unreliable). Each of these protocols has their advantage so it's important to explain both.

#### TCP

TCP is a reliable connection protocol. It works by creating a connection between two computers and then uses that connection to send data to and from each computer. The connection is reliable and the protocol ensures that packets arrive in the order you sent them.

#### UDP

UDP is much simpler than TCP. Instead of establishing a connection between two computers we pick an IP address we want to send data to and a port on that computer. The recipient then listens for data coming into that port. The data is transmitted from machine-to-machine until it arrives at the destination.

However, the data does not always arrive. There's some (small) packet loss when sending data via UDP. There's also no guarantee your packets will arrive in order. In general, packets do arrive and in order, but because there's always a chance of loss or packets arriving in the wrong order, this protocol is unreliable.

#### Which Protocol to Use?

The obvious choice by comparison is to use TCP to send data. However, in networked games it's often UDP which is the better choice:
* TCP requires a certain amount of data to be buffered before it will send. This means that if you have many small packets to send, there will be a delay in sending the packet instead of sending it exactly when you want.
* Another problem with TCP is that when a packet is dropped, the recipient has to send a message back to the sender requesting the packet again, and wait for it to come back. Think of this flaw when trying to synchronize all your players. If a packet is dropped somewhere, everyone has to wait while the lost packet is resent. Any updates that come from the server between those times could be unreliable.

#### Or Both?

We’ve explained the advantages/disadvantages of UDP and TCP but because GameSparks allows you to choose either of these protocols, there's the option of using both. Consider whether you need reliability and order over speed or you need speed over reliability.

GameSparks also allows you send another kind of packet - *unreliable-sequenced*. This has the advantages of UDP packets, but it will drop packets that come in late. Therefore, you always get the most recent positions (for example) and you don’t have to worry about the server receiving a new packet containing an old position update.

### Latency

Latency has the greatest effect on player experience in a networked game:

* Latency is a measure of the time it takes for a packet to be sent to the server.

There are a lot of things that affect latency, but the main factor is how far away you are from the server. Consider this when you are matching players and try to group them into local regions.

### Measure and Make Changes

The quality of your player’s gameplay experience is paramount. Therefore, overall, it's important to carefully monitor your network performance and make tweaks where you can to improve it.

This would include, among other things, making changes to:
* Packet transmission frequency.
* Average packet size.
* Server tick-rate.
* Maximum number of players connected.

You might find you need to make compromises in certain areas and strike a balance between these in order to deliver the best experience.

<q>**Recommended Usage?** Please review the recommended standard usage for bandwidth usage and maximum players at the [top of this page](#Recommended Bandwidth Usage and Maximum Players).</q>

## Game Tips

Apart from general performance tips, there are also networking design tips that will help you manage your game and make it easier to design.

### Server-Side Validation

One model for networked games is to have the server handle all game-logic and transmit updates about the entire game-state back to all players. This is a *server-authoritative* model. Generally, a mixture of server-authoritative and client-side prediction is best, so that:
* The server is not in charge of everything that takes place in the game.
* The client can react to player input without delay.

However, server-validation is also very useful. This allows the server to validate or approve updates that come from the client:
* This might involve keeping a buffer of previous positions for objects and making sure the new position is valid - that is, the player is not cheating or an object has hit a trigger.
* This process can also be used to correct for dropped packets or for any other anti-cheating mechanisms you might want to implement in your game.

### Collision Detection

Collision detection is something that takes some consideration in how you design your networking architecture. The main concern is who decides when a collision has occurred. There are several ways to deal with this, but it generally relates back to ‘fairness’ (and also the latency of your players).

* For example, if player A hits player B during one update, player B might not see that they have been hit during their own update (since latency can cause a delay between updates for each player’s version of the game).

In this case, who registers the collision and send the acknowledgement to the server for validation? The decision is ultimately up to you, but in general it is best take side of fairness. If player 2 gets hit in their game, it should be up to them to register the hit on the server because it guarantees they will have noticed it and won’t feel cheated or that there was a bug.

There are many techniques to deal with cases like this and they mostly come down to game-design, rather than network design. There is an excellent GDC talk by Bungie available [here](http://www.gdcvault.com/play/1014345/I-Shot-You-First-Networking), which discusses how game-design can overcome these kinds of situations.

## Logs

In order to know that your networking is performing efficiently and optimally, you need to keep track of every packet sent back and forth for your game.

Packets should be logged by timestamp and the number of bytes sent and received. Check out the tutorial [here](/Tutorials/Real-Time Services/Clock Synchronization and Network Programming.md) on clock synchronization to see how you can get these data. You can also cache data as they come in to get average readings per second, which is very useful because UDP packet transmission times can vary.

Accompanying these data with details about the category of packet you are sending (such as game-state updates, position updates, collision updates, and so on) will give you a lot of information you can use to monitor your network for problems and see the results of any tweaking you do to improve network performance.

Remember that it's also important that your logs don’t cause performance issues themselves and potentially contaminate the network data, so be careful about how you use logs and how they are saved.
