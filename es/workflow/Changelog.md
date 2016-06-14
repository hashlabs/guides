# CHANGELOG

Mantenemos un CHANGELOG por proyecto. Nos basamos en las ideas de [keepachangelog.com](http://keepachangelog.com).

## Al hacer un Pull Request

Cuando escribas un feature, fix o cambio nuevo, debes agregar una entrada en el
CHANGELOG en la sección de **Unreleased**. Si un Pull Request no tiene
una entrada para los cambios correspondientes, entonces no es valido y
no se puede mergear.

Pueden existir tres tipos de secciones dentro de un Release.

* Added: Nueva funcionalidad que se agrego
* Fixed: Un bug que se corrigió
* Changed: Parte de un codigo que se refactoreo

```markdown
[Unreleased]
### Added
* New Feature

### Fixed
* This annoying bug

### Changed
* This crappy code

## [1.0.1] - 2016-05-19
### Fixed
* Removing messaging locking from notification\_ms.

## 1.0.0 - 2014-05-31
### Added
* Other feature

[Unreleased]: https://github.com/hashlabs/repo/compare/1.0.1...HEAD
[1.0.1]: https://github.com/hashlabs/repo/compare/1.0.0...1.0.1
```

## Versiones

Usamos [Semver](http://semver.org/) para nuestras versiones. Semver
tiene tres niveles en un numero de version.

`MAJOR.MINOR.PATCH`

* MAJOR: Se usa para marcar cambios muy grandes o hitos en un proyecto. Tambien se
  usa para marcar una posible incompatiblidad que versiones anteriores.
* MINOR: Cuando agregas funcionalidad que no representa un hito en el
  proyecto.
* PATCH: Cuando arreglas errores o refactoreas codigo.

## Releases

Un Release es una version que representa el estado de un producto en el
tiempo. Cada Release puede contener uno o mas features/fixes/changes.

A la hora de hacer un deploy a production, se debe subir solo codigo que este asociado a una version. Esto nos facilita el
rastreo de bugs.

Github y Git nos dan `tags`, usamos los tags para marcar versiones en Git.

Para hacer un release los pasos son los siguentes:

1. En el branch master, cambiar el CHANGELOG, moviendo la seccion de **Unreleased** a una
   version.
2. Hacer commit de este cambio con el nombre de la version, `git commit -m "1.0.2"`
3. Crear un tag con la misma version, `git tag 1.0.2`
4. Push los cambios a master `git push upstream master`
5. Push los tags al repo `git push upstream --tags`
