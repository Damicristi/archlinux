<h4>Table of contents</h4>

1. [Author's Linux Machine info](#1)
2. [Hack all my config files](#2)
3. [Extend Display/monitors](#3)
4. [Add full name of user in login manager](#4)
5. [Check package version](#5)
6. [Hide dotfiles in mc file manager](#6)
7. [Create a symlink folderof mount partition](#7)
8. [Use git to track the dotfiles](#8)

<h5 id="1">Author's Linux Machine info</h5>
<asciinema-player src="https://raw.githubusercontent.com/Damicristi/archlinux/master/files/screenfetch"></asciinema-player>

<h5 id="2"> Hack all my config files</h5>
You can find all my config files at [GitHub](https://github.com/Damicristi/dotfiles).

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
$ mkdir ~/FolderToWhichYouWantToSymlink
$ ln -s /mnt/YourPartition ~/FolderToWhichYouWantToSymlink
```

Note: ~ and $HOME are home directory's very close synonyms.

<h5 id="8"> Use git to track the dotfiles</h5>
I use folder named dotfiles to keep track my dotfiles and then, I upload to remote git repository (say, GitHub). Believe me, this is very easy to use.
```
$ mkdir $HOME/dotfiles
$ git init --bare $HOME/dotfiles
$ echo "alias config='/usr/bin/git --git-dir=$HOME/dotfiles --work-tree=$HOME'" >> $HOME/.YourShell-rc-File
```

For example:
```
$ echo "alias config='/usr/bin/git --git-dir=$HOME/dotfiles --work-tree=$HOME'" >> $HOME/.zshrc
```

OR,

Add this line in the .zshrc file:

alias config='/usr/bin/git --git-dir=$HOME/dotfiles --work-tree=$HOME'"

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