Vagrant.require_version ">= 1.4.0"
Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  
  config.vm.provision "docker" do |docker|
    docker.pull_images "geoffreyplitt/docker-couchpotato"
    docker.pull_images "geoffreyplitt/docker-headphones"
    docker.pull_images "geoffreyplitt/docker-megasearch"
    docker.pull_images "geoffreyplitt/docker-sabnzb"
    docker.pull_images "geoffreyplitt/docker-sickbeard"
    
    docker.run "geoffreyplitt/docker-couchpotato", args: "-d -p 5050:5050 -v /vagrant:/vagrant"
    docker.run "geoffreyplitt/docker-headphones",  args: "-d -p 8181:8181 -v /vagrant:/vagrant"
    docker.run "geoffreyplitt/docker-megasearch",  args: "-d -p 5000:5000 -v /vagrant:/vagrant"
    docker.run "geoffreyplitt/docker-sabnzb",      args: "-d -p 8080:8080 -v /vagrant:/vagrant"
    docker.run "geoffreyplitt/docker-sickbeard",   args: "-d -p 8081:8081 -v /vagrant:/vagrant"
  end

  for p in [5050,8181,5000,8080,8081]
    config.vm.network :forwarded_port, host: p, guest: p
  end

  config.vm.provision "shell",
    inline: "echo Done."
end
