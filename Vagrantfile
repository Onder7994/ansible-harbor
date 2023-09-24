servers=[
  {:hostname => "harbor",:ip => "192.168.10.50",:ssh_port => 2230}
]

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = 4096
    vb.cpus = 2
    vb.check_guest_additions = false
    config.vm.box_check_update = false
    config.vm.box = "bento/ubuntu-22.04"
  end

  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
      node.vm.hostname = machine[:hostname]
      node.vm.network "public_network", ip: machine[:ip], bridge: "wlo1"
      node.vm.network "forwarded_port", id: "ssh", host: machine[:ssh_port], guest: 22
      
      node.vm.provider "virtualbox" do |vb|
        file_to_disk = "./#{machine[:hostname]}_disk.vdi"
        vb.customize ['createhd', '--filename', file_to_disk, '--size', 20 * 1024]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]
      end
    end
  end
end
