# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "chef/ubuntu-14.04"
  config.vm.network "private_network", ip: "172.28.128.3"

  config.vm.provider "virtualbox" do |v|
    v.name = 'hwdmediashare'
    v.memory = 1024
    v.cpus = 2
  end


  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "joomla/", "/var/www/hwdmediashare"
  config.vm.synced_folder "logs/", "/var/log/apache2", :owner => 'root', :group => 'vagrant'

  config.vm.provision :shell, :inline => "which chef-solo || wget -O - https://opscode.com/chef/install.sh | sudo bash"
  config.vm.provision :chef_zero do |chef|
    chef.json = {
      mysql: {
        server_root_password: 'ChangeMe'
      },
      hwdmediashare: {
        docroot: '/var/www/hwdmediashare',
        mysql: {
          joomla_db_name: 'joomla',
          joomla_db_user: 'joomla',
          joomla_db_password: 'ChangeMe'
        },
        joomla_package_url: "http://joomlacode.org/gf/download/frsrelease/20021/162256/Joomla_3.4.1-Stable-Full_Package.tar.gz"
      }
    }
    chef.recipe_url = 'https://github.com/marpada/hwdmediashare-cookbook/releases/download/v0.1.2/hwdmediashare-cookbook-v0.1.2.tar.gz'
    chef.run_list = [
        "recipe[apt]",
        "recipe[hwdmediashare::default]"
    ]
  end
end
