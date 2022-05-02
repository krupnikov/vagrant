ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.synced_folder '.', '/home/vagrant/sync', disabled: true
    config.vm.box_check_update = false

    (1..3).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.network "public_network", ip: "10.0.2.#{1+i}"
            node.vm.hostname = "node#{i}"
            config.vm.provider "virtualbox" do |vb|
                vb.cpus = 1
                vb.memory = 2048
                vb.disk = 20
            end
        end
    end
end