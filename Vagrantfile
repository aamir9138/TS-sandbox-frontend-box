require 'yaml'
settings = YAML.load_file 'inventory_vagrant.yml'

Vagrant.configure("2") do |config|
    config.vm.define "TS-sandbox-frontend-vm" do |srv|
      srv.vm.box = "debian/bullseye64"
      srv.ssh.insert_key = false
      srv.vm.hostname = "TS-sandbox-frontend.box"
      srv.vm.network :private_network, ip: settings['all']['vars']['box_ip']
  
      srv.vm.provider :virtualbox do |vb|
        vb.name = "TS-sandbox-frontend_box"
        vb.memory = 4096
        vb.cpus = 2
      end
    end
    config.vm.provision "ansible_local"  do |ansible|
      ansible.install = true
      ansible.version = "latest"
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible/playbook.yml"
      ansible.galaxy_role_file = "ansible/requirements.yml"
      ansible.verbose = true
      ansible.groups = {
        "all" => ["TS-sandbox-frontend-vm"]
      }
    end
  end