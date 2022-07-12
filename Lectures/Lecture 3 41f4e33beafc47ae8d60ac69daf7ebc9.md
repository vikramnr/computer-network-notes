# Lecture 3

## What the Internet is - The IP Service

### IP

- When transport layer has data to send it hands the transport segement to Network layer
- IP layers creates new datagrams and put the transport segement
- IP’s job is to delivery the datagram to the other end, so it sends the data over to link layer

![Untitled](Lecture%203%2041f4e33beafc47ae8d60ac69daf7ebc9/Untitled.png)

- IP model can be characterized by four properties below

| Property | Behavior |
| --- | --- |
| Datagram | Individually routed packets. Hop by hop routing |
| Unreliable | Packets might be dropped |
| Best effort | but only if necessary |
| Connectionless | No per-flow state. Packets might be mis-sequenced. |
- Datagram
    - Self contained - routes the packet created by the information from the header
    - Header containes IP address for destination and source.
    - Hop By Hop - and hop to another router decision is made based on destionation address
    - Routers have forwarding tables which tell where to send the packet when it matches given destination address
    - Router doesn’t know the whole path, but it indexes based on destination table so that it can forward it to next hop towards the final destionation
- Unreliable
    - packets might not be deliveried at all,  or duplicated or get lost due router errors
    - makes no guarantees
- Best effort
    - Packet drops won’t happen just because it feels like it
    - Only drops the packet only if necessary. For example due to packet congestion, next arriving packet will get dropped or due false routing table
    - IP does **promise to only make errors when necessary.**
- Connectionless
    - simple & minimal
    - it doens’t maintain any connection with the destionation
    - no state at all related to communication
    - routes all datagrams individually and independently of all the other datagrams.
    
- **Why is IP service so simple?**
    - Simple, dumb, minimal : Faster, most streamlined and low cost to build and maintain.
    - The end to end principle: where possible, implement features in the end hosts.
        - keeping all intelligence in the end hosts - source and destination, makes the internet simple, faster & minimal
    - Allows of variety of reliable or unreliable services to be built on top
        - If IP were to made reliable, it might not useful in all cases. In video app, there is no point of transmitting the old\lost packet
    - Works over any link layer - makes very few assumptions about the link layer below.

- **IP Service Model - Details**
    1. Tries to prevent packets looping forver
        1. When there is a faulty router table, it might re-send the datagram again to same or past router.
        2. Instead of finding and deleting the packets, IP adds **Hop Count in each header(TTL)**
        3. **Time To Live(TTL) starts at 128 or some number** and reduces as it goes thru each router and when it reaches zero, IP concludes that the packet is stuck in loop and will be removed
    2. Will fragment packets if they are long
        1. When sending over link layer, if the link layer doesn’t have the capcity to transmit the datagram, then IP splits them to two framgements to send them over link layer
        2. It also provides the checksum in headers to end host to assemble the data in correct manner
    3. Uses a header checksum to reduce chances of delivering datagram to wrong destination
    4. Allows for new versions of IP
        1. Currently IPv4 with 32 bit addresses
        2. And IPv6 with 128 bit addresses.
    5. Allows for new options to be added to headers.
        1. Pro: Useful features can added to headers
        2. Con: Extra features to be added in routers as well, breaking the goal of simple service

- **IPv4 Datagram**
    
    ![Untitled](Lecture%203%2041f4e33beafc47ae8d60ac69daf7ebc9/Untitled%201.png)
    
    - Important Feilds in Header
        - Source IP Address
        - Destination IP Address
        - Protocol ID - tells us what inside the data, if it has 6, then it contains TCP segement. Then we pass the data to TCP code to parse the segement correctly. Over 140 protocols avaliable
        - Version - v4 or v6
        - Total Packet Length - 64kBytes (incl., header  + data)
        - TTL - every router should decrement the value and if it reaches zero router should drop it
        - Packet ID, Flags, Fragment Offset - Helps to fragment the data if its too long
        - Type of Service  - Hint about the importance of the packet
        - Header Length
        - Options - options to carry extra information
        - **Checksum -** checksum is calculated over the whole header so that packet is not likely to delivered to wrong destionation by mistake.