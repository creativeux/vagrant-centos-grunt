Vagrant.configure("2") do |config|

  # Force the box to be our known environment
  config.vm.box = "creativeux/centos7-64-docker"

  # Configure port forwarding to expose grunt port and livereload port
  config.vm.network :forwarded_port, host: 9000, guest: 9000
  config.vm.network :forwarded_port, host: 35729, guest: 35729

  # Sync the existing folder to the vagrant VM for pass-through to Docker
  config.vm.synced_folder ".", "/webapp"

  # Args configure the Docker port forwarding and volume mapping.
  # NOTE: '--privileged=true' allows access to passed-through volumes.
  config.vm.provision "docker" do |d|
      d.pull_images "creativeux/centos-grunt:latest"
      d.run "creativeux/centos-grunt",
        args: "--privileged=true -t -i -p 9000:9000 -p 35729:35729 -v /webapp:/var/www",
        daemonize: true
    end
end
