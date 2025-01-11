# Macbook Air Specific instructions

## Wifi

- Download latest tarball from https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git and extract it.
- Copy brcm/bcm43xx-0.fw and brcm/bcm43xx_hdr-0.fw inside /usr/lib/firmware/brcm/
- Add the necessary option to the kernel (I don't remember, search it up).
- Compile and install kernel, then reboot.
- You should be able to use wpa_supplicant with wlan0 now.
