# Lets encrypt SSL certificate renew 

For docker and docker-compose deploymet environment. I will renew for a blog sub domain.

STEP-1: Stop the web server running on 80 port 
```
$ cd ~/www/apps/app_name/
$ docker-compose stop web
```

STEP-2: Renew ssl certificate using ```certbot``` following command
```
$ cd ~/
$ sudo certbot renew --standalone
```

*Note:* 
- This will generate files with details where it's created.
- Generated certificates will valid for 3 months.

STEP-3: Copy following files to the application directory
``` 
$ sudo cp /etc/letsencrypt/live/blog.domain_name.com/fullchain.pem ~/www/apps/app_name/certs/
$ sudo cp /etc/letsencrypt/live/blog.domain_name.com/privkey.pem ~/www/apps/app_name/certs/
```

STEP-4: Start the web server from application docker compose directory.
```
cd ~/www/apps/app_name
$ docker-compose start web
```
