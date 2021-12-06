$script_mysql = <<-SCRIPT
sudo apt-get update && 
sudo mysql < /vagrant/mysql/script/user.sql &&
sudo mysql < /vagrant/mysql/script/schema.sql && 
sudo mysql < /vagrant/mysql/script/data.sql && 
sudo cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && 
sudo service mysql restart
SCRIPT

Vagrant.configure("2") do |config|

  # boxes at https://vagrantcloud.com/search.

  config.vm.box = "hashicorp/bionic64"

  config.vm.box_check_update = true

   config.vm.network "forwarded_port", guest: 3306, host: 3306

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "private_network", ip: "10.80.4.10"
  
    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserver"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql
  end
end


