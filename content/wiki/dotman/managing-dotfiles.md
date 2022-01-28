---
title: Managing Dotfiles
desc: 'Learn how to manage your dotfiles with Dotman.'
category: Dotman
position: 2
---
# Dotfiles

Dotfiles are files that are used to store configuration information. \
Dotfiles are usually stored in the `.config` directory in your home directory but they can be anywhere. \
With dotfiles you can configure your system in a way you can constumize anthing and maintain. \

But maintaing dotfiles is not easy. \
You have to know what files you want to store and where. \
That's why dotman is here to help you.

## Initializing

We will be using a github repo to store our dotfiles. \
To initialize dotman you need to run the following command:

```bash
$ mkdir MyDotfiles
$ dotman init MyDotfiles --git --remote="https://github.com/YOUR_USERNAME/YOUR_REPO" --branch="master"
```

this command will initialize dotman in your current working directory.

## Adding Dotfiles

To add dotfiles you need to have a file to add... :D \
So lets create a file called `.bashrc` and add it to the dotfiles repo:

```bash
$ touch .bashrc
$ echo "echo Hello World!" > .bashrc
```

Now we can add this file to the dotfiles repo:

```bash
$ dotman add my_bashrc .bashrc --description="My bashrc file"
```

You can see 2 things are generated:

- A new folder and file, `files/.bashrc`
- A new dotfile object in `dotman.json`

these files are used to store the dotfile. \
Yes! dotman does not uses symlinks to store dotfiles. \
It makes it easier to manage dotfiles and features.
