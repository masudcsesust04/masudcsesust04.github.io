## VSFTPD: Troubleshoot

**Problem statement:** vsftpd: not found directory given in ```secure_chroot_dir=/var/run/vsftpd/empty```
when try to connect using command ```ftp```.

**Solution:** There are many directories on a standard Linux setup that intentionally reset every reboot. The /tmp directory is one, and /var/run as well includig some others.
For security purposes, sometimes its good to create a new user named 'ftp' just for this purpose. If you are just using it for internal testing and learning, just use ```/var/ftp instea```` of /var/run/vsftpd.

Now stop the vsftpd service:
```
$ sudo service vsftpd stop
```

Create directory as per any of the above instruction:
```
$ sudo mkdir /var/ftp/vsftpd/empty
```

Open file ```/etc/vsftpd/vsftpd.conf``` and replace the path of following key ```secure_chroot_dir``` with the new directory.
```
secure_chroot_dir=/var/run/vsftpd/empty
```
To be
```
secure_chroot_dir=/var/ftp/vsftpd/empty
```

Start vsftpd service:
```
$ sudo service vsftpd start
```

Run following command to check its' working properly:
```
$ ftp
> open
```

## Thank you!
