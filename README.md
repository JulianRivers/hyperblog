# Apuntes Curso Git y Github de platzi
## Comandos

- inicializar el repositorio `git init`
- Agregar el archivo al repositorio `git add nombre_de_archivo.extencion`
- Agregamos los cambios para el repositorio `git commit -m “Mensaje”`
- Agregar los cambios de la carpeta en la que nos encontramos agregar todo `git add .`
- Visualizar cambios `git status`
- Histórico de cambios con detalles `git log nombre_de_archivos.extencion`
- Envía a otro repositorio remoto lo que estamos haciendo `git push`
- Traer repositorio remoto `bashgit pull`
- Se usa para devolver el archivo que se tiene en ram cuando escribimos git add lo devuelve a estado natural mientras esta en staging `git rm --cached archivo.extencion`
- Muestra la lista de configuración de git `git config --list`
- Rutas de acceso a la configuración de git `git config --list --show-origin`
- para usar diff se debe escribir el id de identificación de un commit y otro para comparar las diferencias entre estos

```bash
#commit bc6c8b6c2e4c454b239dd3c6ad73849e2cf683a0 (HEAD -> master)
#Author: Julian Riveros
#Date:   Sun Jan 16 19:05:16 2022 -0500
#    Se especifica mas la informacion del documento
#commit 1c202f564af7906fe74bbe665370c60fb7e3136e
#Author: Julian Riveros 
#Date:   Sun Jan 16 19:01:40 2022 -0500
#    Primer commit: se crea el archivo .txt llamado hola mundo y un contenido aleatorio
#vamos a comparar la primera version con la ultima
git diff 1c202f564af7906fe74bbe665370c60fb7e3136e bc6c8b6c2e4c454b239dd3c6ad73849e2cf683a0
```
---
## Cambios en GitHub: de master a main
- Si continuas con la rama master y tienes cambios puedes utilizar el siguiente comando: `git branch -M main`
## viajes en el tiempo
- El comando **git checkout + ID del commit** nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.
- para volver a una versión anterior y además borrar todos los cambios que se han hecho se usa **git reset ID del commit** Hay dos formas de usar `git reset`: con el argumento `--hard`, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento `--soft`, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.
- `git checkout master archivo` ese es el archivo que desea volver a la version mas actual si desea volver todos e usa un .  
- para enviar al repositorio remoto `git push origin main`
---
## Branch
- para hacer una rama `git branch name`
- para listar las ramas `git branch` se pueden usar parametros como `-v` para q sea mas especifico
- para listar TODAS las ramas `git show-branch --all`
---
## Merge
El comando git merge nos permite crear un nuevo commit con la combinación de dos ramas (la rama donde nos encontramos cuando ejecutamos el comando y la rama que indiquemos después del comando).

- Crear un nuevo commit en la rama master combinandolos cambios de la rama cabecera:
```bash
git checkout main
git merge cabecera
```
- Crear un nuevo commit en la rama cabecera combinando los cambios de cualquier otra rama:
```bash
git checkout cabecera
git merge cualquier-otra-rama
```
Asombroso, ¿verdad? Es como si Git tuviera super poderes para saber qué cambios queremos conservar de una rama y qué otros de la otra. El problema es que no siempre puede adivinar, sobretodo en algunos casos donde dos ramas tienen actualizaciones diferentes en ciertas líneas en los archivos. Esto lo conocemos como un conflicto y aprenderemos a solucionarlos en la siguiente clase.

Recuerda que al ejecutar el comando git checkout para cambiar de rama o commit puedes perder el trabajo que no hayas guardado. Guarda tus cambios antes de hacer git checkout.
- para ver todos las urls de los repositorios remotos `git remote -v`
- para cambiar esa url se `git remote set-url name-repo-remote new-url`
---
## Remote
```bash
#Traer la versión del repositorio remoto y
# hacer merge para crear un commit con los archivos
# de ambas partes. Podemos usar git fetch y git merge
# o solo el git pull con el flag --allow-unrelated-histories:
git pull origin master --allow-unrelated-histories

# Por último, ahora sí podemos hacer git push para guardar
# los cambios de nuestro repositorio local en GitHub:
git push origin master
- para agregar una rama(branch) a github `git push -f name-remote name-branch` ejemplo: `git push -f origin cabecera`
```
---
## Tags
- un tag es el nombre que se le puede dar a una version ejemplos: v0.1 2 v0.2.4
- `git tag -a v0.1 -m "resultado de las primeras clases del curso" name-commit` ejemplo `git tag -a v0.1 -m "resultado de las primeras clases del curso" beca6ad`
- para mostrar a que commit exacto están asignados los tag se usa `git show-ref --tags`
- para eliminar un tag `git tag -d name-tag` pero si se subió a github no se borrará
- para eliminar de github se debe hacer con una referencia interna de github: `git push origin :refs/tag/tag-para-borrar`

