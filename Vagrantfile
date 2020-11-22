# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.network :private_network, ip: "192.168.33.34"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  config.vm.provision "shell", inline: <<-EOT
  echo 'user root process'
  cp -p /usr/share/zoneinfo/Japan /etc/localtime
  apt update -y
  apt install -y make build-essential libssl-dev zlib1g-dev \
  libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev\
  libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl\
  git
  chmod 777 /vagrant/setup.sh
  EOT

  config.vm.provision "shell", privileged: false, inline: <<-EOT
  echo 'user vagrant process'
  cd
  git clone https://github.com/pyenv/pyenv.git ~/.pyenv
  echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
  echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
  echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
  source ~/.bash_profile
  pyenv install 3.8.3
  EOT

end

