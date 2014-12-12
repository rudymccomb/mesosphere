nodes = {
  master01: {
    hostname: 'master01.localdomain',
    ip: '192.168.200.100',
    memory: 2048
  },
  master02: {
    hostname: 'master02.localdomain',
    ip: '192.168.200.101',
    memory: 2048
  },
  master03: {
    hostname: 'master03.localdomain',
    ip: '192.168.200.102',
    memory: 2048
  },
  slave01: {
    hostname: 'slave01.localdomain',
    ip: '192.168.200.110',
    memory: 2048
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

      nodes.each do |k, v|
        h.vm.provision 'shell', inline: "echo #{v[:ip]} #{k} #{v[:hostname]} >> /etc/hosts" unless k == host
      end

    end
  end

end
