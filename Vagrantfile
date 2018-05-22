# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.disksize.size = '50GB'
  config.vm.define "openstack" do |stack|
    stack.vm.box = "ubuntu/xenial64"
    ENV['LC_ALL']="en_US.UTF-8"
    stack.vm.hostname = "openstack"
#    ap.ssh.username = "vagrant"
#    ap.ssh.password = "vagrant"
    stack.vm.network "forwarded_port", guest: 80, host: 8888
    stack.vm.network :private_network, ip: "192.168.0.206"
    stack.vm.synced_folder "./", "/openstack"
    stack.vm.provider "virtualbox" do |vb|
	vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
        vb.gui = false
        vb.memory = "10240"
        vb.cpus = "2"
        vb.name = "openstack"
    end
    stack.vm.provision "ansible" do |ansible|
        ansible.playbook = "roles/playbook.yml"
        ansible.inventory_path = "roles/inventory"
        ansible.become = true
        ansible.verbose = "vv"
    end
  end
end
