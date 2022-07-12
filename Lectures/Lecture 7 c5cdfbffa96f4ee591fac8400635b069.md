# Lecture 7

## Encapsulation

- Encapsulation is the result of **what happens when you combine layers and packet switching.**
- Encapsulation is the principle by which you maintain layer, yet organize information in packets so that it can be shared between layers
- The way it works is by encapsulation data in layers and is shared between them
- For example, the HTTP GET request is the payload for the TCP segement
- The TCP segement encapsulation the GET request becomes the payload for IP Packet.
- The IP packet encapulating TCP segement, GET request becomes the payload for WiFi Frame
- The outer most encapsulation will the WiFi frame, followed by IP, then TCP and HTTP request.

![Untitled](Lecture%207%20c5cdfbffa96f4ee591fac8400635b069/Untitled.png)

**Encapsulation Flexibility**

- Encapsulation allows to layer recursively
- Example: VPN - Virtual Private Network
    - HTTP web payload
    - a TCP segement in
    - an IP network packet in
    - a secure TLS presentation message in
        - a TCP segement in
        - an IP network packet in
        - an Ethernet link frame in

![Untitled](Lecture%207%20c5cdfbffa96f4ee591fac8400635b069/Untitled%201.png)

**Encapsulation Benifits**

- Help of seperation of concerns
- Helps enforce boundaries & layering
- Simplify layer implementations