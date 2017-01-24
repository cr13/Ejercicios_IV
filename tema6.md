# **Ejercicios Tema 6**

###**Ejercicio 1**: Instalar chef en la máquina virtual que vayamos a usar

Una forma rápida de instalarlo es:

    curl -L https://www.opscode.com/chef/install.sh | sudo bash

Para comprobar que la instalación se ha realizado:

    chef-solo -v
![chef-solo version](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/chef-solo_zpshpbivmvf.png)

----------
###**Ejercicio 2**: Crear una receta para instalar la aplicación que se viene creando en la asignatura en alguna máquina virtual o servidor en la nube.

----------
###**Ejercicio 3**: Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

----------
###**Ejercicio 4**: Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

Lo primero que debemos hacer es instalar vagrant:

      sudo apt-get install vagrant

Ahora descargo la imagen de Debian tal y como se explica en los apuntes:

    vagrant box add debian https://github.com/holms/vagrant-jessie-box/releases/download/Jessie-v0.1/Debian-jessie-amd64-netboot.box

![vagrant debian](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrantDebian_zpsl2femgbi.png)

Creamos el fichero Vagranfile:

    vagrant init debian

![vagrantFile](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrantFile_zpslh5rtiml.png)

Ya podemos inicializa la máquina con:

    vagrant up

![vagrant up](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrant-up_zpsu67ckki2.png)

Y nos conectamos con:

    vagrant ssh

![vagrant ssh](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrant-ssh_zpsnwrcc3zr.png)

----------
###**Ejercicio 5**: Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica

Para provisionar nuestra máquina debian creada anteriormente con nginx, debemos modificar el vagrantfile creado anteriormente de la siguiente forma:

![vagrantFile nginx](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrantFile-nginx_zpsu4u6t4hl.png)

Arrancamos la máquina mediante vagrant up y se ejecuta la provisión mediante:

    vagrant provision

![vagrant provision](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vargrant-provision_zpsgubcpwzn.png)

Ahora conectamos por ssh y comprobamos que efectivamente se ha instalado y ha arrancado el servicio:

    vagrant ssh
    sudo service nginx status

![vagrant ssh y estado servicio](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vagrantssh-nginx_zpsafphwzde.png)

----------
###**Ejercicio 6**: Configurar tu máquina virtual usando vagrant con el provisionador chef.

----------
