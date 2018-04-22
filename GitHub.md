# GitHub

Crear un nuevo proyecto o repositorio desde GitHub. Se nos pedira un nombre para el repositorio (prueba).

En caso de que no tengamos todavia ninguno en local podemos usar esta plantilla:

```sh
#create a new repository on the command line

echo "# prueba" >> README.md
git init
git add README.md
git commit -m "first commit"
```

Una vez que ya tengamos un proyecto podemos iniciar GitHub.

```sh
#nos aseguramos de que no haya nada pendiente.
git status

#iniciamos asi la primera vez.
#Conectamos nuestro repositorio local con el rep. remoto.
git remote add origin https://github.com/joskal/prueba.git
git push -u origin master

```

La forma de subir y bajar los cambios de nuestro repositorio a y desde GitHub es fundamentalmente mediante estos dos comandos: **push** y **pull**

Cuando hacemos un **pull** también hacemos un **merge**

```sh
#subir cambios a github
git push <REMOTENAME> <BRANCHNAME> 
#ejemplo:
git push origin master
#Las siguientes veces solo es necesario hacer
git push

#Actualizar el repositorio local con la almacenada en remoto
git pull origin master
#mas adelante solo es necesario hacer
git pull
```

Cuando tenemos cambios en local y al mismo tiempo hay cambios en remoto, al hacer **push** nos dará un error.

Para evitar eso tenemos el comando **fetch **que nos descarga los cambios sin todavía hacer un merge**.**

```sh
git fetch
#ahora si podemos hacer pull
git pull
#y subimos los cambios a remoto
git push
```

Listar los repositorios en remoto

```sh
git remote
#listar junto con la url
git remote -v
```

Por defecto git no sube los tags al repositorio remoto, por lo que hay que hacerlo manualmente. En GitHub, los tags aparecen en el tab release.

```sh
git push --tags
```

**Clonar un repositorio desde github en local**. En GitHub, dentro del tab code, tenemos un botón que pone **clone or download**, copiamos la dirección y la pegamos junto con el siguiente comando:

```sh
#podemos indicarle un nombre de carpeta (ej: demo10) 
git clone https://github.com/joskal/udemy-heroes.git demo10
```
**Clonar un repositorio de otra cuenta en GitHub a la nuestra (Crear un Fork)**. En GitHub, arriba, a la derecha, tenemos el boton de **Fork**. Tan solo tenemos que pulsarlo y automaticamente aparecera una copia en nuestra cuenta.
Los cambios que hagamos en ese fork, podemos proponerlos al usuario due&ntilde;o del repositorio principal a trav&eacute;s del bot&oacute;n **Pull Request**.

Cuando hacemos un **git branch -a** nos puede salir ramas en github que ya han sido borradas. Entonces tenemos que purgarlas en local de la siguiente manera: 

```sh
git remote prune origin
```
Cuando abrimos un **issue** podemos cerrarlo con el boton correspondiente o en local a traves de la terminal. Debemos tomar nota antes del numeral del issue. P.ej: Resolvemos el issue agregando un commit y agregando el comando **fixes #** en el comentario (Tambien podemos poner en lugar de **fixes** la palabra **closes** o **resolves**):
```sh
git commit -am "Agregamos a Nick Fury fixes #3"
#Subimos los cambios a GitHub
git push
```
## wiki
Un wiki es una base de conocimientos relacionado con nuestro pryecto. En Github viene habilitado por medio de un tab habilitado al efecto en la parte superior.

El primer wiki que creamos viene ya con el nombre por defecto: **Home**. Este nombre es obligatorio para el primero y conviene que lo respetemos.

Por defecto cualquiera puede modificar el contenido de nuestras wikis. para evitar esto iremos a la pestaña **settings** y en la sección **features** marcaremos la opción **Restrict editing to collaborators only**. De todas formas aunque cualquiera ya no pueda modificar el contenido, sí que puede verlo.

Podemos referenciar a otros wikis de nuestros repositorios tan solo con el nombre.
```html
[Enlace al wiki](NombreWiki)
```
## Projects
La manera de crear proyectos es como crear una gran pizarra donde se ubicará una serie de columnas que contendrán las notas. Podemos cambiar las notas a otras columnas según nos interese. Las notas se pueden convertir en **issues** pulsando en el botón que aparece en cada nota. Cuando la convirtamos en un issue será tratado como tal, llevándonos a la pestaña **issues** cuando la editemos. 
## GitHub Pages
GitHub proporciona un espacio para montar nuestras webs. Para ello debemos crear un repositorio nuevo con un nombre especial: nuestro nombre de usuario seguido de github.io.
Por ejemplo, si nuestro nombre de usuario es joskal, debemos crear un nuevo repositorio con este nombre:
**joskal.github.io**

