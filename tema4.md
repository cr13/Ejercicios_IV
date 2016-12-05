# **Ejercicios Tema 4**

###**Ejercicio 1**: Instala LXC en tu versión de Linux favorita. Normalmente la versión en desarrollo, disponible tanto en [GitHub](https://github.com/lxc/lxc) como en el [sitio web](https://linuxcontainers.org/) está bastante más avanzada; para evitar problemas sobre todo con las herramientas que vamos a ver más adelante, conviene que te instales la última versión y si es posible una igual o mayor a la 1.0.

Instalamos lxc en ubuntu con **sudo apt-get install lxc**

Chequeamos la configuración con **lxc-checkconfig** para comprobar si es compatible con nuestro SO y que este bien configurado:

![lxc-checkconfig](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/lxc-checkconfig_zpsgifr53lv.png)

Como podemos observar en la imagen esta todo activado con lo cual se puede usar lxc con relativa facilidad, en el caso de no aparece alguno de esas capacidades como activada, LXC no va a funcionar.

----------
###**Ejercicio 2**: Comprobar qué interfaces puente se han creado y explicarlos.

Vamos a crear un contenedor denominado boxUbuntu y vamos a instalar Ubuntu en él:

    sudo lxc-create -t ubuntu -n boxUbuntu

![lxc-ubuntu](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/Captura%20de%20pantalla%20de%202016-12-03%2022-32-45_zps8gv9okug.png)

Como se observa en la imagen al finalizar la instalación nos dice cual es nuestro usuario y contraseña.
A continuación vamos a arrancar el contenedor y conectarnos a él con:

    sudo lxc-start -n boxUbuntu

Una vez que esta arrancado vamos a comprobar con **ifconfig** las interfaces puente se han creado. Para ello vamos abrir un nuevo terminar en el equipo anfitrión y ejecutamos **ifconfig**.

![interfaceslxcgeneradas](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/ifconfigredeslxc_zps4joswia8.png)

Como podemos observar en la imagen se han creado dos interfaces puente la **lxcbr0** y la **vethWH4BMG**. La primera es la encargada de darle acceso a internet al contenedor. Y la vethWH4BMG es la encargada de comunicar el contenedor con otros contenedores.

Otros comandos interesantes:

    sudo lxc-info -n boxUbuntu --> Muestra información del contenedor
    sudo lxc-stop -n boxUbuntu --> Parar el contendor

----------
###**Ejercicio 3**:
####**1)**: Crear y ejecutar un contenedor basado en Debian.

Para crearlo y ejecutarlo repetimos los pasos del ejericio anterio:

    sudo lxc-create -t debian -n boxDebian --> Crea el contenedor
    sudo lxc-start -n boxDebian --> Ejecutamos el contenedor
    sudo lxc-ls --fancy --> Muestra el estado de los contenedores

![crear-ejecutar-estado-lxcDebian](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/crearlxcdebian_zpsu6mpcyqf.png)

####**2)**: Crear y ejecutar un contenedor basado en otra distribución, tal como Fedora. Nota En general, crear un contenedor basado en tu distribución y otro basado en otra que no sea la tuya. Fedora, al parecer, tiene problemas si estás en Ubuntu 13.04 o superior, así que en tal caso usa cualquier otra distro. Por ejemplo, Óscar Zafra ha logrado instalar Gentoo usando un script descargado desde su sitio, como indica en este comentario en el issue.

Voy a crear un contendor Centos como da error al intentarlo crearlo como en los ejercicios anteriores lo he creado de la siguiente forma:

    sudo lxc-create --template download --name boxCentos

Ahora nos pedirá la distribución, la versión y la arquitectura. Elegimos uno de la lista, por ejemplo, centos 7 amd64

    sudo lxc-start -n boxCentos --> Para ejecutar el contenedor
    sudo lxc-ls --fancy --> Muestra el estado de los contenedores

![lxc-centos](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/centos-lxc_zpsrdfp8yui.png)

Para mas información sobre nuestro contenedor:
    sudo lxc-info -n boxCentos

----------
###**Ejercicio 4**:
####**1)**: Instalar lxc-webpanel y usarlo para arrancar, parar y visualizar las máquinas virtuales que se tengan instaladas.

Para instalar el [lxc-webpanel](http://lxc-webpanel.github.io/install.html) tenemos que hacerlo desde el usuario root.
    sudo su
    wget https://lxc-webpanel.github.io/tools/install.sh -O - | bash

![intalaciónLXC-webpanel](http://lxc-webpanel.github.io/install.html)

Desde el navegador localhost:5000 nos logueamos con usuario: admin y passwords: admin

![lxcwebpanelLogin](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/lxcweb_zpsw9otrrar.png)

Una vez logueados nos aparecerá una página de administracion de nuestros contenedores

![lxcwebpanelAdministración](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/lxcwebpanel_zpsitzdzhzx.png)

####**2)**: Desde el panel restringir los recursos que pueden usar: CPU shares, CPUs que se pueden usar (en sistemas multinúcleo) o cantidad de memoria.

Vamos a restringir los recursos del contenedor boxCentos

![restringirRecursos](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/adminlxcpanel_zpse6ojupku.png)

----------
###**Ejercicio 5**: Comparar las prestaciones de un servidor web en una jaula y el mismo servidor en un contenedor. Usar nginx.


----------
###**Ejercicio 6**: Instalar docker.

Para instalar Docker tenemos que ejecutar el siguiente comando:

    sudo apt-get install docker.io
    sudo docker -d & --> Lo iniciamos
    O también:
    sudo service docker start
    sudo service docker status -> Comprueba el estado del servicio
    sudo docker run hello-world -> Comprobamos que funciona 

![sudo docker run hello-world](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/docker_zpsu6yfofep.png)
----------
###**Ejercicio 7**:
####**1)**: Instalar a partir de docker una imagen alternativa de Ubuntu y alguna adicional, por ejemplo de CentOS.
####**2)**: Buscar e instalar una imagen que incluya MongoDB.

----------
###**Ejercicio 8**: Crear un usuario propio e instalar nginx en el contenedor creado de esta forma.


----------
###**Ejercicio 9**: Crear a partir del contenedor anterior una imagen persistente con commit.


----------
###**Ejercicio 10**: Crear una imagen con las herramientas necesarias para el proyecto de la asignatura sobre un sistema operativo de tu elección.
