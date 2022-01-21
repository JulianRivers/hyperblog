# Comandos

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
#Author: Julian Riveros <juliancamilorifo@ufps.edu.co>
#Date:   Sun Jan 16 19:05:16 2022 -0500
#    Se especifica mas la informacion del documento
#commit 1c202f564af7906fe74bbe665370c60fb7e3136e
#Author: Julian Riveros <juliancamilorifo@ufps.edu.co>
#Date:   Sun Jan 16 19:01:40 2022 -0500
#    Primer commit: se crea el archivo .txt llamado hola mundo y un contenido aleatorio
#vamos a comparar la primera version con la ultima
git diff 1c202f564af7906fe74bbe665370c60fb7e3136e bc6c8b6c2e4c454b239dd3c6ad73849e2cf683a0
```
- El comando **git checkout + ID del commit** nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.
- para volver a una versión anterior y además borrar todos los cambios que se han hecho se usa **git reset ID del commit** Hay dos formas de usar `git reset`: con el argumento `--hard`, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento `--soft`, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.
- `git checkout master archivo` ese es el archivo que desea volver a la version mas actual si desea volver todos e usa un .  
