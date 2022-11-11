# Broken grub and can't boot. (UEFI)

## Mounting disks:
1. Boot from Arch or other distros using USB or other disk. Open up terminal.
2. Check drive name and partitions of drive and note label using: ` lsblk ` or `fisk -l`. For example I want to fix arch install on my ssd nvmen1 with partitions nvmen1p1 (boot) and nvmen1p2 (swap) and nvmen1p3 (root).
3. Mount root partition using `mount /dev/root_partition mnt`.
4. Mount boot partition using `mount /dev/boot_partition mnt/boot/efi`
## Reinstall grub
5. Run `pacman -S grub efibootmgr os-prober` just in case.
6. Use `grub-install` command. Arch-wiki says use `
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub` but for my case using `grub-install /dev/nvmen1` to work.
7. `grub-mkconfig -o /boot/grub/grub.cfg`

## Notes
Couldn't boot to Arch cause I messed around with grub Nov 10, 2022. Very quick fix.
Useful links: 
- https://wiki.archlinux.org/title/GRUB
- https://www.addictivetips.com/ubuntu-linux-tips/re-install-grub-on-arch-linux/