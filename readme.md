## Reflection

### Experiment 2.1

#### How to run it, and what happens when you type some text in the clients.

The server initiates by running cargo run --bin server, listening for connections on port 2000. It processes incoming messages and broadcasts them to all connected clients. Clients join by running cargo run --bin client, establishing connections on unused ports. Upon connecting, a client thread loops, handling events via tokio::select!. It broadcasts received messages to all clients and prints/queues messages from its connection reader. Simultaneously, a client thread prints received messages and sends terminal input as messages to the server. New connections are announced on the server. This client-server communication continues with messages flowing between the server's broadcast receiver and clients' connection readers/writers until terminated.

