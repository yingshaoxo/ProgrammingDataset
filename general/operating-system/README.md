# Operating System

## Installation

[https://medium.com/@yingshaoxo/become-a-master-of-ubuntu-system-installation-71fbabab7d6b](https://medium.com/@yingshaoxo/become-a-master-of-ubuntu-system-installation-71fbabab7d6b)

## Recovery or Fix problem for a broken system

1. Go to `recovery mode`
2. Go to `root shell`
3. Repair the broken disk: `fsck /dev/sbX`
4. Reload for writing: `mount -o remount,rw /`
5.  Reset grub:

    ```
    sudo su
    fdisk -l
    mkdir linux
    mount /dev/sdX /mnt/linux
    #update-grub
    grub-install --boot-directory=/mnt/linux /dev/sdX
    ```

## Increase the `memory`

### Check the current status:

```
sudo swapon --show
```

### Create a swap type partition, then modify `/etc/fstab` as the following:

```
# Use 'blkid' to print the universally unique identifier for each device

# the system itself
UUID=514a9b60-d9b4-4108-bd7a-97c61b9aafc9 /               ext4    errors=remount-ro 0       1

# the swap partition
UUID=b9420599-3f79-45a9-ba1e-5b1c0f328ad2      none            swap      sw         0        0

# data disk
UUID=F86D2571D5F6048B /media/data               ntfs    errors=remount-ro,auto,exec,rw,user 0       0
```

> fstab can also be used to mount a disk before getting into an OS

## User System

Login with username and password: `login your_username`

Change password: `passwd your_username`

Get into the root user's shell: `sudo -s` or `sh -s` or `sudo su` or `login root`

Create a user: `useradd your_username`

> Remember, you should always check if you have the root permission or not when you got a new device. Because that's important.
