# Installfest

**Installfest** is the guide I follow to set up a new development environment under Linux.

## What I'll be installing

* Ruby
* Ruby on Rails
* Various Ruby Gems
* Heroku Toolbelt
* Git
* Text editor of choice
  * [Sublime Text](https://www.sublimetext.com/)
  * [Atom](https://atom.io/)
  * [Vim](http://www.vim.org/)
* Terminal customizations

## Instructions

## Install & Configure Git

To install Git:
```bash
sudo apt-get install git
```

To set your name and email type the following:
```bash
git config --global user.name "Your Actual Name"
git config --global user.email "Your Actual Email"
```
Use the same email address for Git, Github and SSH.

To **verify** type the following:
```bash
git config --get user.name
```
You should get back your name. Do the same with your email to verify your email.

## Create An SSH Key

First check if you already have an SSH key.

Type the following:
```bash
ls ~/.ssh/id_rsa
```
If you see the message `No such file or directory`, you don't have an SSH key.

To create an SSH key type the following:
```bash
ssh-keygen -C example@example.com -t rsa
```
Replace `example@example.com` with your email.

Then press `Enter` to accept the default key save location.

Next it will ask you for a passphrase.

| No Passphrase | Passphrase |
| --- | --- |
| Press `Enter` to accept blank passphrase, then press `Enter` again. | Enter a passphrase if you share your Computer with other people. |

Finally add your generated key to the authentication agent by typing the following:
```bash
ssh-add ~/.ssh/id_rsa
```
## Install Ruby & Ruby on Rails

The first step is to intall some dependenies for Ruby.
```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```

Next I'm going to install Ruby using **rvm**.
```
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
curl -L https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.2.3
rvm use 2.2.3 --default
ruby -v
```

Install the documentation for each package locally and then install Bundler.
```
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
gem install bundler
```

Finally install Rails:
```
gem install rails -v 4.2.4
```

Make sure that everything is installed correctly:
```
rails -v
# Expected output
Rails 4.2.4
```

## Install Heroku Toolbelt
Type the following:
```
wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```

Once installed, you'll have access to the heroku command from your command shell.
Login using your heroku credentials:
```
heroku login
```

## Install your text editor of choice
My personal favorite is Sublime Text and Vim (when I want to make some quick changes)

Sublime installation is a pretty straightforward proccess. Just download the version that suits you from Sublime's website and double click to install it.

### Sublime configurations

I use the follow configuration for Sublime:
* [Package Control](https://packagecontrol.io/)
* [Theme - Spacegray](https://packagecontrol.io/packages/Theme%20-%20Spacegray)
* [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)

**Key Bindings** for Markdown Preview:
```
[
	{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"github"} }
]
```

To install vim type:
```
sudo apt-get install vim
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