---
## Stashed:
El stashed nos sirve para guardar cambios para después, Es una lista de estados que nos guarda algunos cambios que hicimos en Staging para poder cambiar de rama sin perder el trabajo que todavía no guardamos en un commit

Ésto es especialmente útil porque hay veces que no se permite cambiar de rama, ésto porque porque tenemos cambios sin guardar, no siempre es un cambio lo suficientemente bueno como para hacer un commit, pero no queremos perder ese código en el que estuvimos trabajando.

El stashed nos permite cambiar de ramas, hacer cambios, trabajar en otras cosas y, más adelante, retomar el trabajo con los archivos que teníamos en Staging pero que podemos recuperar ya que los guardamos en el Stash.

`git stash`
El comando git stash guarda el trabajo actual del Staging en una lista diseñada para ser temporal llamada Stash, para que pueda ser recuperado en el futuro.

Para agregar los cambios al stash se utiliza el comando:

`git stash`
Podemos poner un mensaje en el stash, para asi diferenciarlos en git stash list por si tenemos varios elementos en el stash. Ésto con:

`git stash save "mensaje identificador del elemento del stashed"`
Obtener elelmentos del stash
El stashed se comporta como una Stack de datos comportándose de manera tipo LIFO (del inglés Last In, First Out, «último en entrar, primero en salir»), así podemos acceder al método pop.

El método pop recuperará y sacará de la lista el último estado del stashed y lo insertará en el staging area, por lo que es importante saber en qué branch te encuentras para poder recuperarlo, ya que el stash será agnóstico a la rama o estado en el que te encuentres, siempre recuperará los cambios que hiciste en el lugar que lo llamas.

Para recuperar los últimos cambios desde el stash a tu staging area utiliza el comando:

`git stash pop`
Para aplicar los cambios de un stash específico y eliminarlo del stash:

`git stash pop stash@{<num_stash>}`
Para retomar los cambios de una posición específica del Stash puedes utilizar el comando:

`git stash apply stash@{<num_stash>}`
Donde el <num_stash> lo obtienes desden el git stash list

Listado de elementos en el stash
Para ver la lista de cambios guardados en Stash y así poder recuperarlos o hacer algo con ellos podemos utilizar el comando:

`git stash list`
Retomar los cambios de una posición específica del Stash || Aplica los cambios de un stash específico

Crear una rama con el stash
Para crear una rama y aplicar el stash mas reciente podemos utilizar el comando

`git stash branch <nombre_de_la_rama>`
Si deseas crear una rama y aplicar un stash específico (obtenido desde git stash list) puedes utilizar el comando:

`git stash branch nombre_de_rama stash@{<num_stash>}`
Al utilizar estos comandos crearás una rama con el nombre <nombre_de_la_rama>, te pasarás a ella y tendrás el stash especificado en tu staging area.

Eliminar elementos del stash
Para eliminar los cambios más recientes dentro del stash (el elemento 0), podemos utilizar el comando:

`git stash drop`
Pero si en cambio conoces el índice del stash que quieres borrar (mediante git stash list) puedes utilizar el comando:

`git stash drop stash@{<num_stash>}`
Donde el <num_stash> es el índice del cambio guardado.

Si en cambio deseas eliminar todos los elementos del stash, puedes utilizar:

`git stash clear`
Consideraciones:

El cambio más reciente (al crear un stash) SIEMPRE recibe el valor 0 y los que estaban antes aumentan su valor.
Al crear un stash tomará los archivos que han sido modificados y eliminados. Para que tome un archivo creado es necesario agregarlo al Staging Area con git add [nombre_archivo] con la intención de que git tenga un seguimiento de ese archivo, o también utilizando el comando git stash -u (que guardará en el stash los archivos que no estén en el staging).
Al aplicar un stash este no se elimina, es buena práctica eliminarlo.

---

git grep color -->use la palabra color
git grep la --> donde use la palabra la
git grep -n color–> en que lineas use la palabra color
git grep -n platzi --> en que lineas use la palabra platzi
git grep -c la --> cuantas veces use la palabra la
git grep -c paltzi --> cuantas veces use la palabra platzi
git grep -c “<p>”–> cuantas veces use la etiqueta <p>

git log-S “cabecera” --> cuantas veces use la palabra cabecera en
todos los commits.

grep–> para los archivos
log --> para los commits.
