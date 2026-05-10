## Server Message Block

### Recon

```
nmap -p 139,445 target.com
nmap --script smb-vuln* -p 139,445 [ip]
```

### Enumerate Host
```
# nxc smb [ip]
crackmapexec smb [ip]
```

### List Shares
```
crackmapexec smb [host/ip] --shares
crackmapexec smb [host/ip] -u [user] -p [pass] --shares
crackmapexec smb [host/ip] -u guest -p '' --shares
crackmapexec -N -L //[ip]

smbclient -N -L //[IP]

```

### User Enumeration 
```
crackmapexec smb [ip] -u guest -p '' --rid-brute
```

### Enumerate Files
```
smbclient //[ip]/[share name] -U [username] [password] #With creds
smbclient //[ip]/[share name] -N  #Null authentication


crackmapexec smb 10.10.11.222 -u [username] -p '' -M spider_plus #spider_plus module will run through all the shares and collect data about all the files
```

### CVEs - MSFCONSOLE

msf > use exploit/windows/smb/ms06_025_rasmans_reg     # Vulnerable: Windows RRAS / RASMAN service (older Windows XP/2000/2003 systems)
msf > use exploit/windows/smb/ms08_067_netapi          # Vulnerable: Windows Server service on unpatched Windows XP/Vista/Server 2003/2008
msf > use exploit/windows/smb/ms17_010_eternalblue     # Vulnerable: SMBv1 on unpatched Windows 7/Server 2008 R2 and related systems