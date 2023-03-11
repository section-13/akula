# Location Security
1. Mask Geoclue
```
sudo systemctl mask geoclue
```
2. Stop WLAN scanning (see network section)

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

# Disable WebRTC

WebRTC in Firefox
```
    To disable WebRTC in Firefox:
    Type about:config in the address bar and press Enter.
    In the search bar, type media.peerconnection.enabled and double-click the preference to set its value to false.
```

