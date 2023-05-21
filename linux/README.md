1. Put arch on a flash drive (on mac it's extremely simple with `dd`)

https://wiki.archlinux.org/title/USB_flash_installation_medium

```
dd if=path/to/archlinux-x86_64.iso of=/dev/diskX bs=1m` 
```

2. boot into usb 
3. run `archinstall` (probably use `grub`)
4. `xorg` profile just installs base linux with the packages necessary for gpu drivers
5. configure networking from here with static IP

If you check `pacman -Qqe` this is pretty much what you'll see:
```
base
base-devel
efibootmgr
grub
intel-ucode
linux
linux-firmware
nvidia
xorg-server
xorg-xinit
```

These are pretty great:
```
tmux
vim
openssh
git
tailscale
```

Notes:
- make sure to `systemctl enable` your services (i.e. `sshd` and `tailscaled` so that they start on boot - this way you can easily remotely reboot your server)

This is pretty much all you need for a capable home workstation that you can throw in your closet and access from anywhere.