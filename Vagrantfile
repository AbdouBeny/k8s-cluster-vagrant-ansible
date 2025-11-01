IMAGE_NAME = "bento/ubuntu-22.04" #"ubuntu/jammy64"   # Image to use
MEM = 2048                          # Amount of RAM
CPU = 2                             # Number of processors (Minimum value of 2 otherwise it will not work)
MASTER_NAME="master"                # Master node name
WORKER_NBR = 1                      # Number of workers node
NODE_NETWORK_BASE = "192.168.56"    # First three octets of the IP address that will be assign to all type of nodes
POD_NETWORK = "10.244.0.0/16"    # Private network for inter-pod communication

Vagrant.configure("2") do |config|
  config.vm.box = IMAGE_NAME
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |vbox|
    vbox.memory = MEM
    vbox.cpus = CPU
  end
  # MASTER CONFIG
  config.vm.define MASTER_NAME do |master|
    master.vm.hostname = MASTER_NAME
    master.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.10"
  end
  # WORKERS CONFIG
  (1..WORKER_NBR).each do |i|
    config.vm.define "worker-#{i}" do |worker|
      worker.vm.hostname = "worker-#{i}"
      worker.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.#{i + 10}"
    end
  end  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    # inventory
    ansible.groups = {
      "master" => ["#{MASTER_NAME}"],
      "worker" => ["worker-[1:#{WORKER_NBR}]"]
    }
    ansible.extra_vars = {
      master_ip: "#{NODE_NETWORK_BASE}.10",
      pod_network_cidr: "#{POD_NETWORK}"
    }
  end
end
