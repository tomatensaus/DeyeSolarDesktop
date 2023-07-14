There are many ways to install home assistant.
If you are new to Home Assistant stick to the Home Assistant OS. (You will thank me later)
This is my favourite method as I mainly install on old laptops/desktops/mini pc (The processor can be fairly old but must support 64bit). Eufi boot would be nice but not strictly required (instructions below to boot with grub)

Write a bootable USB disk with Ventoy (usb boot utility) and the Latest Manjaro ISO. Other tools work just as well.
Plug in the network card (we need the network and home assistant needs a wired connection)
Plug the USB into the latop and on boot press F10. F11, F12 or F2 (whatever needed to get the boot menu to show)

Now boot from Ventoy into Manjaro command line
```
systemclt start sshd
ip addr
>>> Now look for the ip address, you are done working on this machine
```

From your desktop
```
ssh manjaro@192.168.4.1   #replace the ip with the one shown
empty password
sudo -i
wget https://github.com/home-assistant/operating-system/releases/download/10.3/haos_generic-x86-64-10.3.img.xz     #replace with the latest version or architecture you need to install
# assume /dev/sda is the hard drive of your home assistant
xzcat haos_generic-x86-64-10.3.img.xz | dd of=/dev/sda bs=1m
```
If your machine supports UEFI you can reboot and it should boot
If UEFI is not supported the load grub below

```
# assume /dev/sda is the hard drive of your home assistant
mount /dev/sda1 /mnt    #this is the EFI boot partition
grub-install --boot-directory=/mnt/boot --force /dev/sda

```
Then just create a /mnt/boot/grub/grub.cfg with the following content:

```
set root=(hd0,gpt1)
configfile (hd0,gpt1)/efi/boot/grub.cfg
```
Now you are done and ready to reboot into Home Assistant
```
reboot
```
Take bootable USB out
Your home assistant server should boot
