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
	```
		GRUB_DISABLE_OS_PROBER=false
	```
	Then run: 

	```
	sudo grub-mkconfig -o /boot/grub/grub.cfg
	```
	Ubuntu should now be detected by Grub and added to the OS menu!
    
 # Black Arch Setup
 ```
 sudo pacman -Sy  <- must do this first before installing the keyring
 sudo pacman -S archlinux-keyring 
 pacman-key --init
 pacman-key --populate archlinux
 pacman-key --refresh-keys
 
 sudo pacman -S gnu-netcat  
 sudo pacman -Syu
 
 sudo pacman -S blackarch 
 ```
 If a package sig is failing, download it individually and install it individually. 
 ```
 sudo pacman -U [downloaded package]
 ```
 
 --noconfirm flag defaults yes to eveything
 - sudo pacman -Rcns removes package and its dependencies as well. <br/>
 - openbsd-netcat and gnu-netcat conflict - one of the repos doesn't have this conflict (openbsd-netcat), chose to install from that repo. 
- Remove all packages with -Rcns that have conflits with the incoming packages. 
- Use the --ignore flag for packages that can't be found
- Mirrors are in /etc/pacman.d try different mirrors when some don't have required packages
- To skip installing a package: ^[package number] will exclude that package from install. 
- the --overwrite '*' flag will overwrite packages that are existing if they conflict <- danger this may break the system

# Reinstall Grub

Mount LUKS partition
```
sudo cryptsetup luksOpen /dev/sda2/ my_vol
sudo mount /dev/mapper/my_vol /mnt
```
chroot
```
sudo arch-chroot /mnt
```
Mount fs and install 
```
sudo mount /dev/sdaX /boot/efi/
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
```

# tor
sudo pacman -S tor <br/>
sudo systemctl start/enable tor
- Change networkmanagers and dns config to use 127.0.0.1:9050 (or tell firefox to use this address as a SOCKS proxy for just firefox tor) 

# Encrypting External Drives
Destroy the drive's partition table by overwriting the drive's head with zeros:
```
lsblk
sudo dd if=/dev/zero of=/dev/sdX count=4096
sudo cryptsetup luksFormat /dev/sdX
```
To Mount LUKS: 
```
cryptsetup open /dev/sdX [drive name (any)]
ls /dev/mapper  # To check the drive was mounted
cryptsetup close [drive name] # To close the drive
```
Make fs on drive: 
```
sudo mkfs -t ext4 /dev/mapper/[drive name]


```
Mount / Unmount LUKS: 
```
sudo cryptsetup open /dev/sdX vaultdrive
sudo mount /dev/mapper/vaultdrive /mnt/hd
```
# Arch Backup with Tar
1. Boot from live CD
2. chroot
```
sudo mkdir /mnt/arch
sudo cryptsetup open /dev/sda1 dr
sudo mount /dev/mapper/dr /mnt/arch
sudo mount /dev/sda2 /mnt/arch/boot/efi
cd /mnt/arch
sudo chroot . /bin/bash
```
3. Run the backup script

## Restoring
To restore from a previous backup, mount all relevant partitions, change the current working directory to the root directory, and execute
```
$ bsdtar --acls --xattrs -xpzf backupfile
```
replacing backupfile with the backup archive. Removing all files that had been added since the backup was made must be done manually. Recreating the filesystem(s) is an easy way to do this. 

# Encrypt Home Drive (Ubuntu or if entire disk is not Encrypted) 
```
sudo apt install ecryptfs-utils cryptsetup
```
1. Create New User
2. Login to new user and run
```
sudo ecryptfs-migrate-home -u <user1>
```
3. Login to old user and get the passphrase (no rebooting before this)
```
ecryptfs-unwrap-passphrase
```

# Changing Passphrase on LUKS
Note the keyslot after the first command: 
```
sudo cryptsetup --verbose open --test-passphrase /dev/sda1
sudo cryptsetup luksChangeKey /dev/sda1 -S [keyslot]
```
# Installing frrm AUR
Example Brave 
```
git clone https://aur.archlinux.org/brave-bin.git
cd brave-bin
makepkg -si
```
