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

## Start a service on system boot:
```sh
sudo systemctl enable <service_name>
```
