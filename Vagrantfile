# -*- mode: ruby -*-
# vim: set ft=ruby :

ENV["LC_ALL"] = "en_US.UTF-8"
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'


Vagrant.configure("2") do |config|
  #Указываем, какую ОС мы будем использовать
  config.vm.box = "ubuntu/focal64"
  #Можно указать конкретную версию сборки 
  #Номера сборок можно посмотреть в Vagrant Cloud
#  config.vm.box_version = "1.0.0"

  #Проброс порта с гостевой машины в хост
  #Порт 80 в созданной ВМ будет доступен нам на порту 8080 хоста
  config.vm.network "forwarded_port", guest: 80, host: 8087
  config.vm.network "private_network", ip: "192.168.56.11", virtualbox__intnet: true

  #Указываем настройки спецификации ВМ
  #Указывается в отдельном цикле
  config.vm.provider "virtualbox" do |vb|
     # Указываем количество ОЗУ и ядер процессора
     vb.memory = "2048"
     vb.cpus = "1"
  end
  
  #Первоначальная настройка созданной ВМ
  #Установка и запуск Веб-сервера Apache2
  config.vm.provision "shell", inline: <<-SHELL
     mkdir -p ~root/.ssh
     cp ~vagrant/.ssh/auth* ~root/.ssh
     sudo apt-get update
     sudo apt-get install -y apache2
  SHELL
end
