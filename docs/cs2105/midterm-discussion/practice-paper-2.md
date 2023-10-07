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

1. 192.168.15.1: **11000000.10101000.0000**1111.00000001, does not match
2. 192.168.177.254: **11000000.10101000.1011**0001.11111110, does not match
3. 192.188.168.230: **11000000.10111100.1010**1000.11100110, match
4. 192.168.169.31: **11000000.10101000.1010**1001.00011111, match

:::tip

Notice that options (1), (2) and (4) share the same two bytes with the subnet mask. Hence, option (3) is incorrect. We now only need to consider the third byte of options (1), (2) and (4), and compare it to match the first four bits of the third byte in the subnet mask.

:::

### Question 14

The presence of a `connect` indicates that the snippet is a TCP client socket. Hence, option A is definitely invoked.

Since the connection is done to a hostname and not an IP address, we need to do a lookup to map the hostname to the IP address. Hence, DNS will be invoked. Since DNS builds on top of UDP, UDP will also be indirectly invoked.

HTTP is not invoked. It is an application layer protocol. TCP connection is not exclusive to HTTP, i.e. other protocols can also invoke TCP, so this snippet is not exclusive to HTTP.

Hence, the answer is C.

### Question 15

### Question 16

### Question 17

### Question 18

### Question 19

### Question 20