boxes = [
    # Clean box, Ubuntu 12.04 LTS - for experimentation
    {
        :name => :web1,
        :ip => '33.33.33.80',
        :playbook => 'web.yml'
    },
    # MongoDB box, with Chef 'mongo' role
    {
        :name => :web2,
        :ip => '33.33.33.81',
        :playbook => 'web.yml'
    },
    # Jenkins master box, with Chef 'jenkins' role
    {
        :name => :loadbalancer,
        :ip => '33.33.33.82',
        :vbox_config => [
            { '--memory' => '1536' }
        ],
        :playbook => 'loadbalancer.yml'
    }
]

Vagrant.configure("2") do |config|
    boxes.each do |opts|
        config.vm.define opts[:name] do |config|
            # Box basics
            config.vm.box = "ubuntu/xenial64"
            config.vm.box_url = "http://files.vagrantup.com/precise64.box"
            config.vm.network :private_network, ip: opts[:ip]
            config.ssh.forward_agent = true
            config.vm.hostname = opts[:name]

            # VirtualBox customizations
            unless opts[:vbox_config].nil?
                config.vm.provider :virtualbox do |vb|
                    opts[:vbox_config].each do |hash|
                        hash.each do |key, value|
                            vb.customize ['modifyvm', :id, key, value]
                        end
                    end
                end
            end
            unless opts[:playbook].nil?
              config.vm.provision "ansible_local" do |ansible|
                ansible.playbook = opts[:playbook]
              end
            end
        end
    end
end