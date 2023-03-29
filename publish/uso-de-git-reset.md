# Uso de `git reset`

`git reset` sirve para deshacer cambios en commits locales. Si un commit se ha publicado a un repositorio remoto hay que usar `git revert` en su lugar.

`git reset` posee 3 parametros según los cuales actua de una u otra forma:

- `--mixed`: Saca los archivos del Stage pero no elimina los cambios que hayamos hecho en los archivos del directorio de trabajo (los archivos del proyecto). Si no se indica ningún parametro es el que se usa por defecto.

- `--hard`: Saca los archivos del Stage y elimina los cambios realizados en los archivos del directorio de trabajo (el directorio del proyecto). Dicho de otra forma, vuelve al estado inicial del commit en el que estamos.

  Si lo combinamos con `HEAD~<numero>` podemos volver a un commit anterior, pero hay que tener encuenta que el Stage actual y los commits posteriores desapareceran (aunque se pueden recuperar con `git reflog` durante un tiempo).

- `--soft`: Al usarse junto con el __identificador SHA de un commit anterior__ nos situa en ese commit anterior __pero sin perder los archivos del Stage actual__.


## Casos de uso

Saca el archivo `<filename>` del Stage: 

```bash
git reset <filename>
```
<br>

Saca todos los archivos del Stage:

```bash
git reset
```
<br>

Idem que el anterior:

```bash
git reset --mixed
```
<br>

Nos devuelve al último commit. Es decir, saca todos los archivos del Stage y borra todos los cambios a los archivos del directorio de trabajo (archivos del proyecto):

```bash
git reset --hard
```
<br>

Nos situa 2 commits atrás. Al usar `--hard` desaparecerán los commits posteriores a ese commit y se vaciará el Stage:

```bash
git reset --hard HEAD~2
```
<br>

Nos situa en el commit con identificador `<SHA-commit>`. Al usar `--soft` se mantendrán los archivos añadidos al Stage:

```bash
git reset --soft <SHA-commit>
```
<br>

## Comandos relacionados con `git reset`

Si usamos `git reset hard HEAD~<numero>` por error `git reflog` nos permite recuperar los commits borrados. En realidad estos commits no se han borrado exactamente, si no que se han quedado "huerfanos" al no tener una ruta directa para que el puntero (`HEAD`) los pueda encontrar.

```bash
git reflog
```
<br>

Nos permite retomar un commit anterior en el repositorio remoto. Pero en lugar de volver hacia atrás y que desaparezcan los commits posteriores como hace `git reset --hard` nos crea un nuevo commit partiendo de ese commit anterior. De esta forma evitamos problemas con otros miembros del equipo que pudieran estar usando alguno de esos commits posteriores.
```bash
git revert
```
<br>
<br>
<hr>

## Fuentes relacionadas
- [git reset (inglés) - atlassian.com](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)
- [git reset (español) - atlassian.com](https://www.atlassian.com/es/git/tutorials/undoing-changes/git-reset)