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

<br>

# 2.2. Modifying the websocket port
To modify the port to be 8080, both the client.rs and the server.rs file needs to be changed. The changes are as follows:
- Client

```
async fn main() -> Result<(), tokio_websockets::Error> {
    let (mut ws_stream, _) =
        ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
            .connect()
            .await?;
    ...
}
```

- Server
```
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    let (bcast_tx, _) = channel(16);

    let listener = TcpListener::bind("127.0.0.1:8080").await?;
    println!("listening on port 8080");

    ...
}
```

After both these changes are made, the server and client will run successfully just like before, except now they're operating on port number 8080 instead of 2000. Both also seem to use the same websocket protocol.
