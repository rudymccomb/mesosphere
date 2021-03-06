nodes = {
  master01: {
    hostname: 'master01.localdomain',
    ip: '192.168.200.100',
    memory: 1024
  },
  master02: {
    hostname: 'master02.localdomain',
    ip: '192.168.200.101',
    memory: 1024
  },
  master03: {
    hostname: 'master03.localdomain',
    ip: '192.168.200.102',
    memory: 1024
  },
  slave01: {
    hostname: 'slave01.localdomain',
    ip: '192.168.200.110',
    memory: 1024
  }
}

VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  nodes.each do |host, attributes|
    config.vm.define host do |h|
      h.vm.hostname = attributes[:hostname]
      h.vm.network 'private_network', ip: attributes[:ip]

      h.vm.provider :virtualbox do |vb|
        vb.gui = true
        vb.customize ['modifyvm', :id, '--memory', attributes[:memory]]
      end

      h.vm.provision 'shell', inline: "echo '# Generated by Vagrantfile' > /etc/hosts"
      h.vm.provision 'shell', inline: "echo '127.0.0.1 localhost' > /etc/hosts"

      nodes.each do |k, v|
        h.vm.provision 'shell', inline: "echo #{v[:ip]} #{k} #{v[:hostname]} >> /etc/hosts"
      end

    end
  end

end
