
Vagrant.configure("2") do |config|
  servers =[
    {
      :hostname => "Server1",
      :box => "bento/ubuntu-18.04",
      :ip => "172.16.1.50",
      :ssh_port => "2200"
    },
    {
      :hostname => "Server2",
      :box => "bento/ubuntu-18.04",
      :ip => "172.16.1.51",
      :ssh_port => "2201"
    },
    {
      :hostname => "Server3",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.56.102",
      :ssh_port => '2202'
    }
  ]

  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      node.vm.synced_folder "../ubuntu", "/home/vagrant/ubuntu"
      node.vm.provision "file", source: "./copiedfile.txt", destination: "/home/vagrant/copiedfile.txt"

      node.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", 512]
          vb.customize ["modifyvm", :id, "--cpus", 1]
      end
  end

  end
  
end
