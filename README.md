# GIT

![GIT](img/git.jpg)

## Una breve historia de Git

Como muchas de las grandes cosas en esta vida, Git comenzó con un poco de destrucción creativa y una gran polémica.

El kernel de Linux es un proyecto de software de código abierto con un alcance bastante amplio. Durante la mayor parte del mantenimiento del kernel de Linux (1991-
2002), los cambios en el software se realizaban a través de parches y archivos. En el 2002, el proyecto del kernel de Linux empezó a usar un DVCS propietario llamado BitKeeper.

En el 2005, la relación entre la comunidad que desarrollaba el kernel de Linux y la compañía que desarrollaba BitKeeper se vino abajo y la herramienta dejó de ser ofrecida de manera gratuita. Esto impulsó a la comunidad de desarrollo de Linux (y en particular a Linus Torvalds, el creador de Linux) a desarrollar su propia herramienta basada en algunas de las lecciones que aprendieron mientras usaban BitKeeper. Algunos
de los objetivos del nuevo sistema fueron los siguientes:

- Velocidad
- Diseño sencillo
- Gran soporte para desarrollo no lineal (miles de ramas paralelas)
- Completamente distribuido
- Capaz de manejar grandes proyectos (como el kernel de Linux) eficientemente (velocidad y tamaño de los datos)

Desde su nacimiento en el 2005, Git ha evolucionado y madurado para ser fácil de usar y conservar sus características iniciales. Es tremendamente rápido, muy eficiente con grandes proyectos y tiene un increíble sistema de ramificación (branching) para
desarrollo no lineal.

## Configurando Git por primera vez

Git trae una herramienta llamada git config, que te permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git. Estas
variables pueden almacenarse en tres sitios distintos:

- Archivo /etc/gitconfig: Contiene valores para todos los usuarios del sistema y todos sus repositorios. Si pasas la opción --system a git config, lee y escribe
específicamente en este archivo.

- Archivo ~/.gitconfig o ~/.config/git/config: Este archivo es específico de tu usuario. Puedes hacer que Git lea y escriba específicamente en este archivo pasando la opción --global.

- Archivo config en el directorio de Git (es decir, .git/config) del repositorio que estés utilizando actualmente: Este archivo es específico del repositorio actual.
- 
Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de .git/config tienen preferencia sobre los de /etc/gitconfig.

## Tu Identidad

Lo primero que deberás hacer cuando instales Git es establecer tu nombre de usuario y dirección de correo electrónico. Esto es importante porque los "commits" de
Git usan esta información, y es introducida de manera inmutable en los commits que envías:

```git
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

De nuevo, sólo necesitas hacer esto una vez si especificas la opción --global, ya que Git siempre usará esta información para todo lo que hagas en ese sistema. Si quieres sobrescribir esta información con otro nombre o dirección de correo para proyectos específicos, puedes ejecutar el comando sin la opción 
--global cuando estés en ese proyecto.

## Comprobando tu Configuración

Si quieres comprobar tu configuración, puedes usar el comando git config --list para mostrar todas las propiedades que Git ha configurado:

Version del git instalado
```git
$ git config --list
```

## Comandos

Version del git instalado
```git
$ git --version 
```
Ayuda sobre comandos git
```git
$ git help
```

Todos los comandos para hacer un commit
```git
$ git help commit
```
***Nota: la tecla q es para salir de esta opcion***

## Obtencion de un Repositorio

![GIT](img/git_1.jpg)

Esto crea un subdirectorio nuevo llamado .git, el cual contiene todos los archivos necesarios del repositorio – un esqueleto de un repositorio de Git.


```git
$ git init
```

Si deseas empezar a controlar versiones de archivos existentes (a diferencia de un directorio vacío), probablemente deberías comenzar el seguimiento de esos archivos y hacer una confirmación inicial. Puedes conseguirlo con unos pocos comandos git add para especificar qué archivos quieres controlar, seguidos de un git commit para confirmar los cambios:

```git
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```

## Clonado del Repositorio

Si deseas obtener una copia de un repositorio Git existente — por ejemplo, un
proyecto en el que te gustaría contribuir — el comando que necesitas es git clone. Si
estás familizarizado con otros sistemas de control de versiones como Subversion, verás
que el comando es "clone" en vez de "checkout". Es una distinción importante, ya que
Git recibe una copia de casi todos los datos que tiene el servidor. Cada versión de
cada archivo de la historia del proyecto es descargada por defecto cuando ejecutas git
clone.


```git
$ git clone https://github.com/libgit2/libgit2
```

Esto crea un directorio llamado libgit2, inicializa un directorio .git en su interior,
descarga toda la información de ese repositorio y saca una copia de trabajo de la
última versión. Si te metes en el directorio libgit2, verás que están los archivos del
proyecto listos para ser utilizados. Si quieres clonar el repositorio a un directorio con
otro nombre que no sea libgit2, puedes especificarlo con la siguiente opción de línea
de comandos:

```git
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

