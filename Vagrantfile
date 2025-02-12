# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

BOX_IMAGE = "MetroStar/spel-minimal-centos-7"
NODE_COUNT = 1

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "centos/7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  #config.vm.network "forwarded_port", guest: 8200, host: 8200

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  #config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  #config.vm.network "private_network", ip: "10.100.0.0"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.synced_folder './salt', '/srv/salt'
  config.vm.synced_folder './.pillar/dev', '/srv/pillar'
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network :private_network, ip: "10.0.1.#{i + 10}"
      subconfig.vm.network "forwarded_port", guest: 8200, host: 8200, auto_correct: true
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    cd /root/
    # yum update -y && yum upgrade -y
    # yum install -y curl unzip epel-release yum-utils jq

    ## Python3
    # yum install -y https://repo.saltstack.com/py3/redhat/salt-py3-repo-2018.3.el7.noarch.rpm

    # Python2
    yum install -y https://repo.saltstack.com/yum/redhat/salt-repo-2018.3.el7.noarch.rpm

    yum clean expire-cache

    yum install salt-master -y
    yum install salt-minion -y

    echo 'Change permission for dirs'
    chmod +x /usr/local/bin/
    chgrp -R root /usr/local/bin
    chown root /usr/local/bin/
    if [[ ! $(grep '/usr/local/bin' /root/.bash_profile) ]]; then
      echo 'export VAULT_ADDR="http://$(hostname):8200"' >> /root/.bash_profile
      echo 'export VAULT_TOKEN=root' >> /root/.bash_profile
      echo 'alias l="ls -lah"' >> /root/.bash_profile
    fi

    if [[ ! $(grep '/usr/local/bin' /home/vagrant/.bash_profile) ]]; then
      echo 'export PATH=$PATH:/usr/local/bin' >> /home//vagrant/.bash_profile
      echo 'export VAULT_ADDR="http://$(hostname):8200"' >> /home/vagrant/.bash_profile
      echo 'export VAULT_TOKEN=root' >> /home/vagrant/.bash_profile
      echo 'alias l="ls -lah"' >> /home/vagrant/.bash_profile
    fi
  SHELL

  config.vm.provision "shell", inline: <<-SHELL

    # echo "Setting the required salt grains for vault..."
    # salt-call --local grains.setval vault '{"dev_mode": true, "dev_configs": "-dev -dev-root-token-id=root", "api_port": 8200, "cluster_port": 8201}'

    echo "Updating salt states/modules/utils/grains..."
    salt-call --local saltutil.sync_all
  SHELL

end
