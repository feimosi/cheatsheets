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
- Use chroot with `arch-chroot /mnt`.
- If the system uses default database and directory locations, you can now update the system's pacman database and upgrade it via `pacman --root=/mnt --cachedir=/mnt/var/cache/pacman/pkg -Syyu` as root.

See more here: [https://wiki.archlinux.org/index.php/pacman](https://wiki.archlinux.org/index.php/pacman#Manually_reinstalling_pacman).

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

## Entering the recovery mode

- in GRUB menu press `e` to edit the linux kernel's run entry
- append `rescue` string at the end 
- press Ctrl + X to approve the changes
