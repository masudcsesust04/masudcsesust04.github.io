# Nginx web server configuration and troubleshooting

Check installed version:

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

