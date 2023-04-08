# Git
* Repositorio: Proyecto.
* Stage o Index: Zona donde se colocar&aacute;n los ficheros antes de hacer un commit.
* Commit: Acci&oacute;n en la que se acomete una instant&aacute;nea o snapshot de los ficheros que est&aacute;n en el stage.
* Branch: Rama, una l&iacute;nea de tiempo paralela a la principal (Master).
- - -
Configurar git con nuestros datos.
```javascript
git config —global user.name "joskal"
git config —global user.email "joskal@icloud.com"
```
Para ver/editar nuestra configuraci&oacute;n global:
```bash
#Para listarlo:
git config --global -l

#Para editarlo:
git config --global -e

#Contenido del fichero de configuracion.
[user]
 name = joskal
 email = joskal@gmail.com
[color]
 ui = true
[alias]
 lg = log --oneline --decorate --all --graph
 s = status -sb
[core]
 editor = mvim
```

Podemos definir alias para hacer mas breve la introducción de comandos.
```bash
git config --global alias.s "status -sb"
git config --global alias.lg "log --oneline --decorate --all --graph"
```

Si queremos editar algun alias ya definido, editaremos el fichero de configuraci&oacute;n explicado anteriormente:
```bash
git config --global -e
```
---

# Repositorios
Para inicializar un repositorio (proyecto):
```bash
git init
```
Para quitar git de un proyecto basta con borrar el directorio .git
```bash
rm -rf ./.git
```
Agregar ficheros al stage (escenario):
```bash
#Todos los ficheros
git add .

#Agregar un fichero o una lista de ellos:
git add fichero1 fichero2 fichero3

#Agregar los archivos modificados:
git add -A

#Quitar del stage un archivo concreto o una lista de ellos:
git reset fichero1

#Para agregar los ficheros de una extension de todos los directorios del proyecto:
git add *.txt

#Idem al anterior pero solo del directorio actual:
git add "*.txt"

#Agregar todos los archivos contenidos en el directorio pdfs:
git add pdfs/

#Para ver el estado de los archivos (los que estan en el stage y los que no,
#los agregados, los modificados, y los removidos)
git status
#forma abreviada:
git status -sb
```

Una vez que agregamos todos los ficheros al stage que nos interesan, creamos el commit:

```sh
git commit -m "Agregados todos los ficheros"
```

Tambien podemos crear el commit a la vez que agregamos ficheros al stage.

```sh
git commit -am "Agregados todos los ficheros"
```

Para corregir el texto del commit actual:

```sh
git commit --amend -m "texto corregido"
#para corregirlo con el editor:
git commit --amend
```

Para ver todos los commits creados hasta el momento:

```sh
git log
#forma abreviada:
git log --oneline
#otra forma abreviada:
git log --oneline --decorate --all --graph
```

Para restaurar los archivos del ultimo commit:

```sh
git checkout -- .
#Para restaurar un archivo concreto:
git checkout -- nom_archivo
```

Resetear hasta el commit indicado a su inicio pero sin borrar los archivos, colocandolos en el stage (—soft -menos destructivo):

```sh
#Resetear el commit actual
git reset --soft HEAD^

#resetear hasta el commit indicado por su hash
gir reset --soft 026a7ff
```

Resetear hasta el commit indicado a su inicio borrando los archivos (—hard -mas destructivo):

```sh
#Resetear el commit actual
git reset —hard HEAD^

#resetear hasta el commit indicado por su hash
git reset —hard 026a7ff
```

Aunque reseteemos hasta el primer commit, siempre es posible recuperar commits listándolos primero con:

```sh
git reflog

#el resultado:
86bac49 (HEAD -> master) HEAD@{0}: reset: moving to 86bac49
026a7ff HEAD@{1}: reset: moving to 026a7ff
c4713f0 HEAD@{2}: reset: moving to c4713f0
c4713f0 HEAD@{3}: commit: ultimo commit
026a7ff HEAD@{4}: reset: moving to 026a7ff
026a7ff HEAD@{5}: commit: Agregamos a Linterna Verde y a Robin
d4fe403 HEAD@{6}: reset: moving to d4fe403
ed86731 HEAD@{7}: commit: Agregamos a linterna verde a los heroes
281510d HEAD@{8}: commit: Editamos el readme.md
d4fe403 HEAD@{9}: commit (amend): Agregamos el dir historia
06cd7e6 HEAD@{10}: commit: Agregamos el dir historia
c9904a1 HEAD@{11}: commit: agregamos las ciudades
caed3ea HEAD@{12}: commit: agregamos los heroes
a3e3ef4 HEAD@{13}: commit: Agregamos las misiones
86bac49 (HEAD -> master) HEAD@{14}: commit (initial): Se agrego el archivo readme.md
```

Copiamos el hash del commit que queremos recuperar y lo hacemos así:

por ejemplo queremos recuperar el commit “Agregamos a Linterna Verde y a Robin” cuyo hash es 026a7ff

```sh
git reset --hard 026a7ff

#Hacemos un git log
* 026a7ff (HEAD -> master) Agregamos a Linterna Verde y a Robin - joskal, 2 hours ago
* d4fe403 Agregamos el dir historia - joskal, 3 hours ago
* c9904a1 agregamos las ciudades - joskal, 3 hours ago
* caed3ea agregamos los heroes - joskal, 3 hours ago
* a3e3ef4 Agregamos las misiones - joskal, 6 hours ago
* 86bac49 Se agrego el archivo readme.md - joskal, 7 hours ago
```

