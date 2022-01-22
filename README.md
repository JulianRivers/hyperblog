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
## viajes en el tiempo
- El comando **git checkout + ID del commit** nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.
- para volver a una versión anterior y además borrar todos los cambios que se han hecho se usa **git reset ID del commit** Hay dos formas de usar `git reset`: con el argumento `--hard`, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento `--soft`, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.
- `git checkout master archivo` ese es el archivo que desea volver a la version mas actual si desea volver todos e usa un .  
- para enviar al repositorio remoto `git push origin main`
---
## merge
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
## remote
```bash
#Traer la versión del repositorio remoto y
# hacer merge para crear un commit con los archivos
# de ambas partes. Podemos usar git fetch y git merge
# o solo el git pull con el flag --allow-unrelated-histories:
git pull origin master --allow-unrelated-histories

# Por último, ahora sí podemos hacer git push para guardar
# los cambios de nuestro repositorio local en GitHub:
git push origin master
```
---
## tags
- un tag es el nombre que se le puede dar a una version ejemplos: v0.1 2 v0.2.4
- `git tag -a v0.1 -m "resultado de las primeras clases del curso" name-commit` ejemplo `git tag -a v0.1 -m "resultado de las primeras clases del curso" beca6ad`
- para mostrar a que commit exacto están asignados los tag se usa `git show-ref --tags`
