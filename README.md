# Socket-Programming-TCP-IP-Connection---Jetson-Nano-to-Jetson-Nano

![SOCKET PROGRAMMING CONNECTION](https://github.com/ElectronicEngineerr/Socket-Programming-TCP-IP-Connection---Jetson-Nano-to-Jetson-Nano/blob/main/jetson-nano-overview-og.jpg)


We will teach you to communicate with TCP/IP connection, called socket programming, between two jetsons.Of course, the communication protocol called this socket program is not only from jetson nano to jetson nano. If you want, you can establish this connection on two microprocessors with their own interface and send data to one of them.


First of all, we need two jetson nanos and two monitors while doing this. Because from someone the data will go, someone will receive the data. We will post a data as text in this github repository for your understanding. To do this we will need two channels. one jetson receiver will work as the other jetson sender.

First of all, we will use the socket library that comes by default when we install the sdk manager. Our most important condition while doing this process is that the two jetson nanons must be in the same network.

>>>SENDER<<<
```
Server IP address and port number
IP_ADDRESS = '192.168.137.217'
PORT = 8000

Creating a client socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

Connecting to the server
client_socket.connect((IP_ADDRESS, PORT))

Sending data
while True:
# Get input from the user
message = input("Write the message you want to send: ")
# Send the data to the server
client_socket.sendall(message.encode())
```



This code is used to establish data communication over TCP/IP between a client and a server. The client connects to the server using the specified IP address and port number, and sends the messages entered by the user to the server.

Firstly, the server's IP address and port number are assigned to variables. Then, a socket is created by the client and a connection is established to the server using the provided IP address and port number.

Next, the user is prompted to enter the message they want to send, and this message is encoded and sent to the server. This process is repeated continuously, and the client keeps sending the messages entered by the user to the server, maintaining the communication.

The entire code allows a client to connect to a server and send the messages entered by the user to the server.


>>>RECEIVER<<<
import threading
import socket

Server IP address and port number
IP_ADDRESS = '192.168.137.217'
PORT = 8000

Creating the server socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

Binding the server socket with the specified IP address and port number
server_socket.bind((IP_ADDRESS, PORT))

Maximum number of clients that can connect
server_socket.listen(5)

Handling client connections and receiving messages
def handle_client(client_socket):
while True:
# Receive data from the client
data = client_socket.recv(1024)
if not data:
break
# Process the received data
print(data.decode())
client_socket.close()

Listening for client connections
while True:
# Accept a client connection
client_socket, client_address = server_socket.accept()
# Create a new thread when a new client arrives
client_thread = threading.Thread(target=handle_client, args=(client_socket,))
client_thread.start() 





This code is used to create a TCP/IP server. The server listens for incoming clients with the specified IP address and port number, and accepts their connections.

First, the server socket is created and binds it with the specified IP address and port number. Then, it starts listening to accept incoming connections from clients at the specified address.

The handle_client function establishes a connection with the client and receives messages from them. This function receives data from the client, processes the received data, and prints it to the screen. This process continues as long as the connection to the client is maintained.

The main loop keeps listening for client connections. When a new client connection arrives, a new thread is created to run the handle_client function. This thread maintains the connection with the client and processes incoming messages.

This code uses the threading module to create a multi-client server. By creating separate threads for each client, the server can communicate with multiple clients simultaneously.

