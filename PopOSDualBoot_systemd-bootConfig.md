# How to Modify `systemd-boot`
1. [Deal with the new systemd-boot (and set a default Windows entry)](https://medium.com/@mijorus/deal-with-the-new-systemd-boot-and-set-a-default-windows-entry-be1814a0c975)
2. [Tech Republic](https://www.techrepublic.com/article/how-to-modify-systemd-boot-on-linux/)
3. [Reddit](https://www.reddit.com/r/pop_os/comments/gjsr6r/psa_how_to_dual_boot_pop_os_with_windows_with_a/)
4. [Installing Pop! OS alongside Windows 10 on different hard drives](https://www.reddit.com/r/pop_os/comments/cju5ym/installing_pop_os_alongside_windows_10_on/)

# Pop!\_OS
After installing Pop!\_OS on my second SSD I found that I could only access Pop!\_OS by restarting the laptop and accessing the [Windows Boot Options Menu](https://www.hongkiat.com/blog/best-ways-access-windows-10-boot/). Although a minor inconvenience, it tripled my boot time for booting into Pop!\_OS. 

After searching for ways around this, I found that options I used in the past, such as EasyBCD that work from the Windows side, did not offer UEFI support. Convinced that Windows would not solve my problem, I attacked it from the Linux side. Options I have used in the past include GRUB2 but I quickly found out Pop!\_OS switched from GRUB2 to `systemd-boot`.

* [GRUB vs systemd-boot](https://www.maketecheasier.com/grub-vs-systemd-boot/)

## `systemd-boot` VS `grub2`
So what are the differences between `systemd-boot` and `grub2`? They are both multi-boot boot loaders that allow users to select between all installed kernels on the system.  

#### `systemd-boot`
`systemd-boot` is smaller and less configurable than `grub2`. It is more easily configurable than `grub2` because it allows users control over installing kernels with config files. The only downsides to `systemd-boot` are it's text only interface and lower number of config options.

#### `grub2`
GRUB is known for being highly configurable and breaking easily due to chain-loaded kernels. Kernels and new operating systems cannot be just "dropped in".

# Create a Windows Entry in `systemd-boot`
1. install and run `os-prober` to find out where Windows boot manager is. Should look like: `/dev/sdb1@/EFI/Microsoft/Boot/bootmgfw.efi:Windows Boot Manager:Windows:efi`
2. run `mount /dev/sdb1 /mnt` to mount the partition containing the windows boot manager.
3. Copy the `Microsoft` folder to linux and place in `/boot/efi/EFI`.

# Linux Commands
| Command | Description |
| :---:   | :---:       |
| os-prober | lists operating system options, used by `grub2` |
| bootctl | controls firmware and boot manager settings | 
| bootctl list | lists all boot options that are known by systemd | 
| sudo -s | start session as root |
| lsblk	  | list all devices and drives on machine and information about them |
| udiskctl | used to mount and perform operations on partitions and drives such as mounting and unmounting |
| mount /dev/drive /mnt/point | mount selected drive at mount point |
| umount /dev/drive | unmount the drive we just mounted in the above command |

* [Mounting Hard Disks and Partitions Using the Linux Command Line](https://www.makeuseof.com/tag/mounting-hard-disks-partitions-using-linux-command-line/)
* [How to Mount and Unmount Storage Devices from the Linux Terminal](https://www.howtogeek.com/414634/how-to-mount-and-unmount-storage-devices-from-the-linux-terminal/)
