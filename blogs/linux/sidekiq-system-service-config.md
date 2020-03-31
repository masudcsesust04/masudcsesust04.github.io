# Configure and run rails sidekiq as system service

SSH login to your host linux box:
```
$ ssh user@x.x.x.x
```

Change directory:
```
$ cd /lib/systemd/system
```

Create sidekiq.service file:
```
$ touch sidekiq.service
```

Open sidekiq.service file:
```
$ vim sidekiq.service
```

Now add following lines:
```
# /usr/lib/systemd/system/sidekiq.service
# Customize this file based on your bundler location, app directory, etc.
# Put this in /usr/lib/systemd/system (CentOS) or /lib/systemd/system (Ubuntu).
# Run:
#   - systemctl enable sidekiq
#   - systemctl {start,stop,restart} sidekiq
#
# This file corresponds to a single Sidekiq process.  Add multiple copies
# to run multiple processes (sidekiq-1, sidekiq-2, etc).
#
# See Inspeqtor's Systemd wiki page for more detail about Systemd:
# https://github.com/mperham/inspeqtor/wiki/Systemd
#
[Unit]
Description=sidekiq
# start us only once the network and logging subsystems are available,
# consider adding redis-server.service if Redis is local and systemd-managed.
After=syslog.target network.target

# See these pages for lots of options:
# http://0pointer.de/public/systemd-man/systemd.service.html
# http://0pointer.de/public/systemd-man/systemd.exec.html
[Service]
Type=simple
WorkingDirectory=/var/www/your_app/current/
ExecStart=/home/user/.rbenv/shims/bundle exec sidekiq -e production # rails bundle path 'ruby -v' will show the path
Environment=RAILS_ENV=production
Environment=MY_DATABASE_PASSWORD=your_db_password
User=app_user
Group=app_user
UMask=0002

# if we crash, restart
RestartSec=1
Restart=on-failure

# output goes to /var/log/syslog
StandardOutput=syslog
StandardError=syslog

# This will default to "bundler" if we don't specify it
SyslogIdentifier=sidekiq

[Install]
WantedBy=multi-user.target
```

Verify systemd sidekiq.service file:
```
$ sudo systemd-analyze verify sidekiq.service
```

Enable sidekiq as system service:
```
$ sudo systemctl enable sidekiq.service
```

Start/Stop/Restart/Status of the service
```
$ sudo service sidekiq start/stop/restart/status
or
$ sudo systemct start/stop/restart/status sidekiq.service
```

Realod service if you change or modify your service file 
```
$ sudo systemctl daemon-reload
```

### Thank you!

