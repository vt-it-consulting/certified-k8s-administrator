Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 600
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      echo "10.0.0.10  cka-master-node" >> /etc/hosts
      echo "10.0.0.11  cka-worker-node1" >> /etc/hosts
      echo "10.0.0.12  cka-worker-node2" >> /etc/hosts
	  echo "10.0.0.13  cka-worker-node3" >> /etc/hosts
  SHELL
  
  config.vm.define "master" do |master|
    master.vm.box = "bento/ubuntu-22.04"
    master.vm.hostname = "cka-master-node"
    master.vm.network "private_network", ip: "10.0.0.10"
    master.vm.provider "virtualbox" do |vb|
        vb.memory = 4048
        vb.cpus = 2
		vb.name = master.vm.hostname
    end
  end

  (1..3).each do |i|
  config.vm.boot_timeout = 600
  config.vm.define "node#{i}" do |node|
    node.vm.box = "bento/ubuntu-22.04"
    node.vm.hostname = "cka-worker-node#{i}"
    node.vm.network "private_network", ip: "10.0.0.1#{i}"
    node.vm.provider "virtualbox" do |vb|
        vb.memory = 3072
		vb.name = node.vm.hostname
        vb.cpus = 2
    end
  end
  
  end
end