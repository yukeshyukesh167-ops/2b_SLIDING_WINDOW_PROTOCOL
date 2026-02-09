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
Server Side

import socket
s = socket.socket()
s.bind(('localhost',9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break
    
    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()
s.close()

Client Side

import socket
c = socket.socket()
c.connect(('localhost',9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))
print("Total frames to send:",len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())

        ack = c.recv(1024).decode()
        if ack:
            print(f"Acknowledgement received: {ack}")
            i +=s

    break
c.close()
## OUPUT
<img width="1097" height="113" alt="image" src="https://github.com/user-attachments/assets/60b109e2-26de-4d41-bd13-399ef8e5febc" />
<img width="1386" height="192" alt="image" src="https://github.com/user-attachments/assets/5bf5f4e2-dcdf-4f79-9c2c-676a8f6c5f6f" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
