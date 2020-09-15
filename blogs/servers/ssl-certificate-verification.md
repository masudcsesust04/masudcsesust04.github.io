# SSL certificate verification while updating DNS record

## Way-1, From the server machine:

Add follow line to ```/etc/hosts``` file:
```
server_ip_address     domain_name
```

Then run follow command if it's working or not:
```
curl --verbose https://live.cardeasexml.com/ultradns.php
```

output will contains following line:
```
* SSL certificate verify ok.
```

## Way-2, From local developmet manchine:

Add following line to ```/etc/hosts``` file:
```
server_ip_address       your_domain_name
```

Now go to browser and visit your app through https:
```
https://your_domain_name.com
```
**Note:** By doing this we are adding a dns record to our local machine which will load the app through domain name and mapped ip address in the ```/etc/hosts``` file.

### Thank you!
