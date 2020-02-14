BOX_IMAGE = "bento/ubuntu-19.10"
NODE_COUNT = 3

Vagrant.configure("2") do |config|
	config.vm.define "gravity-control" do |control|
		control.vm.box = BOX_IMAGE
		control.vm.hostname = "gravity-control"
		control.vm.network :private_network, ip: "10.0.0.10"

		# Run Ansible from the Vagrant VM
		# Run gravity-control playbook only on gravity-control
		control.vm.provision "ansible_local" do |ansible|
			ansible.playbook = "ansible/gravity-control.yml"
		end
	end

	(0..NODE_COUNT-1).each do |i|
		config.vm.define "gravity-node#{i}" do |node|
			node.vm.box = BOX_IMAGE
			node.vm.hostname = "gravity-node#{i}"
            node.vm.network :private_network, ip: "10.0.0.#{i + 10}"
		end
	end

	# Run Ansible from the Vagrant VM
	# Run common playbook on all VMs
	config.vm.provision "ansible_local" do |ansible|
		ansible.playbook = "ansible/common.yml"
	end
end