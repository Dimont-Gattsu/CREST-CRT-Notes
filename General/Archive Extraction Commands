### ZIP Files
```
# List contents
unzip -l file.zip

# Extract (overwrite)
unzip -o file.zip

# Extract to directory
unzip file.zip -d /target/dir

# Extract password protected
unzip -P password file.zip
```

### 7z Files (p7zip-full)
```
# List contents
7z l file.7z

# Extract (preserve structure)
7z x file.7z

# Extract (flatten structure)  
7z e file.7z

# Extract to directory
7z x file.7z -o/target/dir

# Password protected
7z x file.7z -pPassword
```

### Gzip (.gz)
```
# List (with tar)
tar -tvzf file.tar.gz

# Extract
gunzip file.gz
# or
gzip -d file.gz

# Tar + Gzip
tar -xvzf file.tar.gz
tar -xvzf file.tar.gz -C /target/dir
```

### Bzip2 (.bz2)
```
# Extract single file
bunzip2 file.bz2

# Tar + Bzip2
tar -xvjf file.tar.bz2
```

### XZ (.xz)
```
# Extract single file
unxz file.xz
# or
xz -d file.xz

# Tar + XZ
tar -xvf file.tar.xz
```

### Tar (any compression)
```
tar -xvf file.tar          # Uncompressed
tar -xvzf file.tar.gz      # Gzipped
tar -xvjf file.tar.bz2     # Bzip2  
tar -xvf file.tar.xz       # XZ
tar -xvJf file.tar.Z       # Compress
```

**Quick universal:** `file filename` first to identify format, then use appropriate command above.
