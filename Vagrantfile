Vagrant.configure(2) do |config|
  config.vm.box = "generic/centos9s"

  config.vm.provider 'libvirt' do |provider|
    provider.memory = 1024
    provider.cpus = 2
  end

  config.vm.provision "shell", inline: "dnf config-manager --set-enabled crb"
  config.vm.provision "shell", inline: "dnf -y install epel-release epel-next-release"
  config.vm.provision "shell", inline: "dnf -y builddep osbuild"
  config.vm.provision "shell", inline: "dnf -y install git rpm-build ostree"
  config.vm.provision "shell", inline: "git clone https://github.com/osbuild/osbuild", privileged: false
  config.vm.provision "shell", inline: "git clone https://gitlab.com/CentOS/automotive/sample-images.git/ centos-automotive-sample-images", privileged: false

end
