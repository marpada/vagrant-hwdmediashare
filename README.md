Sample Vagrant setup to use the [hwdmediashare
cookbook](https://github.com/marpada/hwdmediashare-cookbook) easily without a
proper Chef development environment.

It will provision a development box for Joomla/hwdMediaShare with all
requirements installed:

* Ubuntu 14.04
* Apache 2.4 + mod_h264 module
* PHP 5.5
* MySQL
* Multimedia conversion tools: ffmpeg, yamdi,
  qt-faststart,imagemagick,...
* [adminer](www.adminer.org) for easy MySQL management
* synced joomla folder

## Getting started

1. Install Vagrant
2. Install VirtualBox
3. Install the [Vagrant omnibus](https://github.com/chef/vagrant-omnibus) plugin
4. Clone this repo
5. vagrant up
6. Make yourself a cup of coffee
7. Profit!

After a successful run http://172.28.128.3 will show Joomla
installation page.

## Going further

While all the chef meat is on the original cookbook <https://github.com/marpada/hwdmediashare-cookbook>, the Vagrant file exposes the most important attributes:

* `node['mysql']['server_root_password']` : MySQL root password
* `node['hwdmediashare']['mysql']['joomla_db_name']` : Joomla DB name
* `node['hwdmediashare']['mysql']['joomla_db_user']` : Joomla DB user
* `node['hwdmediashare']['mysql']['joomla_db_password']` : Joomla DB
* `node['hwdmediashare']['joomla_package_url']` : URL to Joomla tarball
  (.tar.gz)

Several chef community cookbooks are leveraged (apache,mysql,php) so
feel free to override their attributes to your convenience.

## Author and license

Author: David Pando (<david.pando+github@gmail.com>)

License: [MIT License](http://www.opensource.org/licenses/MIT).
