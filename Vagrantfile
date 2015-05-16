# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "web" do |web|
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.network "forwarded_port", guest: 443, host: 8443
    web.vm.network "private_network", ip: "192.168.50.50"
    web.vm.synced_folder "../www/app", "/vagrant-nfs", type: "nfs"
  end

  config.bindfs.bind_folder "/vagrant-nfs", "/var/www/app", :owner => "root", :group => "root"


  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = './site.yml'
    ansible.groups = {
      'web' => ['development'],
      'development' => ['default']
    }

    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant',
      user: 'vagrant',

    }
    ansible.sudo = true
  end
end