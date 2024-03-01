---
sidebar_label: Midterm 23/24 S1
---

# Midterm Solutions (AY23/24 Sem 1)

### Disclaimer

These are very rough solutions that I wrote just for the sake of teaching. I will be improving these in the near future.

### Question 1

By default, web server runs on port 80. This is a rather trivai question, need to check lecture slides.

**Option D: Port 80**

### Question 2

- UDP is connectionless
- UDP is unreliable

**Option A**

### Question 3

- DHCP runs over UDP. Reliability is not a requirement when designing DHCP (Lec 6 & 7 Slide 10)
- DNS clearly runs on top of UDP

**Option D**

### Qeustion 4

RFC stands for Request For Comments

**Option A**

### Question 5

_(skipped, quite straightforward. Refer to tutorial material if you are unsure how to find the checksum)_

### Question 6

- ACK # and SEQ # are for handling duplicates and packet ordering
- Timeout / retransmission for packet loss
- Checksum for bit errors / check corrupted data

**Option B**

### Question 7

Check lecture slides

**Option D**

### Question 8

- HTTP/1.0 is non-persistent
- HTTP/1.1 is persistent

**Option D**

### Question 9

Blocks of private IP addresses:

- 10.0.0.0/8
- 172.16.0.0/12 <-- 172.31.0.1 falls here
- 192.168.0.0/16

**Option C**

### Question 10

304 is "NOT MODIFIED

**Option D**

### Question 11

IP address of the host is only those found under the "ANSWER SECTION". So, it has to be either 202.165.107.50 or 202.165.107.49.

- `AUTHORITY SECTION` specifies the name servers
- `ADDITIONAL SECTION` specifies the IP address of the name servers

**Option D**

### Question 12

Just need to check which one contains consecutiive 1s, followed by consecutive 0s

Option A: 193 (DEC) = 1100 0001 (BIN) breaks this rule.

**Option A**

### Question 13

Also in the lecture slides

**Option D**

### Question 14

- rdt 3.0 does not have NAK. Options C, D, E are immediately incorrect
- Both data and ACK packets can be corrupted.

**Option A**

### Question 15

137.132.80.0 => 137.132.01010000.00000000 <br />
137.132.87.0 => 137.132.01010111.11111111

Host bit consists of 11 bits

**Option B**

### Question 16

- GBN and SR clearly are incorrect. These are pipelined protocols
- UDP and TCP also not

**Option E**

### Question 17

- DHCP is directly invoked
- DHCP runs over UDP. Hence, UDP is indirectly invoked

**Option B**

### Question 18

- First data segment's sequence number: 5
- First ACK segment's ACK number: 15
  ...
- 50th ACK segment ACK number = $15 + 49 \times 10 = 505$

**Option C**

### Question 19

Easy question, no tricks.

$800$ bytes = $800 \times 8$ = $6400$ bits

$$
d_{trans} = \frac{L}{R} = \frac{6400\space\mathrm{bits}}{400,000\space\mathrm{bps}} = 16\space\mathrm{ms}
$$

$$
d_{trans} = \frac{d}{V} = \frac{2,500,000\space\mathrm{m}}{250,000,000\space\mathrm{m/s}} = 10\space\mathrm{ms}
$$

$$
d_{end-to-end} = 16\space\mathrm{ms} + 10\space\mathrm{ms} = 26\space\mathrm{ms}
$$

**Option C**

### Question 20

- Option A matches prefix 011
- Option B does not match any prefix, will go to the otherwise case
- Option C matches prefix 101
- Option D matches prefix 11

**Option B**

### Question 21

3-way handshake has been done, so we need to consider only those $n$ requests.

$$
\begin{align*}
delay &= RTT + d_{trans} \\
&= \sigma + nx
\end{align*}
$$

**Option B**

### Question 22

- UDP header contains $2 \times 32$ bits = 8 byte data
- Payload = $2\times8$ = 16 bytes
- Length field will now store 16 + 8 = 24

**Option C**

### Question 23

Consider that when $F$ arrives, $G$ has not arrived yet. Moreover, $D$ and $F$ are out-of-order.

By the question specification, Bob discards out-of-order packets, so segments $D$ and $F$ won't be acknowledged.

Sends ACK 500

**Option B**

### Question 24

Number of packets = ceil(9000 / 920) = 10 packets

Size of last packet = 9000 - 920 \* 9 + 80 = 800 b

[insert diagram here]

4 ms + 1 ms + 4 ms + 9 \* 1 ms + 0.8 ms = 18.8 ms

**Option C**

### Question 25

Important observation: ACK may be lost

- Option (i) <br/>
  0 is possible. Suppose that the window is [13, 14, 15, 0] where 13 has arrived, but 14 and 15 is lost. 0 is in-transit, so it is possible that 0 is the next packet received.
- Option (ii) <br/>
  2 is not possible. Windows containing 14 is [11, 12, 13, 14] to [14, 15, 0, 1]. If receiver expects 14, some cases possible:
  - 14 is lost: then window will not move, and 2 is not reachable
  - 14 is received after: then 2 is not the next packet received.
- Option (iii) <br/>
  12 is possible. Consider [12, 13, 14, 15] where 12 and 13 is received, 14 and 15 is lost and all ACKs are lost. Window will be retransmitted
- Option (iv) <br/>
  This is not even a valid sequence number :(

**Option A**
