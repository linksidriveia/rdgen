# Fork de LINK — compilación del cliente Link

Este repositorio es un fork de `bryangerlach/rdgen` y se usa solo para compilar el cliente
Link (RustDesk con nombre propio) de LINK.

- `master` es la rama de trabajo de LINK y la rama por defecto: GitHub solo registra los flujos
  que se disparan a mano si estan en la rama por defecto. El servicio rdgen dispara los flujos
  de esta rama (es su valor por defecto; no hace falta `GHBRANCH`).
- El original se compara directamente contra `bryangerlach/rdgen`, no contra una rama de este fork.
- No usar el boton "Sync fork" -> "Discard commits": borraria lo que esta rama fija.

## Qué cambia respecto del original

Los flujos `generator-*` del original bajan en cada compilación los parches de
`.github/patches/` y el crate `printer-adapter` desde `bryangerlach/rdgen@master`.
En este fork los toman de este mismo repositorio, en un commit fijo y revisado:

    cf4a5d2530f8e55506a6344b2460db8659a00221

Así un cambio en el repositorio original no entra en una compilación sin revisión previa.

## Cómo traer novedades del original

1. Traer el original a una rama aparte (no a `master`).
2. Revisar el diff entre el commit fijado y el nuevo (`.github/patches/`, `printer-adapter/`
   y los flujos).
3. Recién entonces llevar los cambios a `master` y reemplazar el commit fijado en
   `.github/workflows/*.yml`.

Además se quitó `docker-build.yml`: publicaba una imagen en Docker Hub en cada subida a
`master` y este fork no publica imágenes (la del servicio se construye con el `Dockerfile`).

## Qué no va en este repositorio

Contraseñas, tokens ni claves. El token de GitHub y la clave del zip viven solo en el
contenedor del servicio y en los secretos del repositorio.
