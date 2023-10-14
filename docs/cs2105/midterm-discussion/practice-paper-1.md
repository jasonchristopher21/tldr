# Practice Paper 1

halo zhan hong

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

### Question 12

Go-Back-N uses cumulative ACK, however do note that this ACK is for the reliable data transfer (rdt) protocols, hence an ACK of $m$ means that the receiver has received all the packets up to packet $m$ (i.e. packet $m$ already arrives).

:::caution

The only time ACK number means something different is only in TCP, where the acknowledgement number represents the first missing byte (ACK $m$ in TCP means everything up to byte $m-1$ has been received)

:::

### Question 13

Option A is incorrect. After sending every TCP segment, ISN will increase by the size of that segment, not by one.

:::caution

TCP Sequence Number is used to identify the **bytes**, and not the segment

:::

Option B is incorrect. They can have the same ISNs, and there wouldn't be any problems that arise with this.

Option C is incorrect. ISN does not determine the amount of data that can be transmitted. The one that determines is called the maximum segment size (MSS)

Option D is correct. ISN is randomly chosen, and agreed upon during the TCP handshake.

### Question 14

Option (i) is correct. DNS lookup will be required to resolve the host name of `www.nus.edu.sg` to its IP address.

Option (ii) is correct. `telnet` builds on top of `TCP` connection.

Option (iii) is incorrect. HTTP is an application layer protocol. Invoking `telnet` does not invoke any HTTP requests.

Option (iv) is incorrect. `telnet` does not initialise the receiver side. In the case that the receiver is not listening, then `Connection Refused` might occur.

### Question 15

Trick question. Take note that the `2105` is the port number of the other host (`sunfire.comp.nus.edu.sg`) and not the current port number where `mySocket` is bound to.

### Question 16

:::tip

In this question, a key point to note here is that the ACK packet can be received at any point in time. Do note that the question does not specify that no more ACK packets are expected here, so it is possible that sequence number 14 is the start of the window

:::

For this question, let us try to look through each possible option, see if they can indeed be the sequence number of the next packet transmitted.

Option A: 4

This option involves cleverly utilising the fact that the $k$ bit sequence number is variable. Hence, we want to utilise the property that it can "wrap around".

Take $k=4$, hence the sequence number now ranges in $[0,2^4-1]$. Set 14 as the start of the window, then the current window would be $[14, 15, 0, 1, 2, 3]$. We expect that when ACK for 15 to 3 is received, then the window will now shift to $[4, 5, 6, 7, 8, 9]$. Hence, it is possible that 4 becomes the next packet transmitted.

Option B: 9

Since the smallest possible $k$ we can achieve is 4, hence the above case would be the only case we can wrap around. We can't expect sequence number 9 to be reached through wrapping around.

So, now let us assume that 9 falls within the same window as 14. That means, the window now becomes [9, 10, 11, 12, 13, 14], so that we hope 9 can be retransmitted next. However, remember that GBN uses cumulative ACK. An ACK number of 14 means that all packets up to packet 14 has been received. Hence, packet 9 won't be retransmitted, and option B is the answer.

Option C: 15

This option would be quite obvious. Taking the window in Option B, once the whole window is sent, when ACK 14 is received, the window will now shift to [15, 16, 17, 18, 19, 20].

Option D: 19

Also possible. Take $k=5$ and consider [13, 14, 15, 16, 17, 18] where all ACKs are received successfully. Window will shift to [19, 20, 21, 22, 23, 24].

Option E: 20

Consider $k=5$ and [14, 15, 16, 17, 18, 19] where all ACKs are received successfully. Window will shift to [20, 21, 22, 23, 24, 25]

### Question 17

Observations:

- Nodes are from node $0$ to node $K+1$. 
- What is the number of links? We can try a very small example, e.g. from node 0 to node 3 ($K=2$). In this case, the links are (0, 1), (1, 2), (2, 3), which is $K+1$ links. Hence, propagation delay is $(K+1)(p)$

:::tip

If in doubt, start with smaller cases to understand the item first. Once you are satisfied (and understood the workings) of the smaller cases, then change the cases into their respective variables.

:::

- Only nodes $1,2,...,K$ will incur a processing time, hence processing delay (combined with queueing delay) is $K*q$

- Now the fun part: The twist here is that we consider only the duration when the last bit of the packet leaves node 0 to when the last bit of the packet arrives at node $K+1$. How does that change our problem?

  Recall that normally when we account for the total delay, we account the duration from when the first bit of the packet leaves the first node, up to when the last bit of the packet arrives at the last node. 

  So what changes here? Last bit leaves - Last bit arrives is simply the duration of first bit leaves - last bit arrives, subtracted by the transmission delay in the first node (first bit leaves - last bit leaves).

  Hence, transmission delay now occurs only in nodes $1, 2, ..., K$ instead of $0, 1, 2, ..., K$, giving us a transmission delay of $K * d_{trans}$

- To accomodate $d_{trans}$, we need to consider the total data divided by the transmission rate. Total data is $(L+h)$ and transmission rate is $C$, so $d_{trans} = \frac{L+h}{C}$.

Now, we can combine the pieces together

$$
\begin{align*}
d_{end-to-end} &= d_{proc} + d_{queue} + d_{trans} + d_{prop} \\
&= qK + K (\frac{L+h}{C}) + p(K+1)\\
&= qK + K(\frac{L+h}{C}) + pK + p\\
&= p + K(\frac{L+h}{C} + p + q)\\
\end{align*}
$$

Hence we obtain option A.

### Question 18

Quite straightforward. Size of the last TCP segment without the header data would be 

$$
\begin{align*}
\mathrm{size} &= \mathrm{File\space size}\space \% \space \mathrm{MSS} \\
&= 9,990 \% 1,000 \\
&= 990 \space \mathrm{bytes}
\end{align*}
$$

Hence, last TCP segment would contain 990 bytes of file data + 20 bytes of header = 1,010 bytes.

### Question 19

Can do a normal checksum. Don't forget the carry

### Question 20

Rather difficult question.

Note that the transmission rate of A - R is smaller than the transmission rate of R - B. Link A - R now becomes the main bottleneck.

If we draw the diagram, we can obtain the following items:

Number of packets is $8\times10^4\div1000=80$ packets, hence the end-to-end delay is equivalent to the transmission delay of each packet from A to R, added by the tiny little transmission delay for the last packet from R to B, since the transmission delay of other packets from R to B is "absorbed" by the overwhelming transmission delay from A to R.

End-to-end delay: $80\times\frac{1000}{1000} + \frac{1000}{2000}=80.5$