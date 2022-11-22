# Manjaro

Often, I'll install Manjaro to simplify the multi-boot setting process.

1. `manjaro-chroot -a` if you have a Boot LiveCD
2. `update-grub`
3. `grub-install /dev/**`

> The boot menu of Manjaro will auto-remember the last selection of OS. So you don't have to choose which OS to boot next time when you boot your machine.

## Crontab

Often, we use `crontab -e` to set up a schedule to run our software.

I use the following command line a lot, because it will run the software when the computer start:

```bash
@reboot /home/yingshaoxo/.bin/your_software

#'chmod 777 your_software' is required to make sure that file is runable
```

You may also run the following command to enable `crontab` service:

```
systemctl enable cronnie
systemctl start cronnie
```
