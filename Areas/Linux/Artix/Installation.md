---
Title: Artix Runit Installation Guide
Author: S
---
# Artix Runit

## Check UEFI compatibility

```sh
ls /sys/firmware/efi/efivars
```

## Sync clock

```sh
timedatectl set-ntp true
```

## Format disk with fdisk

```sh
fdisk /dev/sda
```

### Primary Partition 1 (boot)

* sda1
* +1G
* /boot

### Primary Partition 2 (root)

* sda3
* +20G
* /

### Primary Partition 3 (home)

* sda4
* Usually all remaining space
* /home

## Create Filesystems

```sh
mkfs.ext4 -L ROOT /dev/sda2
mkfs.ext4 -L HOME /dev/sda3
```

For UEFI:
```sh
mkfs.fat -F32 /dev/sda1
fatlabel /dev/sda1 BOOT
```

For BIOS:
```sh
mkfs.ext4 -L BOOT /dev/sda1
```

## Mount Filesystems

```sh
mount /dev/disk/by-label/ROOT /mnt
mkdir /mnt/boot /mnt/home
mount /dev/disk/by-label/BOOT /mnt/boot
mount /dev/disk/by-label/HOME /mnt/home
```

## Install systemfiles

```sh
basestrap /mnt base base-devel runit elogind-runit linux linux-firmware vim
fstabgen -U /mnt >> /mnt/etc/fstab
```

## Switch to new system

```sh
artix-chroot /mnt
bash
```


# Bootloader

## Install grub

For BIOS:
```sh
pacman -S grub
grub-install --target=i386-pc /dev/sda
```

For UEFI:
```sh
pacman -S grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

## Configure grub

```sh
grub-mkconfig -o /boot/grub/grub.cfg
```

# Configure system

## Set up a network manager

```sh
pacman -S networkmanager networkmanager-runit
ln -s /etc/runit/sv/NetworkManager/ /etc/runit/runsvdir/current
```

## Set hostname

```sh
echo {hostname} > /etc/hostname #Replace {hostname} with desired hostname
```

## Set Root password

```sh
passwd
```

## Set Locale

```sh
vim /etc/locale.gen #Uncomment desired locals
echo LANG=nl-BE.UTF-8 > /etc/locale.conf
ln -sf /usr/share/zoneinfo/Europe/Brussels /etc/localtime
locale-gen
hwclock --systohc
```


# Finishing up Artix installation

* Close current sh with `exit`
* Unmount all drives with `umount -R /mnt`
* Reboot to new installation with `reboot now`