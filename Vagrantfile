 Vagrant.configure("2") do |config|
	 config.vm.box = "hashicorp/precise32"
	 config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
	 config.vm.provision :shell, path: "bootstrap.sh"

 end
