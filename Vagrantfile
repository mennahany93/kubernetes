Vagrant.configure("2") do |config|
  config.vm.define "controller" do |controller|
  	controller.vm.box = "ubuntu/bionic64"
        controller.vm.hostname = "k8-controller"
  	controller.vm.network "private_network", ip: "192.168.33.10"

  	controller.vm.provider "virtualbox" do |vb|
     		vb.memory = "1536"
   	end
  end

  config.vm.define "worker" do |worker|
  	worker.vm.box = "ubuntu/bionic64"
        worker.vm.hostname = "k8-worker"
  	worker.vm.network "private_network", ip: "192.168.33.20"

  	worker.vm.provider "virtualbox" do |vb|
     		vb.memory = "1536"
   	end
  end
end
