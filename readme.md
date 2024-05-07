## Reflection

### Experiment 2.1

#### How to run it, and what happens when you type some text in the clients.

The server initiates by running cargo run --bin server, listening for connections on port 2000. It processes incoming messages and broadcasts them to all connected clients. Clients join by running cargo run --bin client, establishing connections on unused ports. Upon connecting, a client thread loops, handling events via tokio::select!. It broadcasts received messages to all clients and prints/queues messages from its connection reader. Simultaneously, a client thread prints received messages and sends terminal input as messages to the server. New connections are announced on the server. This client-server communication continues with messages flowing between the server's broadcast receiver and clients' connection readers/writers until terminated.
<img width="1229" alt="Screenshot 2024-05-07 at 13 00 34" src="https://github.com/PeakFiction/Module10PartZwei/assets/112671939/98d32244-52f9-4289-ae8f-6853165e3d24">


### Experiment 2.2
To change the server's listening port from 2000 to 8080, by modifying the TcpListener::bind address in the server code. However, the client still tries connecting to port 2000, breaking the application. Adjust the ClientBuilder::from_uri input to the new port address, allowing the client to connect to port 8080 successfully. Both server and client use the tokio_websockets package, implying they use the same WebSocket protocol. The server listens on the configured address and port, accepts TCP connections, and upgrades them to WebSocket connections using ServerBuilder. Clients establish WebSocket connections via ClientBuilder, facilitating bidirectional communication between server and clients.