# Location Security
1. Mask Geoclue
```
sudo systemctl mask geoclue
```
2. Stop WLAN scanning (see network section)

## MAC Address Randomization
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

# Firefox Browser Settings
## Disable WebRTC
WebRTC in Firefox
```
    To disable WebRTC in Firefox:
    Type about:config in the address bar and press Enter.
    In the search bar, type media.peerconnection.enabled and double-click the preference to set its value to false.
```
## Disable WebGL
```
about:config
webgl.disabled
```
## Enable Fingerprinting Protection
Note: This one causes white flashes while running the browser in dark mode
```
about:config
privacy.resistFingerprinting
privacy.resistFingerprinting.block_mozAddonManager
```

# Disable Camera
```
# Once
sudo modprobe -r uvcvideo

# All
cd /etc/modprobe.d
echo "blacklist uvcvideo" > nocamera.conf"

# View modules
lsmod
```
