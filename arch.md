# Arch Linux

## Reinstall a package
```sh
pacman -S <pkg_name>
```

## Downgrading packages
```sh
cd /var/cache/pacman/pkg/
pacman -U <pkg_file_name>
```

## Pacman history
```sh
/var/log/pacman.log
```

## Repairing the Pacman database

- Boot using the Arch installation media.
- Mount the system's root filesystem, e.g. `mount /dev/sdaX /mnt` as root.
- If the system uses default database and directory locations, you can now update the system's pacman database and upgrade it via `pacman --root=/mnt --cachedir=/mnt/var/cache/pacman/pkg -Syyu` as root.

See more here: [https://wiki.archlinux.org/index.php/pacman](https://wiki.archlinux.org/index.php/pacman#Manually_reinstalling_pacman).

## Switch environment from live to installed system
```sh
arch-chroot /mnt
```

## Bypass invalid or corrupted package (PGP signature) error

```sh
pacman -U /var/cache/pacman/pkg/antergos-keyring-*.pkg.tar.xz
```

This work, since pacman doesn’t check sigs on local packages by default. 

## Skip a package from being upgraded
```sh
vim /etc/pacman.conf
IgnorePkg=<pkg1> <pkg2>
```

## Start a service on system boot:
```sh
sudo systemctl enable <service_name>
```

## Copy to clipboard
```sh
cat ~/.ssh/id_rsa.pub | xclip -selection clipboard 
```

## View the entire file with highlighted matches
```sh
egrep --color 'pattern|$' <file>
```

## Clean old journal logs
```sh
journalctl --vacuum-size=500M
```

## Clean old pacman packages
```sh
paccache -d -k 1
paccache -r -k 1
```

## Entering the recovery mode

- in GRUB menu press `e` to edit the linux kernel's run entry
- append `rescue` string at the end 
- press Ctrl + X to approve the changes

## `error while loading shared libraries: libicuuc.so: cannot open shared object file: No such file or directory`

- boot into a live system
- `mount /dev/sdaX /mnt`
- `pacman -r /mnt -Syu`

_If needed_

```sh
sudo mount -t proc /dev/sdaX /mnt/proc
sudo mount -t devtmpfs /dev/sdaX /mnt/dev
sudo mount -t sysfs /dev/sdaX /mnt/sys
```

## Restore GRUB on an encrypted disk

NOTE: Make sure to boot the Live USB in the UEFI mode

- sudo su
- cryptsetup open /dev/sdaX CryptName
- mount /dev/mapper/CryptVolumeGroupName-rootvol /mnt
- mount /dev/sda2 /mnt/boot
- mount /dev/sda1 /mnt/boot/efi
- arch-chroot /mnt
- grub-mkconfig -o /boot/grub/grub.cfg
- grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Antergos-grub
