Vagrant.configure("2") do |config|
  # Definir las máquinas virtuales
  (1..2).each do |i|
    config.vm.define "webserver#{i}" do |webserver|
      webserver.vm.box = "ubuntu/bionic64" # Imagen base de Ubuntu 18.04
      webserver.vm.network "forwarded_port", guest: 80, host: 8080 + i # Puerto 8081 para la segunda VM
      webserver.vm.provider "virtualbox" do |vb|
        vb.memory = "512" # Asignar 512 MB de RAM
      end

      # Configuración del provisionamiento
      webserver.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install -y apache2
        sudo systemctl enable apache2
        sudo systemctl start apache2
        sudo mkdir -p /var/www/html/mywebsite
        sudo cp /vagrant/index.html /var/www/html/mywebsite/index.html
        sudo chown -R www-data:www-data /var/www/html/mywebsite
      SHELL
    end
  end
end
