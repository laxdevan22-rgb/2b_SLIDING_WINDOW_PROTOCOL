# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## SimpleServer.py:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Waiting for connection...")
conn, addr = s.accept()
print("Connected to", addr)
while True:
 data = conn.recv(1024).decode()
 if not data:
   break
 print("Frames received:", data)
 ack = "ACK for " + data
 conn.send(ack.encode())
conn.close()
```
## SimpleClient.py:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = list(range(1, n+1))
i = 0

while i < n:
    send_frames = frames[i:i+w]
    msg = " ".join(map(str, send_frames))
    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()
    print("Received:", ack)

    i += w

s.close()
```


## OUPUT
## SimpleServer:

<img width="1425" height="208" alt="694364729-55f8bd5b-66ca-4297-92e1-ce12f9dd8538" src="https://github.com/user-attachments/assets/237391aa-3d1c-4fe9-87f4-de142fad179f" />

## SimpleClient:

<img width="1437" height="232" alt="694365103-81c53caa-3363-4ad5-bec2-ad69bc1925e9" src="https://github.com/user-attachments/assets/22743fe6-29d0-45c8-8825-fc0c053a7bfd" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
