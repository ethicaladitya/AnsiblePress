# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  site_dir = "/var/www/wordpress/"

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "web" do |web|
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.network "forwarded_port", guest: 443, host: 8443
    web.vm.network "private_network", ip: "192.168.50.50"
    web.vm.synced_folder "../WordPress", site_dir, owner: 'vagrant', group: 'www-data', mount_options: ['dmode=776', 'fmode=775']

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