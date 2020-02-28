# Setup and configure MySQL using docker and docker-compose

*Caution: Before starting please make sure you have installed docker and docker-compose.*

### Create a folder in your home directory.
```
$ mkdir mysql
$ cd mysql
$ mkdir mysql-data
$ touch docker-compose.yml 
$ touch .env.secrets
```
 
### Add folliwng lines to docker-compose.yml file
```
version: '3.1'

services:
  db:
    image: mysql:5.7
    restart: always
    env_file:
      - .env.secrets
    ports:
      - 3306:3306
    volumes:
      - ./mysql-data:/var/lib/mysql
```

*Note:* 
- Folder ```mysql-data``` will be used to store MySQL data files which is mapped with docker volumes using docker compose.
- Open your terminal window and navigate to mysql directory where docker-compose.yml file is located.
- Any ```docker-compose``` command will work only if you are in the same location where docker-compose.yml file is.

### Add folliwng lines to ```.env.secrets``` file
```
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=dev_db
MYSQL_USER=dev_user
MYSQL_PASSWORD=devpass
MYSQL_HOST=db
```

*Note:* 
- We are defining mysql root user password
- Creating a sample database called dev_db
- A sample user with password along with root user
- MySQL data host db which is the service name defined in docker-compose.yml file

### Up and Run MySQL
```
$ docker-compose up 
or
$ docker-compose up -d 
```

*Note:*
- First command will run MySQL service attached in terminal with showing continuous log
- Second command will run MySQL as a daemon service with detaching from terminal. Off course we can see the log using a seperate command.

### MySQL daemon service log 
```
$ docker-compose logs db
```

### Enter into mysql docker container
```
$ docker-compose exec db bash
```

*Note:* Here ```db``` is the service name defined in docker-compose.yml file.

### Enter into MySQL console
```
$ mysql -uroot -p
```

*Note:* It will work only if you run above command after entering mysql docker container. Which i have done in our previous step.

### Troubleshoot and create a test database
```
$ SHOW databases;
$ CREATE DATABASE test;
```

### Exit MySQL console
```
$ quit;
```

### Exit MySQL docker container
```
$ exit
```

**Important**: *Use **127.0.0.1** as MySQL hostname when need to connect this MySQL docker service from your development application or MySQL database SQL clients like Workbench, Dbeaver etc.*

  
