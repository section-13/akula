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
	- >>> sudo grub-mkconfig -o /boot/grub/grub.cfg
		- Ubuntu should now be detected by Grub and added to the OS menu!
    
 # Black Arch Setup
 
 sudo pacman -S archlinux-keyring <br/>
 sudo pacman -s gnu-netcat  <br/>
 sudo pacman -Syu  <br/>
 
 sudo pacman -Rcns removes package and its dependencies as well. <br/>
 openbsd-netcat and gnu-netcat conflict - one of the repos doesn't have this conflict (openbsd-netcat), chose to install from that repo. 
- Remove all packages with -Rcns that have conflits with the incoming packages. 

 