Git te permite usar distintos protocolos de transferencia. El ejemplo anterior usa el
protocolo https://, pero también puedes utilizar git:// o
usuario@servidor:ruta/del/repositorio.git que utiliza el protocolo de transferencia SSH.

## Guardar datos en el repositorio

Recuerda que cada archivo de tu repositorio puede tener dos estados: rastreados y sin rastrear.

Los archivos rastreados (tracked files en inglés) son todos aquellos archivos que
estaban en la última instantánea del proyecto; pueden ser archivos sin modificar,
modificados o preparados. Los archivos sin rastrear son todos los demás - cualquier otro
archivo en tu directorio de trabajo que no estaba en tu última instantánea y que no
está en el área de preparación (staging area). Cuando clonas por primera vez un
repositorio, todos tus archivos estarán rastreados y sin modificar pues acabas de sacarlos
y aun no han sido editados.

La herramienta principal para determinar qué archivos están en qué estado es el
comando git status. Si ejecutas este comando inmediatamente después de clonar un
repositorio, deberías ver algo como esto:

```git
$ git status
On branch master
nothing to commit, working directory clean
```

Esto significa que tienes un directorio de trabajo limpio - en otras palabras, que no hay
archivos rastreados y modificados.

Supongamos que añades un nuevo archivo a tu proyecto, un simple README. Si el archivo no existía antes y ejecutas git status, verás el archivo sin rastrear de la
siguiente manera:

```git
$ echo 'My Project' > README
$ git status
On branch master
Untracked files:
    (use "git add <file>..." to include in what will be committed)
    README
    nothing added to commit but untracked files present (use "git add" to track)
```

Puedes ver que el archivo README está sin rastrear porque aparece debajo del
encabezado “Untracked files” (“Archivos no rastreados” en inglés) en la salida. Sin
rastrear significa que Git ve archivos que no tenías en el commit anterior. Git
no los incluirá en tu próximo commit a menos que se lo indiques explícitamente. Se
comporta así para evitar incluir accidentalmente archivos binarios o cualquier otro
archivo que no quieras incluir. Como tú sí quieres incluir README, debes comenzar a
rastrearlo.

## Rastrear Archivos Nuevos

Para comenzar a rastrear un archivo debes usar el comando git add. Para comenzar a
rastrear el archivo README, puedes ejecutar lo siguiente:

```git
$ git add README
```

```git
$ git status
On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    new file: README
```

Puedes ver que está siendo rastreado porque aparece luego del encabezado “Cambios a
ser confirmados” (“Changes to be committed” en inglés). Si confirmas en este punto, se
guardará en el historial la versión del archivo correspondiente al instante en que
ejecutaste git add. Anteriormente cuando ejecutaste git init, ejecutaste luego git add
(files) - lo cual inició el rastreo de archivos en tu directorio. El comando git add
puede recibir tanto una ruta de archivo como de un directorio; si es de un directorio,
el comando añade recursivamente los archivos que están dentro de él.

## Preparar Archivos Modificados

Vamos a cambiar un archivo que esté rastreado. Si cambias el archivo rastreado llamado
“CONTRIBUTING.md” y luego ejecutas el comando git status, verás algo parecido a esto:

