Vagrant.configure("2") do |config|
  config.vm.box = "precise64"

  config.vm.network "forwarded_port", guest: 22, host: 2222
  config.vm.network "forwarded_port", guest: 2230, host: 2230, id: 'ssh'
  config.vm.network "forwarded_port", guest: 2231, host: 2231, id: 'ssh1'
  config.vm.network "forwarded_port", guest: 2232, host: 2232, id: 'ssh2'

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

  config.vm.provision "ansible" do |ansible|
      ansible.verbose = "vvv"
      ansible.playbook = "vagrant.yml"
      ansible.inventory_path = 'inventory'
      ansible.sudo_user = "vagrant"
      ansible.limit = "all"
  end
end
