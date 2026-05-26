```
impacket-registry-read DOMAIN/user:Password123@TARGET-IP \
  -key "HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion" \
  -value ProductName
```

If you want all values under a key instead of just one:
```
impacket-registry-read DOMAIN/user:Password123@TARGET-IP \
  -key "HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion" \
  -enum_values
```
