Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"
  config.vm.network :forwarded_port, guest: 22, host: 2223, id: "ssh"
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  # ~/.ssh/id_rsa.pub is a file in the host machine
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"
  config.vm.provision "shell", inline: <<-SCRIPT
    apt update
    apt install -y curl
    curl -sSL https://get.haskellstack.org/ | sh
    cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
  SCRIPT
end
