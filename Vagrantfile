# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :db do |db_config|
    db_config.vm.box = "precise64"
    db_config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    db_config.vm.network :forwarded_port, guest: 8983, host: 8983
    db_config.vm.network :forwarded_port, guest: 5000, host: 5050
    db_config.vm.network :private_network, ip: "192.168.33.20"
  
    db_config.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/dbservers.yml"
      ansible.inventory_path = "vagrant_ansible_inventory_db"
    end
  end
  

  config.vm.define :web do |web_config|
    web_config.vm.box = "precise64"
    web_config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    
    web_config.vm.network :forwarded_port, guest: 80, host: 8080
    web_config.vm.network :private_network, ip: "192.168.33.10"
  
    web_config.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/webservers.yml"
      ansible.inventory_path = "vagrant_ansible_inventory_web"
    end
  end
  
end