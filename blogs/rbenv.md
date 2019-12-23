# Rbenv, Ruby and Rails installation 

## Update ```apt``` repositories 
```
$ sudo apt update
```

## Install ```ruby``` dependencies[optional]
```
$ sudo apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev
```

## Check ```git``` version 
```
$ git --version
```

**Note:** By default it's installed with linux distributions. Install git if not installed.

## Install GCC compiler
```
$ sudo apt install gcc
```
**Note:** Is required to compile packages from source. We will be using it for rbenv source compilation.

## Install make 
```
$ sudo apt install make
$ sudo apt install make-guile
```

## Remove RVM if you are using it as existing ruby versio manager. Otherwise ignore this step.
```
$ rvm implode
or 
$ rm -rf ~/.rvm
```

**Note:** Also make sure all of the .rvm files and folder are deleted.

## Install rbenv using git clone from github repository
```
$ cd ~/
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

**Note:** It will clone rbenv in a ```.rbenv``` hidden folder. 

### Compile dynamic bash extension of cloned ```rbenv``` repository
```
$ cd ~/.rbenv && src/configure && make -C src
```

### Add following lines to your ```~/.bashrc``` file
```
export PATH="$HOME/.rbenv/bin:$HOME/.rbenv/shims:$PATH"
which rbenv > /dev/null && eval "$(rbenv init -)"
```

### Initialize ```rbenv``` to enable ```shims``` and autocompletion.
```
$ ~/.rbenv/bin/rbenv init
```

### Re-open your terminal window then run
```
$ type rbenv
```

### Install ```ruby-build``` plugin
```
$ cd ~/.rbenv
$ mkdir plugins
$ cd plugins
$ git clone https://github.com/rbenv/ruby-build.git
```

## Install Ruby

### Check list of available ruby version
```
$ rbenv install -l
or 
$ rbenv install list
```

### Install a specific ruby version from the available list.
```
$ rbenv install 2.6.5
```

### Run following command once you install a ```ruby``` version
```
$ rbenv rehash
```

### Set global ```ruby``` using ```rbenv``` 
```
$ rbenv global 2.6.5
```

## Install ```bundler``` ruby gem
```
$ gem install bundler
```
**Note:** Bundler is a ```ruby``` package manager to manage gems.

## Install ```rails``` framework 
```
$ gem install rails
```

**Note:** It will install latest version of rails compatible with your current ruby. Use ```gem install rails -v 5.2.5``` to install a specific rails version.

## Install NodeJS
```
$ sudo apt install nodejs
```

**Note:** For ```javascript``` runtime environment of rails projects.
