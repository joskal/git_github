# Git
* Repositorio: Proyecto.
* Stage o Index: Zona donde se colocar&aacute;n los ficheros antes de hacer un commit.
* Commit: Acci&oacute;n en la que se acomete una instant&aacute;nea o snapshot de los ficheros que est&aacute;n en el stage.
* Branch: Rama, una l&iacute;nea de tiempo paralela a la principal (Master).
- - -
Configurar git con nuestros datos.
```javascript
git config —global user.name "joskal"
git config —global user.email "joskal@gmail.com"
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

Para agregar los ficheros de una extension de todos los directorios del proyecto:
git add *.txt

#Idem al anterior pero solo del directorio actual:
git add "*.txt"

```
