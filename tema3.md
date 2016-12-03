# **Ejercicios Tema 3**

###**Ejercicio 1**: Darse de alta en algún servicio PaaS tal como Heroku, Nodejitsu, BlueMix u OpenShift.

Estaba dado de alta en Openshift por lo que me he dado de alta en Heroku y BlueMix

----------
###**Ejercicio 2**: Crear una aplicación en OpenShift o en algún otro PaaS en el que se haya dado uno de alta. Realizar un despliegue de prueba usando alguno de los ejemplos.

Si ya estas registrado, solo tendríamos que introducir nuestro usuario y contraseña, sino deberíamos registrarnos.
Una vez ya logeados en la web,nos aparecerá una primera página de bienvenida con una serie de pasos a seguir para crear nuestra aplicación. Dicha página solo aparecerá cuando no tengamos ninguna aplicación creada, de tener alguna aplicación creada nos deberíanaparecer una lista con las aplicaciones para acceder a la que queramos.

Vamos a crear una aplicación
Openshift como dije anteriormente dispone de una serie de pasos para la creación de la aplicación y a continuación un enlace “Create your first application now”, el cual pulsaremos para empezar.

El primer paso será elegir el tipo de aplicación, vamos a buscar y elegir WordPress 4.

![CrearApp](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/crearapp_zpsjw3mnizc.png)

El segundo paso es añadir una URL y un dominio y darle a "Create Application".

![Config](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/configApp_zpsmqgf5zxi.png)

![creadaApp](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/creadaApp_zps3gryhdij.png)

Una vez creada la aplicación pulsamos en "Continue to the application overview page".
Esto nos lleva a la página de nuestras aplicaciones, pulsamos en ella y nos aparece una ventana de Información necesaria e instalación.

![infoNecesaria](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/instalacionWordpress_zpsbrsfuyo3.png)

Una vez instalado, ya tendriamos Wordpress instalado y nos debe aparecer la siguiente página:

![escritorioWordPress](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/escritorioWordpress_zpsac9psdjd.png)

En ella podemos hacer las modificaciones necesarias para adaptar a nuestro gusto la aplicación

----------
###**Ejercicio 3**:Realizar una app en express (o el lenguaje y marco elegido) que incluya variables como en el caso anterior.

He usado la aplicación de creación de Porras y apuestas que viene en el repositorio proporcionado en el tema, pero usando mongodb.
Enlace de [mi aplicación al repositorio](https://github.com/cr13/Ejer3Tema3)

Demo de una insercción por consola:

![porra](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/porra_zpsx5et1tau.png)

Demo de porras existentes:

![porraweb](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/porraweb_zps3wlxgfjs.png)

----------

###**Ejercicio 4**:Crear pruebas para las diferentes rutas de la aplicación.

Ejecutamos las pruebas con mocha, y como podemos ver pasa los test:

![test](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/test_zps64vznwff.png)
----------

###**Ejercicio 5**:Instalar y echar a andar tu primera aplicación en Heroku.

Pasos para hacer funcionar nuestra app en Heroku

    sudo heroku login
    sudo heroku apps:create --region eu porraheroku
    sudo heroku addons:create mongolab:sandbox
    sudo heroku auth:token
    - copiar el token
    git push heroku master

    - En username podeis dejarlo en blanco y en password pegar el codigo del token

    sudo heroku addons:open mongolab
    sudo heroku ps:scale web=1
    sudo heroku logs --tail // para activar el modo debug
    sudo heroku open  //para abrir en el navegador

Vamos a insertar una porra, una apuesta y el resultado final del partido

![insertardatosporra](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/porraHeroku_zpshoudlxel.png)

Vamos a ver la porra en el navegador

![verporraweb](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/porraherokuweb_zpsryaa0rfp.png)
----------

###**Ejercicio 6**:Usar como base la aplicación de ejemplo de heroku y combinarla con la aplicación en node que se ha creado anteriormente. Probarla de forma local con foreman. Al final de cada modificación, los tests tendrán que funcionar correctamente; cuando se pasen los tests, se puede volver a desplegar en heroku.

Añadimos .travis.yml al repositorio
Activamos en travis el repositorio
Sincronizamos el repositorio de github en heroku
Activamos en heroku el CI

![ActivamosCI](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/ciHeroku_zps2scsv0bz.png)

----------
###**Ejercicio 7**:Haz alguna modificación a tu aplicación en node.js para Heroku, sin olvidar añadir los tests para la nueva funcionalidad, y configura el despliegue automático a Heroku usando Snap CI o alguno de los otros servicios, como Codeship, mencionados en StackOverflow

----------
###**Ejercicio 8**:Preparar la aplicación con la que se ha venido trabajando hasta este momento para ejecutarse en un PaaS, el que se haya elegido.

----------
