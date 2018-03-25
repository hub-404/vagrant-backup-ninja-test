# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.box_check_update = false

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder ".", "/vagrant", type: "nfs", disabled: true
  config.vm.provider :virtualbox do |vb|
        vb.memory = 2048
        vb.cpus = 2
        vb.linked_clone = true
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end
  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.become_user = 'root'
      ansible.become = true
      ansible.verbose = "v"
      ansible.compatibility_mode = '2.0'
      if ENV['ANSIBLE_TAGS'] then ansible.tags = ENV['ANSIBLE_TAGS']; end
  end

end
