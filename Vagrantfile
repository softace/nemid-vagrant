# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?("vagrant-vbguest")
#    config.vbguest.no_install  = true
    config.vbguest.auto_update = false
#    config.vbguest.no_remote   = true
  end

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/jammy64"

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

  # Basics
  mozilla_firefox = <<-MOZILLA
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
MOZILLA

  config.vm.provision "shell", inline: <<-SHELL
timedatectl set-timezone Europe/Copenhagen
locale-gen da_DK.UTF-8
update-locale LANG=da_DK.UTF-8
add-apt-repository --yes ppa:mozillateam/ppa
apt-get update
apt-get --yes upgrade
echo -e "#{mozilla_firefox.gsub("\n","\\n")}" > /etc/apt/preferences.d/mozilla-firefox
apt-get install -y jq unzip wget libgl-dev libegl-dev firefox firefox-locale-da
SHELL

  # NemId Nøglefilsprogram
  nemidnoglefilsprogram_version = "1.10.0"
  nemidnoglefilsprogram_file = "nemidnoglefilsprogram-#{nemidnoglefilsprogram_version}.deb"
  config.vm.provision "shell", inline: <<-SHELL
wget --quiet https://www.medarbejdersignatur.dk/nemid-noglefilsprogram/download/#{nemidnoglefilsprogram_file}
dpkg -i #{nemidnoglefilsprogram_file}
SHELL

  # Firefox extension
  #For details, see https://www.medarbejdersignatur.dk/nemid-noglefilsprogram/download/dlconfig.js
  firefox_addon_version = "1.41"
  firefox_addon_file = "nnp_firefox-#{firefox_addon_version}.xpi"
  config.vm.provision "shell", inline: <<-SHELL
wget --quiet https://www.medarbejdersignatur.dk/nemid-noglefilsprogram/download/#{firefox_addon_file}
mv #{firefox_addon_file} /usr/lib/firefox/browser/extensions/`unzip -qqc #{firefox_addon_file} manifest.json | jq -r '.applications.gecko.id'`.xpi
SHELL

  # Firefox extension user-agent switcher
  uas_extension_version = "0.4.8"
  uas_extension_file = "user_agent_string_switcher-#{uas_extension_version}.xpi"
  config.vm.provision "shell", inline: <<-SHELL
wget --quiet https://addons.mozilla.org/firefox/downloads/file/3952467/#{uas_extension_file}
mv #{uas_extension_file} /usr/lib/firefox/browser/extensions/`unzip -qqc #{uas_extension_file} manifest.json | jq -r '.browser_specific_settings.gecko.id'`.xpi
SHELL

  config.vm.provision "shell", inline: <<-SHELL
echo "Installation er færdig. Åbn en browser med"
echo "vagrant ssh -- -X firefox -no-remote"
SHELL

end