Podemos seleccionar una plantilla para nuestra web entrando en **settings / GitHub pages / Choose a theme**

Al seleccionar una plantilla se nos generarán dos archivos: **\_config.yml** (plantilla) e **index.md** (contenido).

Para averiguar el enlace donde se publicará nuestra página iremos a **settings / Hithub pages** Donde aparecerá el enlace como **Your site is published at https://joskal.github.io**.

**Github pages** no está limitado a estos dos archivos. En su lugar podemos subir un conjuntos de ficheros html, css y javascript que trabajaremos en local. Para ello visualizaremos todos los ficheros en la pestaña **Code** y acto seguido pincharemos en el botón **Clone or Download**. Copiamos la url que nos aparecerá y en un terminal, dentro del directorio de nuestra elección escribiremos esto:
```bash
git clone https://github.com/joskal/joskal.github.io.git
```
Optamos por eliminar o renombrar los ficheros creados antes y empezamos a crear nuestra estructura web con un **index.html**.

Podemos tener alojado un espacio web en cada repositorio. Para ello debemos crear un directorio **docs** en el repositorio en cuestión y alojar en él los ficheros que conformarán la web. Inmediatamente después nos vamos a **settings / GitHub Pages / Source** y elegimos la opción **master branch / docs folder**.
## SSH
Para generar una clave ssh en local: Desde nuestro directorio home, comprobar si existe el directorio **.ssh**, si no es así, lo creamos. Hacemos  **cd ~/.ssh** e introducimos el siguiente comando con nuestro email:
```bash
ssh-keygen -t rsa -C "miemail@mail.com"
```
Con esto se nos generará dos archivos: **id_rsa** (clave privada) y **id_rsa.pub** (clave pública).

Ahora procederemos a verificar la conexión ssh en github. Entramos en **Settings / SSH and GPG keys** y pulsamos en **New SSH key**. Introducimos un titulo (p.ej: iMac joskal) para nuestra clave ssh en **Title** y en el campo **key** pegaremos el contenido del archivo **id_rsa.pub**, pinchamos en **Add SSH key**. Y ahora nos pedirá nuestra contraseña de Github. En caso de que nos equivoquemos podemos borrar la clave y volver a empezar.

A continuación vamos a realizar la conexión desde nuestra máquina con github.
```bash
ssh -T git@github.com
```
La forma de clonar un repositorio en local por ssh es la siguiente:
```bash
# Clonar el repositorio yeoman por ssh
git clone git@github.com:joskal/yeoman.git
```

## Tokens
Los tokens de acceso personal son una especie de llaves para acceder a distintas partes de github, entre ellos los gist.

**Settings / Developer settings / personal access tokens**.

Podemos crear tantos tokens como necesitemos, pero a la hora de crearlos conviene tomar nota de ellos en cuanto lo generemos, ya que no volverán a mostrarse cuando volvamos a acceder. Pero sí podemos regenerar uno nuevo editándolo y pulsando el botón **Regenerate token**. 

## Gists
Los gists son una herramienta ideal para programadores, las cuales permiten compartir nuestro código con otros usuarios. Son repositorios, por lo general, de uno o más ficheros.

La forma de acceder a los gists es pinchando en el icono de usuario y después en **your gists** o directamente introduciendo la url: **https://gist.github.com/**

Una vez en la página, introduciremos una descripción del gist y el contenido del fichero.Si queremos agregar otro fichero tan sólo tenemos que pulsar en **Add file**. Al terminar pulsaremos uno de los dos botones al efecto: **Create secret gist** o **Create public gist**. El primer botón lo que hace realmente es que el gist no aparezca en los resultados de búsqueda de github mientras que el segundo sí.

Al pinchar en un gist se nos aparecen varios botones, entre ellos un cuadro de lista con las siguientes opciones:
* **embed**: Con esta opción podemos insertar el gist como un código javascript (en caso de que el gist lo sea) insertando en nuestro editor la dirección proporcionada al lado.
