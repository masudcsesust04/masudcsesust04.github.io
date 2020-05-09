# Development Environment Setup and Configuration

*Important notice:*
- For a newly installed linux distribution.
- Arch based manjaro linux is my favorite from last 2 years.
- You can follow this document to prepare your development environment for ubuntu, redhat/centOS etc. distros.
- Just replace 'pacman' with 'apt' (for ubuntu) or 'yum' for redhat/centOS and -S by 'install'. Please see htop installation in this document.    

## Update and install linux system packages.
```
$ sudo pacman -Syyu
```

## Install htop
Arch linux
```
$ sudo pacman -S htop
```

Ubuntu linux
```
$ sudo apt install htop
```

Redhat/Cent OS linux
```
$ sudo yum install htop
```

## Install Monaco font
Reference link to install Monaco font: https://gist.github.com/masudcsesust04/f2504b23cc81f52b478da2d5deb4caf2
 
## Terminal settings
- Intial terminal size set columns=100, rows=18
- Font set to 'Monaco Regular 12' after installing monaco
- Checked run command as login shell from command tab.

## Install vim or neovim
```
$ sudo pacman -S vim
$ sudo pacman -S neovim
```

I will install **neovim** as my default command line editor. 

## Neovim symlink with vim or vi command to open the editor
Add following line to your ```~/.bash_profile``` file
```
alias vi="vim"
alias vim="nvim"
```

Re-open terminal or reload ```~/.bash_profile``` file in the terminal window
``` 
$ source ~/.bash_profile
```

## Install sdkman to install java based software packages
```
$ curl -s "https://get.sdkman.io" | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
$ sdk version
$ sdk list
$ sdk list java
```

## Install Java
```
$ sdk install java 13.0.2-zulu
$ sdk install java 20.0.0.r11-grl
```
Visit https://sdkman.io/ to learn more about SDKMAN.

## Install git
- By default it's installed with the linux based OS distributions. 

Check installed git version by running
```
$ git --version
```

## Set git commit username and email
```
git config --global user.name "Md. Masud Rana"
git config --global user.email "youremail@example.com"
git config --global user.signingkey YOUR_GPG_KEY
git config --global commit.gpgsign true
git config --global --list
```

## Set usefull git command aliases
```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.last 'log -1 HEAD'
```

Note: Sample ```~/.gitconfig``` file https://github.com/masudcsesust04/dotfiles/blob/master/git/.gitconfig 

## Install github-desktop using AUR repository
Install fakeroot
```
$ sudo pacman -S fakeroot # Used for installation from source
```

Clone github-desktop from https://aur.archlinux.org/packages/github-desktop/  arch repository
```
$ cd github-desktop
$ makepkg -si
```

## Vim/nvim as git commit default editor
```
$ git config --global core.editor "nvim"
```

## Show git branch name to the terminal

Add following line to ```~/.bash_profile```
```
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

export PS1="\n\[\e[01;33m\]\u\[\e[0m\]\[\e[00;37m\]@\[\e[0m\]\[\e[01;36m\]\h\[\e[0m\]\[\e[00;37m\] \t \[\e[0m\]\[\e[01;32m\]\w\[\e[0m\]\[\e[01;37m\]\[\e[01;37m\]\$(parse_git_branch) \[\e[0m\]\n$ "
```

Restart terminal, or run 
```
$ source ~/.bash_profile
```

## Install docker and docker compose
- Open software center (add/remove software) application 
- Search by 'docker' then select 'docker' and 'docker-compose' to install

## Enable docker service/process to run while system is up and running
```
$ systemctl start docker
$ gpasswd -a $USER docker
$ systemctl enable docker
```

Fix permission denied error for docker command without sudo
```
$ sudo chmod 666 /var/run/docker.sock 
```

Check if docker installed properly
```
$ docker ps
$ docker images
```

## Install MySQL using docker and docker compose
Follow https://masudcsesust04.github.io/blogs/setup-mysql-using-docker this link to install MySQL

## Install MySQL client for arch linux
```
$ sudo pacman -S maridb-clients
```
*This package is required to connect mysql from ruby on rails or other programming languages. There are alternatives for ofther linux distributions.*

## Install rbenv
Arch linux GCC and make installation
```
$ sudo pacman -S gcc
$ sudo pacman -S make      
```

Ubuntu linux required make-guile as well
```  
$ sudo apt install gcc
$ sudo apt install make      
$ sudo apt install make-guile 
```
*Above packages are used compile and install software packages from source code. I will be using this for rbenv installation in the next step.*

Clone Rbenv git repository to your home directory
```
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

Build and install from rbenv from source
```
$ cd ~/.rbenv && src/configure && make -C src
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
$ ~/.rbenv/bin/rbenv init
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
```

Reload terminal shell then run
```
$ curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
```

Ruby build plugins
```
$ mkdir -p "$(rbenv root)"/plugins 
$ git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```

## Install Ruby
```
$ rbenv install --list
$ rbenv install 2.6.5
$ rbenv rehash
$ rbenv versions
$ rbenv version
$ rbenv global 2.6.5
$ ruby -v
```

## Install Rails
```
$ gem install bundler
$ gem install rails
$ gem install rails -v 5.2
$ rails -v
```

## Install nodeJS
```
$ sudo pacman -S nodejs
```

## SSH key setup
- Copy and paste your backed up ```.ssh``` folder to home directory 
- Otherwise create a new SSH key

Enable ssh key
```
$ ssh-add 
```

## Browser installation
- Firefox Developer Edition: Developer edition of popular firefox browser.
- Firefox: Standalone web browser.
- Chromium 

## Install text/code editor 
- GEdit: Is the official text editor GNOME desktop environment. It's my primary GUI text editor for development now a days as it's the feature rich with very minimal resource usage.
- VS Code: Is my second choice now a days. It's use way more resource than GEdit.
- Sublime: Lightweight text editor.

## Create project directory 
- Clone each of your working project repository from SCM(Github, Bitbucket, Gitlab etc.) or 
- Copy paste backed up source code directories in this directory

## Install utility softwares from software/app center [*based on your need]
- Gunome todo: Todo manager
- gitk / gitG / Qgit: Git GUI client.
- Gparted: Is a free partition editor for graphically managing your disk partition.
- Oracle VMWare: Run several virtual system on a single host computer.
- DBeaver: Universal database manager and SQL client.
- Deluge: Cross platform BitTorrent client. 
- Documents: A document manager application for GNOME.
- Umbrollo: For UML design
- Gnumeric: A high-precision spreadsheet program.
- SeaMonkey: Your web, the way you like it. For safe internet suite.
- GNU Radio: General purpose DSP and SDR toolkit.
- Sweeper: System cleaning utility.
