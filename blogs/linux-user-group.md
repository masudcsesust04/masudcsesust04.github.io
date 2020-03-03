# Linux/Unix user and group management

Login as super user 
```
$ su -
```

Create/Add new user
```
$ useradd user_name 
```

Verify user is creaded or not 
```
$ cat /etc/passwd
```

Set password
```
$ passwd user_name 
```

Remove/delete user
```
$ userdel user_name
```
Remove deleted user's home directory
```
$ userdel -r user_name
```

Create/add group 
```
$ groupadd group_name
```

Verify groups
```
$ cat /etc/group
```

Add user to group
```
$ usermod -a -G {group_name} {user_name}
```
*Here, -g = primary group, -G = Secondary group*

Remove/Delete group
```
$ groupdel group_name
```

Count number of groups
```
$ wc -l /etc/group
```
