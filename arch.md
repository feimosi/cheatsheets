# Arch Linux

## Reinstall a package
```sh
pacman -S <pkg_name>
```

## Downgrading packages

Pacman
```sh
cd /var/cache/pacman/pkg/
pacman -U <pkg_file_name>
```

Yay
```sh
cd ~/.cache/yay/<package_folder>
pacman -U <file_name>.pkg.tar.zst     
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

## Show journal errors since the last boot
```sh
journalctl -p 3 -xb -1 
```

## Cut the video file
```sh
ffmpeg -i video.mp4 -ss 00:00:00 -t 00:00:20 -async 1 out.mp4
```

## Scale the video file
```sh
ffmpeg -i input.mp4 -vf scale=400:-2 output400.mp4
```

## Concatenate video files
```sh
printf "file '%s'\n" ./*.mp4 > mylist.txt
ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.mp4
```

## Compress the video file
```sh
ffmpeg -i input.mp4 -vcodec libx265 -crf 28 output.mp4
```
Note: a reasonable CRF range for H.265 may be 24 to 30 - lower CRF values correspond to higher bitrates, and hence produce higher quality videos.\
Source: https://unix.stackexchange.com/a/38380

## Clean old pacman packages
```sh
paccache -ruk0 # remove all uninstalled packages
paccache -dk 2 # dry-run
paccache -rk 2 # remove older than 2 last versions
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

> In case of the following error: `Waiting 30 seconds for device ‘/dev/disk/by-label/` <br>
  `cd dev/disk/by-label` <br>
  `ls` <br>
  `mv [Current name] [Missing name]`

- sudo su
- cryptsetup open /dev/sdaX CryptName
- mount /dev/mapper/CryptVolumeGroupName-rootvol /mnt
- mount /dev/sda2 /mnt/boot
- mount /dev/sda1 /mnt/boot/efi
- arch-chroot /mnt
- grub-mkconfig -o /boot/grub/grub.cfg
- grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Antergos-grub

UPDATED:

With Rufus v3 make bootable USB in UEFI (MBR) mode. F12 to show the boot menu.

- sudo su
- \# (optional) check partitions IDs  
  fdisk -l 
- cryptsetup open /dev/nvme0n1p7 mycrypt
- mount /dev/mapper/mycrypt /mnt
- \# list volumes  
  btrfs subvolume list -p /mnt 
- umount /mnt
- mount -o subvol=@ /dev/mapper/mycrypt /mnt
- mount -o subvol=@log /dev/mapper/mycrypt /mnt/var/log
- mount -o subvol=@cache /dev/mapper/mycrypt /mnt/var/cache
- mount -o subvol=@home /dev/mapper/mycrypt /mnt/home
- mount /dev/nvme0n1p6 /mnt/boot/
- mount /dev/nvme0n1p1 /mnt/boot/efi
- arch-chroot /mnt/
- grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=EndeavourOS-grub
- grub-mkconfig -o /boot/grub/grub.cfg

➡ https://discovery.endeavouros.com/system-rescue/repair-a-non-booting-grub/2021/03/

## Encrypt external drive

1. In GParted, change partition table from MSDOS to GPT
1. Create an unformatted partiion on the disk 
1. Check partiion ID with `lsblk --fs`, e.g. sda1
1. `sudo cryptsetup luksFormat /dev/sda1`
1. `sudo cryptsetup open /dev/sda1 drive` -> `lsblk` -> "drive" should appear on the list
1. `sudo mkfs.btrfs /dev/mapper/drive`
1. `sudo mount /dev/mapper/drive /mnt/`
1. `sudo chown marek:marek /run/media/marek/c0bfaf54-8574-4ac1-ab9a-db166deb96e9` - set the correct ID from `lsblk`
1. `sudo umount /mnt`
1. `sudo cryptsetup close drive`

➡ https://www.youtube.com/watch?v=ZNaT03-xamE

## Reinstall all packages

chroot steps from above and then:

```sh
pacman -Qqn | pacman -S -
```

force reinstall a specific package:

```sh
pacman -S --overwrite "*" linux
```

## Changing default app

Check the current default for mime type:
```sh
xdg-mime query default inode/directory
```

Update the default:
```sh
xdg-mime default org.gnome.Nautilus.desktop inode/directory
```

➡ https://www.youtube.com/watch?v=z3F0hTigMvU

## List packages that depend on a package 

```sh
pacman -Qi ruby-xdg | grep 'Required'  
```

## Strip metadata from image files

```sh
mogrify -auto-orient -strip ./*.jpg
```

## Compress and resize images to reduce size

```sh
mogrify -resize 70% -quality 75 *.jpg
```

## Convert images into a PDF file

```sh
convert *.jpg -quality 75 Scanned.pdf
```

## Show image GPS metadata

```sh
exiv2 -g "Exif.GPSInfo"  photo.jpg  
```

## Reset image GPS metadata

```sh
exiv2 -M "set Exif.GPSInfo.GPSLongitude 0/1 0/1 0/1" photo.jpg  
exiv2 -M "set Exif.GPSInfo.GPSLatitude 0/1 0/1 0/1" photo.jpg  
```
