# Nginx web server configuration and troubleshooting

### Check installed version:

```
$ nginx -v
```

If above command is not working then follow below steps:
1. Use the ps command to grab path for nginx
```
ps aux | grep nginx
```

2. Once found(may match any of below) use full path:
```
$ /opt/nginx/sbin/nginx -v
$ /usr/sbin/nginx -v
$ sudo /usr/sbin/nginx -v
$ sudo /usr/local/sbin/nginx -v
```

### Nginx configuration is OK

```
$ sudo nginx -t
```

Issue-1: 
**Problem statement:** Getting following error after updating nginx while stoping the server and starting it again. In my case, I have updated nginx 1.16.1 to 1.19.2 on Redhat linux 7.
```
nginx: [emerg] module "/usr/lib64/nginx/modules/ngx_http_image_filter_module.so" version 1016001 instead of1019002 in /usr/share/nginx/modules/mod-http-image-filter.conf:1
nginx: configuration file /etc/nginx/nginx.conf test failed
```
Sometime ```nginx -t``` show wrong error message so use ```sudo nginx -t```

**Root cause:** ```sudo yum update nginx``` updated the nginx version but some of the core module was not upated. So i needed to remove those module particularly (ngx_http_image_filter_module) and installed again.

**Solution:**
```
$ sudo yum remove nginx-mod*
$ sudo yum install nginx-module-*
```