```git
$ git status
On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    new file: README
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: CONTRIBUTING.md
```

## Estado Abreviado

Si bien es cierto que la salida de git status es bastante explícita, también es verdad
que es muy extensa. Git ofrece una opción para obtener un estado abreviado, de
manera que puedas ver tus cambios de una forma más compacta. Si ejecutas git status
-s o git status --short, obtendrás una salida mucho más simplificada.


```git
$ git status -s
    M README
    MM Rakefile
    A lib/git.rb
    M lib/simplegit.rb
    ?? LICENSE.txt
```

Los archivos nuevos que no están rastreados tienen un ?? a su lado, los archivos que
están preparados tienen una A y los modificados una M. El estado aparece en dos
columnas - la columna de la izquierda indica el estado preparado y la columna de la
derecha indica el estado sin preparar. Por ejemplo, en esa salida, el archivo README está
modificado en el directorio de trabajo pero no está preparado, mientras que
lib/simplegit.rb está modificado y preparado. El archivo Rakefile fue modificado,
preparado y modificado otra vez por lo que existen cambios preparados y sin preparar.

## Ignorar Archivos

A veces, tendrás algún tipo de archivo que no quieres que Git añada
automáticamente o más aun, que ni siquiera quieras que aparezca como no rastreado.
Este suele ser el caso de archivos generados automáticamente como trazas o archivos
creados por tu sistema de compilación. En estos casos, puedes crear un archivo llamado
.gitignore que liste patrones a considerar. Este es un ejemplo de un archivo .gitignore:

```git
$ cat .gitignore
    *.[oa]
    *~
```

La primera línea le indica a Git que ignore cualquier archivo que termine en “.o” o
“.a” - archivos de objeto o librerías que pueden ser producto de compilar tu código. La
segunda línea le indica a Git que ignore todos los archivos que terminen con una
tilde (~), la cual es usada por varios editores de texto como Emacs para marcar
archivos temporales.

Si el comando git status es muy impreciso para ti - quieres ver exactamente que ha
cambiado, no solo cuáles archivos lo han hecho - puedes usar el comando git diff.


```git
$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
    Please include a nice description of your changes when you submit your PR;
    if we have to read the whole diff to figure out why you're contributing
    in the first place, you're less likely to get feedback and have your change
    -merged in.
    +merged in. Also, split your changes into comprehensive chunks if you patch is
    +longer than a dozen lines.
    If you are starting to work on a particular area, feel free to submit a PR
    that highlights your work in progress (and note in the PR title that it's
```

Este comando compara lo que tienes en tu directorio de trabajo con lo que está en el
área de preparación. El resultado te indica los cambios que has hecho pero que aun no
has preparado.

Si quieres ver lo que has preparado y será incluido en la próxima confirmación, puedes
usar git diff --staged. Este comando compara tus cambios preparados con la última
instantánea confirmada.

## Confirmar tus Cambios

Ahora que tu área de preparación está como quieres, puedes confirmar tus cambios.
Recuerda que cualquier cosa que no esté preparada - cualquier archivo que hayas
creado o modificado y que no hayas agregado con git add desde su edición - no será
confirmado. Se mantendrán como archivos modificados en tu disco. En este caso,
digamos que la última vez que ejecutaste git status verificaste que todo estaba
preparado y que estás listo para confirmar tus cambios. La forma más sencilla de
confirmar es escribiendo git commit:

```git
$ git commit
```

(Para obtener una forma más explícita de recordar
qué has modificado, puedes pasar la opción -v a git commit. Al hacerlo se incluirá en el
editor el diff de tus cambios para que veas exactamente qué cambios estás
confirmando). Cuando sales del editor, Git crea tu confirmación con tu mensaje
(eliminando el texto comentado y el diff).

Otra alternativa es escribir el mensaje de confirmación directamente en el comando
commit utilizando la opción -m:

```git
$ git commit -a -m 'added new benchmarks'
    [master 83e38c7] added new benchmarks
    1 file changed, 5 insertions(+), 0 deletions(-)
```

