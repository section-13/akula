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

## Stop Hardware Wifi Scanning
Scan wifi networks and find AP BSSID: 
```
sudo iwlist scanning
```
Edit /etc/NetworkManager/system-connections/[network-name]
```
[wifi]
bssid=92:07:4F:2A:5E:49 # your bssid
mac-address-blacklist=
mode=infrastructure
seen-bssids=92:07:4F:2A:5E:49; # still your bssid
ssid=Heronnet
```
