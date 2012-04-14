---
layout: post
title: Tutorial de Git en Español
category: programacion
tags: git tutorial español vcs mercurial hg
---

> Este tutorial es una traducción con algunos agregados de [Git Tutorial](http://www.vogella.de/articles/Git/article.html), de [Lars Vogel](http://www.vogella.de/).

<br />

> Para la traducción se han mejorado algunas cosas para adaptarlas al habla hispana. De todas maneras, el vocabulario usado puede resultarte raro. No estoy de acuerdo con traducir todas las palabras desde el inglés al español, porque muchas veces esto es imposible. Me he encontrado en libros de bases de Datos que me hablan de "comprometer" una transacción, cuando podrían directamente haber usado la palabra "commit". Por eso, tales palabras quedan en inglés, como corresponde. También puede resultarte raro que transforme esas palabras en verbos y las conjuge, como por ejemplo, la acción de hacer un "commit" la llamo "comitear". Si nunca lo escuchaste, no te preocupes, porque esta es la jerga que se utiliza en la industria.

*  1\. [Git](#Git)
    *    1.1\. [¿Qué es Git?](#que-es-git)
    *    1.2\. [Terminología importante](#terminologia-importante)
    *    1.3\. [Staging index](#staging-index)
*   2\. [Instalación](#Instalacion)
*   3\. [Configuración](#Configuracion)
    *   3.1\. [Configuración del usuario](#configuracion-del-usuario)
    *   3.2\. [Resaltado de colores](#resaltado-de-colores)
    *   3.3\. [Ignorar ciertos archivos](#ignorar-archivos)
*   4\. [Empezando con Git](#empezando-con-git)
    *   4.1\. [Creando contenido](#creando-contenido)
    *   4.2\. [Crear el repositorio y hacer un commit](#creando-el-repositorio)
    *   4.3\. [Ver las diferencias via diff y commitear los cambios](#ver-diferencias-via-diff)
    *   4.4\. [Status, Diff y el log de Commit](#status-diff-log)
    *   4.5\. [Corrección de mensajes de commit - git amend](#correccion-mensajes-commit-git-amend)
    *   4.6\. [Eliminar archivos](#eliminar-archivos)
    
*   5\. [Trabajando con repositorios externos](#repositorios-externos)
    *   5.1\. [Creando un repositorio Git externo](#crear-repositorio-externo)
    *   5.2\. [Subir los cambios a otro repositorio - Push](#subir-cambios-push)
    *   5.3\. [Add remote](#add-remote)
    *   5.4\. [Mostrar los repositorios externos existentes](#mostrar-repositorios-externos)
    *   5.5\. [Clonar tu repositorio](#clonar-repositorio)
    *   5.6\. [Trayendo los cambios - Pull](#trayendo-cambios-pull)
*   6\. [Revertir cambios](#revertir-cambios)
*   7\. [Etiquetando en Git - Tagging](#etiquetando-git)
*   8\. [Branches y Merging](#branch-merge)
    *   8.1\. [Branches](#branches)
    *   8.2\. [Merging](#merging)
    *   8.3\. [Borrar un branch](#borrar-branch)
*   9\. [Resolviendo conflictos después de un merge](#resolviendo-conflictos-merge)
*   10\. [Rebase](#rebase)
    *   10.1\. [Utilizando rebase para varios commits en un mismo branch](#utilizando-rebase-varios-commits-branch)
    *   10.2\. [rebase entre branches](#rebase-entre-branches)
    *   10.3\. [Buenas prácticas para el uso de rebase](#buenas-practicas-rebase)
*   11\. [Creando y aplicando parches](#creando-aplicando-parches)
*   12\. [Definiendo un alias](#definiendo-alias)
*   13\. [Ignorando un archivo / directorio](#ignorando-archivo-directorio)
*   14\. [Otros comándos útiles](#otros-comandos-utiles)
*   15\. [Instalando un servidor Git](#instalando-servidor-git)
*   16\. [Repositorios remotos online](#repositorios-remotos-online)
    *   16.1\. [Clonando repositorios remotos](#clonando-repositorios-remotos)
    *   16.2\. [Agregando más repositorios remotos](#agregando-mas-repositorios-remotos)
    *   16.3\. [Operaciones remotas via HTTP y un proxy](#operacion-remota-http-proxy)
*   17\. [Proveedores de hosting Git](#proveedores-hosting-git)
    *   17.1\. [GitHub](#github)
    *   17.2\. [Bitbucket](#bitbucket)
*   18\. [Herramientas gráficas para Git](#herramientas-graficas-git)
*   19\. [Obtené la versión original para Kindle](#version-original-kindle)
*   20\. [Preguntas y comentarios](#preguntas-comentarios)
*   21\. [Links  y recursos útiles](#links-recursos-utiles)

<h2 id="Git">1. Git</h2>
<h3 id="que-es-git">1.1. ¿qué es Git?</h3>

Git es un sistema de control de versiones distribuído (scvd) escrito en C. Un sistema de control de versiones permite la creación de una historia para una colección de archivos e incluye la funcionalidad para revertir la colección de archivos a otro estado. Otro estado puede significar a otra colección diferente de archivos o contenido diferente de los archivos.

Podés, por ejemplo, cambiar la colección de archivos a un estado de 2 días atras, o podés cambiar entre los estados para caracteristicas experimentales y problemas de producción.

Esta colección de archivos generalmente es llamada "código fuente". En un sistema de control de versiones distribuído todos tienen una copia completa del código fuente (incluyendo la historia completa del código fuente) y puede realizar operaciones referidas al control de versiones mediante esa copia local. El uso de un scvd no requiere un repositorio central.

Si haces cambios al código fuente, haces esos cambios relevantes para el control de versiones (los agregas al staging index) y después los agregas al repositorio (commit).

Git mantiene todas las versiones. Por lo tanto podés revertir a cualquier punto en la historia de tu código fuente usando Git.

Git realiza los commits a tu repositorio local y es posible sincronizar ese repositorio con otros (tal vez remotos) repositorios. Git te permite clonar los repositoriso, por ejemplo, crear una copia exacta de un repositorio incluyendo la historia completa del código fuente. Los dueños de los repositorios pueden sincronizar los cambios via `push` (transfiere los cambios al repositorio remoto) o `pull` (obtiene los cambios desde un repositorio remoto).

Git soporta el concepto de `branching`, es decir, podés tener varias versiones diferentes de tu código fuente. Si querés desarrollar una nueva característica, podés abrir un `branch` en tu código fuente y hacer los cambios en este `branch` sin afectar el principal desarrollo de tu código.

Git puede ser usado desde la linea de comandos; esta manera será la descripta en este tutorial. También existen herramientas gráficas, por ejemplo Egit para el IDE Eclipse, pero estas herramientas no van a ser descriptas en este tutorial.

<h3 id="terminologia-importante">1.2. Terminología importante</h3>

<br />
<table>
    <tr>
        <th>Término</th>
        <th>Definición</th>
    </tr>
    <tr>
        <td>Repositorio</td>
        <td>Un repositorio contiene la historia, las diferentes versiones en el tiempo y todas los distintos branch y etiquetas. En Git, cada copia del repositorio es un repositorio completo. El repositoro te permite obtener revisiones en tu copia actual.</td>
    </tr>
    <tr>
        <td>Branch</td>
        <td>Un branch es una linea separada de código con su propia historia. Te es posible crear un nuevo branch de a partir de uno existente y cambiar el código independientemente de otros branches. Uno de los branches es el original (generalmente llamado master). El usuario selecciona un branch y trabaja en ese branch seleccionado, el cual es llamado copia actual (working copy). Seleccionar un branch es llamado "obtener un branch" (checkout a branch)</td>
    </tr>
    <tr>
        <td>Etiquetas (Tags)</td>
        <td>Un tag (una etiqueta) apunta a un cierto punto en el tiempo en un branch específico. Con un tag, es posible tener un punto con un tiempo al cual siempre sea posible revertir el código, por ejemplo, ponerle el tag "testing" al código 25.01.2009</td>
    </tr>
    <tr>
        <td>Commit</td>
        <td>Vos hacés un commit de los cambios a un repositorio. Esto crea una revisión nueva la cual puede ser obtenida después, por ejemplo si querés ver el código fuente de una versión anterior. Cada commit contiene el autor y el que realizó el commit (comiteador), siendo así posible identificar el origen del cambio. El autor y el comiteador pueden ser diferentes personas.</td>
    </tr>
    <tr>
        <td>URL</td>
        <td>Una URL en Git determina la ubicación de un repositorio.</td>
    </tr>
    <tr>
        <td>Revisión</td>
        <td>Representa una versión del código fuente. Git identifica revisiones con un id SHA1. Los id son de 160 bits de largo y son representados en hexadecimal. La última versión puede ser direccionada a través de "HEAD", la versión anterior mediante "HEAD-1" y así siguiendo.</td>
    </tr>
</table>
<br />

<h3 id="staging-index">1.3. Staging index (el índice)</h3>

Git requiere que los cambios sean marcados explicitamente para el próximo commit. Por ejemplo, si haces un cambio en un archivo y querés que y querés que ese cambio sea relevante para el próximo commit, es necesario que agregues el archivo a lo que se llama comunmnete "staging index" mediante el comando `git add`. Dicho índice será una imagen completa de los cambios.

Los nuevos archivos siempre deben ser explicitamente añadidos al índice. Para archivos que ya han sido comiteados podés usar la opción -a durante el commit.

<h2 id="Instalacion">2. Instalación</h2>

En Ubuntu podés instalar la herramienta de consola de Git con el siguiente comando:

{% highlight bash %}
sudo apt-get install git-core
{% endhighlight %}

Para otras distribuciones de Linux deberías consultar la documentación correspondiente a la distro.

Una versión de Git para Windows podés encontrarla en el sitio del proyecto msysgit. La URL es: http://code.google.com/p/msysgit/ .

<h2 id="Configuracion">3. Configuración</h2>

Git te permite almacenar configuraciones globales en el archivo .gitconfig. Ese archivo debe ser ubicado en tu directorio de usuario (el home). Como mencioné anteriormente Git almacena el comiter y el autor para cada commit. Esta y otra información adicional puede ser almacenada en la configuración global.

A continuación veremos cómo configurar Git para utilizar un usuario y dirección de correo electrónico en particular, habilitar los colores y cómo decirle a Git que ignore ciertos archivos.

<h3 id="configuracion-del-usuario">3.1. Configuración del usuario</h3>

Configurá tu usuario e email para Git mediante los siguientes comandos:

{% highlight bash %}
    # Configura el usuario que será usado por git
    # Obviamente deberías usar tu nombre
    git config --global user.name "Santiago Basulto"
    # Lo mismo para el correo electrónico
    git config --global user.email "santiago.basulto-nospam@example.com"
    # Configurar para que todos los cambios generen un push por defecto
    git config --global push.default "matching"
{% endhighlight %}

<h3 id="resaltado-de-colores">3.2. Resaltado de colores</h3>

Esto activará el resaltado de colores en la consola:

{% highlight bash %}
    git config --global color.status auto
    git config --global color.branch auto
{% endhighlight %}

<h3 id="ignorar-archivos">3.3. Ignorar ciertos archivos</h3>

Git puede ser configurado para que ignore ciertos archivos y directorios. Esta configuración es realizada mediante el archivo `.gitignore`. Este archivo puede estar en cualquier directorio y puede contener patrones para archivos. Por ejemplo, es posible decirle a git que ignore el directorio `bin` y todos los archivos que finalicen con la extensión `pyc` (archivos de python compilados) mediante el siguiente patrón en el archivo .gitignore en el directorio principal.

<pre>
    bin
    *.pyc
</pre>

Git también ofrece la configuración global core.excludefile para especificar de manera global qué patrones ignorar.

<h2 id="empezando-con-git">4. Empezando con Git</h2>

A continuación trataré de guiarte a través de una utilización típica de Git. Vas a crear algunos archivos, crear un repositorio Git local y commitear los archivos en este repositorio. Después clonaremos el repositorio y haremos push y pull entre los repositorios. Los comentarios (marcados con #) antes de cada comando explican las acciones específicas.

Abrí una consola para comenzar.

<h3 id="creando-contenido">4.1. Creando contenido</h3>

Los comandos a continuación crean algunos archivos con algo de contenido y después son puestos bajo el control de versiones.

{% highlight bash %}
    # Navegá hasta el home
    cd ~/
    # Crea un directorio
    mkdir ~/repo01
    # Ingresá a ese directorio
    cd repo01
    # Crea un nuevo directorio
    mkdir datafiles
    # Crea algunos archivos
    touch test01
    touch test02
    touch test03
    touch datafiles/data.txt
    # Poné algo de texto adentro en el primer archivo
    ls > test01
{% endhighlight %}

<h3 id="creando-el-repositorio">4.2. Crear el repositorio y hacer un commit</h3>

Cada repositorio Git es almacenado en la carpeta `.git` del directorio en el cual el repositorio ha sido creado. Este directorio contiene la historia completa del repositorio. El archivo `.git/config` contiene la configuración local del repositorio.

A continuación crearemos un repositorio Git, agregamos los archivos al índice del repositorio y commiteamos los cambios.

{% highlight bash %}
    # Inicializamos el repositorio local Git
    git init
    # Agregamos todo (archivos y directorios) al repositorio
    git add .
    # Hacemos un commit al repositorio
    git commit -m "Initial commit"
    # Muestra el log (un historial)
    git log
{% endhighlight %}

<h3 id="ver-diferencias-via-diff">4.3. Ver las diferencias via diff y commitear los cambios</h3>

El comando `diff` de Git permite al usuario ver los cambios hechos. Para probar esto, hacé algunos cambios a un archivo y fijate qué te muestra `diff`

Después comitea los cambios al repositorio.

{% highlight bash %}
    # Hacé algunos cambios al archivo
    echo "Este es un cambio" > test01
    echo "y este es otro cambio" > test02

    # Check the changes via the diff command
    # Mirá los cambios con el comando diff
    git diff

    # Comitea los cambios, -a comitea los cambios de los archivos modificados
    # pero no agrega automaticamente nuevos archivos
    git commit -a -m "Hay nuevos cambios"
{% endhighlight %}

<h3 id="status-diff-log">4.3. Status, Diff y el log de Commit</h3>

A continuación utilizaremos comandos que te ayudarán a ver el estado actual de tu repositorio y un log de todos los commits.

{% highlight bash %}
    # Hacé algunos cambios al archivo
    echo "Nuevo cambio" > test01
    echo "y otro nuevo cambio" > test02

    # Mirá el estado actual de tu repositorio
    # (qué archivos han cambiado, son nuevos o eliminados)
    git status

    # Muestra las diferencias entre los archivos no comiteados
    # y el último commit en el branch actual
    git diff

    # Agrega los cambios al índice y comitea
    git add . && git commit -m "Más cambioos - con un error en el mensaje de commit"

    # Muestra el histórico de commits en el branch actual
    git log

    # Muestra una linda vista gráfica de los cambios
    gitk --all
{% endhighlight %}

<h3 id="correccion-mensajes-commit-git-amend">4.5. Corrección de mensajes de commit - git amend</h3>

El comando `amend` hace posible cambiar el último mensaje de commit.

En el ejemplo anterior el mensaje de commit era incorrecto y tenía un error. A continuación lo corregimos mediante el parámetro `--amend`.

{% highlight bash %}
    git commit --amend -m "Más cambios, ahora correctos"
{% endhighlight %}

<h3 id="eliminar-archivos">4.6. Eliminar archivos</h3>

Si eliminas un archivo que está bajo el control de versiones, el comando `git add .` no tendrá en cuenta que has eliminado el archivo. Es neceasrio que uses el comando `git commit` con la bandera `-a` o el comando `git add` con la bandera `-A`.

{% highlight bash %}
    # Crea un archivo y agregalo al control de versiones
    touch nonsense.txt
    git add . && git commit -m "un nuevo archivo ha sido creado"
    # Elimina el archivo
    rm nonsense.txt
    # Proba hacer un commit de la forma normal -> no va a andar
    git add . && git commit -m "elimine el archivo, pero no anda"
    # Ahora hace un commit con la bandera -a
    git commit -a -m "El archivo nonsense.txt ahora si fue eliminado del índice"
    # Alternativamente podrías agregar los archivos borrados al índice mediante
    git add -A . 
    git commit -m "El archivo nonsense.txt ahora si fue eliminado del índice"
{% endhighlight %}

<h2 id="repositorios-externos">5. Trabajando con repositorios externos</h2>

<h3 id="crear-repositorio-externo">5.1. Creando un repositorio Git externo</h3>

Ahora crearemos un repositorio Git remoto. Git te permite almacenar este repositorio remoto tanto en la red como localmente.

Un repositorio Git estandar es diferente de un repositorio remoto. Un repo estandar contiene el código fuente y el repositorio Git. Podés trabajor directamente en este directorio ya que este contiene una copia de todos los archivos.

Los repositorios remotos no contienen las copias de todos los archivos. Estos solo tienen los archivos del repositorio, la información perteneciente a Git. Para crear tal repositorio utilizá la bandera --bare.

Para simplificar los siguientes ejemplos, el repo será creado localmente en el filesystem.

{% highlight bash %}
    # Dirigite al repo
    cd ~/repo01
    # hace un clone con la bandera --bare
    git clone --bare . ../remote-repository.git

    # Comprobá que el contenido es idéntico al directorio .git en repo01
    ls ~/remote-repository.git
{% endhighlight %}

<h3 id="subir-cambios-push">5.2. Subir los cambios a otro repositorio - Push</h3>
Hacé algunos cambios y subilos desde tu primer repositorio al repositorio remoto mediante estos comandos

{% highlight bash %}
    # Navegá hasta el primer repo
    cd ~/repo01

    # Hacé algunos cambios en los archivos
    echo "Hola hola, prendé tu radio" > test01
    echo "Chau chau, apagá la radio" > test02

    # Comitea los cambios, -a comiteara los cambios para archivos modificados
    # pero no agrega automaticamente nuevos archivos
    git commit -a -m "Algunos cambios"

    # Subí los cambios
    git push ../remote-repository.git
{% endhighlight %}

<h3 id="add-remote">5.3. Add remote</h3>

Siempre es posible subir cambios a un repositorio Git mediante su URL completa. Pero también es posible agregar un "apodo" a un repositorio mediante el comando `git remote add`. `origin` es un nombre especial que es normalmente usado de forma automática, si clonas un repositorio Git. `origin` indica el repositorio original desde el cual has empezado. Ya que nosotros comenzamos desde el principio, este nombre está aun disponible.

{% highlight bash %}
    # agregá ../remote-repository.git con el nombre origin
    git remote add origin ../remote-repository.git 

    # Otros cambios
    echo "Agregué un repo remoto" > test02
    # Commit
    git commit -a -m "Test para el nuevo repo remoto origin"
    # sube automaticamente a origin
    git push origin
{% endhighlight %}

<h3 id="mostrar-repositorios-externos">5.4. Mostrar los repositorios externos existentes</h3>

Para ver las definiciones existentes de los repositorios remotos, utilizá el siguiente comando:

{% highlight bash %}
    # Muestra los repositorios externos existentes
    git remote
{% endhighlight %}

<h3 id="clonar-repositorio">5.5. Clonar tu repositorio</h3>

Crea un nuevo repositorio en un nuevo directorio con los siguientes comandos:

{% highlight bash %}
    # Navegá al home
    cd ~
    # Crea un nuevo directorio
    mkdir repo02

    # Navegá al nuevo directorio
    cd ~/repo02
    # clonalo
    git clone ../remote-repository.git .
{% endhighlight %}

<h3 id="trayendo-cambios-pull">5.6. Trayendo los cambios - Pull</h3>

Pull te permite obtener los últimos cambios de otro repositorio. En tu segundo repositorio, hacé unos cambios, subilos (push) a tu repositorio remoto y después traelos (con un pull) desde el primer repo.

{% highlight bash %}
# Navegá hacia el home
cd ~

# Navegá al segundo repo
cd ~/repo02
# Hacé algunos cambios
echo "Un cambio" > test01
# Commit
git commit -a -m "Un cambio"

# Subí los cambios al repo remoto
# Origin es automaticamente mantenido ya que clonamos desde este repositorio
git push origin

# Navegá al primer repositorio y traete los cambios
cd ~/repo01
git pull ../remote-repository.git/
# reivsá los cambios
less test01
{% endhighlight %}

<h2 id="revertir-cambios">6. Revertir cambios</h2>

Si creas archivos en tu copia actual que no quisieses comitear, es posible desecharlos.

{% highlight bash %}
    # Crea un nuevo archivo con algo de contenido
    touch test04
    echo "esto no sirve" > test04

    # Hacé un dry-run para ver que ocurriría desde el último cambio
    # -n es lo mismo que --dry-run
    git clean -n

    # Ahora lo borra
    git clean -f
{% endhighlight %}
You can check out older revisions of your source code via the commit ID. The commit ID is shown if you enter the git log command. It is displayed behind the commit word.

Es posible obtener (mediante un check out) revisiones anteriores de tu código mediante el ID de commit. El ID de commit se muestra si ingresás el comando `git log`. Es mostrado después de la palabra commit.

{% highlight bash %}
    # Navegá al hoome
    cd ~/repo01
    # obtene un log
    git log

    # copiá uno commit viejo y obtené las revisiones anteriores
    git checkout nombre\_del\_commit
{% endhighlight %}

Si no agregaste los cambios al índice, también es posible revertir los cambios directamente.

{% highlight bash %}
    # algún cambio sin sentido
    echo "sin sentido" > test01
    # no ha sido agregado al índice, por lo tanto
    # simplemente podemos obtener la versión anterior
    git checkout test01
    # Comprobá el contenido
    cat test01
    # Otro cambio sin sentido
    echo "otro cambio sin sentido" > test01
    # Agregamos el archivo al índice
    git add test01
    # Recuperamos el archivo en el índice
    git reset HEAD test01
    # Obtenemos la versión vieja desde el índice
    git checkout test01
{% endhighlight %}
También es posible revertir los commits mediante el siguiente comando:

{% highlight bash %}
    # Revertir un commit
    git revert commit_name
{% endhighlight %}

Si borraste un archivo pero no has hecho el cambio en el índice, o comiteado el cambio, es posible volver a obtener ese archvio.

{% highlight bash %}
    # borramos el archivo
    rm test01
    # revertimos la eliminación
    git checkout test01
{% endhighlight %}
		
Si agregaste el archivo al índice pero no querés comitearlo, es posible elminarlo del índice mediante el comando `git reset`.

{% highlight bash %}
    # creamos un archivo
    touch incorrecto.txt
    # lo agregamos al índice accidentalmente
    git add .
    # lo borramos del índice
    git reset incorrecto.txt
    # borramos el archivo
    rm incorrect.txt
{% endhighlight %}

Si borraste un directorio y no has comiteado los cambios es posible recuperarlo mediante el siguiente comando:

{% highlight bash %}
    git checkout HEAD -- directorio\_a\_recuperar
{% endhighlight %}

<h2 id="etiquetando-git">7. Etiquetando en Git - Tagging</h2>

Git tiene la opción de etiquetar (taguear) ciertas versiones para encontrarlas de forma más fácil en el futuro. Lo más común es utilizarlo para etiquetar una cierta versión que ha sido largada en producción.

Es posible listar los tags disponibles mediante este comando:

{% highlight bash %}
    git tag
{% endhighlight %}

Podés crear un nuevo tag de la siguiente manera. Con el parámetro -m especificás la descripción del tag.

{% highlight bash %}
    git tag version1.6 -m 'version 1.6'
{% endhighlight %}

Si querés acceder al código asociado con ese tag:

{% highlight bash %}
    git checkout tag\_name
{% endhighlight %}

<h2 id="branch-merge">8. Branches y Merging</h2>

<h3 id="branches">8.1. Branches y Merging</h3>

Git te permite crear branches. Branches, el plural de branch, son copias independientes del código fuente que pueden ser cambiadas independientemente de las otras. El branch por defecto es llamado _master_. Git te permite crear branches de forma muy rápida y barato en cuanto a recursos. Es recomendable utilizar branches frecuentemente.

El siguiente comando lista todos los branches disponibles localmente. El branch actualmente activo es marcado con un asterisco _\*_

{% highlight bash %}
    git branch
{% endhighlight %}

Si querés ver todos los branches (incluyendo aquellos remotos), utilizá el siguiente comando.

{% highlight bash %}
git branch -a
{% endhighlight %}

Es posible crear un nuevo branch de la siguiente manera.

{% highlight bash %}
    # Sintaxis: git branch <nombre> <hash>
    # <hash> es opcional
    # si no es especificado se utiliza el del último commit
    # si es especificado se utiliza el del commit correspondiente
    git branch testing
    # cambiá al nuevo branch
    git checkout testing
    # algunos cambios
    echo "Algo nuevo en este branch" > test01
    git commit -a -m "algo nuevo"
    # Volvé al branch master
    git checkout master
    # comprobá que el contenido de test01 es el anterior
    cat test01
{% endhighlight %}

<h3 id="merging">8.2. Merging</h3>

Merge te permite combinar los cambios de dos branches. Merge realiza el comunmente llamado _merge de tres versiones_ entre la última imagen de dos branches, basado en el más reciente ancestro en común de ambos.

Como resultado se obtiene una nueva imagen. Es posible hacer un merge entre los cambios de un branch y el actualmente activo mediante el siguiente comando.

{% highlight bash %}
    # sintaxis: git merge <nombre-del-branch>
    git merge testing
{% endhighlight %}

Si un conflicto ocurre, Git marcará el conflicto en el archivo y el programador tiene que resolver el conflicto manualmente. Después de resolverlo, puede agregar el archivo al índice y comitear el cambio.

<h3 id="borrar-branch">8.3. Borrar un branch</h3>

Para eliminar un branch que ya no es necesario, podés utilizar el siguiente comando.

{% highlight bash %}
    # borra el branch 'testing'
    git branch -d testing
    # comprobá que el branch fue borrado
    git branch
{% endhighlight %}

<h2 id="resolviendo-conflictos-merge">9. Resolviendo conflictos después de un merge</h2>

Un conflicto ocurre si dos personas han modificado el mismo contenido y Git no puede determinar automaticamente como deberían ser aplicados ambos cambios.

Git requiere que los conflictos sean resueltos manualmente. En esta sección; primero crearemos un conflicto y después lo resolveremos y aplicaremos el cambio al repositorio.

De la siguiente manera creamos un conflicto.

{% highlight bash %}
    # navegá al primer directorio
    cd ~/repo01
    # algunos cambios
    touch conflictivo.txt
    echo "Cambio en el primer repo" > conflictivo.txt
    # agregamos al índice y comiteamos
    git add . && git commit -a -m "Creamos el conflicto 1"

    # Navegamos al segundo directorio
    cd ~/repo02
    # más cambios
    touch conflictivo.txt
    echo "Cambio en el segundo repo" > conflictivo.txt
    # agregamos al índice y comiteamos
    git add . && git commit -a -m "Creamos el conflicto 2"
    # Hacemos un push al master
    git push

    # ahora tratá de hacer un push desde el primer directorio
    # navegá al primer directorio
    cd ~/repo01
    # Tratá de hacer un push -> ocurrirá un error
    git push
    # obtené los cambios
    git pull origin master
{% endhighlight %}

Git marca el conflicto en el archivo afectado (conflictivo.txt). El archivo debería tener el siguiente contenido.

    <<<<<<< HEAD
    Cambio en el primer repo
    =======
    Cambio en el segundo repo
    >>>>>>> b29196692f5ebfd10d8a9ca1911c8b08127c85f8
   
La parte superior (sobre la linea ====) contiene el contenido de tu repositorio, y la parte inferior es la que tiene el contenido del repositorio remoto. Ahora podés editar el archivo manualmente y después comitear los cambios. Alternativamente, podrías usar el comando `git mergetool`. `git mergetool` lanza una herramienta configurable que muestra los cambios en una pantalla dividida.

{% highlight bash %}
# podes editar el archivo manualmente o usar
git mergetool
# Te pedirá que selecciones qué herramienta para
# resolver el conflicto deseas utilizar 
# por ejemplo en ubuntu podés usar la herramienta "meld"
# después de resolver los conflictos manualmente, los comiteamos
git commit -m "conflictos resueltos"
{% endhighlight %}

<h2 id="rebase">10. Rebase</h2>

<h3 id="utilizando-rebase-varios-commits-branch">10.1 Utilizando rebase para varios commits en un mismo branch</h3>

El comando `rebase` te permite combinar varios commits en uno único. Esto es útil ya que permite al usuario reescribir un poco de la historia de los commits (haciendo algo de limpieza) antes de hacer un push de los cambios a un repositorio remoto.

A continuación crearemos varios commits que serán combinados más adelante.

{% highlight bash %}
    # Crea un nuevo archivo
    touch rebase.txt

    # agregamos al índice y comiteamos
    git add . && git commit -m "rebase.txt añadido al índice"

    # Algunos cambios tontos
    echo "contenido" >> rebase.txt
    git add . && git commit -m "agregué contenido"
    echo " más contenido" >> rebase.txt
    git add . && git commit -m "agregué más contenido"
    echo " más contenido" >> rebase.txt
    git add . && git commit -m "agregué más contenido"
    echo " más contenido" >> rebase.txt
    git add . && git commit -m "agregué más contenido"
    echo " más contenido" >> rebase.txt
    git add . && git commit -m "agregué más contenido"
    echo " más contenido" >> rebase.txt
    git add . && git commit -m "agregué más contenido"

    # mirá el log (largo, no?)
    git log
{% endhighlight %}

Ahora combinaremos los últimos siete commits. Podés hacer esto interactivamente mediante el siguiente comando.

{% highlight bash %}
git rebase -i HEAD~7
{% endhighlight %}

Esto abre tu editor preferido y te deja editar el mensaje de commit o compactar (mediante `squash` - `s`) / arreglar (mediante `fixup` - `f`) el commit con el último.

La opción de compactar (squash) combina los mensajes de commit mientras que arreglar (fixup) ignora los mensajes.

<h3 id="rebase-entre-branches">10.2 rebase entre branches</h3>

También podés usar Git para hacer un rebase entre dos branches. Como describimos anteriormente, el comando `merge` combina los cambios de dos branches. Rebase toma los cambios de un branch, crea un patch y lo aplica al otro branch.

El resultado final del código fuente es el mismo que con `merge` pero la historia de commit es más limpia. La historia parece ser lineal.

{% highlight bash %}
    # Crea un nuevo branch
    git branch testing
    # checkout del branch
    git checkout testing
    # Hacemos algunos cambios
    echo "Haremos un rebase con el master" > test01
    # hacemos un commit al branch testing
    git commit -a -m "Algo nuevo en el branch"
    # Hacemos un rebase con el master
    git rebase master
{% endhighlight %}

<h3 id="buenas-practicas-rebase">10.1 Buenas prácticas para el uso de rebase</h3>

Siempre deberías chequear tu historial local antes de hacer un push con tus nuevos cambios a otro repositorio Git.

Git te permite hacer commits locales. Esta característica es frecuentemente utilizada para tener puntos a los cuales volver si algo sale mal más adelante durante el desarrollo de nuevas funcionalidades. Si haces esto, antes de hacer un push deberías mirar tu historial local y validar si estos commits son relevantes para otros desarrolladores.

Si todos esos commits son parte de la implementación de una funcionalidad en particular, lo más probable es que quieras resumirlos en un único commit antes de hacer el push.

El rebase interactivo consiste basicamente en reescribir la historia. Es seguro hacer esto siempre y cuando los commits no han sido subidos (mediante un puhs) a otro repositorio. Esto significa que los commits solo deben ser reescritos mientras no se haya hecho un push.

Si reescribis algo y después haces un push de un commit que ya está presente en otros repositorios Git, en realidad parecerá como si hubieses implementado algo que alguien ya implementó en el pasado.

<h2 id="creando-aplicando-parches">11. Creando y aplicando parches</h2>

Un parche (patch) es un archivo de texto que contiene cambios para el código fuente. Este archivo puede ser enviado a alguna persona y esta persona puede usar dicho archivo para aplicar los cambios a su repositorio.

Los siguientes comandos crean un branch, hacen algunos cambios, crean un parche y aplican el parche al master.

{% highlight bash %}
    # creamos un nuevo branch
    git branch mybranch
    # usamos este branch
    git checkout mybranch
    # hacemos algunos cambios
    touch test05
    # cambiamos el contenido de un archvio
    echo "New content for test01" >test01
    # comiteamos esto al branch
    git add .
    git commit -a -m "primer commit en el branch"

    # creamos un parche -> sintaxis: git format-patch master
    git format-patch origin/master
    # se crea el archivo 0001-primer-commit-en-el-branch.patch

    # obtenemos el master
    git checkout master

    # aplicamos el parche
    git apply 0001-primer-commit-en-el-branch.patch
    # hacemos un commit normal en el master
    git add .
    git commit -a -m "parche aplicado"

    # borramos el archivo
    rm 0001-primer-commit-en-el-branch.patch
{% endhighlight %}

<h2 id="definiendo-alias">12. Definiendo un alias</h2>

Un alias en Git te permite crear tus propios comandos Git. Por ejemplo, podés definir un alias que sea una forma más corta para tu comando favorito o podés combinar varios comandos con un alias.

Por ejemplo, a continuación definimos el comando `git add-commit` que combina `git add . -A` y `git commit -m`. Después de definir este comando, podés usarlo de la siguiente manera: `git add-commit -m "mensaje"`

{% highlight bash %}
    git config --global alias.add-commit '!git add . -A && git commit'
{% endhighlight %}
		
Unfortunately, defining an alias is at the time of writing this not completely supported in msysGit. You can do single aliases, e.g. ca for ca = commit -a) but you can't do ones beginning with ! .

Desafortunadamente, la funcionalidad de los alias al momento de finalizar estas lineas no está completamente soportado en *msysGit*. Podés hacer alias simples (para un solo comando), por ejemplo utilizar el alias `ca` para `commit -a` pero no podes hacer los que comienzan con un *!*.

<h2 id="ignorando-archivo-directorio">13. Ignorando un archivo / directorio</h2>

Algunas veces deseamos que algunos archivos o directorios no sean incluídos en tu repositorio Git. Si los agregas al archivo *.gitignore*, Git comenzará a ignorarlose desde ese momento. Esto quiere decir que no los eliminará del repo. Por lo tanto, la última versión seguirá estando en el índice. Para que sean eliminados del índice podés usar:

{% highlight bash %}
    # eliminamos el directorio .metadata del repo
    git rm -r --cached .metadata
    # eliminamos el archivo test.txt del repo
    git rm --cached test.txt
{% endhighlight %}

Esto no quiere decir que sean eliminados del historial de commits. Si realmente deseas que sean borrados del historial, consultá el comando `git filter-branch` que te permite reescribir el historial de commits.

<h2 id="otros-comandos-utiles">14. Otros comándos útiles</h2>

La siguiente lista contiene algunos comandos de Git que son útiles para el trabajo diario.

<table>
    <tr>
        <th>Comando</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td><code>git blame "nombre-archivo"</code></td>
        <td>Muestra quién creó o modificó el archivo</td>
    </tr>
    <tr>
        <td><code>git checkout -b mi-branch master~1</code></td>
        <td>Crea un branch basándose en el master sin incluir el último commit</td>
    </tr>
</table>

<h2 id="instalando-servidor-git">15. Instalando un servidor Git</h2>

Como describí anteriormente no es necesario un servidor. Podés utilizar simplemente el filesystem o un proveedor público de Git, como Github o Bitbucket. De todas fromas, algunas veces es conveiente tener nuestro propio servidor. Instalarlo en Ubuntu es relativamente sencillo.

Primero comprobá que tenés instalado *ssh*.

{% highlight bash %}
    apt-get install ssh
{% endhighlight %}

Si no instalaste Git, es necesario que lo hagas:

{% highlight bash %}
    sudo apt-get install git-core
{% endhighlight %}

Crea un nuevo usuario para Git.

{% highlight bash %}
    sudo adduser git
{% endhighlight %}

Ahora logueate con el usuario de Git y crea un repositorio.

{% highlight bash %}
    # logueate en el servidor
    # para probar podes usar localhost
    ssh git@DIRECCION_IP_DEL_SERVER


    # Crea el repositorio
    git init --bare example.git
{% endhighlight %}

Ahora podés comitear al repositorio remoto.

{% highlight bash %}
    mkdir gitexample
    cd gitexample
    git init
    touch README
    git add README
    git commit -m 'primer commit'
    git remote add origin git@DIRECCION_IP_DEL_SERVER:example.git
    git push origin master
{% endhighlight %}

<h2 id="repositorios-remotos-online">16. Repositorios remotos online</h2>

<h3 id="clonando-repositorios-remotos">16.1 Clonando repositorios remotos</h3>

Git también soporta operaciones remotas. Git soporta varios tipos de protocolos de transporte; el protocolo nativo de Git es llamado *git*.

A continuación clonaremos un repositorio existente mediante el protocolo git.

{% highlight bash %}
    git clone git@github.com:vogella/gitbook.git
{% endhighlight %}

Alternativamente podrías clonar el mismo repositorio mediante el protocolo http.

{% highlight bash %}
    # clonamos a través de HTTP 
    git clone http://vogella@github.com/vogella/gitbook.git
{% endhighlight %}

<h3 id="agregando-mas-repositorios-remotos">16.2 Agregando más repositorios remotos</h3>

Si clonas un repositorio remoto, el repositorio original será llamado automaticamente `origin`.

Podés hacer push con los cambios a este repositorio `origin` mediante `git push origin`. Por supuesto, para hacer un push al repo reomoto tenés que contar con los permisos de escritura para tal repo.

También podés agregar más repositorios remotos a tu repositorio mediante el comando `git remote add [nombre] [url_repo]`. Por ejemplo si clonaste el repositorio de arriba con el protocolo git, podés agregar tambien el protocolo `https` de la siguiente manera:

{% highlight bash %}
    // agregamos el protocolo https
    git remote add githttp https://vogella@github.com/vogella/gitbook.git
{% endhighlight %}

<h3 id="operacion-remota-http-proxy">16.3 Operaciones remotas via HTTP y un proxy</h3>

Es posible utilizar el protocolo HTTP para clonar repositorios Git. Es especialmente útil si tu firewall bloquea todo excepto HTTP.

Git también provee soporte para acceso http mediante un servidor proxy. El siguiente comando Git podría por ejemplo, clonar un repositorio mediante http y un proxy. Podés incluir la variable proxy en general para todas las aplicaciones o solamente para Git.

Este ejemplo usa variables de entorno (enviroment variables).

{% highlight bash %}
    # Linux
    export http_proxy=http://proxy:8080
    # Windows
    # Set http_proxy=http://proxy:8080 
    git clone http://dev.eclipse.org/git/org.eclipse.jface/org.eclipse.jface.snippets.git
    # Push al origin usando http
    git push origin
{% endhighlight %}

Este ejemplo utiliza la configuracion de Git

{% highlight bash %}
    # Set proxy for git globally
    # proxy para git global
    git config --global http.proxy http://proxy:8080
    # para comprobar las configuraciones del proxy
    git config --get http.proxy
    # por si necesitas borrar la configuración del proxy
    git config --global --unset http.proxy
{% endhighlight %}

<h2 id="proveedores-hosting-git">17. Proveedores de hosting Git</h2>

En lugar de crear tu propio servidor, también es posible utilizar un servicio de hosting. Los proveedores de hosting de Git más populares son [Github](https://github.com/) y [Bitbucket](https://bitbucket.org/). Ambos ofrecen almacenamiento gratuito con ciertas limitaciones.

<h3 id="github">17.1 GitHub</h3>

Git Hub es gratuito para todos los repositorios públicos, o sea que si querés tener repositorios privados que solo son visibles por las personas que vos elegis, tenés que pagarle a GitHub una tarifa mensual.

GitHub requiere que crees lo que se llama una *key ssh* (llave SSH). Una descripción para crear dicha llave en Ubuntu puede ser encontrada en la sección de *ssh key creation* en el sitio de Ubuntu. Para windows remitite a *ssh key generation* de *msysgit*.

Create una cuenta en GitHub y crea un repositorio. Después de crear el repositorio en GitHub obtendrás una descripción de todos los comandos que necesitás ejecutar para subir tu proyecto a GitHub. Seguí las instrucciones.

Las instrucciones deberían ser similares a las siguientes:

{% highlight bash %}
Global setup:
 Set up git
  git config --global user.name "tu nombre"
  git config --global user.email tu.email@gmail.com
      
proximos pasos:
  mkdir gitbook 
  cd gitbook
  git init
  touch README
  git add README
  git commit -m 'primer commit'
  git remote add origin git@github.com:vogella/gitbook.git
  git push -u origin master
      
Ya contás con un repo?
  cd repo_existente
  git remote add origin git@github.com:vogella/gitbook.git
  git push -u origin master
{% endhighlight %}

<h3 id="bitbucket">17.2 Bitbucket</h3>

Bitbucket provee ilimitados repositorios públicos y privados, aunque el número de participantes para un repositorio privado está actualmente limitaod a 5 colaboradores. Es decir, si tenés más de 5 desarrolladores que necesitan acceder a ese repo privado vas a tener que pagar.

<h2 id="herramientas-graficas-git">18. Herramientas gráficas para Git</h2>

Este tutorial se basó en el uso de la consola de comandos para Git. Si querés podes hechar un vistazo a las herramientas gráficas para el trabajo con Git. Git provee dos herramientas gráficas. *gitk* muestra el historial y *git gui* muestra un editor que te permite realizar operaciones Git.

El proyecto de Eclipse EGit provee integración de Git en Eclipse, el cual ya está incluído en la última versión de Eclipse.

<h2 id="version-original-kindle">19. Obtené la versión original para Kindle</h2>

La versión original de este tutorial en inglés para Kindle está disponible aquí:

<a href='http://www.amazon.com/dp/B0067QNR56' target='_blank'><img src='http://www.vogella.de/articles/Git/images/150x200xgitbook.png.pagespeed.ic.YTQVJJZYBB.png' /></a>

<h2 id="preguntas-comentarios">20. Preguntas y comentarios</h2>

Podés incluir tus preguntas y comentarios en la sección de abajo, de comentarios. Existe un grupo en inglés: [www.vogella.de Google Group](http://groups.google.com/group/vogella)

<h2 id="links-recursos-utiles">21. Links  y recursos útiles</h2>

La mayoría de la documentación está en inglés, por eso en primera instancia decidí escribir/traducir este tutorial. Sin embargo, incluyo algunos links útlies. *Si conocés alguno que quisieras incluir podés sugerirlo en la sección de comentarios*.

*   [Sitio oficial de Git](http://git-scm.com/) - INGLES
*   [EGit para Eclipse](http://eclipse.org/egit/) - INGLES
*   [msysgit - Git para Windows](http://code.google.com/p/msysgit/) - INGLES
*   [Sitio de referencia de Git creado por un team de GitHub](http://gitref.org/) - INGLES
*   [Cheat sheet](http://github.com/guides/git-cheat-sheet) - INGLES
