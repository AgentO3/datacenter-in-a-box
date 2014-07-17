Vagrant.configure("2") do |config|
  config.vm.box = "precise64"

# Here I forward the ssh ports to the host machine. This gives Ansible access to those docker containers
# via ssh. We must specify an id for the ports as seen below otherwise Vagrant will say that port is already
# taken. I'm not really sure why but this works. I would rather not have to do this, so if you have a better
# answer let me know.

  config.vm.network "forwarded_port", guest: 22, host: 2222
  config.vm.network "forwarded_port", guest: 2230, host: 2230, id: 'ssh'
  config.vm.network "forwarded_port", guest: 2231, host: 2231, id: 'ssh1'
  config.vm.network "forwarded_port", guest: 2232, host: 2232, id: 'ssh2'

# Here is where docker container are provisioned by Vagrant. I choose to use vovimayhem/centos-vagrant because it's setup with ssh, a vagrant user, and the Vagrant ssh key. This allows me to use the default Vagrant key to access these boxes.

  config.vm.provision "docker" do |d|
      d.run "app-server1",
        image: "vovimayhem/centos-vagrant",
        daemonize: true,
        args: "-p 2230:22",
        auto_assign_name: true
      d.run "app-server2",
        image: "vovimayhem/centos-vagrant",
        daemonize: true,
        args: "-p 2231:22",
        auto_assign_name: true
      d.run "app-server3",
        image: "vovimayhem/centos-vagrant",
        daemonize: true,
        args: "-p 2232:22",
        auto_assign_name: true
  end

# Here we run the anisble playbook vagrant.yml against the docker containers in this Vagrant box. 

  config.vm.provision "ansible" do |ansible|
      ansible.verbose = "vvv"
      ansible.playbook = "vagrant.yml"
      ansible.inventory_path = 'inventory'
      ansible.sudo_user = "vagrant"
      ansible.limit = "all"
  end
end
