Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder '.', '/home/vagrant/sync', disabled: true
    config.vm.box_check_update = false

    (1..3).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.hostname = "node#{i}.local"
            node.vm.network "private_network", ip: "192.168.56.#{1+i}",
                name: "vboxnet0"
            node.vm.provider "virtualbox" do |vb|
                vb.cpus = 1
                vb.memory = 2048
            end
        end
    end

    config.vm.provision :shell do |s|
        ssh_pub_key = File.readlines("id_rsa.pub").first.strip
        s.inline = <<-SCRIPT
            echo "SSH key provisioning."
            echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        SCRIPT
    end
end