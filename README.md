# Vagrant getting started

## Project Setup

1. Vagrant command for initializing a directory for usage:`vagrant init`

```bash
$ vagrant init
```
## Installing a box

1. Box are added to vagrant with `vagrant box`.
```bash
$ vagrant box add hashicorp/precise3
```

## Up and SSH

1. Run virtual machine without a UI with `vagrant up`
```bash
$ vagrant up
```

2. SSH into the machine `vagrant ssh`.
```bash
$ vagrant ssh
```
## Synced Folders

1. Vagrant shares your project directory to the `/vagrant` directory in your gest machine.

```bash

$ vagrant up

$ vagrant ssh

vagrant@precise32:~$ ls /vagrant
Vagrantfile

vagrant@precise32:~$ touch /vagrant/foo
vagrant@precise32:~$ exit

$ ls
foo Vagrantfile
```

