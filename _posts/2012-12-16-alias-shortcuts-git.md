---
layout: post
title: "Alias útiles de Git"
category: git
tags: programacion git alias shortcut
---

Una de las filosofías de linux (heredada de Unix seguramente) ha sido eliminar tareas repetitivas.  Cada vez que nos encontramos haciendo lo mismo una y otra vez es necesario buscar alguna forma de eliminar la repetición y buscar la eficiencia. Una de esos casos se da con Git. A continuación te muestro un pedazo de mi `.gitconfig`:

    [color]
        status = auto
        branch = auto
        ui = true
    [alias]
        cm = commit
        br = branch
        co = checkout
        df = diff
        st = status -sb
        lol = log --graph --decorate --abbrev-commit
        bdiff = diff --name-status
        lg = log --graph --pretty=oneline --abbrev-commit
        sh = show --abbrev-commit
        ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate
        ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --numstat
        dl = "!git ll -1"
        dlc = diff --cached HEAD^

Los primeros son simplemente shortcuts para no tener que escribir las palabras completas. Después de un tiempo `cm` se vuelve mucho más cómodo que `commit`. Después hay algunos más "complejos", describo los más importantes:

#### st = status -sb

Después de pasar horas con Git, te das cuenta que el simple `status` es demasiado verborrágico. Te da información separada y siempre te imprime carteles de cómo agregar o sacar archivos del índice. Por ejemplo, esta es una captura de `git status`:

![git status](http://i.imgur.com/zQsQY.png)

Y esta de `git st` (es decir `status -sb`):

![git st](http://i.imgur.com/sVdha.png)

Como podrás observar, es un comando mucho más conciso. Informa qué archivos han cambiado (los marcados con la letra _M_) y cuáles son nuevos (_??_). La información del branch (`-b`) tal vez no es tan necesaria porque estoy usando [.git-completion.sh](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash) (muy recomendado). Pero sirve tener un resumen ahí.


#### lol = log --graph --decorate --abbrev-commit

`log` es uno de los comandos más amplios y útiles de Git. La verdad es demasiado amplio, y muchas veces complica. Este alias lo encontré en internet, y me es muy útil. El `--grap` dibuja a la izquerda un pequeño gráfico que representa la historia de commits (entre branches por ejemplo). El `--decorate` complementa esta información agregando datos de branches y tags. El `abbrev-commit` simplemente abrevia el hash del commit.

Esta es la salida de `git log`:

![git log](http://i.imgur.com/k0gIN.png)

Y esta la de `git lol` (`log --graph --decorate --abbrev-commit`):

![git log](http://i.imgur.com/Icmt9.png)

Como para este proyecto no uso branches, no se ve bien el gráfico, cuando tenga un ejemplo mejor voy a cambiar la img.


#### bdiff = diff --name-status

Este comando simplemente muestra qué archivos han sido cambiados, de forma bastante escueta y concisa. Es parecida al `git st`, pero este solo muestra archivos **que han cambiado**, no muestra archivos nuevos.


#### lg = log --graph --pretty=oneline --abbrev-commit

Esta es una versión más concisa de `git lol`, que simplemente muestra cada commit dentro del grafo de commits.

#### El resto...

Hay más alias, pero son más específicos. Los principales están listados arriba.

Eso es todo. Si tenés alguno para compartir, postealo en los comentarios!
