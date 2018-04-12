Vagrant.configure(2) do |config|
config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
$script = <<-SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at
SCRIPT
  config.vm.define "node1" do |node1|
    node1.vm.box = "bento/centos-7.4"
    node1.vm.network "private_network", ip: "192.168.0.101"
    node1.vm.hostname = "node1"
  end
  config.vm.define "node2" do |node2|
    node2.vm.box = "bento/centos-7.4"
    node2.vm.network "private_network", ip: "192.168.0.102"
    node2.vm.hostname = "node2"
    node2.vm.provision "shell", inline: $script
    node2.vm.network "forwarded_port", guest: 8080, host: 9999
  end
end
