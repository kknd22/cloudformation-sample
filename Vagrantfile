# Vagrant multi-machine sample setup

Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')

Vagrant.configure("2") do |config|
  config.vm.define :vm1 do |vm1|
    vm1.vm.box = "geerlingguy/centos7"
    vm1.vm.network :private_network, ip: "10.0.0.10"
    vm1.vm.hostname = "vm1"
    vm1.vm.network :forwarded_port, guest: 80, host: 8088
    vm1.vm.provision "shell", inline: <<-SHELL
      yum update -y 
      yum install ansible -y
      yum install git -y
    SHELL
  end

  config.vm.define :vm2 do |vm2|
    vm2.vm.box = "geerlingguy/centos7"
    vm2.vm.network :private_network, ip: "10.0.0.11"
    vm2.vm.hostname = "vm2"
    vm2.vm.network :forwarded_port, guest: 3306, host: 3306
    vm2.vm.provision "shell", inline: <<-SHELL
      yum update -y 
      yum install ansible -y
      yum install git -y
    SHELL
  end
end
