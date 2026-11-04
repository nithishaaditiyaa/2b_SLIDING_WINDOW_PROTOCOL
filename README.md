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

# SERVER.py :

```

import socket

s = socket.socket()
s.connect(('localhost', 1234))

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print("Received frames:", data)
    s.send("Acknowledgement received from the server".encode())

s.close()

```

# CLIENT.py :

```

import socket

skt = socket.socket()
skt.bind(('localhost', 1234))
skt.listen(5)
print("Waiting for server connection...")
c, addr = skt.accept()

while True:
    try:
        size = int(input("Enter number of frames to send: "))
        if size > 0:
            break
        print("Enter a positive number.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

frames = list(range(size))

while True:
    try:
        window = int(input("Enter Window Size: "))
        if 0 < window <= size:
            break
        print("Enter a valid window size.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

start = 0

while start < len(frames):
    end = min(start + window, len(frames))
    c.send(str(frames[start:end]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print(ack)
    start = end

c.close()
skt.close()

```

## OUPUT

<img width="1238" height="90" alt="image" src="https://github.com/user-attachments/assets/efa28b88-e672-47a4-bb04-cb0ccd763f6d" />





<img width="1330" height="155" alt="image" src="https://github.com/user-attachments/assets/f490207a-0003-4802-85e7-ac4e776ec9a4" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
