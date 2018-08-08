# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt-get -qq update
      sudo apt-get -qq install -y python-pip unzip jq ruby apt-transport-https ca-certificates curl software-properties-common docker-ce ack-grep
      pip install -q terrafile
      pip install -q aws-sam-cli
      pip install -q awscli
      sudo gem install terraforming
      wget --quiet https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip
      unzip terraform_0.11.7_linux_amd64.zip
      mkdir -p /home/ubuntu/bin/
      mv terraform /home/ubuntu/bin/
      rm -f terraform_0.11.7_linux_amd64.zip
      sudo usermod -aG docker ubuntu
      wget --quiet -c https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz
      tar xzf go1.9.linux-amd64.tar.gz
      sudo mv go /usr/local/
      sudo chown -R root:root /usr/local/go
      echo "PATH=\$PATH:/usr/local/go/bin" | sudo tee /etc/profile.d/go.sh
      cat << EOF >> /home/ubuntu/.bashrc
alias ..='cd ..'
alias ...='cd ../..'
alias ls='ls -G'
alias ll='ls -lG'
alias dir='ls -lG'
alias gits='git status'
alias gs='git status'
alias gl='git log'
alias ga='git add'
alias gd='git diff'
alias gita='git add'
alias gitc='git commit -m'
alias gitco='git checkout'
alias gpl='git pull'
alias gph='git push'
alias gba='git branch -a'
alias gg='git graph --all'
alias tmp='cd ~/tmp;ls -l'
alias okta='go get github.com/segmentio/aws-okta && aws-okta add'
aws configure
PATH=$PATH:/usr/local/go/bin:~/go/bin
EOF
   SHELL
end
