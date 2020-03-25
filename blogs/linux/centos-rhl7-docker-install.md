# CentOS/RHL Docker, Docker compose installation

1. Remove older version of Docker[*optional]
```
$ sudo yum remove docker docker-common docker-selinux docker-engine-selinux docker-engine docker-ce
```

2. Install dependent packages
```
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

3. Use the following command to set up the stable repository.
```
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```    

4. Install the latest version of docker engine
```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

5. Troubleshoot docker version
```
$ docker --version
```

6. Download the current stable release of docker compose
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

7. Apply executable permissions to the binary.
```
$ sudo chmod +x /usr/local/bin/docker-compose
```

8. Symlink executable to run docker compose.
```
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

9. Check docker-compose version
```
$ docker-compose --version
```

### Thank you!
