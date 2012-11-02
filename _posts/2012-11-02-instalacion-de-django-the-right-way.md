---
layout: post
title: "Instalación de Django - 'The right way'"
category: django
tags: programacion django virtualenv python
---

Lo que me lleva a escribir este post es lo siguiente:

**a)** He visto muchas preguntas de cómo instalar Django

**b)** Todas las respuestas son pésimas

El problema no está en el "cómo instalar Django" sino en qué ambiente se instala para desarrollar con Django. Es decir, instalar Django es muy simple, no hay mayores complejidades. Pero me parece que cualquier persona que esté comenzando con Django debería comenzar de la mejor manera posible, es decir, con un entorno de trabajo bien armado. A continuación listo algunos puntos a tener en cuenta. Hago aquí una aclaración: esta es la forma que yo pienso es mejor para desarrollar con Django. Tal vez alguien tenga otra idea de cómo hacerlo, es posible. En tal caso puede compartirla, será bienvenido. Además, la idea es instalar Django, pero la mayoría de los puntos sirven para trabajar sobre cualquier proyecto de Python.

A modo de resumen, este no es un post del tipo "Instalá Django en 2 minutos". Si estás buscando algo similar te recomiendo que vuelvas a Google. De todas maneras lo más probable es que vuelvas en un tiempo cuando el "Instalá Django en 2 minutos" ya no sea rentable.

## Linux

Django es python, python se lleva bien con Linux. Una sola vez traté de instalar Python y Django en Windows. Claudiqué a los cinco minutos. Expongo las razones por las que deberías usar Linux:

1. **Facilidad**: Como ya mencioné, Linux se lleva bien con python. Más allá del dato anecdótico de que Python venga instalado en el 99% de las distros, en general, es mucho más fácil programar en entornos Linux

2. **Similaridad con el server**: ¿Te pusiste a pensar qué servidor vas a usar para alojar tu aplicación? Lo más probable es que sea sobre Linux. Entonces deberías desarrollar sobre Linux para familiarizarte con el entorno, para evitar problemas a futuro (codificación de caracteres, entorno, permisos, etc).

3. **Seguridad**: No voy a alimentar la interminable batalla de qué sistema operativo es más seguro. Lo que sí digo es que si desarrollas sobre Windows y hosteas sobre Linux, entonces podés llegar a tener algunos problemas de seguridad (sobre todo debido a los permisos).

