# **Ejercicios Tema 5**

###**Ejercicio 1**: Instalar los paquetes necesarios para usar KVM. Se pueden [seguir estas instrucciones](https://wiki.debian.org/KVM#Installation). Ya lo hicimos [en el primer tema](http://jj.github.io/IV/documentos/temas/Intro_concepto_y_soporte_fisico), pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

Vamos a comprobar la compatibilidad de nuestro sistema con KVM, podemos comprobarlo de varias formas:

    * sudo kvm-ok
    * egrep '(vmx|svm)' --color=always /proc/cpuinfo
    * egrep -c '(vmx|svm)' /proc/cpuinfo //si el valor mostrado es mayor que 0 indica que la virtualización está soportada.

Comprobación de comptibilidad del sistema con KVM

![Comprobación de compatibilidad con KVM](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/compatibilidad_kvm_zpsljwaavfo.png)

Una vez que verificamos que nuestro sistema es compatible pasamos a la instalació de los paquetes necesarios.

    sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils virtinst

Añadimos nuestro usuario a los grupos libvirtd y kvm:

    sudo adduser `id -un` libvirtd
    sudo adduser `id -un` kvm

Después de la instalación, necesitamos reiniciar para que nuestro usuario se convierta en un miembro efectivo de los grupos de usuarios kvm y libvirtd

     kill all -1 gnome-shell

Comprobamos el estado de la instalación     

    virsh -c qemu:///system list

![Comprobación de instalación de KVM](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/comprobacionInstalacionKVM_zps0kgwf0yp.png)

También podemos añadir una interfaz gráfica,como no es necesario yo no la voy a instalar.

    sudo apt-get install virt-manager

----------
###**Ejercicio 2**:
####**1)**: Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar [CoreOS](https://coreos.com/) (que sirve como soporte para Docker) [GALPon Minino](http://minino.galpon.org/en), hecha en Galicia para el mundo, [Damn Small Linux](http://www.damnsmalllinux.org/download.html), [SliTaz](http://www.slitaz.org/en/) (que cabe en 35 megas) y [ttylinux](http://freecode.com/projects/ttylinux/) (basado en línea de órdenes solo).

**SliTaz**

Primero vamos a crear el disco duro de 8G:

    qemu-img create -f qcow2 slitaz.qcow2 8G

Segundo [descargamos](http://mirror.slitaz.org/iso/4.0/slitaz-4.0.iso) e instalamos una imagen SliTaz:

    qemu-system-x86_64 -hda slitaz.qcow2 -cdrom slitaz-4.0.iso

![SliTaz FNU][1]  ![SliTaz Live][2]

[1]: http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/SliTaz_zpsizemtj9c.png
[2]: http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/SliTaz%20live_zpsf3ixhlur.png "SliTaz"

**Debian**

Creamos una imagen de disco virtual con:

    qemu-img create -f qcow2 debian.qcow2 8G

[Descargamos](http://cdimage.debian.org/debian-cd/8.6.0/multi-arch/iso-cd/) e instalamos Debian

    qemu-system-x86_64 -machine accel=kvm -hda debian.qcow2 -cdrom debian-8.6.0-amd64-i386-netinst.iso -m 1G -boot d

**CoreOS**

Creamos una imagen de disco virtual con:

    qemu-img create -f qcow2 coreOS.qcow2 8G

[Descargamos](https://coreos.com/os/docs/latest/booting-with-iso.html) e instalamos CoreOS

    qemu-system-x86_64 -machine accel=kvm -hda coreOS.qcow2 -cdrom coreos_production_iso_image.iso -m 1G -boot d

![CoreOS](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/coreOS_zpsm5sityib.png)


Para ejecutarla debemos poner:

    qemu-system-x86_64 -boot order=c -drive file="nombre de la maquina",if=virtio

ejemplo

    qemu-system-x86_64 -boot order=c -drive file=coreOS.qcow2,if=virtio


####**2)**:Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

Instalaré SLliTaz en VirtualBox.

Para ello creamos una nueva máquina, asignando la RAM que vaya a usar. Después creamos un disco duro virtual VDI con el tamaño que queramos. Finalmente le montamos la ISO en la cargadora de CD virtual y la arrancamos.(Todo gráficamente)

![creamos maquina virtual][1] ![SliTaz iniciamos VB][2] ![SliTaz Live][3]

[1]: http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vbslitaz_zpsmljf0byh.png
[2]: http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/bvslitazinstalacion_zpsmtaikfyo.png
[3]: http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/vbslitazlive_zpstcspxuht.png "Virtual box SliTaz live"

----------
###**Ejercicio 3**: Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con **qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img**

Voy ha usar el benchmark de Sysbench

1. Instalamos el sysbench:

    sudo apt-get install sysbench**

2. Creamos un entorno de trabajo:

    sysbench --test=fileio --file-total-size=5G prepare

3. Ejecutamos los tests y mostramos los resultados:

    sysbench --test=fileio --file-total-size=5G \
           --file-test-mode=rndrw --init-rng=on \
           --max-time=300 --max-requests=0 run

4. Limpiamos el espacio ocupado:

    sysbench --test=fileio --file-total-size=5G cleanup

----------
###**Ejercicio 4**:Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y **ssh**.

----------
###**Ejercicio 5**: Crear una máquina virtual ubuntu e instalar en ella alguno de los servicios que estamos usando en el proyecto de la asignatura.


----------
###**Ejercicio 6**: Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.

----------
