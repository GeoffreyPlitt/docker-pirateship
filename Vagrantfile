Vagrant.require_version ">= 1.4.0"
Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  
  config.vm.provision "docker" do |docker|
    docker.pull_images "geoffreyplitt/docker-couchpotato"
    docker.pull_images "geoffreyplitt/docker-sickbeard"
    docker.pull_images "geoffreyplitt/docker-headphones"
    docker.pull_images "geoffreyplitt/docker-sabnzb"
    docker.pull_images "geoffreyplitt/docker-megasearch"
    
    docker.run "geoffreyplitt/docker-couchpotato", args: "-d -p 5050:5050"
    docker.run "geoffreyplitt/docker-sickbeard", args: "-d -p 8081:8081"
    docker.run "geoffreyplitt/docker-headphones", args: "-d -p 8181:8181"
    docker.run "geoffreyplitt/docker-sabnzb", args: "-d -p 8080:8080"
    docker.run "geoffreyplitt/docker-megasearch", args: "-d -p 5000:5000"
  end

  for p in [5050,8081,8181,8080,5000]
    config.vm.network :forwarded_port, host: p, guest: p
  end

  config.vm.provision "shell",
    inline: "echo Done."
end