Mostrar diferencias entre los archivos que están en el stage y los que acabamos de modificar

```sh
git diff
#Si ya estan todos en el stage:
git diff --staged
```

Renombrar o mover ficheros dentro de git

```sh
git mv destruir-mundo.txt salvar-mundo.txt
#ver resultado:
git status --oneline
## master
R  destruir-mundo.txt -> salvar-mundo.txt
```

Eliminar ficheros dentro de git

```sh
git rm salvar-mundo.txt
#Ver resultado:
git status --oneline
## master
D  salvar-mundo.txt
```

Cuando renombramos o borramos desde el bash con **mv** o **rm**, podemos actualizar los cambios en el stage de la siuiente manera:

```sh
git add -u
```

Podemos ignorar aquellos ficheros y directorios que no queremos en el repositorio creando un fichero .gitignore y colocando en el mismo los nombres dichos ficheros.

```sh
#Ej. Contenido .gitignore

*.log
node_modules/
```

Para ver el commit que nos interesa:

```sh
# por defecto visualiza el master
git show
git show [hash]
```

Branches (ramas)
----------------

Un branch (rama) es una linea temporal paralela al master. Cuando creamos archivos que todavía no queremos incorporar al repositorio master podemos crear una rama independiente para ello.

Por ej. acabamos de crear un fichero llamado villanos.md. Como no sabemos aún que irá en nuestro proyecto creamos una rama llamada rama-villanos de la siguiente manera:

```sh
git branch rama-villanos
```

Para listar las ramas creadas y la que está activa:

```sh
git branch

* master
  rama-villanos
```

Para cambiar a otra rama empleamos el comando que nos permitía ir a otro commit.

```sh
git checkout rama-villanos
```

Para ver las diferencias entre ramas.

```sh
git diff master rama-villanos
```

Para unir la rama que nos interesa al repositorio principal (master), primeramente tenemos que cambiar a la rama master.

Seguidamente uniremos la rama rama-villanos a la rama master con el comando **merge**.

```sh
git checkout master
git merge rama-villanos

Updating 62c8a10..d85d1db
Fast-forward
 villanos.md | 5 +++++
 1 file changed, 5 insertions(+)
 create mode 100644 villanos.md
```

Al hacer un git log aparecen ya juntas las dos ramas.

```sh
* d85d1db (HEAD -> master, rama-villanos) Agregado Flash Reverso - joskal, 9 hours ago
* b518d86 Agregando villanos.md - joskal, 9 hours ago
* 62c8a10 Agregando el gitignore - Strider, 9 weeks ago
* ac0d374 Borramos la historia de batman - Strider, 9 weeks ago
```

Al margen de que las hayamos unido, la rama villanos sigue existiendo aparte, con lo cual podemos borrarla tranquilamente.

```sh
git branch -d rama-villano
```

Disponemos de otra forma de crear una rama y automaticamente entrar en ella.

```sh
git checkout -b rama-villanos
```

Realizamos todos los cambios que queramos en ficheros y unimos las ramas.

```sh
git checkout master
git merge rama-villanos
```

Cuando aparece la palabra `**Fast Forward**` después de un merge, significa que la union de las ramas se realizo sin problemas, ya que no existian commits en la rama a la cual unimos los cambios.

Tags (etiquetas)
----------------

los tags son referencias a un commit en concreto.

```sh
#por defecto se pone el tag en el HEAD
git tag SuperRelease

#para ver todos los tags
git tag

#para borrarlo
git tag -d SuperRelease

#Para poner un tag a un commit especifico se indica su hash
git tag -a version0.1 4e809d4 -m "version alfa"

#mostrar informacion de un tag
git show version0.1
```

Stash (guardado rapido provisional)
-----------------------------------

Sirve para colocar el trabajo actual en un espacio temporal para posteriormente retomarlo.

Consiste en guardar temporalmente aquellos ficheros que estan en el stage y descartarlos en el **stash**. Una vez que hacemos git stash podemos hacer todas las modificaciones que necesitemos provisionalmente hasta que salimos del stash volviendo hasta donde estaba todo antes de entrar dicho comando.

WIP: Work In Progress

```sh
#Comenzar el stash
git stash

#listar los stash
git stash list

#info sobre los stash
git show stash

#volver al estado antes del stash
git stash apply

#borrar los cambios hechos en el stash
git stash drop

git stash clear 

#recuperar el trabajo del stash
#git stash apply
#git stash drop
git stash pop

```

Rebase
------

Sirve para actualizar el punto donde creamos las ramas y los commits.

```sh
#Actualizar una rama
git branch
git checkout rama-misiones
git rebase master
git log
git checkout master
git merge rama-misiones
#opcionalmete borramos la rama
git branch -d rama-misiones
```

Editar los dos ultimos commits del HEAD.

```sh
#opcion -i interactivo (modo editor)
git rebase -i HEAD~2
```

Con un rebase interactivo podemos:

* Unir dos o mas commits en uno solo
* Reordenar commits
* Corregir mensajes de commits
* Separar commits






