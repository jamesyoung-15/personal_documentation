# Installing Arch-ARM on Raspberry Pi
NOTE: Tested on my Raspberry PI 3B+ haven't tried on other Raspberry devices.

Install relevant Arch ARM from: https://archlinuxarm.org/about/downloads. Can use wget eg: `wget http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-armv7-latest.tar.gz`.
## Format, Partition, Mount, and Transfer Drive
1. Insert microSD or whatever storage that's used for boot.
2. `sudo fdisk -l` to get device then format with `sudo fdisk /dev/device_name`.
3. Type `o` to purge any pre-existing partitions, make sure nothing important in there. Can type `p` to check partitions. Create boot partition by typing `n` for new partition then `p` for primary and press `ENTER` to use default first sector then `+100M` for last sector.
4. Type `t` then `c` to set first partition to type W95 FAT32 (LBA).
5. Create Root partition by typing `n` for new partition then `p` for primary. Type `2` for second partition on drive then set it to your desired size. For most cases I just accept default and use rest of storage.
6. Write partition with `w`.
7. Create filesystem for boot and root partition using mkfs and mount it with commmands below:
``` bash
mkfs.vfat /dev/device_name_partition1
mkfs.ext4 /dev/device_name_partition2
mkdir boot
mkdir root
sudo mount /dev/device_name_partition1 ./boot
sudo mount /dev/device_name_partition2 ./root
```
8. Extract content of Arch Arm content to root. Eg if using ArchLinuxARM-rpi-armv7-latest.tar.gz then use: `sudo tar -xpf ArchLinuxARM-rpi-armv7-latest.tar.gz -C ./root` then `sync`.
9. Move boot files to boot partition using `mv root/boot* boot`.
10. Unmount partitions with `umount boot root`.

Now when inserting the disk into a Raspberry PI the PI should boot to Arch ARM. 
## Post-Installion Setup
Best practice is to use ethernet and setup ssh to PI if possible. 
### Wifi:
``` bash
cd /etc/wpa_supplicant
vim home-network # can also use nano or other terminal editor if vim not installed
```
In home-network file enter:
```
network={
  ssid="YOURSSID"
  psk="YOURWIFIPASSWORD"
}
```
Run below command to connect:
``` bash
wpa_supplicant -i wlan0 /etc/wpa_supplicant/home-network &
dhcpcd wlan0 #gets DHCP address
```
Haven't tested this is based on wiki not sure if it works. Preferable to use ethernet. Also alternative if possible is to use `wifi-menu` but this command is discontinued in original Arch so uncertain if works.

### Pacman and AUR
Update keys for Pacman
``` bash
pacman-key --init
pacman-key --populate archlinuxarm
pacman -Syu
```
AUR Helper (Using Paru but same for yay)
``` bash
sudo pacman -S git
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```
### User setup
``` bash
passwd #set password for root
pacman -S sudo vim # if vim not installed, not necessary if using nano
# Below creates user and allows it to use sudo
visudo # Search for the line that contains `%wheel ALL=(ALL) ALL` and uncomment it. Save the file.
useradd -d /home/YOURUSERNAME -m -G wheel -s /bin/bash YOURUSERNAME # create your user 
passwd YOURUSERNAME # set password for created user
userdel alarm # optionally delete user alarm
exit # optionally exit out of root then you can login to user
```
Optionally set hostname with: `hostnamectl set-hostname YOURHOSTNAME`

### I/O Pins
GPIO: To be able to use the GPIO pins from Python, use the RPi.GPIO library. Install this using pip install, the AUR package wiki list doesn't seem to exist or something. 

For more post-installation setup, check https://archlinuxarm.org/wiki/Raspberry_Pi, but note it's a bit outdated/not all packages listed are available anymore. Check forum tab or google other things.
