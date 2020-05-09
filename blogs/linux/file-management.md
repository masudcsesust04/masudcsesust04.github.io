# File operation and management

### File/Directory copy source to destination directory: 

Copy ```/source_dir``` to ```/destination_dir```
```
$ cp -R /source_dir /destinatioin_dir/
```

Copy files with same ownership
```
$ cp -aR /source_dir /destinatioin_dir/
```

When destination directory is already exist only need to copy files and sub folders
```
$ cp -RT /source_dir /desitnation_dir/
```

Copy files with displaying copying process
```
$ cp -avR /source_dir /desitnation_dir/
```

Copy only the content of ```/source_dir``` directory to ```/destination_dir```
```
$ cp -avR /source_dir/* /destination_dir/
```

Copy multiple directories like, ```/etc``` and ```/var``` to ```/opt``` directory
```
$ cp -avR /etc /var /opt/
```
