---
title: Arch Linux Installation Guide on QEMU/KVM
---

**Warning**: If you are using Fedora be sure to add this to your network config
```
sudo nano /etc/libvirt/network.conf

firewall_backend = "iptables"
```


### Partition the disk
```
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
```
fdisk-l
```
Device
/dev/vda1
/dev/vda2
/dev/vda3

### Format the partitions
```
mkfs.ext4 /dev/vda3
mkfs.fat -F 32 /dev/vda1
```
### Initialize the swap
```
mkswap /dev/vda2
```

### Mount the file system
```
mount /dev/vda3 /mnt
mount --mkdir /dev/vda1 /mnt/boot
swapon /dev/vda2
```
#### Check partititons
```
lsblk
```

### Pacman conf
```
nano /etc/pacman.conf
```
Uncomment ParallelDownloads = 5
Ctrl + O Enter Ctrl + X
### Install essential packages
```
pacstrap -K /mnt base linux linux-firmware nano base-devel
```

# Configure the system

### Fstab
```
genfstab -U /mnt >> /mnt/etc/fstab
```
### Chroot
```
arch-chroot /mnt
```
### Time
```
ln -sf /usr/share/zoneinfo/_Region_/_City_  /etc/localtime
hwclock --systohc
```
### Localization
```
nano /etc/locale.gen
```
Ctrl+W en_US Enter Uncomment(delete #) en_US.UTF-8 UTF-8
Ctrl+O Enter Ctrl+X
#### Generate locale
```
locale-gen
```
#### Set the language
```
nano /etc/locale.conf
```
LANG=en_US.UTF-8

### Host
```
nano /etc/hostname
```
user
#### Set password for root
```
passwd
```

#### Add permissions
```
useradd -m -G wheel -s /bin/bash user
```
#### Set password for user
```
passwd user
```

```
EDITOR=nano visudo
```
Uncomment this line by deleting #
```
%wheel ALL=(ALL:ALL) ALL
```

### Edit Loader.conf
```
bootctl install
nano /boot/loader/loader.conf
```
default arch.com
timeout 3
console-mode keep
editor no

```
nano /boot/loader/entries/arch.conf
```
title arch
linux /vmlinuz-linux
initrd /initramfs-linux.img
options root=/dev/vda3 rw

```
systemctl enable systemd-boot-update.service
```
```
pacman -Syu pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber networkmanager 
```
```
systemctl enable NetworkManager.service
```

### Check GPU
```
lspci
```
VGA compatible controller: Virtio GPU

```
pacman -S xf86-video-vesa mesa xorg-server plasma-meta kde-applications-meta sddm konsole dolphin kate

systemctl enable sddm.service --now
```
exit
reboot
