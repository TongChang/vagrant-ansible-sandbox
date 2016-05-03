# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_git = <<INSTALL_GIT
  echo provisioning git...
  apt-get install git -y
INSTALL_GIT

$install_curl = <<INSTALL_Curl
  echo provisioning curl...
  apt-get install curl -y
INSTALL_Curl

$install_vim = <<INSTALL_VIM
  echo provisioning vim...
  apt-get install vim -y
  curl -o /home/vagrant/.vimrc https://raw.githubusercontent.com/TongChang/dotfiles/master/vim/_vimrc
INSTALL_VIM

$install_ansible = <<INSTAL_Ansible
  echo provisioning ansible...
  apt-get ansible
INSTAL_Ansible
Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty32"

  config.vm.define :manager do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2001, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.11"

    node.vm.provision "manager-git", type: "shell" do |s|
      s.inline = $install_git
    end

    node.vm.provision "manager-vim", type: "shell" do |s|
      s.inline = $install_vim
    end
  end

  config.vm.define :rpi_1 do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2011, id: "ssh"
    node.vm.network :forwarded_port, guest: 80, host: 8000, id: "http"
    node.vm.network :private_network, ip: "192.168.33.12"
  end

end
