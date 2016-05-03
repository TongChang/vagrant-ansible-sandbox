# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_git = <<INSTALL_GIT
  if ! dpkg -l git; then
    echo provisioning git...
    apt-get install git -y
  else
    echo skip provision git...
  fi
INSTALL_GIT

$install_curl = <<INSTALL_Curl
  if ! dpkg -l curl; then
    echo provisioning curl...
    apt-get install curl -y
  else
    echo skip provision curl...
  fi
INSTALL_Curl

$install_vim = <<INSTALL_VIM
  if ! dpkg -l vim; then
    echo provisioning vim...
    apt-get install vim -y
  else
    echo skip provision vim...
  fi

  if [ ! -f /home/vagrant/.vimrc ]; then
    echo downloading vimrc...
    curl -o /home/vagrant/.vimrc https://raw.githubusercontent.com/TongChang/dotfiles/master/vim/_vimrc
  else
    echo skip download vimrc...
  fi
INSTALL_VIM

$install_ansible = <<INSTAL_Ansible
  if ! dpkg -l ansible; then
    echo provisioning ansible...
    apt-get install ansible -y
  else
    echo skip provision ansible...
  fi
INSTAL_Ansible

$create_id_rsa = <<CREATE_id_rsa
  if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
    echo create id_rsa...
    ssh-keygen -t rsa -N bebop -C bebop -f /home/vagrant/.ssh/id_rsa
  else
    echo skip create id_rsa...
  fi
CREATE_id_rsa

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty32"

  config.vm.define :rpi_1 do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2011, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.12"
  end

  config.vm.define :manager do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2001, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.11"

    node.vm.provision "manager-git", type: "shell" do |s|
      s.inline = $install_git
    end

    node.vm.provision "manager-vim", type: "shell" do |s|
      s.inline = $install_vim
    end

    node.vm.provision "manager-ansible", type: "shell" do |s|
      s.inline = $install_ansible
    end

    node.vm.provision "manager-id_rsa", type: "shell" do |s|
      s.inline = $create_id_rsa
    end
  end

end
