# Arch Linux

## Downgrading packages
```sh
cd /var/cache/pacman/pkg/
pacman -U <package_file_name>
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
