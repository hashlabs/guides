# Git

## Como mantener un repositorio

* Evita incluir archivos en Git que sean especificos de tu ambiente de desarrollo.
* Borra los branches locales y remotes despues que se mergeados.
* Siempre desarrolla en un nuevo feature branch.
* Haz rebase frecuentemente de master a tu branch, para mantenerlo
  actualizado con upstream.
* Crea un [pull request](PullRequests.md) cuando termines tu
  trabajo.
* Evita tener mas de 1 feature por branch.

## Para escribir un feature

Crea un feature branch local basado en master. Nuestra convencion para
nombres de branches es

`<tus iniciales>/#<numero del ticket>`

Por ejemplo. Mi nombre es Orlando Del Aguila, mis iniciales son **od**.
Mi feature branch para el ticket #22 seria `od/#22`

```
git checkout master
git pull upstream
git checkout -b <branch-name>
```

Haz rebase de master en vez de hacer pull

```
git checkout master
git pull
git checkout -
git rebase master
```

Haz **squash** de tus commits usando `git rebase -i master`.

Una vez que termines tu feature, pushealo a upstream

```
git push upstream od/EX-123
```

Crea un pull request para que sea revisado por los miembros de tu
equipo.
