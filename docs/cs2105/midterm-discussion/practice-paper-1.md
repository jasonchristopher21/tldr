# Practice Paper 1

### Question 1

Let us see through each of the options:

A. Client must always be alive<br/>
Not really, Client can just disconnect and technically connection is lost then (it's a client side problem)

B. Server offers service while client requests for service from server<br/>
Yup, Client would need to request for service from server. It's called a "server" because it "serves" / provide "service"

C. Only server can transmit data to client.<br/>
D. Only client can transmit data to server.<br/>
HTTP Requests can have data in the body (e.g. `POST`/`PUT`/`PATCH` requests), hence client can send data to the server. HTTP Responses can have data, obviously.

E. Server must run either DNS or HTTP protocol.<br/>
This is possible. You can, for example, do direct IP Address Access, or you can also build say a Peer-to-peer (P2P) network where users communicate directly with each other

Hence, the appropriate answer is B.

### Question 2

Option A is correct. UDP is a process-to-process communication protocol (hence port numbers are used)

Option B is incorrect. UDP is a process-to-process protocol, unlike IP which is a host-to-host protocol.

Option C is incorrect. UDP is unreliable.

Option D is incorrect. There is no guarantee that minimal throughput and timing is obtained. Remember, timing and latency is something we cannot guarantee.

Option E is incorrect. UDP is not connection-oriented.

### Question 3

Let us see through each of the options:

A. A call setup is always performed before data transmission starts.<br/>
In telecommunication, call setup is the process of establishing a virtual circuit across a telecommunications network. Call setup is typically accomplished using a signaling protocol. Since Internet uses packet-switching protocols (not circuit-switching protocols like mobile telecoms), we do not need to establish a virtual circuit, as we can utilise current routing mechanisms to transmit the packets.

B. The Internet is structured as a network of networks.<br/>
It is called the "Interconnected Network" for a reason.

C. A packet passes through no more than two autonomous systems to reach
destination host.<br/>
Nope, can pass through other systems also (e.g. if you want to send file from NUS to MIT, will pass through lots of different systems depending on region)

D. The only access network technologies allowed are Ethernet and Wi-Fi.<br/>
Ever heard of mobile networks? Satellite communication?

Hence, the appropriate answer is B.

### Question 4

:::info

UDP server will use the same socket for all clients. TCP server will use one socket as a welcome socket, then creates a socket for each client connection

:::

Recall that for a TCP server, there will be a welcome socket, and for each of the connection, the server will need to create a separate socket. Hence, there would be 1 welcome socket and $n$ respective client sockets, giving us a total of $n+1$ sockets.

### Question 5

Lecture definition: This is a persistent connection.

### Question 6

Let us consider each option:
- Queueing delay: Not constant, this can also depend on the network congestion at a certain point in time.
- Transmission delay: Not constant. Larger packets will incur larger transmission delay, since $d_{trans} = \frac{L}{R}$
- Propagation delay: Constant, since the question mentions that the packets will go through the **same route** to the destination. Hence, distance remains constant, and speed of propagation should also remain constant as the medium of propagation is the same.
- Processing delay: Not constant. Larger packets will incur greater processing delay.

### Question 7

### Question 8

:::info

TCP Acknowledgement Number: This is the sequence number of the **next byte** of data expected by the receiver.<br/>
TCP ACKs up to the first missing byte in the stream (Cumulative ACK).

The sequence number of a TCP segment is the sequence number of the first byte in that segment.

Example: If a packet of 100 bits is sent to the receiver, which contains sequence number {0, 1, 2, ..., 99}. The receiver expects the next byte of data as sequence number #100, so the receiver sends ACK 100.

:::

Let us consider each option:

A. If a TCP segment has sequence number $m$, then ACK for this segmeent will have acknowledgement number $m$.<br/>
False, if a TCP segment has sequence number $m$, then if the segment arrives OK, then the ACK should be greater than $m$, since byte $m$ is well received. ACK number would be the first missing byte in the stream.

B. If a TCP segment has sequence number $m$, then ACK for this segment will have acknowledgement number $m+1$.<br/>
False, unless if the TCP segment only consist of 1 byte. Suppose if the segment has length $L$, meaning it sends $L$ bytes of data in the segment, then the ACK would have been acknowledgement number $m+L$.

C. Host A is sending a file to host B over a TCP connection. If B has no data to send to A, B will not send ACK packets because B cannot piggyback the acknowledgments on data. <br />
False, you can send acknowledgements with no content.

D. TCP doesn't function correctly in a network that may re-order packets.<br/>
False, since TCP is capable of buffering out-of-order packets.

Hence, answer should be E. None of the rest.

### Question 9

A valid subnet mask is those that have a form of `1`s, optionally followed by `0`s. If this pattern is violated, it is no longer a subnet mask.

An example is `11111100` or `11111111`. This is a valid subnet mask.

Whereas `01110000` or `11010001`, these are invalid subnet masks.

To solve this question, you can convert to binary and you should be able to detect the answer.

### Question 10


### Question 11

GBN sender has only one timer to keep track of the last un-ACK-ed packet.

SR sender has multiple timers to keep track of each un-ACK-ed packet.

TCP sender has one timer to keep track of the segment that is sent.