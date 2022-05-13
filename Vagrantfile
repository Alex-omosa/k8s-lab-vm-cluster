Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    
    # config.vm.define "load-balancer" do |loadbalancer|
    #     loadbalancer.vm.hostname = "loadbalancer"
    #     loadbalancer.vm.network "private_network", ip: "192.168.56.40"
    #     loadbalancer.vm.provider "virtualbox" do |loadbalancer|
    #             loadbalancer.memory = "1048"
    #     end
    # end

    (1..3).each do |i| 
        config.vm.define "worker-#{i}" do |worker|
            worker.vm.hostname = "worker-#{i}"
            worker.vm.network "private_network", ip: "192.168.56.#{i+50}"
            # Allow password authentication
            config.vm.provision "shell", inline: <<-SHELL
                sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
                systemctl restart sshd.service
            SHELL
            worker.vm.provider "virtualbox" do |worker|
                worker.memory = "2048"
            end
        end
    end

    # (1..3).each do |i| 
    #     config.vm.define "controller-#{i}" do |controller|
    #         controller.vm.hostname = "controller-#{i}"
    #         controller.vm.network "private_network", ip: "192.168.56.#{i+60}"
    #         controller.vm.provider "virtualbox" do |controller|
    #             controller.memory = "1048"
    #         end
    #     end
    # end

end