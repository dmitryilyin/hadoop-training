nodes = {
    'node-1' => {'ip' => '192.168.0.11'},
    'node-2' => {'ip' => '192.168.0.12'},
    'node-3' => {'ip' => '192.168.0.13'},
}

Vagrant.configure('2') do |config|
  config.vbguest.auto_update = false

  config.vm.box = 'boxcutter/centos72'
 
  config.vm.synced_folder '.', '/vagrant', type: 'virtualbox'
  config.vm.synced_folder 'provisioning', '/etc/ansible', type: 'virtualbox'

  config.vm.provider 'virtualbox' do |vb|
    vb.gui = false
    vb.memory = '2048'
    vb.cpus = 2
  end

  nodes.each do |node_name, node_settings|
    config.vm.define node_name do |node_config|

      node_config.vm.hostname = node_name
      node_config.vm.network 'private_network', ip: node_settings['ip']

      if node_name == 'node-1'
        node_config.vm.network 'forwarded_port', guest: 8080, host: 8080
      end

      node_config.vm.provision 'ansible_local' do |ansible|
        ansible.install_mode = 'default'
        ansible.verbose = true
        ansible.install = true
        ansible.limit = node_name
        ansible.playbook = "provisioning/#{node_name}.yml"
        ansible.host_vars = nodes
      end

    end
  end

end
