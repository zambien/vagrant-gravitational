Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-19.10"

    # Run Ansible from the Vagrant VM
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
    end

end
