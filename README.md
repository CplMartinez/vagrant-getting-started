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

##Provisioning

1. Create the following shell script and save it as `bootstrap.sh` in the same directory as your Vagrantfile:

```bash
#!/usr/bin/env bash

apt-get update
apt-get install -y apache2
if [ -L /var/www/ ]; then
	rm -rf /var/www
	ln -fs /vagrant /var/www
fi
```
2. We do this by editing the Vagrantfile, wich should now look like this:
```ruby
Vagrant.configure("2") do |config|
	config.vm.box = "hashicorp/precise32"
	config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
	config.vm.provision :shell, path: "bootstrap.sh"
end
```
3. After everything is configured, just run `vagrant up` or `vagrant reload --provision` if guest machine is already running from previous step.

4. SSH into the machine

```bash
$ vagrant ssh

vagrant@precise32 wget -qO- 127.0.0.1
 ```

##Networking

1. Doing so is a simple edit to the Vagrantfile, which now looks like this:

```ruby
Vagrant.configure("2") do |config|
	config.vm.box = "hashicorp/precise32"
	config.vm.provision :shell, path: "bootstrap.sh"
	config.vm.networking :forwarded_port, guest: 80, host: 4567
	config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
end
```
2. Run `vagrant reload` or `vagrant up`

3. Load [http://127.0.0.1:4567](http://127.0.0.1:4567) 

##Share


### Login to hashicorps atlas

1. Before being able to share your Vagrant envoriment you'll need an account on [HashiCorp's Atlas](https://atlas.hashicorp.com/) don't worry, it's free. Once you have an account, log using `vagrant login`

```bash
$ vagrant login
Username or Email: hugobrilhante
Password (will be hidden):
You're now logged in!
```

### Share
1. Once you're logged in, run `vagrant share`

```bash
$ vagrant share
...
==> default: Your Vagrant Share is running! Name: rambunctious-orangutan-8613
==> default: URL: http://rambunctious-orangutan-8613.vagrantshare.com
...
```

#Teardown

1. Check [Vagrant docs](https://docs.vagrantup.com/v2/getting-started/teardown.html)
