# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Output
client.py
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()

```

server.py

```


server.py
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()

```
## OUTPUT

server.py <br>
<img width="1071" height="186" alt="image" src="https://github.com/user-attachments/assets/f87aefa7-de01-4430-8231-b662649d3ac7" /> <br>
client.py <br>
<img width="915" height="131" alt="image" src="https://github.com/user-attachments/assets/5fbc82b1-c5d2-4aea-a76c-5db6a380263a" /> <br>
ipconfig <br>
<img width="1140" height="827" alt="image" src="https://github.com/user-attachments/assets/aa0dd9ad-10e6-4438-93bc-6ae36cb9f3bc" /> <br>
ping <br>
<img width="1145" height="846" alt="image" src="https://github.com/user-attachments/assets/60b5c753-764a-4039-a796-c6519fd21f34" /> <br>
tracert <br>
<img width="1022" height="418" alt="image" src="https://github.com/user-attachments/assets/fc330e79-2f5f-4ae4-bbd3-85382859b8b5" />


## Result
Thus Execution of Network commands Performed 
