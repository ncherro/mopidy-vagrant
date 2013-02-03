# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

  config.vm.box = "lucid32"
  config.vm.box_url = "http://files.vagrantup.com/lucid32.box"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe("mopidy")
    chef.json = {
      :mopidy => {
        :spotify_username => ENV['SPOTIFY_USERNAME'],
        :spotify_password => ENV['SPOTIFY_PASSWORD'],
        :http_server_hostname => '::',
        :http_server_port => 6680,
        :http_server_static_dir => '/vagrant/www',
      }
    }
  end

  config.vm.customize ["modifyvm", :id, "--audio", "coreaudio"]
  config.vm.customize ["modifyvm", :id, "--audiocontroller", "hda"]

  # port forward our http server
  config.vm.forward_port 6600, 6601
  config.vm.forward_port 6680, 4567

end
