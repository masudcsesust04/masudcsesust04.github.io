# Set UNIX/LINUX environment variables

Check environment variables:
```
$ printenv | less
```

Set environment variable:
```
$ MY_VAR='value'
```

Check and troubleshoot:
```
$ echo $MY_VAR
$ set | grep MY_VAR # returns the value
$ printenv MY_VAR # returns empty
$ export MY_VAR # set environment variable
$ printenv MY_VAR # will show the expected output
```
Note: Will be set for current login shell temporarily. Restarting shell or relogin can't remember this var.

For permanent varible set add variables to following file as key value pair:
```
$ vim /etc/environment
```
Note: seeing the effect relogin the shell.

