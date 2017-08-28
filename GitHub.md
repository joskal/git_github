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
