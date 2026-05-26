### Search for Exploits
```bash
# Basic search
searchsploit apache 2.4.49
searchsploit mysql 5.5
searchsploit --cve 2021-44228

# Title only (faster, less noise)
searchsploit -t apache 2.4.49

# Exact match
searchsploit -e wordpress 5.2.3

# Exclude PoC/DoS
searchsploit linux kernel 4.4 --exclude="(PoC)|dos"

# Update database first
searchsploit -u
```

### Find & Get Exploit Path
```bash
# Get path/ID of specific exploit
searchsploit -p 49705
# Output: /usr/share/exploitdb/exploits/linux/remote/49705.py
```

### Copy Exploit to Current Directory
```bash
# Mirror (copy) exploit to cwd
searchsploit -m 49705
# Creates: 49705.py in current directory
```

***

## MSFconsole - Load Searchsploit Exploit

### Method 1: Direct path (most reliable)
```bash
msfconsole
msf6 > use /usr/share/exploitdb/exploits/linux/remote/49705.py
# OR copy first:
searchsploit -m 49705
msf6 > use ./49705.py
```

### Method 2: If already in exploits/
```bash
# After searchsploit -m 49705
msf6 > search apache
msf6 > use exploit/linux/http/apache_modcgi_bash_env_exec
```

### Method 3: By EDB-ID
```bash
msf6 > search edb-49705
msf6 > use [matching_module]
```

**Workflow:**
1. `searchsploit apache 2.4.49` → Find EDB-ID (e.g. `49705`)
2. `searchsploit -p 49705` → Get full path
3. `searchsploit -m 49705` → Copy to current dir
4. `msfconsole`
5. `use ./49705.py` → Load exploit
6. `set RHOSTS 10.10.10.10`
7. `exploit`

**Pro tip:** Always `searchsploit -u` before searching!
