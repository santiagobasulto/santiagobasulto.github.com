---
layout: post
title: Comandos útiles de Git para el día a día
category: programacion
tags: git comandos branch mergeado merged
published: false
---

#### Borrar un branch remoto (http://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-both-locally-and-in-github)

As of Git v1.7.0, you can delete a remote branch using:
git push origin --delete <branchName>

The above is syntactic sugar for

git push origin :<branchName>
which was added in Git v1.5.0 "to delete a remote branch or a tag."

#### Ver si un branch fue mergeado en otro

La forma más fácil es usando el flag `--contains` con el comando `git-branch`. Suponé que tenemos un repo con 3 branches: `master`, `not-merged-branch`, `merged-branch` (se entiende por los nombres cuáles están mergeados y cuáles no).

En este ejemplo `merged-branch` ya está mergeado en `master`. Así que lo vamos a comprobar con `--contains`:

    # nos paramos en master
    $ git checkout master

    $ git branch --contains merged-branch
    * master
      merged-branch

En este caso el comando lista dos branches y lo que significa es que los cambios contenidos en `merged-branch` están en ambos branches. En `merged-branch` obviamente, y en `master`, lo que indica que ya está mergeado.

Veamos qué ocurre si preguntamos por `not-merged-branch`:

    $ git branch --contains not-merged-branch
      not-merged-branch

En este caso solo devuelve el mobre del branch. Obviamente cada branch se contiene a si mismo. Es decir que los cambios de este branch no están presentes en ningún otro branch.

Como resumen, el comando `git branch --contains BRANCH_NAME` devuelve los branches que contienen BRANCH_NAME. Si devuelve solamente BRANCH_NAME, entonces no está mergeado en ningún lado.

Para obtener una descripción más detallada de los cambios podemos usar el comando `git-log`. Esto lo hacemos para saber cuáles commits no están en el branch.

Por ejemplo, para `not-merged-branch`:

    $ git log not-merged-branch ^master
    commit a01a172092cb5588c54ab2e04d8b92a7a8d9ca1f
    Author: Pepe <--->
    Date:   Wed Jan 23 16:48:22 2013 -0300

        El mensaje de commit

`git log BRANCH1 ^BRANCH2` muestra todos los commits de `BRANCH1` que no están en `BRANCH2`.

Por último hay dos comandos que listan todos los branches mergeados o no mergeados, respectivamente:

    $ git branch --merged
    * master
      merged-branch

    $ git branch --no-merged
      not-merged-branch

_Fuente:_ [http://stackoverflow.com/questions/1710894/using-git-show-all-commits-that-are-in-one-branch-but-not-the-other](http://stackoverflow.com/questions/1710894/using-git-show-all-commits-that-are-in-one-branch-but-not-the-other)

_Fuente:_ [http://stackoverflow.com/questions/226976/how-can-i-know-in-git-if-a-branch-has-been-already-merged-into-master](http://stackoverflow.com/questions/226976/how-can-i-know-in-git-if-a-branch-has-been-already-merged-into-master)

#### Mostrar commits en un branch ignorando merges

Para mostrar todos los commits en un branch pero que no fueron traidos por merges de otros branches podemos usar este comando:

    $ git log --no-merges --first-parent

**Importante**: Es importante que los branch mergeados no hayan sido Fast-Forward merges. Por las dudas, te recomiendo siempre agregar el flag `--no-ff` a `git-merge`.
_Fuente:_ [http://stackoverflow.com/questions/8527139/showing-commits-made-directly-to-a-branch-ignoring-merges-in-git](http://stackoverflow.com/questions/8527139/showing-commits-made-directly-to-a-branch-ignoring-merges-in-git)

#### Mostrar commits de un usr en particular

_Fuente:_ [http://stackoverflow.com/questions/4259996/how-can-i-view-a-git-log-of-just-one-users-commits](http://stackoverflow.com/questions/4259996/how-can-i-view-a-git-log-of-just-one-users-commits)
