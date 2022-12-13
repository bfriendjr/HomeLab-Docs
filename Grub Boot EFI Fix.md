# # Grub Boot EFI Fix

You can skip installation of grub.

After your installation is complete boot into kali-live and run these commands:
<br/>
<br/>
```powershell
sudo -i passwd root
```
```powershell
sudo mount /dev/sda* /mnt
```
```powershell
sudo mkdir /mnt/dev
```
```powershell
sudo mkdir /mnt/proc
```
```powershell
sudo mkdir -p /mnt/sys/firmware/efi/efivars
```
```powershell
sudo mount -—bind /dev /mnt/dev
```
```powershell
sudo mount -—bind /proc /mnt/proc
```
```powershell
sudo mount -—bind /sys /mnt/sys
```
```powershell
sudo mount -—bind /sys/firmware/efi/efivars /mnt/sys/firmware/efi/efivars
```
```powershell
sudo mkdir -p /mnt/boot/efi
```
```powershell
su root
```
```powershell
sudo mount /dev/sda+ /mnt/boot/efi
```
```powershell
sudo mount -o remount,rw /dev/sda+ /mnt/boot/efi
```
```powershell
sudo mkdir /mnt/hostrun
```
```powershell
sudo mount -—bind /run /mnt/hostrun
```
```powershell
sudo chroot /mnt
```
```powershell
sudo mkdir /run/lvm
```
```powershell
mount —-bind /hostrun/lvm /run/lvm
```
```powershell
sudo grub-install /dev/sda
```
```powershell
sudo update-grub
```
```powershell
exit
```
```powershell
sudo umount /mnt/dev
```
```powershell
sudo umount /mnt/proc
```
```powershell
sudo umount /mnt/sys/firmware/efi/efivars
```
```powershell
sudo umount /mnt/sys
```
```powershell
sudo umount /mnt/boot/efi
```
```powershell
sudo umount /mnt/hostrun
```
```powershell
sudo umount /mnt/run/lvm
```
```powershell
sudo umount /mnt
```

REBOOT and remove thumb drive.

``/dev/sda*`` is your linux filesystem. Like mine is /dev/sda3.<br/>
``/dev/sda+`` is your EFI partition which is most likely /dev/sda1.<br/>
Use **fdisk -l** to list all partitions.<br/>
/dev/sda in ``grub-install /dev/sda`` is the name of your storage device, not the name of partition. Use ``fdisk -l`` to see the name of your storage device.
<br/><br/><br/>
#HomeLab/Kali