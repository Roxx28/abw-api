# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
	config.vm.hostname = "abw-api"
	config.vm.box = "ubuntu/xenial64"

	config.vm.network "forwarded_port", guest: 3000, host: 3000, host_ip: "127.0.0.1"

	config.vm.provider "virtualbox" do |vb|
		vb.memory = "1024"
	end

	config.vm.provision "shell", inline: <<-SHELL
		apt-get update

		apt-get install -y build-essential
		apt-get install -y curl

		# Nodejs
		curl -sL https://deb.nodesource.com/setup_6.x | bash -
		apt-get install -y nodejs

		npm install -g express

		# MongoDB
		apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
		echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list

		apt-get update
		apt-get install -y mongodb-org

		service mongod start
	SHELL
end
