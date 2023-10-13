# Practice Paper 2

### Question 1

Let us consider the options that are provided

Option A: HTTP runs on top of TCP. This is true, you can capture the packets using wireshark.

Option B: HTTP is an application layer protocol. This is true as per the lecture examples.

Option C: In HTTP/1.0, the server will close the connection after every request. This is true, since HTTP/1.0 is non-persistent.

Option D: In HTTP/1.1, the default connection type is persistent. This is also true.

Option E: HTTP is only used to download HTML data from a Web server. This is false, because HTTP can be used to send data to the Web server (e.g. `POST` / `PUT` / `PATCH`)

### Question 2

:::info

Multiplexing: Receive incoming data from the host, "pack" these and send as packets

Demultiplexing: Receive incoming packets from the lower layer, "unpack" these and sent them to the host

:::

Correct answer would be demultiplexing.

### Question 3

Let us consider each of the options.

Option A is correct, this is the purpose of DNS.

Option B is also correct. It is possible that a certain host name can have multiple canonical names, and each CNAME will be associated to a separate IP address.

Say facebook.com, this can refer to many IP addresses. You can check this using a `dig` command.

Option C is incorrect. DNS query can be cached in the Local DNS server, in this case the root server won't be accessed if the cache exists.

Option D is correct. UDP is port 53, compared to TCP is port 80.

Option E is correct. Remember this screen?

