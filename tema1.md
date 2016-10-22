# **Ejercicios Tema 1**

###**Ejercicio 1**: Consultar en el catálogo de alguna tienda de informática el precio de un ordenador tipo servidor y calcular su coste de amortización a cuatro y siete años. [Consultar este artículo en Infoautónomos sobre el tema.](http://infoautonomos.eleconomista.es/consultas-a-la-comunidad/988/)

El servidor escogido es el [HP ProLiant ML310e G8 XE E3-1220/8GB/2TB](https://www.pccomponentes.com/hp-proliant-ml310e-g8-xe-e3-1220-8gb-2tb)

Sobre el equipo:

 - Procesador  Intel Xeon (4 núcleos, 3,1 GHz, 8 MB, 69 W)
 - Disco duro dos unidades de 1TB (2x1TB)
 - Unidad Óptica Unidad DVD-ROM JackBlack SATA de media altura
 - Memoria RAM 8GB
 - Tarjetas de red Adaptador Ethernet 330i de 1 Gb y 2 puertos por controlador
 - Control de energía
	 - Tipo de fuente de alimentación (1) kit de fuente de alimentación integrada de fábrica de 350 W con varias salidas
 - Fuente de alimentación 350W
 - Dimensiones (Ancho x Profundidad x Altura) 175 x 475.2 x 368.2 mm
 - Peso 18.96 kg

Vamos a calcular su amortización:

- Precio con IVA:  769 €

- IVA (21%): 133.46€

- Total Sin IVA:  635,54 €

**Amortización a 4 años** es la siguiente teniendo en cuenta que corresponde a un 25% por año:

769  * 0.25  =  **192.25€** cada año.

**Amortización a 7 años**
Si consideramos que el servidor  se amortiza más los primeros años y menos los últimos años, tenemos que cada año:

- **Primer año:** 769 * 0.25  = 192.25€
- **Segundo año:** 769 * 0.25 = 192.25€
- **Tercer año:** 769 * 0.15 = 115.35€
-  **Cuarto año:** 769 * 0.15 = 115.35€
- **Quinto año:** 769 * 0.10 = 76.9€
- **Sexto año:** 769  * 0.05 = 38.45€
- **Séptimo año:** 769 * 0.05 = 38.45€

----------
###**Ejercicio 2**:Usando las tablas de precios de servicios de alojamiento en Internet y de proveedores de servicios en la nube, Comparar el coste durante un año de un ordenador con un procesador estándar (escogerlo de forma que sea el mismo tipo de procesador en los dos vendedores) y con el resto de las características similares (tamaño de disco duro equivalente a transferencia de disco duro) en el caso de que la infraestructura comprada se usa sólo el 1% o el 10% del tiempo.

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
