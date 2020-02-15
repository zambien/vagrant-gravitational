API_VERSION = 2

# Require YAML module
require 'yaml'

# Read YAML file with box details
vagrant_config = YAML.load_file('./vagrant_config.yaml')

Vagrant.configure("2") do |config|
	config.vm.define "gravity-control" do |control|
		control.vm.box = vagrant_config["box-image"]
		control.vm.hostname = "gravity-control"
		control.vm.network :private_network, ip: "10.0.0.10"
		control.vm.provider "virtualbox" do |v|
			v.memory = vagrant_config['gravity_control']['memory']
			v.cpus = vagrant_config['gravity_control']['cpus']
		end

		# Run Ansible from the Vagrant VM
		# Run gravity-control playbook only on gravity-control
		control.vm.provision "ansible_local" do |ansible|
			ansible.playbook = "ansible/gravity-control.yml"
		end
	end

	(0..vagrant_config['gravity_nodes']['count'] - 1).each do |i|
		config.vm.define "gravity-node#{i}" do |node|
			node.vm.box = vagrant_config["box-image"]
			node.vm.hostname = "gravity-node#{i}"
            node.vm.network :private_network, ip: "10.0.0.#{i + 11}"
			node.vm.provider "virtualbox" do |v|
				v.memory = vagrant_config['gravity_nodes']['memory']
				v.cpus = vagrant_config['gravity_nodes']['cpus']
			end
		end
	end

	# Run Ansible from the Vagrant VM
	# Run common playbook on all VMs
	config.vm.provision "ansible_local" do |ansible|
		ansible.playbook = "ansible/common.yml"
	end
end