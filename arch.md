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
