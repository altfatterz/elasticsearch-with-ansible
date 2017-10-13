Vagrant.configure("2") do |config|

  # create daily-data-loader node
  config.vm.define "elasticsearch" do |es_config|
    es_config.vm.box = "geerlingguy/centos7"
    es_config.vm.hostname = "elasticsearch"
    es_config.vm.network :private_network, type: "dhcp"
    es_config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "elasticsearch_vm"
    end
    es_config.vm.provision "ansible" do |ansible|
      ansible.playbook = "install.yml"
    end
  end

end
