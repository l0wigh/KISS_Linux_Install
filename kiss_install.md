# KISS Linux Install Guide

This is my own way to install KISS Linux on "any" computer.

- Features :
    - EFI System
    - Grub
    - Stripped down Archlinux Kernel

## Preparation

- Download latest archlinux iso
- Download a lightweight live distro like Antix
- Boot Lightweight distro
- Create and format partitions (EFI 600mb / Swap 2*RAM / Filesystem)
- Mount Filesystem on /mnt
- `mkdir /mnt/boot`
- Mount EFI on /mnt/boot
- Download KISS chroot
- cd /mnt && tar xvf KISS chroot

## Chroot (Stage 1) 

- `/mnt/bin/kiss-chroot /mnt`
- `swapon /dev/sdXX`
- `cd /root && mkdir repos && cd repos`
- `git clone https://codeberg.org/kiss-community/repo && git clone https://codeberg.org/kiss-community/community`
- Activate repos signatures as shown in the READMEs
- `export KISS_PATH="$HOME/repos/repo/core:$HOME/repos/repo/extra:$HOME/repos/community/community:$KISS_PATH"`
- `kiss update`
- `cd /var/db/kiss/installed && kiss build *`
- `kiss b grub efibootmgr e2fsprogs wpa_supplicant dhcpcd libelf perl zstd baseinit bkeymaps util-linux`
- `cd /root && mkdir tools && cd tools && curl -fLO https://raw.githubusercontent.com/cemkeylan/genfstab/refs/heads/master/genfstab && chmod +x genfstab`
- `genfstab > /etc/fstab`
- Add swap partition to /etc/fstab : `/dev/sdXX none swap sw 0 0`
- `cd /root && mkdir kernel && cd kernel`
- Curl latest kernel (or something close or equal to the last archlinux one)
- `curl -fLO https://gitlab.archlinux.org/archlinux/packaging/packages/linux/-/blob/main/config`
- `tar xvf linux...`

## Chroot (Stage 2)

- Reboot to Archlinux iso
- Activate and connect to wifi with iwctl
- Activate usb tethering
- Mount Filesystem on /mnt
- Mount EFI on /mnt/boot
- `/mnt/bin/kiss-chroot /mnt`
- `swapon /dev/sdXX`
- `cd /root/kernel/linux... && cp ../config ./.config`
- Edit arch/x86/Makefile to find and remove the posttest part (kinda useless and very long for us)
- `make localyesconfig && make && make modules && make modules_install && make install`
- `mv /boot/vmlinuz /boot/vmlinuz-VERSION`
- `mv /boot/System.map /boot/System.map-VERSION`
- `grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`
- `grub-mkconfig -o /boot/grub/grub.cfg`
