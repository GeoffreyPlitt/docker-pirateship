Vagrant.require_version ">= 1.4.0"
Vagrant.configure("2") do |config|
  config.vm.box = "precise64"

  # MEDIA folders - change FIRST param to your paths.
  config.vm.network "private_network", type: :dhcp # This is necessary for NFS to work with DHCP
  config.vm.synced_folder "/Volumes/LaCie/Movies", "/vagrant/MEDIA/Movies", type: "nfs"
  config.vm.synced_folder "/Volumes/LaCie/TV Shows", "/vagrant/MEDIA/TV", type: "nfs"
  config.vm.synced_folder "~/Music", "/vagrant/MEDIA/Music", type: "nfs"
  config.vm.synced_folder "/Volumes/LaCie/Downloads", "/vagrant/MEDIA/Complete", type: "nfs"
  config.vm.synced_folder "/Volumes/LaCie/Incomplete", "/vagrant/MEDIA/Incomplete", type: "nfs"
  config.vm.synced_folder "/Volumes/LaCie/NZB", "/vagrant/MEDIA/NZB", type: "nfs"

  # Port mappings
  for p in [5050,8181,5000,8080,8081]
    config.vm.network :forwarded_port, host: p, guest: p
  end

  # Ensure VM has Docker
  config.vm.provision "docker"

  # Run the bootstrap script below
  config.vm.provision :shell, :inline => $BOOTSTRAP_SCRIPT
end

$BOOTSTRAP_SCRIPT = <<EOF
  set -e # Stop on any error
  export DEBIAN_FRONTEND=noninteractive
  
  # get docker images
  docker pull geoffreyplitt/docker-couchpotato
  docker pull geoffreyplitt/docker-headphones
  docker pull geoffreyplitt/docker-megasearch
  docker pull geoffreyplitt/docker-sabnzb
  docker pull geoffreyplitt/docker-sickbeard

  # kill any running containers
  docker ps -q | while read CID; do docker kill $CID; done

  # start the containers
  docker run -d -p 5050:5050 -v /vagrant:/vagrant -entrypoint=/bin/bash geoffreyplitt/docker-couchpotato -l -c 'python CouchPotatoServer/CouchPotato.py --config_file /vagrant/configs/couchpotato.settings.conf'
  docker run -d -p 8181:8181 -v /vagrant:/vagrant -entrypoint=/bin/bash geoffreyplitt/docker-headphones -l -c 'cd headphones && python Headphones.py --config /vagrant/configs/headphones.config.ini'
  docker run -d -p 5000:5000 -v /vagrant:/vagrant -entrypoint=/bin/bash geoffreyplitt/docker-megasearch -l -c 'cd usntssearch/NZBmegasearch && ln -s /vagrant/configs/megasearch.custom_params.ini custom_params.ini && python mega2.py'
  docker run -d -p 8080:8080 -v /vagrant:/vagrant -entrypoint=/bin/bash geoffreyplitt/docker-sabnzb -l -c 'mkdir -p .sabnzbd && ln -s /vagrant/configs/sabnzb.sabnzbd.ini .sabnzbd/sabnzbd.ini && sabnzbdplus -s 0.0.0.0:8080'
  docker run -d -p 8081:8081 -v /vagrant:/vagrant -entrypoint=/bin/bash geoffreyplitt/docker-sickbeard -l -c 'cd my-sickbeard-install && python SickBeard.py --config /vagrant/configs/sickbeard.config.ini'

  echo
  docker ps
  echo
  echo DONE.
EOF