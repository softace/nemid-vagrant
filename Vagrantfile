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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

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
  config.vm.synced_folder "#{ENV['HOME']}/.oces", "/home/vagrant/.oces"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Name for VirtualBox
    vb.name = "NEMID_keyfile"

    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  firefox_addon_version = "1.41"
  firefox_addon_file = "nnp_firefox-#{firefox_addon_version}.xpi"
  nemidnoglefilsprogram_version = "1.10.0"
  nemidnoglefilsprogram_file = "nemidnoglefilsprogram-#{nemidnoglefilsprogram_version}.deb"

  config.vm.provision "shell", inline: <<-SHELL
timedatectl set-timezone Europe/Copenhagen
locale-gen da_DK.UTF-8
apt-get update
apt-get upgrade
apt-get install -y jq unzip wget firefox firefox-locale-da
wget --quiet https://www.medarbejdersignatur.dk/nemid-noglefilsprogram/download/#{firefox_addon_file}
mv #{firefox_addon_file} /usr/lib/firefox/browser/extensions/`unzip -qqc #{firefox_addon_file} manifest.json | jq -r '.applications.gecko.id'`.xpi
wget --quiet https://www.medarbejdersignatur.dk/nemid-noglefilsprogram/download/#{nemidnoglefilsprogram_file}
dpkg -i #{nemidnoglefilsprogram_file}
SHELL

end
