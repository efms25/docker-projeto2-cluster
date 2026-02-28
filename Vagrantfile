machines = {
  "master" => {"memory" => "1024", "cpus" => 1, "image" => "bento/ubuntu-22.04", "ip" => "192.168.56.101"},
  "node01" => {"memory" => "1024", "cpus" => 1, "image" => "bento/ubuntu-22.04", "ip" => "192.168.56.102"},
  "node02" => {"memory" => "1024", "cpus" => 1, "image" => "bento/ubuntu-22.04", "ip" => "192.168.56.103"},
  "node03" => {"memory" => "1024", "cpus" => 1, "image" => "bento/ubuntu-22.04", "ip" => "192.168.56.104"},
}

Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpus"]
      end
      machine.vm.provision "shell", path: "docker-install.sh"
      if name == "master"
        machine.vm.provision "shell", path: "master-setup.sh"
      else
        machine.vm.provition "shell", path: "worker-setup.sh"
      end 
    end
  end
end