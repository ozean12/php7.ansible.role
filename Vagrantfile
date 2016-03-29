# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Ubuntu 14.04
  config.vm.define "ubuntu" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.network "private_network", ip: "10.0.0.10"
    
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "setup.yml"
      ansible.sudo = true
    end
  end

  # CentOS 6.7
  #config.vm.define "centos6", primary: true do |node|
  #    node.vm.box = "bento/centos-6.7"
  #    node.vm.network "private_network", ip: "10.0.0.10"
  
  #    node.vm.provision "ansible" do |ansible|
  #        ansible.playbook = "setup.yml"
  #        ansible.sudo = true
  #    end
  #end
  
  # CentOS 7.2
  #config.vm.define "centos7", primary: true do |node|
  #    node.vm.box = "bento/centos-7.2"
  #    node.vm.network "private_network", ip: "10.0.0.10"
  
  #    node.vm.provision "ansible" do |ansible|
  #        ansible.playbook = "setup.yml"
  #        ansible.sudo = true
  #    end
  #end
  
end
