# Rama `link` — compilación del cliente Link (LINK)

Este repositorio es un fork de `bryangerlach/rdgen` y se usa solo para compilar el cliente
Link (RustDesk con nombre propio) de LINK.

- `master` se deja igual al original, para comparar y traer novedades.
- `link` es la rama de trabajo. El servicio rdgen dispara los flujos de esta rama (`GHBRANCH=link`).

## Qué cambia respecto del original

Los flujos `generator-*` del original bajan en cada compilación los parches de
`.github/patches/` y el crate `printer-adapter` desde `bryangerlach/rdgen@master`.
En esta rama los toman de este fork, en un commit fijo y revisado:

    cf4a5d2530f8e55506a6344b2460db8659a00221

Así un cambio en el repositorio original no entra en una compilación sin revisión previa.

## Cómo traer novedades del original

1. Sincronizar `master` con el original.
2. Revisar el diff entre el commit fijado y el nuevo (`.github/patches/`, `printer-adapter/`
   y los flujos).
3. Recién entonces llevar los cambios a `link` y reemplazar el commit fijado en
   `.github/workflows/*.yml`.

## Qué no va en este repositorio

Contraseñas, tokens ni claves. El token de GitHub y la clave del zip viven solo en el
contenedor del servicio y en los secretos del repositorio.
