# Installfest
**Installfest** is the guide I follow to set up a new development environment under Linux.
## What I'll be installing
* Ruby
* Ruby on Rails
* Node.js
* Various Ruby Gems
* Heroku Toolbelt
* Git
* Text editor of choice
  * [Atom](https://atom.io/)
  * [Sublime Text](https://www.sublimetext.com/)
  * [Vim](http://www.vim.org/)
* Terminal customizations

## Instructions
## Install & Configure Git
To install Git:
```
$ sudo apt-get install git
```
To set your name and email type the following:
```
$ git config --global user.name "Your Actual Name"
$ git config --global user.email "Your Actual Email"
```
Use the same email address for Git, Github and SSH.

To **verify** type the following:
```
$ git config --get user.name
```
You should get back your name. Do the same with your email to verify your email.

## Create An SSH Key

First check if you already have an SSH key.

Type the following:
```
$ ls ~/.ssh/id_rsa
```
If you see the message `No such file or directory`, you don't have an SSH key.

To create an SSH key type the following:
```
$ ssh-keygen -t rsa -b 4096 -C "example@example.com"
```
Replace `example@example.com` with your email.

Then press `Enter` to accept the default key save location.

Next it will ask you for a passphrase.

| No Passphrase | Passphrase |
| --- | --- |
| Press `Enter` to accept blank passphrase, then press `Enter` again. | Enter a passphrase if you share your Computer with other people. |

Finally add your generated key to the authentication agent by typing the following:
```
$ ssh-add ~/.ssh/id_rsa
```
Finally copy the content of **id_rsa.pub** and paste in your GitHub account.

## Install Ruby & Ruby on Rails
First I'm going to install [RVM](http://rvm.io/).

We'll use `curl` to install RVM.
```
$ sudo apt-get install curl
```
Once curl is finished installing paste the following:
```
$ gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```
Then type the following to install RVM:

**Note**: Append `--rails` or `--ruby` for all in one installation.
```
$ \curl -sSL https://get.rvm.io | bash -s stable
```
In my case:
```
$ \curl -sSL https://get.rvm.io | bash -s stable --ruby
```
Check ruby version:
```
$ ruby -v
```
Install **Node.js**:
```
$ sudo apt-get install nodejs
```
Then install **bundler**:
```
$ gem install bundler
```
and finally **rails**:
```
$ gem install rails
```
Check rails version:
```
$ rails -v
```
## Install Heroku Toolbelt
Type the following:
```
$ wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```
Once installed, you'll have access to the heroku command from your command shell.
Login using your heroku credentials:
```
$ heroku login
```
## Install your text editor of choice
My personal favorite is Atom and Vim (when I want to make some quick changes)

Atom installation is a pretty straightforward process. Just download it from https://atom.io/ and double click to install it.

**Note:** I noticed that under Ubuntu GNOME 16.04 LTS you can't install it directly due to some dependencies issues.

To install it open your terminal and type:
```bash
$ sudo dpkg -i atom_package.deb
```
If you get a dependencies missing error type the following to install the missing dependencies:
```bash
$ sudo apt-get install -f
```
To install vim type:
```
$ sudo apt-get install vim
```
## Terminal Customizations
### Tab completion
As the name says. When you hit tab one of the following gets auto-completed:
* local and remote branch names
* local and remote tag names
* .git/remotes file names
* git 'subcommands'
* tree paths within 'ref:path/to/file' expressions
* file paths within current working directory and index
* common --long-options

To enable this open **bashrc** `nano ~/.bashrc` and add the following line at the end of the file:
```
## Enable tab completion
source ~/Scripts/git-completion.bash # git-completion.bash location
									 # You can find git-completion.bash
									 # in this repo
```
### New colours
Add the following at the end of the **.bashrc** file:
```
# colors!
green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
reset="\[\033[0m\]"
```
### Change command prompt
Add the following at the end of the **.bashrc** file:
```
### Change command prompt
source ~/Scripts/git-prompt.sh # git-prompt.sh location
							   # You can find git-prompt.sh
							   # in this repo
export GIT_PS1_SHOWDIRTYSTATE=1
# '\u' adds the name of the current user to the prompt
# '\$(__git_ps1)' adds git-related stuff
# '\W' adds the name of the current directory
export PS1="$purple\u$green\$(__git_ps1)$blue \W $ $reset"
export NVM_DIR="/home/username/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
```
