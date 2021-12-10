Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64" #l/p: vagrant/vagrant
  #config.vm.hostname = "test"
  config.vm.disk :disk, size: "10GB", primary: true
  config.vm.network "public_network", ip: "192.168.0.129"
  
  config.vm.provider "virtualbox" do |vb|
  vb.gui = true
  vb.memory = "2048"
  end

  
  config.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt-get install -y curl vim wget htop tmux 
 
  sudo apt-get install -y \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg \
      lsb-release
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  sudo apt-get update && \
  sudo apt-get install -y docker-ce docker-ce-cli containerd.io && \
  sudo groupadd docker && \
  sudo usermod -aG docker $USER && \
  newgrp docker
  
  SHELL
   
end
