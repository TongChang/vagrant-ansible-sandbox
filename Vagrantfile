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
    chown vagrant:vagrant /home/vagrant/.ssh/id_rsa
  else
    echo skip create id_rsa...
  fi
CREATE_id_rsa

$setup_bashrc = <<SETUP_Bashrc
  IS_SETUPED=`grep "set -o vi" /home/vagrant/.bashrc | wc -l`

  if [ ! 1 -eq ${IS_SETUPED} ]; then
    echo setup bashrc...
    echo "set -o vi" >> /home/vagrant/.bashrc
  else
    echo skip setup bashrc...
  fi
SETUP_Bashrc

$setup_id_rsa_pub = <<SETUP_id_rsa_pub
  if ! dpkg -l sshpass; then
    echo install sshpass...
    apt-get install sshpass -y
  else
    echo skip install sshpass...
  fi

  sshpass -p "vagrant" scp  -oStrictHostKeyChecking=no vagrant@192.168.33.11:/home/vagrant/.ssh/id_rsa.pub /home/vagrant/manager_pub
  phrase=`cat /home/vagrant/manager_pub`
  IS_SETUPED=`grep "${phrase}" /home/vagrant/.ssh/authorized_keys | wc -l`

  if [ ! 1 -eq ${IS_SETUPED} ]; then
    echo setup id_rsa_pub...
    cat /home/vagrant/manager_pub >> /home/vagrant/.ssh/authorized_keys
  else
    echo skip setup id_rsa_pub...
  fi

  rm -f /home/vagrant/manager_pub

SETUP_id_rsa_pub

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

    node.vm.provision "manager-ansible", type: "shell" do |s|
      s.inline = $install_ansible
    end

    node.vm.provision "manager-id_rsa", type: "shell" do |s|
      s.inline = $create_id_rsa
    end

    node.vm.provision "manager-bashrc", type: "shell" do |s|
      s.inline = $setup_bashrc
    end

  end

  config.vm.define :rpi_1 do |node|
    node.vm.network :forwarded_port, guest: 22, host: 2011, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.12"

    node.vm.provision "rpi_1-get-id_rsa-pub", type: "shell" do |s|
      s.inline = $setup_id_rsa_pub
    end
  end

end
