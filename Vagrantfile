
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "bento/ubuntu-16.04"

  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.synced_folder "code/", "/var/www"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.define 'test1.dev' do |node|
    node.vm.hostname = 'test1.dev'
    node.vm.network :private_network, ip: '192.168.101.100'
    node.hostmanager.aliases = %w(www.web1.dev)
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provision/playbook.yml"
    ansible.verbose = "vvvv"
  end

end