
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure("2") do |config|

	config.vm.define "vm-1" do |srv|

		srv.vm.box = "centos/8"
		srv.vm.provider "virtualbox" do |vb|
		vb.memory = "2048" 
		vb.cpus="1"
		vb.name="centos_8"
		end
	srv.vm.provision "shell", inline: <<-SHELL
	uname -r
#изменение репо обновления
	cd /etc/yum.repos.d/ && sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* && sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
#Импорт открытого ключа из репозитория ELRepo
	sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
#Установка ELRepo
	sudo  yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
#Установка последнего ядра
	sudo yum -y --enablerepo=elrepo-kernel install kernel-ml
#Настройка загрузки с новым ядром
	sudo  grub2-set-default 0
	sudo reboot
	uname -r
	SHELL
	end


end