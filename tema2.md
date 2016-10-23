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

Crear o actualizar package.json

    - npm install -g grunt-cli
    - Dentro de la carpeta de nuestro proyecto
      - npm init (completamos el formulario y ponemos yes)

Yo tenia creado ya el package.json y al realizar los pasos se me ha autocompletado.

    {
      "name": "clasifica_empresas",
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
      },
      "devDependencies": {
        "docco": "^0.7.0",
        "grunt": "^0.4.5",
        "grunt-docco": "^0.4.0",
        "should": "^7.1.1",
        "supertest": "^1.1.0"
      },
      "description": "Sitio Web con las siguientes funcionalidades:",
      "main": "app.js",
      "repository": {
        "type": "git",
        "url": "git+https://github.com/cr13/Califica_empresas.git"
      },
      "author": "Cristóbal Rodríguez Reina",
      "license": "ISC",
      "bugs": {
        "url": "https://github.com/cr13/Califica_empresas/issues"
      },
      "homepage": "https://github.com/cr13/Califica_empresas#readme"
    }


----------

###**Ejercicio 5**:Automatizar con **grunt** y **docco** (o algún otro sistema) la generación de documentación de la librería que se cree. Previamente, por supuesto, habrá que documentar tal librería.

Tenemos que instalar:

    - npm install -g grunt-cli
    - npm install docco grunt-docco --save-dev

Una vez instalado, nos vamos al directorio raiz de grunt-docco en mi caso se ha creado en node_modules/grunt-docco dentro de mi proyecto.

Conetenio de Gruntfile.js

    module.exports = function(grunt) {

      grunt.initConfig({
        clean: { tests: ["docs"] },

        jshint: {
          grunt: ['Gruntfile.js'],
          tasks: ['tasks/docco.js'],
          tests: ['test/*.js'],
          options: {
            node: true
          }
        },

        docco: {
          tests: {
            src: ['test/**/*.js', 'test/**/*.coffee'],
            dest: "docs/"
          },
          'custom-css-test': {
            src: ['test/**/*.js'],
            dest: 'docs/',
            options: {
                css: 'test/fixtures/custom.css',
                output: 'docs/'
            }
          }
        },

        nodeunit: {
          tests: ['test/*_test.js']
        }
      });

      grunt.loadTasks('tasks');

      grunt.loadNpmTasks('grunt-contrib-nodeunit');
      grunt.loadNpmTasks('grunt-contrib-jshint');
      grunt.loadNpmTasks('grunt-contrib-clean');
      grunt.loadNpmTasks('grunt-release');
      // Carga el plugin de grunt para hacer esto
      grunt.loadNpmTasks('grunt-docco');

      // Tarea por omisión: generar la documentación
      grunt.registerTask('default', ['docco']);
      grunt.registerTask('test', ['clean:tests', 'docco', 'nodeunit:tests']);
      grunt.registerTask('lint', ['jshint:grunt', 'jshint:tasks', 'jshint:tests']);
      grunt.registerTask('default', ['lint', 'docco']);
    };

Ahora, solo nos faltaría generar la documentación con el comando << grunt docco >>.
La documentación se generará en el directorio docs.

----------

###**Ejercicio 6**:Para la aplicación que se está haciendo, escribir una serie de aserciones y probar que efectivamente no fallan. Añadir tests para una nueva funcionalidad, probar que falla y escribir el código para que no lo haga (vamos, lo que viene siendo TDD).



----------

###**Ejercicio 7**:Convertir los tests unitarios anteriores con assert a programas de test y ejecutarlos desde **mocha**, usando descripciones del test y del grupo de test de forma correcta. Si hasta ahora no has subido el código que has venido realizando a GitHub, es el momento de hacerlo, porque lo vas a necesitar un poco más adelante.



----------

###**Ejercicio 8**:Haced los dos primeros pasos antes de pasar al tercero.
