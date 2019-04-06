# Linux

___


#### Increasing the `memory`

###### Check the current status:
```
sudo swapon --show
```

###### Create a swap type partition, then modify `/etc/fstab` similar to the following:
```
# the system itself
UUID=514a9b60-d9b4-4108-bd7a-97c61b9aafc9 /               ext4    errors=remount-ro 0       1

# the swap partition
UUID=b9420599-3f79-45a9-ba1e-5b1c0f328ad2      none            swap      sw         0        0

# data disk
UUID=F86D2571D5F6048B /media/data               ntfs    errors=remount-ro,auto,exec,rw,user 0       0
```

> fstab can also be used to mount a disk before get into OS

____

