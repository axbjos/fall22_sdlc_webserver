# -*- mode: ruby -*-
# vi: set ft=ruby :

# Single Server LAMP Stack Running the PHP Crude CRUD Web Application
# See the GitHub repo for details

# Vagrant uses Ruby, so Ruby Do Loop...
Vagrant.configure("2") do |config|
  
    # Use an appropriate box here!!!!! Uncomment the line applicable to you!!!!
    # For Intel Windows/Mac using Virtualbox (and only Virtualbox) use
    # In other words for an Intel PC, uncomment the line below and comment (or remove)
    # the lines for an ARM based Mac...
    config.vm.box = "ubuntu/focal64"

    # You could port forward to the webserver
    # config.vm.network "forwarded_port", guest: 80, host: 8080
    # or set a static ip so it is always at the same ip
    # or do something complete different if you know what you are doing.
    #####for host only make sure you know what you are doing - ask for help!!!
    config.vm.network "private_network", ip: "192.168.56.11"
  
    # Now move on to web server provisioning
  
    # Copy necessary files to the VM
    # This copies a simple file out to the webserver that can be used to verify PHP is working
    config.vm.provision "file", source: "phptest.php", destination: "phptest.php"
  
    # Now run a bunch of shell commands to get the web app in place
    config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      apt-get install -y php libapache2-mod-php php-mysql
      systemctl restart apache2.service
      cp phptest.php /var/www/html
  
      echo "loading php web app"
      git clone https://github.com/axbjos/phpcrudecrudapp.git
      cd phpcrudecrudapp
      mv * /var/www/html
    SHELL
  
  end