File: fileutil.h, client.cpp, server.cpp, Makefile  
Author: Yao guo, Qi zhao 
USCID: 2176023892, 2704862514  
Email: yaog@usc.edu, zhao726@usc.edu  
Description: 
Two setting for this lab
The Delay (RTT) of 10ms with the Loss rate of 1%
The Delay (RTT) of 200ms with the Loss rate of 20%
Create the connection between sender and receiver, then transfer at least 1GB data under this circumstance. 
The total time for the file to make the one-way trip will be used as criteria for the performance.
Using UDP for file transmission and TCP for acknowledgements. There are two sockets, one is for file transmission. The other is for acknowledgement transmission. Acknowledgement is the block ids which blocks are successfully sent. 


Process:  


Server side:
1.Create two sockets, one is for file transmission, one is for ACKs transmission.
2.Bind the sockets.
3.Wait data transmission from the client.
4.Receive the file size from the client  via ACKs socket and create a check table.
5.Begin to receive the blocks from the client.
6.Send ACKs back to tell the client which blocks are successfully sent and update the 7.check table. 


Client side:
1.Create two sockets, one is for file transmission, one is for ACKs transmission.
2.Send the file size to the server via ACK socket .
3.Create a thread to monitor the blocks which used to read ACK from server. 
4.Make a check table and send blocks to the server via file transfer socket.
5.Receive the ACKs, update the check table and begin retransmission for those blocks which are not successfully sent, if successfully sent, skip it. 
6.When all blocks are successfully sent, close the sockets.


Reference:


Most part refer as:
“UDP Server-Client implementation in C” by Amitds 
https://www.geeksforgeeks.org/udp-server-client-implementation-c/


“Socket Programming in C/C++”
https://www.geeksforgeeks.org/socket-programming-cc/


“Bitwise operations in C”
https://en.wikipedia.org/wiki/Bitwise_operations_in_C