A pesar de que puede resultar muy útil para ajustar los commits tal como quieres, el
área de preparación es a veces un paso más complejo de lo que necesitas para tu flujo
de trabajo. Si quieres saltarte el área de preparación, Git te ofrece un atajo sencillo.
Añadiendo la opción -a al comando git commit harás que Git prepare
automáticamente todos los archivos rastreados antes de confirmarlos, ahorrándote el paso
de git add.

## Eliminar Archivos

Para eliminar archivos de Git, debes eliminarlos de tus archivos rastreados (o mejor
dicho, eliminarlos del área de preparación) y luego confirmar. Para ello existe el
comando git rm, que además elimina el archivo de tu directorio de trabajo de manera
que no aparezca la próxima vez como un archivo no rastreado.

```git
$ rm PROJECTS.md
$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    deleted: PROJECTS.md
    no changes added to commit (use "git add" and/or "git commit -a")
```

Otra cosa que puedas querer hacer es mantener el archivo en tu directorio de trabajo
pero eliminarlo del área de preparación. En otras palabras, quisieras mantener el
archivo en tu disco duro pero sin que Git lo siga rastreando. Esto puede ser
particularmente útil si olvidaste añadir algo en tu archivo .gitignore y lo preparaste
accidentalmente, algo como un gran archivo de trazas a un montón de archivos
compilados .a. Para hacerlo, utiliza la opción --cached:

```git
$ git rm --cached README
```

## Cambiar el Nombre de los Archivos

Al contrario que muchos sistemas VCS, Git no rastrea explícitamente los cambios de
nombre en archivos. Si renombras un archivo en Git, no se guardará ningún metadato
que indique que renombraste el archivo.

Por esto, resulta confuso que Git tenga un comando mv. Si quieres renombrar un
archivo en Git, puedes ejecutar algo como

```git
$ git mv file_from file_to
```

## Ver el Historial de Confirmaciones
Después de haber hecho varias confirmaciones, o si has clonado un repositorio que ya
tenía un histórico de confirmaciones, probablemente quieras mirar atrás para ver qué
modificaciones se han llevado a cabo. La herramienta más básica y potente para hacer
esto es el comando git log.

```git
$ git clone https://github.com/schacon/simplegit-progit
```

```git
$ git log
```

El comando git log proporciona gran cantidad de opciones para mostrarte exactamente
lo que buscas. Aquí veremos algunas de las más usadas.
Una de las opciones más útiles es -p, que muestra las diferencias introducidas en cada
confirmación. También puedes usar la opción -2, que hace que se muestren únicamente
las dos últimas entradas del historial

Esta opción muestra la misma información, pero añadiendo tras cada entrada las
diferencias que le corresponden. Esto resulta muy útil para revisiones de código, o para
visualizar rápidamente lo que ha pasado en las confirmaciones enviadas por un
colaborador. También puedes usar con git log una serie de opciones de resumen. Por
ejemplo, si quieres ver algunas estadísticas de cada confirmación, puedes usar la opción --stat

```git
$ git log --stat
```

opción realmente útil es --pretty, que modifica el formato de la salida. Tienes
unos cuantos estilos disponibles. La opción oneline imprime cada confirmación en una
única línea, lo que puede resultar útil si estás analizando gran cantidad de
confirmaciones. Otras opciones son short, full y fuller, que muestran la salida en un
formato parecido, pero añadiendo menos o más información, respectivamente.

```git
$ git log --pretty=oneline
```

La opción más interesante es format, que te permite especificar tu propio formato. Esto resulta especialmente útil si estás generando una salida para que sea analizada por otro programa —como especificas el formato explícitamente, sabes que no cambiará en futuras actualizaciones de Git—.

```git
$ git log --pretty=format:"%h - %an, %ar : %s"
```

