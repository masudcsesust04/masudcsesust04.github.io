## SASS application add and configure new clients domain 

### Step-1: SSH login to the remote server
```
$ ssh username@ip_address
```

Note: Must purchase a ssl certificate for the clients domain you can even try letsencrypt as well.

### Step-2: Navigate to the nginx ```site-enabled``` directory
```
$ cd /etc/nginx/site-enabled/
```

### Step-3: Create a config file named with ```maindomain.clientdomain.conf``` and add content below
```
# redirect www to non-www
server {
  server_name www.clientdomain.com;
  return 301 $scheme://clientdomain.com$request_uri;
}

server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;

  server_name clientdomain.com www.clientdomain.com;

  ssl_certificate /etc/letsencrypt/live/cloudepa.com/fullchain.pem; # managed by Certbot
  ssl_certificate_key /etc/letsencrypt/live/cloudepa.com/privkey.pem; # managed by Certbot
  include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
  ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

  location / {
    proxy_pass          https://clientdomain.ourdomain.com/;
    proxy_set_header    Accept-Encoding "";
    proxy_set_header    Host clientdomain.ourdomain.com;
    proxy_set_header    X-Forwarded-Ssl on;
    proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header    X-Forwarded-Proto $scheme;
    proxy_set_header    origin 'https://clientdomain.ourdomain.com'; # to fix login and form submission from same origin issue

    #sub_filter_types   text/css text/xml;
    sub_filter_types   *;
    sub_filter         clientdomain.ourdomain.com clientdomain.com;
    sub_filter_once off;
  }
}
```

### Step-4: Check and restart NGINX web server

Check configuration is ok
```
$ sudo nginx -t
```

Now restart the web server:
```
$ sudo service nginx restart
```


### Step-4: Finally tell clients to add dns settings for thier domain(ex- cleintdomain.com) and create A record and CNAME for www.
```
A @ [ip address of ourdomain.com where app is hosted]
CNAME www @
or CNAME www clientdomain.com

```

Everything is running properly and you are all done!
