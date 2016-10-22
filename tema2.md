# **Ejercicios Tema 2**

###**Ejercicio 1**: Instalar alguno de los entornos virtuales de node.js (o de cualquier otro lenguaje con el que se esté familiarizado) y, con ellos, instalar la última versión existente, la versión minor más actual de la 4.x y lo mismo para la 0.11 o alguna impar (de desarrollo).

El entorno virtual para node.js que voy a instalar es NVM.

1º Vamos a descargarnos el script.

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0 32.1/install.sh | bash
o con  Wget:

    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash

2º Para ver las versiones existentes

    nvm ls-remote

3º Voy a instalar las siguientes versiones
  - La última más estable
        nvm install stable
  - La última de la v4.x
        nvm install v4.6.1
  - La última de la v0.x
        nvm install v0.12.17

4º Para ver las versiones instaladas

    cr13@cr13-ubuntu:~$ nvm ls
    ->     v0.12.17
           v4.6.1
           v6.9.0
     default -> stable (-> v6.9.0)
     node -> stable (-> v6.9.0) (default)
     stable -> 6.9 (-> v6.9.0) (default)
     iojs -> N/A (default)
     lts/* -> lts/boron (-> v6.9.0)
     lts/argon -> v4.6.1
     lts/boron -> v6.9.0



  - Para utilizar una versión u otra

        nvm use <<version>>

        Ejemplo:

        cr13@cr13-ubuntu:~$ nvm use v6.9.0
        Now using node v6.9.0 (npm v3.10.8)

  - Para parar el entorno virtual

        nvm deactivate.

----------

###**Ejercicio 2**:Como ejercicio, algo ligeramente diferente: una web para calificar las empresas en las que hacen prácticas los alumnos. Las acciones serían
- Crear empresa
- Listar calificaciones para cada empresa
- Crear calificación y añadirla (comprobando que la persona no la haya añadido ya)
borrar calificación (si se arrepiente o te denuncia la empresa o algo)
- Hacer un ránking de empresas por calificación, por ejemplo
- Crear un repositorio en GitHub para la librería y crear un pequeño programa que use algunas de sus funcionalidades.

Si se quiere hacer con cualquier otra aplicación, también es válido. Se trata de hacer una aplicación simple que se pueda hacer rápidamente con un generador de aplicaciones como los que incluyen diferentes marcos MVC. Si cuesta mucho trabajo, simplemente prepara una aplicación que puedas usar más adelante en el resto de los ejercicios.
Para la realización de este ejercicio he creado una página web y he tenido que instalar xampp, jade y express.

![Página Principal](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/ejer2Tema2_zps5qizl7nd.png)

[Enlace a mi repositorio](https://github.com/cr13/Califica_empresas)

----------

###**Ejercicio 3**:Ejecutar el programa en diferentes versiones del lenguaje. ¿Funciona en todas ellas?

Si, me funcionan las tres versiones que tengo instaladas.

![Prueba de diferentes versiones de NVM](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/pruebadeversiones_zpsrubqovwh.png)

----------

###**Ejercicio 4**:Crear una descripción del módulo usando **package.json**. En caso de que se trate de otro lenguaje, usar el método correspondiente.

Mi package.json

    {
      "name": "application-name",
      "version": "0.0.1",
      "private": true,
      "scripts": {
          "start": "nodejs ./bin/www"
      },
      "dependencies": {
          "express": "~4.0.0",
          "static-favicon": "~1.0.0",
          "morgan": "~1.0.0",
          "cookie-parser": "~1.0.1",
          "body-parser": "~1.0.0",
          "debug": "~0.7.4",
          "jade": "~1.3.0",
          "mysql": "~2.9.0"
      }
    }


----------

###**Ejercicio 5**:Automatizar con **grunt** y **docco** (o algún otro sistema) la generación de documentación de la librería que se cree. Previamente, por supuesto, habrá que documentar tal librería.



----------

###**Ejercicio 6**:Para la aplicación que se está haciendo, escribir una serie de aserciones y probar que efectivamente no fallan. Añadir tests para una nueva funcionalidad, probar que falla y escribir el código para que no lo haga (vamos, lo que viene siendo TDD).



----------

###**Ejercicio 7**:Convertir los tests unitarios anteriores con assert a programas de test y ejecutarlos desde **mocha**, usando descripciones del test y del grupo de test de forma correcta. Si hasta ahora no has subido el código que has venido realizando a GitHub, es el momento de hacerlo, porque lo vas a necesitar un poco más adelante.



----------

###**Ejercicio 8**:Haced los dos primeros pasos antes de pasar al tercero.

Para la comparativa he escogido por un lado un servidor dedicado que ofrece  [leaseweb](https://www.leaseweb.com/dedicated-server/configure/23895) con las siguientes características:

![xeon](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/ejer2a_zps1nvq2srm.png)

- **Procesador:** Intel Quad Core X3430
- **RAM:**  8GB
- **Disco Duro:**  2x500GB SATA2  
- **Coste:**  45.99€/mes

Por otro lado he escogido una máquina virtual de Azure con las siguientes carácteristicas:

Es una instancia [A3](https://azure.microsoft.com/es-es/pricing/calculator/):

![Azure](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/ejer2b_zpsijsfptd3.png)

- **Procesador:** 4 núcleos
- **RAM:**  7 GB
- **Disco Duro:** 285GB
- **Coste:**  0,202 €/h

**Si se usa el 1% del tiempo:**

Precio del servidor dedicado en Leaseweb: 45.99€/mes * 12 meses = **551,88€**

Precio del servidor Azure( en la nube ): 0,202 €/h =>150,58 €/MES * 0.01 = 1.5058€/MES  * 12 Meses = **18.07€**

**Si se usa el 10% del tiempo:**

Precio del servidor dedicado en Leaseweb: 45.99€/mes * 12 meses = **551,88€**

Precio del servidor Azure( en la nube ): 0,202 €/h =>150,58 €/MES *  0.1 = 15.058€/Mes * 12 Meses = **180.7€**

Como acabamos de demostrar  la opción de usar máquinas virtuales en la nube es mucho más económica que la opción de utilizar un servidor dedicado.


----------
###**Ejercicio 3.1**:¿Qué tipo de virtualización usarías en cada caso? [Comentar en el foro](https://github.com/JJ/IV16-17/issues/1)

Para una virtualización plena o completa usaría máquinas virtuales ya que se pueden tener varios sistemas operativos completos y distintos, utilizando hipervisores como son VMware Player o VirtualBox, etc.

Si quisiéramos ejecutar aplicaciones de  Windows u otro sistema operativo en Linux, cómo por ejemplo, usando WINE usaría una virtualización de aplicación

Si quisiéramos tener nuestro servicio de almacenamiento, virtualizando la memoria utilizaría virtualización parcial ya que nos facilita la escalabilidad del hardware y el control de errores

Usaría la virtualización de entornos de desarrollo en el caso de tener que usar dos versiones de phyton y evitar así crear conflictos con el sistema u otros proyectos.

----------
###**Ejercicio 3.2**:Crear un programa simple en cualquier lenguaje interpretado para Linux, empaquetarlo con CDE y probarlo en diferentes distribuciones.

El programa creado es:

    # Fichero ejer3.py

    #!/usr/bin/env python
	import math

	def cribaEratostenes(lista):
		n= lista[len(lista)-1]
		raiz = math.sqrt(n)
		for i in range(int(raiz)):
			j=i+1
			while j <len(lista):
				if lista[j]%lista[i] == 0:
					lista.pop(j)
				j+=1

		print lista

	tope = int(raw_input("Escriba un numero natural: "))
	lista=list(range(2,tope+1))
	cribaEratostenes(lista)

Lo siguiente que he hecho ha sido instalar cde en mi equipo, para ello:

    sudo apt-get install cde
Después empaquetamos el script con:

`cde python ejer3.py  `

Nos situamos en el directorio  /Ejercicios/cde-package/cde-root/Ejercicios  donde encontramos el fichero **python.cde**

    vagrant@vagrant:/Ejercicios$ cd cde-package/cde-root/Ejercicios/$ ./python.cde ejer3.py
    Escriba un numero natural: 5
	[2, 3, 5]

----------
###**Ejercicio 4**:Comprobar si el procesador o procesadores instalados tienen estos flags. ¿Qué modelo de procesador es? ¿Qué aparece como salida de esa orden?


Con el comando:

    cat /proc/cpuinfo

El modelo de procesador es el :

	Intel(R) Core(TM) i7-3632QM CPU @ 2.20GHz

Para la salida que aparece al visualizar los flags es la siguiente::

    egrep '^flags.*(vmx|svm)' /proc/cpuinfo
Obtengo la salida:
![Flags](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/flag_zpsdulstv8i.png)

Como podemos observar mi equipo dispone de capacidades para la virtualización.

----------
###**Ejercicio 5.1**: Comprobar si el núcleo instalado en tu ordenador contiene este módulo del kernel usando la orden kvm-ok.

Lo primero que debemos hacer es instalar kvm:

    sudo apt-get install cpu-checker

Ahora desde la terminal ejecutamos:

	 sudo kvm-ok
![KVM-OK](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/kvm-ok_zps4uwlthlb.png)



----------
###**Ejercicio 5.2**:  Instalar un hipervisor para gestionar máquinas virtuales, que más adelante se podrá usar en pruebas y ejercicios.

Ya tenia instalado Virtualbox y VMware.