| Opción | Descripción de la salida |
|--------|--------------------------|
|%H |Hash de la confirmación
|%h |Hash de la confirmación abreviado
|%T |Hash del árbol
|%t |Hash del árbol abreviado
|%P |Hashes de las confirmaciones padre
|%p |Hashes de las confirmaciones padre abreviados
|%an |Nombre del autor
|%ae |Dirección de correo del autor
|%ad |Fecha de autoría (el formato respeta la opción -–date)
|%ar |Fecha de autoría, relativa
|%cn |Nombre del confirmador
|%ce |Dirección de correo del confirmador
|%cd |Fecha de confirmación
|%cr |Fecha de confirmación, relativa
|%s  |Asunto

Puede que te estés preguntando la diferencia entre autor (author) y confirmador
(committer). El autor es la persona que escribió originalmente el trabajo, mientras que el
confirmador es quien lo aplicó. Por tanto, si mandas un parche a un proyecto, y uno
de sus miembros lo aplica, ambos recibiréis reconocimiento —tú como autor, y el
miembro del proyecto como confirmador—.

Las opciones oneline y format son especialmente útiles combinadas con otra opción
llamada --graph. Ésta añade un pequeño gráfico ASCII mostrando tu historial de
ramificaciones y uniones:


```git
$ git log --pretty=format:"%h %s" --graph
```

| Opción | Descripción |
|--------|-------------|
| -p | Muestra el parche introducido en cada confirmación.
| --stat | Muestra estadísticas sobre los archivos modificados en cada confirmación.
| --shortstat | Muestra solamente la línea de resumen de la opción --stat.
| --name-only | Muestra la lista de archivos afectados.
| --name-status | Muestra la lista de archivos afectados, indicando además si fueron añadidos, modificados o eliminados.
| --abbrev-commit | Muestra solamente los primeros caracteres de la suma SHA-1, en vez de los 40 caracteres de que se compone.
| --relative-date | Muestra la fecha en formato relativo (por ejemplo, “2 weeks ago” (“hace 2 semanas”)) en lugar del formato completo.
| --graph | Muestra un gráfico ASCII con la historia de ramificaciones y uniones.
| --pretty | Muestra las confirmaciones usando un formato alternativo.Posibles opciones son oneline, short, full, fuller y format (mediante el cualpuedes especificar tu propio formato).

## Deshacer Cosas

En cualquier momento puede que quieras deshacer algo. Aquí repasaremos algunas
herramientas básicas usadas para deshacer cambios que hayas hecho. Ten cuidado, a
veces no es posible recuperar algo luego que lo has deshecho. Esta es una de las pocas áreas en las que Git puede perder parte de tu trabajo si cometes un error.

```git
$ git commit --amend
```

Este comando utiliza tu área de preparación para la confirmación. Si no has hecho
cambios desde tu última confirmación (por ejemplo, ejecutas este comando justo después
de tu confirmación anterior), entonces la instantánea lucirá exactamente igual y lo único que cambiarás será el mensaje de confirmación.

```git
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

## Deshacer un Archivo Preparado

Las siguientes dos secciones demuestran cómo lidiar con los cambios de tu área de
preparación y tú directorio de trabajo. Afortunadamente, el comando que usas para
determinar el estado de esas dos áreas también te recuerda cómo deshacer los cambios en ellas. Por ejemplo, supongamos que has cambiado dos archivos y que quieres
confirmarlos como dos cambios separados, pero accidentalmente has escrito git add * y
has preparado ambos.


```git
$ git add .
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    renamed: README.md -> README
    modified: CONTRIBUTING.md
