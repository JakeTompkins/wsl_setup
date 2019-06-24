_DISCLAIMER We heavily recommend a minimal hardware configuration to consider this Windows Linux Subsystem setup: A SSD drive and at least 8Go RAM are mandatory_

#Setup instructions

The following instructions will help you to get ready for [Le Wagon](http://www.lewagon.org) fullstack bootcamp:

- Grab a text editor, where you'll spend your day and nights

- Install a package manager

- Pimp your Terminal

- Setup git and GitHub

- Install Ruby

##Prerequisites

First you need to check your machine runs on Windows 10 build 1615 or later. Follow theses steps to [check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number). For earlier versions of Windows 10, follow [Le Wagon Windows setup](WINDOWS.md).

## Ubuntu on Windows

Download [Ubuntu on Windows](https://www.microsoft.com/fr-fr/store/p/ubuntu/9nblggh4msv6?rtc=1) from the Windows Store. Once download has completed, select _Launch_. This will open a console window. Wait for installation to complete then you will be prompted to create your LINUX user account. Create your LINUX username and password. This user account has no relationship to your Windows username and password and hence can be different.

You're now ready to use your Linux environment 👏.

First we’re going to download a better terminal application. Download Hyper from https://hyper.is/ and install it.

Once Hyper has installed, run the application, then hit “ctrl + ,” to open the configuration file. 

Find the line: 

```javascript
shell: ‘’.
```



Change it to: 

```javascript
shell: ‘*C:\\Windows\\System32\\wsl.exe*’
```



Now find ```shellArgs``` just below it, and set it to: ```shellArgs[]```,

Restart Hyper

Hyper is where you will interact with your system through Ubuntu. You will have to copy-paste a lot of commands in this guide. While copying to the clipboard works as everywhere else by selecting the text, and pressing `Ctrl` + `C`, pasting into the terminal is done by right-clicking anywhere within the terminal window.

Start with this command that installs a few useful utilities that will be needed later:

```bash
sudo apt update

sudo apt install -y apt-transport-https unzip gnome-terminal
```

:point_up: This command will ask for your password with: `[sudo] password for <username>:`. The Linux terminal won't give you any feedback, like `\*`, as you might be used to. You just have to type it correctly, and then press `Enter`. If you type it wrong, you will be asked again otherwise the terminal will remember it until it is closed.

## Menlo for Powerline font

Menlo for Powerline is a fancy font for your terminal. Download it from [abertsch/Menlo-for-Powerline repository](https://github.com/abertsch/Menlo-for-Powerline/raw/master/Menlo%20for%20Powerline.ttf) on GitHub. Once download has completed, double-click on the `Menlo for Powerline.ttf` file and install it on windows.

Then open preferences in Hyper (ctrl + ,), and add ‘Menlo for Powerline’ to the beginning of the fonts

## GitHub account

Have you signed up to GitHub? If not, [do it right away](https://github.com/join).

:point_right: **[Upload a picture](https://github.com/settings/profile)** and put your name correctly on your GitHub account. This is important as we'll use an internal dashboard with your avatars. Please do it **now**.

## Git

To install `git`, first open up Hyper.

Then copy this line with `Ctrl` + `C`:

```bash

sudo apt install -y git

```

:bulb: To **paste it in the terminal**, you need to use `Ctrl` + `Shift` + `V` OR right click.

## Visual Studio Code - Your text editor

A text editor is one of the most important tools of a developer.

Download Visual Studio Code from [here](https://code.visualstudio.com/) and install it in Windows. 

Now let’s install some useful plugins! Restart Hyper (or run the command ```bash exec zsh```)

Copy and paste this long command.

```bash
code --install-extension patbenatar.advanced-new-file Atishay-Jain.All-Autocomplete mgmcdermott.vscode-language-babel ZneuRay.erb-vscode-snippets misogi.ruby-rubocop

```

## Oh-my-zsh - Fancy your Terminal

We will use the shell named `zsh` instead of `bash`, the default one.

```bash

sudo apt install -y zsh curl vim imagemagick jq

```

We need to install the latest version of nodejs:

```bash

curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -

sudo apt install -y nodejs

```

```bash

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# it will ask for your session password

```

Be careful, those commands will ask you to type your password twice. At the end

your prompt should look like this:

![](images/ubuntu_oh_my_zsh.png)

If it doesn't, **ask a teacher**.

To make this change stick, restart your laptop

## GitHub

We need to generate SSH keys which are going to be used by GitHub and Heroku

to authenticate you. Think of it as a way to log in, but different from the

well known username/password couple. If you already generated keys

that you already use with other services, you can skip this step.

Open a terminal and type this, replacing the email with **yours** (the

same one you used to create your GitHub account). It will prompt

for information. Just press enter until it asks for a **passphrase**.

```bash

mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"

```

**NB:** when asked for a passphrase, put something you want (and that you'll remember),

it's a password to protect your private key stored on your hard drive. You'll type,

nothing will show up on the screen, **that's normal**. Just type the passphrase,

and when you're done, press `Enter`.

Then you need to give your **public** key to GitHub. Run:

```bash

cat ~/.ssh/id_ed25519.pub

```

It will prompt on the screen the content of the `id_ed25519.pub` file. Copy that text,

then go to [github.com/settings/ssh](https://github.com/settings/ssh). Click on

**Add SSH key**, fill in the Title with your computer name, and paste the **Key**.

Finish by clicking on the **Add key** green button.

To check that this step is completed, in the terminal run this. You will be

prompted a warning, type `yes` then `Enter`.

```bash

ssh -T git@github.com

```

If you see something like this, you're done!

```bash

# Hi --------! You've successfully authenticated, but GitHub does not provide shell access

```

If it does not work, try running this before trying again the `ssh -T` command:

```bash

ssh-add ~/.ssh/id_ed25519

```

Don't be in a rush, take time to [read this article](http://sebastien.saunier.me/blog/2015/05/10/github-public-key-authentication.html) to get a better

understanding of what those keys are used for.

## Dotfiles (Standard configuration)

Hackers love to refine and polish their shell and tools. We'll start with a great default configuration provided by [Le Wagon](http://github.com/lewagon/dotfiles), stored on GitHub. As your configuration is personal, you need your own repository storing it, so you first need to fork it to your GitHub account.

:arrow_right: [Click here to **fork**](https://github.com/lewagon/dotfiles/fork) the `lewagon/dotfiles` repository to your account. Forking means that it will create a new repo in your GitHub account, identical to the original one. You'll have a new repository on your GitHub account, `your_github_username/dotfiles`. We need to fork because each of you will need to put specific information (e.g. your name) in those files.

Open your terminal. **Don't blindly copy paste this line**, replace `replace_this_with_your_github_username` with *your*

own github usernickname.

```bash

export GITHUB_USERNAME=replace_this_with_your_github_username

# Eample:

#   export GITHUB_USERNAME=ssaunier

```

Now copy/paste this very long line in your terminal. Do **not** change this one.

```bash

Export WIN_DIR=`pwd` && cd ~ && git clone [git@github.com](mailto:git@github.com):$GITHUB_USERNAME/dotfiles.git ~/ && cd $WIN_DIR

```

Run the `dotfiles` installer.

```bash

cd ~/dotfiles

zsh install.sh

```

Then run the git installer:

```bash

cd ~/dotfiles

zsh git_setup.sh

```

:point_up: This will **prompt** you for your name (`Firstname Lastname`) and your email.

Be careful, you **need** to put the **same** email as the one you sign up with on GitHub.

## Auto-start `ssh-agent`

You don't want to be asked for your passphrase every time you communicate with a distant repository. So you need to add the plugin `ssh-agent` to `oh my zsh`.

First open `.zshrc` file:

```bash

code ~/.zshrc

```

Spot the line starting with `plugins=` Then add `ssh-agent` to the plugins list. The list should look like:

```

plugins=(gitfast last-working-dir common-aliases sublime zsh-syntax-highlighting history-substring-search ssh-agent)

```

Save the `.zshrc` file with `Ctrl` + `S` and you can close VS Code

## Installing Ruby (with [rbenv](https://github.com/sstephenson/rbenv))

First we need to clean up any previous Ruby installation you might have:

```bash

rvm implode && sudo rm -rf ~/.rvm

# If you got "zsh: command not found: rvm", carry on. It means `rvm` is not

# on your computer, that's what we want!

rm -rf ~/.rbenv

```

Then in the terminal, run:

```bash

sudo apt-get update

sudo apt-get install -y zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev

git clone https://github.com/rbenv/rbenv.git ~/.rbenv

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc

echo 'eval "$(rbenv init -)"' >> ~/.zshrc

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build

echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.zshrc

```

**Close your terminal and open it again** (Alt+F4 and restart it). If you get a warning, just **ignore** it from now (Ruby is not installed yet).

Now, you are ready to install the latest ruby version, and set it as the default version.

Run this command, it will **take a while (5-10 minutes)**

```bash

rbenv install 2.5.3

```

Once the ruby installation is done, run this command to tell the system

to use the 2.5.3 version by default.

```bash

rbenv global 2.5.3

```

Then **restart** your Terminal again (close it and reopen it).

```bash

ruby -v

```

You should see something starting with `ruby 2.5.3p`. If not, ask a teacher.

## Installing some gems

---

:warning: If you are in **China** :cn:, you should update the way we'll install gem with the following commands. If you are not in China, well just skip this and go directly to the next `gem install` command!

```bash

# China only!

gem sources --remove https://rubygems.org/

gem sources -a https://gems.ruby-china.com/

gem sources -l

# *** CURRENT SOURCES ***

# https://gems.ruby-china.com/

# Ruby-china.com must be in the list now

```

---

All, please run the following line:

```bash

gem install rake bundler rspec rubocop rubocop-performance pry pry-byebug hub colored octokit

```

**Never** install a gem with `sudo gem install`! Even if you stumble upon a Stackoverflow answer

(or the Terminal) telling you to do so.

## Postgresql

In a few weeks, we'll talk about SQL and Databases and you'll need something called Postgresql,

an open-source robust and production-ready database. Let's install it now.

Download Postgres for Windows from here: https://www.postgresql.org/download/windows/

Click through the installer, but on the last page be sure not to run (THAT THING I DONT REMEMBER)

Now in your terminal, we need to install a couple dependencies so that your ubuntu can talk to Postgres on Windows.

```Bash

sudo apt-get install postgresql-contrib

sudo -u postgres psql -p 5432 -h localhost --command "CREATE ROLE `whoami` LOGIN createdb;"

```

Now, in your windows file explorer, go to C:/Users/YOUR_USER_NAME/Program Files/Postgres/11/data

Find and open the file named pq_hba.conf

Change all values from from ```md5``` to ```trust```

## Check-up

Let's check if you successfully installed everything.

Quit all opened Terminal, open a new one and run the following commands:

```bash

curl -Ls https://raw.githubusercontent.com/lewagon/setup/master/check.rb > _.rb && ruby _.rb || rm _.rb

```

It should tell you if your workstation is ready :) If not, ask a teacher.

## Alumni

Register as a Wagon alumni by going to [kitt.lewagon.com/onboarding](http://kitt.lewagon.com/onboarding). Select your batch, sign in with GitHub and enter all your information.

Your teacher will then validate that you are indeed part of the batch. You can ask him to do it as soon as you completed the registration form.

Once the teacher has approved your profile, go to your email inbox. You should have 2 emails:

- One from Slack, inviting you to the Le Wagon Alumni slack community (where you'll chat with your buddies and all the previous alumni). Click on **Join** and fill the information.

- One from GitHub, inviting you to `lewagon` team. **Accept it** otherwise you won't be able to access the lecture slides.

## Slack

Download and install the Slack app from [slack.com](https://slack.com/downloads/windows), and install it.

Launch the app and sign in to `lewagon-alumni` organization.

Make sure you upload a picture there.

You can also sign in to Slack on your iPhone or Android device!

The idea is that you'll have Slack open all day, so that you can share useful links / ask for help / decide where to go to lunch / etc.

Enjoy your ride with Le Wagon :)