# CentOS/RHL Docker, Docker compose installation

## Docker
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
$ sudo yum install docker-ce
```

5. Enable docker service
```
$ sudo systemctl enable docker.service
```

6. Start, Stop, Restart docker service on CentOS7/RHEL7
```
$ sudo systemctl start docker.service
$ sudo systemctl stop docker.service
$ sudo systemctl restart docker.service
$ sudo systemctl status docker.service
```

7. Troubleshoot docker version
```
$ docker --version
```

## Docker compose
1. Download the current stable release of docker compose
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. Apply executable permissions to the binary.
```
$ sudo chmod +x /usr/local/bin/docker-compose
```

3. Symlink executable to run docker compose.
```
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

4. Check docker-compose version
```
$ docker-compose --version
```

### Thank you!
