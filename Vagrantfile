# -*- mode: ruby -*-
# vi: set ft=ruby :

Dotenv.load
Vagrant.configure(2) do |config|
  config.vm.box = "futureys/centos-7"
  config.vbguest.no_install = true
  config.vm.provider "virtualbox" do |vm|
    vm.memory = 2048
  end

  config.vm.hostname = "rails"
  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 443, host: 443
  config.vm.network :forwarded_port, guest: 3000, host: 3000
  # config.vm.synced_folder "./", "/vagrant", type:"nfs"
  config.vm.provision "ansible_local" do |ansible|
    ansible.install        = false
    ansible.inventory_path = "./inventories/development"
    ansible.playbook       = "playbook.yml"
    ansible.skip_tags      = "cleaning"
    ansible.verbose        = "vvv"
    ansible.extra_vars        = {
        mysql_5_7_root_password: ENV['MYSQL_5_7_ROOT_PASSWORD'],
        mysql_5_7_user_password: ENV['MYSQL_5_7_USER_PASSWORD']
    }
  end
end
