# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"

  (1..3).each do |n|
    node_id = "node#{n}"
    ip_address = "192.168.33.1#{n}"

    config.vm.define node_id do |c|
      c.vm.network "private_network", ip: ip_address
      c.vm.host_name = node_id

      c.vm.provision "shell", inline: <<-SHELL
        curl https://download.docker.com/linux/centos/docker-ce.repo -o /etc/yum.repos.d/docker.repo
        yum makecache fast
        yum install net-tools docker-ce -y

        systemctl start docker
      SHELL
    end
  end
end
