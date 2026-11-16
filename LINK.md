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

Además, los pasos que bajan y suben artefactos entre trabajos usaban en el original
`actions/download-artifact@master` y `actions/upload-artifact@master`. Esas ramas `master`
quedaron congeladas en 2020 (versión 2 de las acciones) y ya no ven los artefactos que sube
`actions/upload-artifact` v7: la primera compilación de LINK (16/11/2026, corrida 43806040927)
falló en "Restore bridge files" con "Unable to list artifacts for the run". En este fork esos
pasos usan las mismas versiones que el resto de los flujos, fijadas por commit:
`actions/download-artifact` v4 y `actions/upload-artifact` v7. Al traer novedades del original,
no volver a `@master` en esas acciones.

## Qué no va en este repositorio

Contraseñas, tokens ni claves. El token de GitHub y la clave del zip viven solo en el
contenedor del servicio y en los secretos del repositorio.
