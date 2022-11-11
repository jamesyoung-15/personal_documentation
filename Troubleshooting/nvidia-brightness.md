# My Laptop Issue (Pop OS)

## Brightness keyboard control not working with discrete NVIDIA GPU on laptop
On my Lenovo Legion 5 laptop with AMD 4800h and NVIDIA 2060 running POP OS, brightness control doesn't work once I switch to discrete GPU for some reason. This didn't occur on older versions of NVIDIA drivers so it's a driver issue. 

Issue seems to be with backlight in `/sys/class/backlight`. More specifically on my device I have `amdgpu_bl0` and `nvidia_0` modules in `/sys/class/backlight`. When I'm in integrated, the brightness control on the keyboard changes the value of `/sys/class/backlight/amdgpu_b10/brightness` which works as intended. However when I switch to discrete GPU when I try to change brightness with keyboard it writes the value to `/sys/class/backlight/nvidia_0/brightness` but it does nothing to the brightneess.

My quick fix is just to write this into a bash script and also an alias in `.bashrc` and run it if I need to change brightness. Not great but since I don't often change brightness on discrete GPU it's good enough.
``` bash
#!/bin/bash

read -p 'Input brightness (0-255): ' brightness

echo $brightness | sudo tee /sys/class/backlight/amdgpu_bl0/brightness
```

Best solution would be to downgrade NVIDIA driver to something like 470.xx (when brightness didn't fuck up) but wtv.

Resources: 
- https://wiki.archlinux.org/title/backlight
- https://gist.github.com/x1unix/67c154d42aa5c8333f43a69acceff635 (solution here didn't work for me but still useful info)