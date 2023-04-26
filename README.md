# Flask-MySQL
Practica Servicios Telematicos Python Flask + MySQL

Vagrantfile


# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :generic do |generic|
    generic.vm.box = "generic/centos8"
    generic.vm.network :private_network, ip: "192.168.50.3"
    generic.vm.hostname = "generic"
  end
end

---------------------------------------------------------------------------------------------------------

IMPORTANTE DESACTIVAR SELINUX Y EL FIREWALLD!!!!!!!!!!!!

DESACTIVAR SELINUX

vim /etc/selinux/config

PARAR EL SERVICIO FIREWALLD

service firewalld stop

---------------------------------------------------------------------------------------------------------

INSTALAR TODOS LOS PAQUETES Y DEPENDENCIAS A CONTINUACIÓN:

To Install Flask using pip3:

sudo yum install epel-release
sudo yum install python3-pip
pip3 –V
sudo pip3 install Flask
pip3 freeze | grep Flask

To Install MySQL and libraries:

sudo yum update
sudo wget https://dev.mysql.com/get/mysql80-community-release-el7-7.noarch.rpm
sudo rpm -Uvh mysql80-community-release-el7-7.noarch.rpm
sudo yum install mysql-server
sudo systemctl start mysqld
sudo systemctl status mysqld

MySQL + Flask Support

sudo yum install mysql-devel
sudo yum install python3-devel
sudo yum install gcc
sudo pip3 install flask-mysqldb

---------------------------------------------------------------------------------------------------------

A CONTINUACIÓN INSTALAR LOS PAQUETES PARA CORRER LA DOCUMENTACIÓN DE SWAGGER!!!!!!

sudo yum install git

Especificación API en Json format

pip3 install apispec

Plugin para integrar apispec y flask

pip3 install apispec-webframeworks

Librería de serializacion / deserializacion

pip3 install marshmallow

Verifique la instalación

pip3 freeze

Ejemplo de código Flask + Swagger

git clone https://github.com/omondragon/swagger-example

El directorio static de este repositario, pegarlo en var/www/my-project/app

---------------------------------------------------------------------------------------------------------

PARA LA PARTE DE MYSQL:

Recordar tener prendido el servicio mysqld

sudo systemctl start mysqld
sudo systemctl status mysqld

mysql -u root -p (dar espacio cuando pida contraseña)

USE myflaskapp

CREATE TABLE articulos(id INT(11) PRIMARY KEY, title VARCHAR(100), author VARCHAR(100), create_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP);

Show TABLES;

DESCRIBE articulos;

INSERT INTO articulos VALUES (1,'articulo 1','Juan Duque', '2023-04-25'); (para tener un ejemplo)

SELECT * FROM articulos;
---------------------------------------------------------------------------------------------------------

UNA VEZ TODO INSTALADO CORRER:

ubicado en /var/www/my-project correr:

export FLASK_ENV=development
python3 -m flask run --host=0.0.0.0

LISTO, SALUDOS! :)

---------------------------------------------------------------------------------------------------------

PARA CONFIGURACIÓN DE APACHE Y DESPLEGAR:

sudo yum install httpd 
sudo yum install python3-mod_wsgi

vim /etc/httpd/conf/httpd.conf

WSGIScriptAlias / /var/www/my-project/application.wsgi

<VirtualHost *>
	ServerName www.servicios.com
	<Directory /var/www/my-project/>
		Order deny,allow
		Allow from all
	</Directory>
</VirtualHost>
