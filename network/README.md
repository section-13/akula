# Sockets and Port Connection Analysis

## Netstat
Port Connections
```
netstat
```

## SS
Sockets analyzer
```
ss -aln | grep [port]
```

# MAC Address Randomization
```
# Add to /etc/NetworkManager/NetworkManager.conf
# Configuration file for NetworkManager.
# See "man 5 NetworkManager.conf" for details.

[device]
wifi.scan-rand-mac-address=yes

[connection]
wifi.cloned-mac-address=random
ethernet.cloned-mac-address=random
connection.stable-id=${CONNECTION}/${BOOT}
```
