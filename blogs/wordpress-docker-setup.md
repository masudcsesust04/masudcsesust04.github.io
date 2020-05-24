# Wordpress setup using docker, docker-compose and MySQL.

**Step-1:** Create a folder in your host machine. For example, I have created ```blog``` directory under ```/home``` directory.

**Step-2:** Create ```docker-compose.yml``` file in the folder ```blog``` created last step and paste content below.
```
version: '3'

volumes:
  db_data:

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: [root_password]
      MYSQL_DATABASE: [wordpress_db]
      MYSQL_USER: [username]
      MYSQL_PASSWORD: [user_password]
    ports:
      - 3306:3306

  wordpress:
    depends_on:
      - db
    image: wordpress:5.2.2
    working_dir: /var/www/html
    volumes:
      - ./wp-content:/var/www/html/wp-content
      - ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: [db_username]
      WORDPRESS_DB_PASSWORD: [db_user_password]
      WORDPRESS_DB_NAME: [wordpress_db_name]
    ports:
      - 8080:80
```

**Note:**
- Review and modify the wordpress (docker image) version and volume mapped here as per your needs.
- Must use the volume mentioned here. In my case i used ```/blog``` folder under the directory to manage volumes in my host machine. in this folder ```wp-content``` is used to store all of the wordpress content and ```uploads.ini``` file is using to map and initialization of upload file size limit.
- You may need to adjust it as per the size of downloaded size(in my case it was 600MB) of the wp app using all-in-one wp migration content later one adjust as you want to restrict the file or content upload limit(ex- 10MB - 20 MB).  

**Step-3:** Sample ```uploads.ini``` file content.
```
file_uploads = On
upload_max_filesize = 600M
post_max_size = 600M
```

**Step-4:** Create database name, user and password for the application. FYI, Please update ```docker-compose.yml``` file as yours in ```environment``` block. 

**Step-5:** Check the port mapped here is open and available from clients machine using follwoing command.
```
$ sudo ufw status verbose
```
**Note:** It will show all of the open ports. If the port mapped in the ```docker-compose.yml``` file is not open and don't show in the list of above command then open it. 

Open a particular port using following command
```
$ sudo ufw allow [port_number]/tcp
```

**Step-6:** You can run the appliation in docker container any of the following command 

Verbose mode:
```
$ docker-compose up
``` 

Detache mode:
```
$ docker-compose up -d
``` 

**Step-7:** Now visit the application it will ask for  and set language, username and passowrd to enter in the admin panel.

## Migration
If you have a previous wordpress app then you have to take a backup and import it in the new site:
- 1, Install all-in-one wp migration plugin to the old site and activate it.
- 2, Take backup (plugin -> Export) from old site using the installed plugin
- 3, Install all-in-one-migration plugin to dockerized wp app as per **step-7** and activate the plugin.
- 4, Click on plugin's import link and select backedup file to start importing. 

**Note:** Once complete you will be able to access the admin panel with your old application username and passwords and all of the content will be shown here as well.
