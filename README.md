# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
Server 
```
import socket
import os

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)
print(f"Server listening on {host}:{port}...")

c, addr = s.accept()
print(f"Connected to client: {addr}")

filename = 'sample.txt'

try:
    with open(filename, 'rb') as f:
        print(f"Sending {filename}...")
        while True:
            data = f.read(1024)
            if not data:
                break
            c.send(data)
    print("File sent successfully.")

except FileNotFoundError:
    print(f"Error: '{filename}' not found in {os.getcwd()}")

c.shutdown(socket.SHUT_WR)
c.close()
s.close()
print("Connection closed.")
```

Client
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000

s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file.txt', 'wb') as f:
    while True:
        print('Receiving data...')
        data = s.recv(1024)

        if not data:
            break  
        print(f"Data chunk received: {len(data)} bytes")
        f.write(data)

print('Successfully received the file.')
s.close()
print('Connection closed.')
```
## OUPUT
Server side

<img width="779" height="201" alt="image" src="https://github.com/user-attachments/assets/f7f48930-51a1-4263-bbe6-3d0eb2b53ea3" />

Client side

<img width="693" height="192" alt="image" src="https://github.com/user-attachments/assets/330756fb-a665-45f3-8c38-036b3a63aff6" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
