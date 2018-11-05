Vagrant.configure("2") do |config|
  config.vm.define "master" do |master|
  	master.vm.box = "ubuntu/bionic64"
        master.vm.hostname = "k8-master"
  	master.vm.network "private_network", ip: "192.168.33.10"

  	master.vm.provider "virtualbox" do |vb|
     		vb.memory = "1536"
   	end
  end

  config.vm.define "slave" do |slave|
  	slave.vm.box = "ubuntu/bionic64"
        slave.vm.hostname = "k8-slave"
  	slave.vm.network "private_network", ip: "192.168.33.20"

  	slave.vm.provider "virtualbox" do |vb|
     		vb.memory = "1536"
   	end
  end
end
