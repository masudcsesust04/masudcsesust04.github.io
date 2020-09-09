# Linux/Unix user, password expires/aging and group management

### User management
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

Change existing user password
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

### User password aging time management

To list current aging type by ```chage``` command 
```
$ chage -l username
or
$ chage --list username
```

Set or update aging type of a user
```
$ chage username # Interactive mode command
```

Set password expire date for an user using chage option ```-M```
```
$ chage -M 10 username # 10 days from current date
```

Set password expire date for an user using chage option ```-E``` with YYYY-MM-DD fromat
```
$ chage -E "2021-05-31" username
```

Force the user account to be locked after X number of inactivity days
```
$ chage -I 10 usename
```

To disable/turn off password aging for an user accounit
```
$ chage -m 0 -M 99999 -I -1 -E -1 username
```
Here,
- -m 0 will set the minimum number of days between password change to 0
- -M 99999 will set the maximum number of days between password change to 99999
- -I -1 (number minus one) will set the “Password inactive” to never
- -E -1 (number minus one) will set “Account expires” to never.

### Group management
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

Add user to suders group:
```
$ usermod -aG sudo newuser
Or
$ sudo usermod -aG sudo newuser
```
Here, The ```-aG``` option tells the system to append the user to the specified group. (The ```-a``` option is only used with ```G```.)

Verify user belongs to sudo group:
```
$ groups newuser
```

Verify sudo access:
```
$ su - newuser
```

Count number of groups
```
$ wc -l /etc/group
```
