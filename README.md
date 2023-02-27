# akula-setup

# OS Install

1. Install Ubuntu
	/dev/sda1: /boot
	/dev/sda2: /boot/efi
	/dev/sda3: /

2. Install BlackArch
	/dev/sda1: Overwrite with /boot
	/dev/sdas2: Overwrite with /boot/efi flag: boot
	/dev/sda4: Encrypted /
3. Reinstall Ubuntu
	/dev/sda3: / Install the bootloader on /dev/sda3
4. Boot into Arch 
	- May need to use F12 Boot Menu to select the UEFI Arch Option. 
	- The UEFI Boot menu can be used to make arch grub the default again if it got displaced by Ubuntu
	- Add this line at the end of /etc/default/grub: 
		GRUB_DISABLE_OS_PROBER=false
	- sudo grub-mkconfig -o /boot/grub/grub.cfg
		- Ubuntu should now be detected by Grub and added to the OS menu!
    
 # Black Arch Setup
 ```
 sudo pacman -Sy <- must do this first before installing the keyring
 sudo pacman -S archlinux-keyring <br/>
 sudo pacman -S gnu-netcat  <br/>
 sudo pacman -S blackarch <br/>
 ```
 
 --noconfirm flag defaults yes to eveything
 - sudo pacman -Rcns removes package and its dependencies as well. <br/>
 - openbsd-netcat and gnu-netcat conflict - one of the repos doesn't have this conflict (openbsd-netcat), chose to install from that repo. 
- Remove all packages with -Rcns that have conflits with the incoming packages. 
- Use the --ignore flag for packages that can't be found
- Mirrors are in /etc/pacman.d try different mirrors when some don't have required packages

Keyring permission problems: <br/>
```
pacman-key --init
pacman-key --populate archlinux
```

# tor
sudo pacman -S tor <br/>
sudo systemctl start/enable tor
- Change networkmanagers and dns config to use 127.0.0.1:9050 (or tell firefox to use this address as a proxy for just firefox tor) 
