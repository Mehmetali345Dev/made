---
title: Generating installer scripts
desc: 'Learn how to create installers from your dotfiles with Dotman.'
category: Dotman
position: 3
---
# Installers
With dotman you can create installers to install dotfiles. \
You can create installers to install dotfiles from a git repo, \
You can do anything you want with installers. \
They are basically automaticly generated bash scripts that will install dotfiles and run your custom commands.

We will create an basic installer that installs our dotfiles:

```bash
$ dotman installer add my_installer --description="My installer"
```

## Commands

This command will create a new installer called `my_installer` and add it to `dotman.json`. \
But it does not have any custom commands. \
So why not add some?

```bash
$ dotman command add "echo I'm Pickle Riiiick!!"
```

## Generating

We added a dotfile, \
an installer, \
and a command. \
Now we need to generate the installer. 

In dotman installers will generate in the `installers` directory. \
with their own unique name: `installer[my_installer].sh` 

So let's generate the installer:
```bash
$ dotman generate my_installer
```

Tada...! You created your own dot with dotman! \
and you can use it to install dotfiles.
