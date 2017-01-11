# **Ejercicios Tema 5**

###**Ejercicio 1**: Instalar los paquetes necesarios para usar KVM. Se pueden [seguir estas instrucciones](https://wiki.debian.org/KVM#Installation). Ya lo hicimos [en el primer tema](http://jj.github.io/IV/documentos/temas/Intro_concepto_y_soporte_fisico), pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

----------
###**Ejercicio 2**:
####**1)**: Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar [CoreOS](https://coreos.com/) (que sirve como soporte para Docker) [GALPon Minino](http://minino.galpon.org/en), hecha en Galicia para el mundo, [Damn Small Linux](http://www.damnsmalllinux.org/download.html), [SliTaz](http://www.slitaz.org/en/) (que cabe en 35 megas) y [ttylinux](http://freecode.com/projects/ttylinux/) (basado en línea de órdenes solo).


####**2)**:Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.


----------
###**Ejercicio 3**: Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con **qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img**


----------
###**Ejercicio 4**:Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y **ssh**.

----------
###**Ejercicio 5**: Crear una máquina virtual ubuntu e instalar en ella alguno de los servicios que estamos usando en el proyecto de la asignatura.


----------
###**Ejercicio 6**: Instalar una máquina virtual con Linux Mint para el hipervisor que tengas instalado.

----------
