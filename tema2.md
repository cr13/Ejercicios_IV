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

Tenemos que instalar:

    - npm install -g grunt-cli
    - npm install docco grunt-docco --save-dev

Una vez instalado, nos vamos al directorio raiz del proyecto y nos creamos el Gruntfile.js.

Conetenio de Gruntfile.js

    'use strict';

    module.exports = function(grunt) {

      // Configuración del proyecto
      grunt.initConfig({
      pkg: grunt.file.readJSON('package.json'),
      docco: {
          debug: {
          src: ['*.js'],
          options: {
              output: 'docs/'
          }
          }
      }
      });

      // Carga el plugin de grunt para hacer esto
      grunt.loadNpmTasks('grunt-docco');

      // Tarea por omisión: generar la documentación
      grunt.registerTask('default', ['docco']);
    };

Ahora, solo nos faltaría generar la documentación con el comando << grunt docco >>.
La documentación se generará en el directorio docs.

----------

###**Ejercicio 6**:Para la aplicación que se está haciendo, escribir una serie de aserciones y probar que efectivamente no fallan. Añadir tests para una nueva funcionalidad, probar que falla y escribir el código para que no lo haga (vamos, lo que viene siendo TDD).

    //Permite mostrar todas las empresas y sus respectivas puntuaciones
     app.get('/mostrarclasificacion',  function(req, res){
       var objBD = BD();
       objBD.query('SELECT * FROM ranking', function( error, resultado, fila){
         assert.ok(!error,"Error en la consulta del ranking");
         assert.notEqual(resultado.length,0,"No exisite niguna puntuación en estos momentos");
         res.render('ranking', {datos:resultado } );
       });
     });

  ----------

  ###**Ejercicio 7**:Convertir los tests unitarios anteriores con assert a programas de test y ejecutarlos desde **mocha**, usando descripciones del test y del grupo de test de forma correcta. Si hasta ahora no has subido el código que has venido realizando a GitHub, es el momento de hacerlo, porque lo vas a necesitar un poco más adelante.

 1º Preparamos nuestro test.js
    var assert = require('assert');
     var mysql = require('mysql');

     //----------------------------------------------------------------
     //Funcion para conectar a la base de datos
     function BD(){
       var conexion = mysql.createConnection({
         host: 'localhost',
         user: 'root',
         password: 'cr',
         port: 3306,
         database: 'clasifica_empresa'
       });
       return conexion;
     }

     //----------------------------------------------------------------

     describe("Prueba Test",function(done){
       //Permite insertar una nueva empresa en el sistema
       it("Insertar una nueva empresa",function(){
         var objBD = BD();
     	  objBD.query('INSERT INTO `clasifica_empresa`.`empresas` (`nombre_empresa`) VALUES ("daitsu")', function( error ){
            assert.ok(!error,"Error al insertar la empresa");
            objBD.end(done);
         });
       });
       //Permite mostrar todas las empresas del sistema que un usuario dado no ha votado
       it("Mostrar listado de empresas que faltan por votar",function(){
         var objBD = BD();
         objBD.query('SELECT `ID`,`nombre_empresa` FROM empresa WHERE not EXISTS (select voto.IDempresa from voto where empresa.ID=voto.IDempresa and voto.Borrado='+1+' and voto.DNIvotante='+254785236+')', function( error,resultado,fila){
           assert.ok(!error,"Error en la consulta de empresas");
           assert.notEqual(resultado.length,0,"No hay empresas en el sistema o ya has votado en todas");
           objBD.end(done);
         });
       });
     });

 2º Instalamos npm install -g mocha
 3º Probamos nuestro test con mocha test/test.js

 ![mocha test](http://i1266.photobucket.com/albums/jj540/Juantan_Tonio/mochoo_zps7j2tdozp.png)

----------

###**Ejercicio 8**:Haced los dos primeros pasos antes de pasar al tercero.
