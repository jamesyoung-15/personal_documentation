# Overclocking with AMD GPU

I use CoreCtrl software on Linux for AMD GPU. Worked on my RX 570 and RX 6900XT. However need to add kernel parameter to unlock more features. More specifically add `amdgpu.ppfeaturemask=0xffffffff` to `/etc/default/grub` in the `GRUB_CMDLINE_LINUX_DEFAULT=` line then regenerate bootloader with `grub-mkconfig -o /boot/grub/grub.cfg`. 

More info: https://github.com/BeanGreen247/Linux_NVIDIA_GPU_Overclocking_Guide

# NVIDIA GPU

I haven't tested on my laptop NVIDIA GPU but useful link for reference in future: https://github.com/BeanGreen247/Linux_NVIDIA_GPU_Overclocking_Guide