La distro que utilizo yo es [Ubuntu](http://www.ubuntu.com/) (orgullosamente desde la versión [6.10](http://en.wikipedia.org/wiki/List_of_Ubuntu_releases#Ubuntu_6.10_.28Edgy_Eft.29)). No hay mucha diferencia entre las distros a la hora de setear el entorno para desarrollo, así que podés elegir la que más te guste.

## Python

Parece obvio pero es importante decidir sobre qué versión de python vas a desarrollar. Tal vez sea incluso necesario decidir qué implementación vas a usar (Cpython, Jython, PyPy, etc), aunque lo más probable es que uses CPython.

La versión si es un tema importante. La primer decisión reside en si vamos a utilizar Python 2.X o Python 3. Si vas a arrancar un proyecto de cero y tenés la posibilidad de hostear tu propia aplicación, te recomiendo que trates de usar Python 3. Las ventajas a la larga son muchas.

Si vas a utilizar Python 2.X debés decidir si vas a usar Python 2.7 o Python 2.6. En este caso deberías preguntarte dónde vas a hostear la aplicación y qué librerías vas a necesitar. Obviamente siempre es prferible utilizar la última versión.

Si estás usando Linux python ya viene instalado (la versión actual con ubuntu es 2.7.2+). Si querés usar python3 debés instalarlo:

	sudo apt-get install python3

## PIP

> **Por favor, no uses easy_install!** Frase textual de Daniel Lindsley en una charla de Tastypie.

PIP es un "package manager" para python, sirve para instalar librerías de python de forma fácil. No es necesario bajar las librerías e instalarlas (`python setup.py install`). Hay varias maneras de instalarlo. Algunos prefieren usar easy_install, a mi la verdad me da lo mismo. Si usás Ubuntu, una forma fácil es la siguiente:

	sudo apt-get install python-pip

## Virtualenv

Virtualenv es lo mejor que le podría haber pasado a Python. Lo que hace es generar ambientes "aislados" para desarrollar. Es decir, que uno puede tener distintos ambientes (o "entornos") con distintas librerías instaladas. Podemos tener un virtualenv que se llame "django-1.4" que tenga instalado Django 1.4 para nuestro proyecto, y otro que se llame "prueba-django-1.5" para probar cosas con Django 1.5. Esto es solo un ejemplo, uno puede tener todos los virtualenv que quiera con las librerías instaladas que quiera. Las ventajas son

1. Uno puede tener varios ambientes en la misma PC/Laptop y hacer las pruebas que quiera. Los virtualenvs se crean y se borran de forma muy fácil.
2. Si rompemos algo, con alguna dependencia rara, o alguna instalación defectuosa, lo único que hay que hacer es crear un virtualenv nuevo. Easy peasy.
3. No es necesario ser root (no más `sudo ...`) para instalar paquetes nuevos. Se instalan todos bajo nuestro usuario.

Para instalarlo, una vez que tenemos PIP instalado hacemos:

	sudo pip install virtualenv

Una vez instalado, para crear un virtualenv hacemos:

	virtualenv prueba-django-1.4

eso nos genera un directorio `prueba-django-1.4/`. El siguiente paso es "activar" ese virtualenv:

	source prueba-django-1.4/bin/activate

Listo! en ese momento vamos a estar trabajando dentro de ese virtualenv. Ahora podemos instalar librerías y se instalaran solamente para ese virtualenv.

## Django

Finalmente llegamos a instlar Django. Una vez que tenemos PIP y virtualenv, todo es más fácil:

	virtualenv prueba-django-1.4
	source prueba-django-1.4/bin/activate
	pip install django


Eso es todo. Django va a estar instalado en ese virtualenv. Hagamos una prueba:

	django-admin.py startproject prueba_django

Si lo anterior anduvo, quiere decir que ya tenés instalado Django. Probá abrir otra terminal e invocar a `django-admin`. No debería ser posible. Eso quiere decir que Django está instalado solamente para ese virtualenv. Obviamente podemos crear varios virtualenvs e instalar en todos Django.

## Git

Esta parte parece innecesaria. Para mi es fundamental tener un sistema de control de versiones a la hora de desarrollar. Más allá de usar o no un repositorio centralizado, cualquier tarea de programación que lleve más de 5 minutos debería basarse en un CVS. Yo uso GIT, pero podés usar Mercurial, SVN, el que más te guste. En ubuntu:

	sudo apt-get install git

## Virtualenvwrapper

Virtualenvwrapper es una utilidad para simplificar la creación, eliminación y uso de virtualenvs. Se basa en virtualenvs y lo único que hace es darnos más facilidad para su uso. La idea es, una vez instalado poder ejecutar estos comandos:

	mkvirtualenv prueba-django-1.4   # Crea el virtualenv en un lugar centralizado
	workon prueba-django-1.4         # Activa el virtualenv sin necesidad de source ...
	deactivate                       # Desactiva el virtualenv
	rmvirtualenv prueba-django-1.4   # Elimina el virtualenv

Para instalarlo:

	sudo pip install virtualenvwrapper


Después en tu `.bashrc` (en el home de tu usuario: `/home/TU-USUARIO/.bashrc`) agregá estas lineas al final:

	export WORKON_HOME=$HOME/.virtualenvs            # Acá se crean todos los virtualenvs
	export PROJECT_HOME=$HOME/code/python/projects   # Acá se crean los Proyectos (http://virtualenvwrapper.readthedocs.org/en/latest/projects.html#project-management)
	source /usr/local/bin/virtualenvwrapper.sh

## Extra: usando un requirements.txt

Una de las funciones más interesantes de pip es la posibilidad de utilizar un archivo donde guardar todos las dependencias de nuestro proyecto. De esa forma, podemos ejecutar un solo comando y tenerlas todas instaladas. Para hacer esto solamente debés crear un archivo "requirements.txt" y ponerlo en el root de tu proyecto (todo esto es opcional, pero son buenas prácticas para seguir). Por ejemplo, dentro de `prueba_django` podemos guardar nuestro `requirements.txt` con todas las dependencias de nuestro proyecto.

	cd prueba_django
	echo "django" > requeriments.txt

Una vez que tenemos todas las dependencias listadas en requirements.txt las instalamos todas de una:

	workon prueba-django-1.4
	pip install -r requirements.txt

Acá hay un ejemplo de un `requeriments.txt` real: https://github.com/toastdriven/django-tastypie/blob/master/requirements.txt


Listo, he llegado al final. Se que es un poco largo y al principio tedioso, pero a la larga, una metodología como esta simplifica y acelera mucho el desarrollo. Espero a ti también te sirva.
