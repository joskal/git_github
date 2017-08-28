# gulp.js

Instalar gulp globalmente
```sh
sudo npm install -g gulp
```

Comprobar versiones
```sh
node --version
npm --version
gulp --version
```
---

Para usar gulp en nuestros proyectos debemos hacer una instalación local en nuestro directorio de trabajo.

Primero vamos a generar el fichero package.json

```js
npm init
```

Después de lo cual se nos preguntará por una serie de datos (nombre, correo, directorio, descripción, etc..) y nos generará un fichero package.json.

A continuación instalaremos gulp de forma local en el directorio de nuestro proyecto junto con otros paquetes útiles. Nos generará un directorio con las dependencias (node\_modules)

```sh
npm install --save-dev gulp gulp-sass browser-sync
```

con la opción —save iremos grabando en package.json los nombres de los paquetes que vayamos instalando.

Este es el contenido del fichero package.json generado:

```json
{
  "name": "prueba1",
  "version": "1.0.0",
  "description": "pruebas en gulp",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Jose Callealta",
  "license": "ISC",
  "devDependencies": {
    "browser-sync": "^2.18.13",
    "gulp": "^3.9.1",
    "gulp-sass": "^3.1.0"
  }
}
```

gulpfile.js
-----------

En este fichero se definirán las tareas a ejecutar por gulp.

En primer lugar se declara una variable por cada paquete instalado.

```json
var gulp 		    = require('gulp');
var sass 		    = require('gulp-sass');
var browserSync	= require('browser-sync');
var reload 		  = browserSync.reload;
```

Después se definen las tareas correspondientes con **gulp.task. **Dentro de task se indicarán el origen **gulp.src()** y el destino **gulp.dest()** de la tarea.

```js
gulp.task('sass',function(){
	gulp.src('scss/app.scss')
		.pipe(sass({
			includedPaths: ['scss']
		}))
		.pipe(gulp.dest('app/css'));
});
```

Asimismo también tenemos el método **gulp.watch. **Que comprueba si se han realizado cambios en determinados ficheros o directorios e inicia la tarea especificada.

```js
gulp.watch('js/**/*.js', function(event) {
  console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
});
```

Si no especificamos ninguna tarea al llamar a **gulp, **se ejecutará la que definamos por defecto (**default**)

```js
gulp.task('default', ['serve']);
```gulp browser-sync
-----------------

```js
var gulp 		= require('gulp');
var browserSync	= require('browser-sync');
var reload 		= browserSync.reload;
var ficheros	= ["app/**/*.html", "app/css/**/*.css", "app/js/**/*.js"];

gulp.task('serve',function(){
	browserSync.init(ficheros,{
		server:{
			baseDir: 'app'
		}
	})
});

// Observar cambios en los ficheros
gulp.watch(ficheros, function(event) {
  console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
});

gulp.task('default', ['serve']);

```

gulp-sass browser-sync
----------------------

```js
var gulp 		    = require('gulp');
var sass 		    = require('gulp-sass');
var browserSync	= require('browser-sync');
var reload 		  = browserSync.reload;

gulp.task('sass',function(){
	gulp.src('scss/app.scss')
		.pipe(sass({
			includedPaths: ['scss']
		}))
		.pipe(gulp.dest('app/css'));
});

gulp.task('serve',['sass'],function(){
	browserSync.init(["app/css/*.css", "app/js/*.js", "app/*.html"],{
		server:{
			baseDir: 'app'
		}
	})
});

gulp.task('watch', ['sass', 'serve'], function(){
	gulp.watch(['scss/*.scss'], ['sass']);
});

gulp.task('default', ['serve']);
```