```

Justo debajo del texto “Changes to be committed” (“Cambios a ser confirmados”, en
inglés), verás que dice que uses git reset HEAD <file>... para deshacer la preparación.
Por lo tanto, usemos el consejo para deshacer la preparación del archivo CONTRIBUTING.md:

```git
$ git reset HEAD CONTRIBUTING.md
```

## Deshacer un Archivo Modificado

¿Qué tal si te das cuenta que no quieres mantener los cambios del archivo
CONTRIBUTING.md? ¿Cómo puedes restaurarlo fácilmente - volver al estado en el que estaba en la última confirmación (o cuando estaba recién clonado, o como sea que haya
llegado a tu directorio de trabajo)? Afortunadamente, git status también te dice cómo hacerlo. En la salida anterior, el área no preparada lucía así:

```git
Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: CONTRIBUTING.md
```

```git
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    renamed: README.md -> READMEmd
```

## Trabajar con Remotos

Para poder colaborar en cualquier proyecto Git, necesitas saber cómo gestionar
repositorios remotos. Los repositorios remotos son versiones de tu proyecto que están
hospedadas en Internet o en cualquier otra red. Puedes tener varios de ellos, y en cada
uno tendrás generalmente permisos de solo lectura o de lectura y escritura. Colaborar
con otras personas implica gestionar estos repositorios remotos enviando y trayendo
datos de ellos cada vez que necesites compartir tu trabajo.

```git
$ git remote -v
origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
```

## Añadir Repositorios Remotos

En secciones anteriores hemos mencionado y dado alguna demostración de cómo añadir
repositorios remotos. Ahora veremos explícitamente cómo hacerlo. Para añadir un remoto nuevo y asociarlo a un nombre que puedas referenciar fácilmente, ejecuta git remote add [nombre] [url]:

```git
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
pb https://github.com/paulboone/ticgit (fetch)
pb https://github.com/paulboone/ticgit (push)
```

A partir de ahora puedes usar el nombre pb en la línea de comandos en lugar de la
URL entera. Por ejemplo, si quieres traer toda la información que tiene Paul pero tú
aún no tienes en tu repositorio, puedes ejecutar git fetch pb

```git
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
* [new branch] master -> pb/master
* [new branch] ticgit -> pb/ticgit
```

## Traer y Combinar Remotos
El comando irá al proyecto remoto y se traerá todos los datos que aun no tienes de
dicho remoto. Luego de hacer esto, tendrás referencias a todas las ramas del remoto, las cuales puedes combinar e inspeccionar cuando quieras. Si clonas un repositorio, el comando de clonar automáticamente añade ese repositorio remoto con el nombre “origin”. Por lo tanto, git fetch origin se trae todo el trabajo nuevo que ha sido enviado a ese servidor desde que lo clonaste (o desde la última vez que trajiste datos). Es importante destacar que el comando git fetch solo trae datos a
tu repositorio local - ni lo combina automáticamente con tu trabajo ni modifica el trabajo que llevas hecho. La combinación con tu trabajo debes hacerla manualmente
cuando estés listo.

```git
$ git fetch [remote-name]
```

## Enviar a Tus Remotos

Cuando tienes un proyecto que quieres compartir, debes enviarlo a un servidor. El
comando para hacerlo es simple: git push [nombre-remoto] [nombre-rama]. Si quieres enviar tu rama master a tu servidor origin (recuerda, clonar un repositorio establece esos nombres automáticamente), entonces puedes ejecutar el siguiente comando y se enviarán todos los commits que hayas hecho al servidor:

```git
$ git push origin master
```

## Inspeccionar un Remoto
Si quieres ver más información acerca de un remoto en particular, puedes ejecutar el
comando git remote show [nombre-remoto]. Si ejecutas el comando con un nombre en
particular, como origin, verás algo como lo siguiente:

```git
$ git remote show origin
* remote origin
    Fetch URL: https://github.com/schacon/ticgit
    Push URL: https://github.com/schacon/ticgit
    HEAD branch: master
    Remote branches:
    master tracked
    dev-branch tracked
    Local branch configured for 'git pull':
    master merges with remote master
    Local ref configured for 'git push':
    master pushes to master (up to date)
```

## Eliminar y Renombrar Remotos
Si quieres cambiar el nombre de la referencia de un remoto puedes ejecutar git remote rename. Por ejemplo, si quieres cambiar el nombre de pb a paul, puedes hacerlo con git
remote rename:

```git
$ git remote rename pb paul
$ git remote
origin
paul
```

## Etiquetado
Como muchos VCS, Git tiene la posibilidad de etiquetar puntos específicos del
historial como importantes. Esta funcionalidad se usa típicamente para marcar versiones de lanzamiento (v1.0, por ejemplo).

## Listar Tus Etiquetas
```git
$ git tag
```
## Crear Etiquetas

```git
$ git tag -a v1.4 -m 'my version 1.4'
```