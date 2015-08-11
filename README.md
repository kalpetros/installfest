# Installfest

**Installfest** is the guide I follow to set up a new development environment under Linux.

## What I'll be installing

- Ruby
- Rails
- Git
- Text editor of choice
	- Sublime Text 2
	- Atom
- Various Ruby Gems

## Instructions

### Step 1: Install packaged software and libraries
```bash
sudo apt-get install autoconf automake bison build-essential curl git-core libapr1 libaprutil1 libc6-dev libltdl-dev libreadline6 libreadline6-dev libsqlite3-0 libsqlite3-dev libssl-dev libtool libxml2-dev libxslt-dev libxslt1-dev libyaml-dev ncurses-dev nodejs openssl sqlite3 zlib1g zlib1g-dev
```
### Step 2: Install Git

Type this in the terminal:
```bash
sudo apt-get install git
```
### Step 3: Install RVM

Type the following in the terminal to install RVM:
```bash
curl -L get.rvm.io | bash -s stable
```
This will print a long message.

Then verify RVM

Type this in the terminal:
```bash
type rvm | head -1
```
Expected result:

rvm is a function

Type this in the terminal:
```bash
rvm -v
```
Expected result:
```bash
rvm 1.x.x (stable) by Wayne E. Seguin (wayneeseguin@gmail.com), Michal Papis <mpapis@gmail.com> [https://rvm.io/]
```
### Step 4: Install Ruby

Type this in the terminal:
```bash
curl -L get.rvm.io | bash -s stable
```
Then sit back and wait. It will take some time. This downloads and compiles Ruby.

When it is finished type the following:
```bash
rvm use 2.2
rvm --default use 2.2
```
To verify that all went good, type the following:
```bash
ruby -v
```
Expected result:
ruby 2.2.1p85 (2015-02-26 revision 49769) [x86_64-linux]

### Step 5: Install Rails

Type this in the terminal:
```bash
gem install rails
```
### Step 6: Install your text editor of choice

- Sublime Text
	- To install it download it from [here.](http://www.sublimetext.com/)
- Atom
	- To install it download it from [here.](https://atom.io/)

## Configure Git

Type this in the terminal:
```bash
git config --global user.name "Your Actual Name"
git config --global user.email "Your Actual Email"
```
Use the same email address for Git, Github and SSH.

To verify type the following:
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
If you see the message `No such file or directory`, you don't have an SSH key

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