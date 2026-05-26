## Discovery
```
# Basic UDP port scan
nmap -sU -p 69 <IP>

# Service/version detection + basic scripts
nmap -sU -p 69 -sV <IP>

# TFTP specific enumeration (tries common files)
nmap -sU -p 69 --script=tftp-enum <IP>
```

## Basic Usage
```
# Interactive client
tftp <target-ip> 69

# Download a file (interactive)
tftp> get file.bin
tftp> get pxelinux.cfg/default

# One‑liner download (no interactive shell)
tftp <target-ip> -c get file.bin
```

## Uploading / Testing Write Access
```
# Upload (if server allows write)
tftp <target-ip> -c put localfile remotefile

# Check if directory is writable
tftp <target-ip> -c put test.txt test.txt
tftp <target-ip> -c get test.txt
```

## Common Files / Paths to Try
```
# PXE / boot
pxelinux.cfg/default
pxelinux.cfg/01-<mac-address>
boot.ipxe
undionly.kpxe
lpxelinux.0

# OS deployment / unattended install
ks.cfg
kickstart.cfg
preseed.cfg
preseed.cfg.gz
autoyast.xml

# Network devices / routers / switches
startup-config
running-config
config.text
vlan.dat
router.cfg
switch.cfg

# Firmware / images
firmware.bin
image.bin
*.ios
*.bin
```

## Brute‑Forcing / Enumerating Files

Because TFTP has no directory listing, you often have to brute force filenames to discover what’s on the share.

## Simple Bash Loop (tftp client)
```
TARGET_IP=""
WORDLIST=""

for f in $(cat "$WORDLIST"); do
  echo "[*] Trying $f"
  tftp "$TARGET_IP" -c get "$f" 2>/dev/null
  if [ -s "$f" ]; then
    echo "[+] Found and downloaded: $f"
  else
    rm -f "$f" 2>/dev/null
  fi
done
```

## Using nmap tftp-enum
```
# Uses a built‑in list of common config/boot files
nmap -sU -p 69 --script=tftp-enum <target-ip>
```
