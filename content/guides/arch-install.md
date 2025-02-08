---
title: Arch Linux Installation Guide on QEMU/KVM
---

**Warning**: If you are using Fedora be sure to add this to your network config

```bash
sudo nano /etc/libvirt/network.conf

firewall_backend = "iptables"
```


### Partition the disk
```bash
fdisk -l

cfdisk /dev/<disk_to_partition>
```
- Select *gpt* for label type
- Create new partition
- 500m for partition size, EFI System for type
-  Create new partition
- 4G for partition size, Linux Swap for type
- Create new partition
- Remanining size for partition size, Linux filesystem for type
- Select Write, type yes and select Quit
- Check if the partition is ok
```bash
fdisk-l
```
Device
/dev/vda1
/dev/vda2
/dev/vda3

### Format the partitions
```bash
mkfs.ext4 /dev/vda3
mkfs.fat -F 32 /dev/vda1
```
### Initialize the swap
```bash
mkswap /dev/vda2
```

### Mount the file system
```bash
mount /dev/vda3 /mnt
mount --mkdir /dev/vda1 /mnt/boot
swapon /dev/vda2
```
#### Check partititons
```bash
lsblk
```

### Pacman conf
```bash
nano /etc/pacman.conf
```
Uncomment ParallelDownloads = 5
Ctrl + O Enter Ctrl + X
### Install essential packages
```bash
pacstrap -K /mnt base linux linux-firmware nano base-devel
```

# Configure the system

### Fstab
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
### Chroot
```bash
arch-chroot /mnt
```
### Time
```bash
ln -sf /usr/share/zoneinfo/_Region_/_City_  /etc/localtime
hwclock --systohc
```
### Localization
```bash
nano /etc/locale.gen
```
Ctrl+W en_US Enter Uncomment(delete #) en_US.UTF-8 UTF-8
Ctrl+O Enter Ctrl+X
#### Generate locale
```bash
locale-gen
```
#### Set the language
```bash
nano /etc/locale.conf
```
LANG=en_US.UTF-8

### Host
```bash
nano /etc/hostname
```
user
#### Set password for root
```bash
passwd
```

#### Add permissions
```bash
useradd -m -G wheel -s /bin/bash user
```
#### Set password for user
```bash
passwd user
```

```bash
EDITOR=nano visudo
```
Uncomment this line by deleting #
```bash
%wheel ALL=(ALL:ALL) ALL
```

### Edit Loader.conf
```bash
bootctl install
nano /boot/loader/loader.conf
```
default arch.com
timeout 3
console-mode keep
editor no

```bash
nano /boot/loader/entries/arch.conf
```
title arch
linux /vmlinuz-linux
initrd /initramfs-linux.img
options root=/dev/vda3 rw

```bash
systemctl enable systemd-boot-update.service
```
```bash
pacman -Syu pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber networkmanager 
```
```bash
systemctl enable NetworkManager.service
```

### Check GPU
```bash
lspci
```
VGA compatible controller: Virtio GPU

```bash
pacman -S xf86-video-vesa mesa xorg-server plasma-meta kde-applications-meta sddm konsole dolphin kate

systemctl enable sddm.service --now
```
exit

unmount

reboot
