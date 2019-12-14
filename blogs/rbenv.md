# Rbenv, Ruby and Rails installation 

Remove RVM if you are using it as existing ruby versio manager. Otherwise ignore this step.
```
$ rvm implode
or 
$ rm -rf ~/.rvm
```
Note: Also make sure all of the .rvm files and folder are deleted.

## Install rbenv

It's pretty simple just clone rbenv from git repository
```
$ cd /home/username/
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```
Note: It will clone rbenv in a ```.rbenv``` hidden folder. 

Compile dynamic bash extension
```
$ cd ~/.rbenv && src/configure && make -C src
```

Add following lines to your ```~/.bashrc``` file
```
export PATH="$HOME/.rbenv/bin:$HOME/.rbenv/shims:$PATH"
which rbenv > /dev/null && eval "$(rbenv init -)"
```

Initialize rbenv to enable shims and autocompletion.
```
$ ~/.rbenv/bin/rbenv init
```

Re-open your terminal window then run
```
$ type rbenv
```

Install ```ruby-build``` plugin
```
$ cd ~/.rbenv/plugins/ruby-build
$ git clone https://github.com/rbenv/ruby-build.git
```

## Install ruby

Check list of available ruby version
```
$ rbenv install -l
or 
$ rbenv list
```

Install a specific ruby version from available list.
```
$ rbenv install 2.0.0-p247
```

Run following command once you install a ruby version
```
$ rbenv rehash
```

Now install ```bundler``` ruby gem
```
$ gem install bundler
```

## Install rails 
```
$ gem install rails
```
Note: it will install latest version of rails compatible with your current ruby.
