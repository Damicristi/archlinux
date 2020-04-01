<h4>Table of contents</h4>

0. [Arch Linux Installation](#0)
1. [Author's Linux Machine info](#1)
2. [Hack all my config files](#2)
3. [Extend Display/monitors](#3)
4. [Add full name of user in login manager](#4)
5. [Check package version](#5)
6. [Hide dotfiles in mc file manager](#6)
7. [Create a symlink folder of mount partition](#7)
8. [Use git to track the dotfiles](#8)
9. [Auto mount the external drives using udiskie](#9)


<h5 id="0">Arch Linux Installation</h5>
It is always a wise decision to follow Arch Linux installation from arch wikipage at <a href="https://wiki.archlinux.org/index.php/installation_guide">link</a>.

<h5 id="1">Author's Linux Machine info</h5>
<asciinema-player src="https://raw.githubusercontent.com/Damicristi/archlinux/master/files/screenfetch"></asciinema-player>

<h5 id="2"> Hack all my config files</h5>
You can find all my config files at <a href="https://github.com/Damicristi/dotfiles">Github</a>.

<h5 id="3"> Extend Display/monitors (install mons from pacaur)</h5>
<asciinema-player src="https://raw.githubusercontent.com/Damicristi/archlinux/master/files/mons"></asciinema-player>

<h5 id="4"> Add full name of user in login manager</h5>
```
sudo chfn -f "Firstname Lastname" "username"
```

<h5 id="5"> Check package version</h5>
```
pacman -Qi package-name
```

<h5 id="6"> Hide dotfiles in mc file manager</h5>
It's annoying when I see dot(files | folders) all the time in Midnight Commander file manager (mc for short). 
So, to get rid off: Use ESC+period (.) or ALT+ period or click F9 -> O -> P -> h -> o.

<h5 id="7">Create a symlink folder of mount partition</h5>
I use ~Store Room as a symlink folder of mount ntfs partition. You can do so by:
```
$ ln -s /mnt/YourPartition ~/FolderToWhichYouWantToSymlink
```

Note: ~ and $HOME are home directory's very close synonyms.

<h5 id="8"> Use git to track the dotfiles</h5>
I use folder named .dotfiles to keep track my dotfiles and then, I upload to remote git repository (say, GitHub). Believe me, this is very easy to use.
I strongly recommend to use period (.) infront of folder (or file) name, if the folder(or file) is not use very often such that it will be consider as hidden.
```
$ mkdir $HOME/.dotfiles
$ git init --bare $HOME/.dotfiles
$ echo "alias config='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'" >> $HOME/.YourShell-rc-File
```

For example:
```
$ echo "alias config='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'" >> $HOME/.zshrc
```

OR,

Add this line in the .zshrc file:
```
alias config='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'"
```

I've created an alias named config which means instead of using the command git, we use config.

Usage:

First, go to the dotfile path to which you want to track.
```
$ config add .filename
$ config commit -m "+ .filename"
```

Then, add newly created remote repository in your local machine, after that push it.
```
$ config push origin master
```

Note: I use "+" in my commit message as "Added my".

<h5 id="9"> Auto mount the external drives using udiskie</h5>
I use "udiskie" package (GUI for udisks2) to auto-mount my external drives, and in i3wm config, I added this line:
```
exec --no-startup-id udiskie -nas
```

where flags nas means notification, auto-mount and smart tray respectively.

I also created a symlink folder named "External Devices" in the home directory by doing these:

1. Create a directory name as /media:
```
$ sudo mkdir /media
```

2. Open nano by typing this:
```
$ sudo nano /etc/udev/rules.d/99-udisks2.rules
```

Paste this command and save it:
```
# UDISKS_FILESYSTEM_SHARED
# ==1: mount filesystem to a shared directory (/media/VolumeName)
# ==0: mount filesystem to a private directory (/run/media/$USER/VolumeName)
# See udisks(8)
ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1"
```

2. Create symlink as:
```
$ ln -s /media ~/External\ Devices
```

<b>Bonus tip:</b> I also use "lsd" pacakge to have icon when I want to list all files & folders inside a directory. 
Simply, this is an alternative to ls command. You can create an alias as ls for lsd in your shell config.