![](https://helpdeskgeek.com/wp-content/pictures/2022/04/image-23.png)

### Question 4

Lecture note. A port number is 16 bytes long.

### Question 5

Manageable chunks = packets. Strong indicator that this is packet switching.

### Question 6

This is a tricky question. Note that it says sending **process** to receiving **process**. Hence, this refers to process-to-process communication, not host-to-host communication. Hence, this would be a transport layer protocol.

### Question 7

Quite obvious. 404 means not found.

### Question 8

Tutorial example. UDP client can send data without the UDP server to exist in the first place. This is because UDP does not need to establish a connection between the client and the server.

Option A: This is correct. As per tutorial question.

Option B: This is incorrect. A UDP client can send data without the UDP server to exist, and no exception will be thrown. The client will just wait indefinitely (like me waiting for a girlfriend to come to my life T_T)

Option C: This is incorrect. On the lecture example, you will see that the client does not need to make a `connect` function call to connect with the server.

Option D: This is incorrect. UDP server can just accept from any connection, since it does not create a new socket for each connection.

### Question 9

`nslookup` is used to find the DNS mapping between the hostname and IP address.

![](https://media.discordapp.net/attachments/816338612001701899/1160140227189420052/image.png?ex=653393c8&is=65211ec8&hm=b06724e189da061a4b0123c583a5b58e0902a03879203144ee979d6d9fbb233e&=&width=697&height=600)

### Question 10

If a corrupted packet or ACK is received, then it does nothing, since timeout will trigger a retransmission anyways. Check the FSM of rdt 3.0 for more details.

### Question 11

Retransmission:

- GBN will retransmit all packets within the sender window
- SR will retransmit only that packet that was timeout
- TCP will retransmit just that segment that triggered a timeout.

### Question 12

Selective repeat receiver will send an ACK for each packet that arrives. Hence, ACK $m$ means that the receiver has received packet $m$, does not imply other packets.

### Question 13

The provided subnet is: **11000000.10101000.1010**0000.00000000 up to the first 20 bits.

| Option | IP Address      | Binary Representation                   | Match? |
| ------ | --------------- | --------------------------------------- | ------ |
| i      | 192.168.15.1    | **11000000.10101000.0000**1111.00000001 | No     |
| ii     | 192.168.177.254 | **11000000.10101000.1011**0001.11111110 | No     |
| iii    | 192.188.168.230 | **11000000.10111100.1010**1000.11100110 | No     |
| iv     | 192.168.169.31  | **11000000.10101000.1010**1001.00011111 | Yes    |

:::tip

Notice that options (1), (2) and (4) share the same two bytes with the subnet mask. Hence, option (3) is incorrect. We now only need to consider the third byte of options (1), (2) and (4), and compare it to match the first four bits of the third byte in the subnet mask.

:::

:::info

Another alternative to seeing this problem can be, if I can determine the range of the IP addresses that fall inside the subnet mask, then I can determine which IP addresses are in the subnet mask, without converting each of them into the binary representation.

Notice that the range basically depends on the third byte. Hence,

Lower bound: `11000000.10101000.10100000.00000000` -> `192.168.160.0`<br/>
Upper bound: `11000000.10101000.10101111.11111111` -> `192.168.175.255`

Basically anything that falls within 192.168.160._ to 192.168.175._ should be considered under the subnet mask.

:::

### Question 14

The presence of a `connect` indicates that the snippet is a TCP client socket. Hence, option A is definitely invoked.

Since the connection is done to a hostname and not an IP address, we need to do a lookup to map the hostname to the IP address. Hence, DNS will be invoked. Since DNS builds on top of UDP, UDP will also be indirectly invoked.

HTTP is not invoked. It is an application layer protocol. TCP connection is not exclusive to HTTP, i.e. other protocols can also invoke TCP, so this snippet is not exclusive to HTTP.

Hence, the answer is C.

### Question 15

The intuition behind this question is, how many segments will cause a wrap-around (i.e. exhaust the sequence numbers from 12,345 to $2^{32}-1$, then back from 0 to 2,105 + 1,024).

Sequence number of the first byte: 12,345
Sequence number of the segment after the last segment: 2,105 + 1,024 = 3,129

Number of bytes sent in total: $2^{32} + 3,129 - 12,345 = 4,294,958,080$ bytes
Hence, number of segments is $\frac{4,294,976,512}{1024}=4,194,295$ segments

### Question 16

Out of the available options, only 2 does not fall in the criteria of $6 \pm (3-1)=6\pm 2$.

0 is reachable, because it is possible that the window is [6, 7, 0] since the sequence number only uses 3 bits. In this case, the scenario that 0 is the next packet being sent is:

- Suppose the previous window is [5, 6, 7]
- Sender receives ACK5 and ACK7. Window now shifts to [6, 7, 0]
- Sender did not receive ACK6, triggers timeout. Packet 6 is now being sent
- Sender receives ACK6.
- Window will now shift to [0, 1, 2], Packet 0 is being sent next.

### Question 17

You can check the following diagram:

Analysis:

- Propagation delay from A - R and R - B is only triggered once, since data is sent back-to-back. <br/> Hence, $d_{prop} = 0.1s + 0.15s = 0.25s$.
- For transmission delay, it is $2 * k + 0.5s$, since it seems that the variable item is the 2s transmission delay. 0.5 s transmission delay in host A is only incurred once by the first packet.

Hence, total delay is $0.25 + 0.5 + 2k = 0.75 + 2k$.

### Question 18

Stop and wait protocol: ACK must be received before another packet can be sent. Since each packet has the same transmission rate, transmission delay and propagation delay, it is possible for us to consider only the throughput of one packet, instead of the entire 10 packets. (duh, who wants to count more if you can count less :O)

- Transmission delay: $d_{trans} = \frac{1000 \times 8}{10^6} = 8 ms$
- Round trip time: 24 ms

Throughput: $\frac{file size}{end-to-end delay} = \frac{1000 \times 8}{0.008 + 0.024} = 250 \space kbps$

### Question 19

:::info

UDP length field is inclusive of **both** the data and the UDP header

:::

UDP header consists of 32 \* 2 bits = 64 bits = 8 bytes. Hence, if the UDP packet does not have any data inside, then the length should still reflect the header length, which is 8. In binary representation, this is `1000`.

### Question 20

Note the following:

- First green arrow will send a value of S = 30, since X expects byte #30 to come next from the A = 30 value of the first blue arrow.
- First green arrow will send a value of A = 200, since Y expects byte #200 to come next, as bytes 100 - 199 has arrived from X in the first blue arrow.
- Since all packets from X has safely arrived at Y, by the time third arrow is sent, A = 100 (seq num of first packet) + 300 (length received) = 400
- Since this is the third packet sent by Y, seq num would be 30 + 100 + 100 = 230.

Hence, S = 230 and A = 400