# 2.1. Original code of broadcast chat
Server:
![Server](img/server.jpg)

Client 1:
![Client1](img/client1.jpg)

Client 2:
![Client2](img/client2.jpg)

Client 3:
![Client3](img/client3.jpg)

After running the server with `cargo run --bin server` and running the three clients with `cargo run --bin client`, I noticed that when the clients are first instantiated, the server prints out "New connection from 127.0.0.1:5173X", indicating that another client has just connected to it. 

Every time I entered a message in the different clients, the server printed out the client address that sent each message & the message itself. Each client was also able to see its own message and other clients' messages reported back from the server, simulating a broadcast chat system.
