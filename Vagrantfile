Vagrant.configure("2") do |config|

  config.ssh.insert_key = false
  config.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'

  (1..3).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "geerlingguy/centos7"
      node.vm.hostname = "node#{i}"
      node.vm.network :private_network, ip: "10.0.15.2#{i}"
      node.vm.network "forwarded_port", guest: 9200, host: "920#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.name = "elasticsearch_vm_#{i}"
      end
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "install.yml"
      end
    end
  end

end
