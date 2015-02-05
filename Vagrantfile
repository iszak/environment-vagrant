VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = "harkonnen"
  config.vm.box      = "../packer/build/ubuntu-14.04.1-virtualbox.box"

  config.vm.network "private_network", ip: "192.168.13.37"

  config.ssh.forward_agent = true

  config.sshfs.paths = {
    "/home/vagrant/public" => "mount/public/",
    "/home/vagrant/log"    => "mount/log/"
  }

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end


  config.vm.provision "shell", path: "provisioners/shell/bootstrap.sh"


  config.vm.provision "puppet" do |puppet|
    puppet.hiera_config_path = "provisioners/puppet/hiera.yaml"
    puppet.module_path       = "provisioners/puppet/modules"
    puppet.manifests_path    = "provisioners/puppet/manifests"
    puppet.manifest_file     = "default.pp"

    # puppet.options           = "--verbose --debug"
  end
end
