---
estado: Terminado
tags:
  - aprendizaje
  - base_de_datos
  - entidad/relacion
  - estructuras
proyecto: base-de-datos
Creacion: 2026-03-24T16:05:00
Revision: 2026-03-24T16:05:00
---
# Agregacion

## El Problema

Una relación es una vinculación entre dos o más entidades. Pero, ¿qué pasa si necesitamos vincular una relación con una entidad?

Basados en los conceptos del modelo entidad-relación básico, esto no es posible. Por eso existe la **agregación**.

## Definición

> [!important]
> La **agregación** consiste en convertir una relación en entidad. Esto permite vincular esa relación (ahora convertida en entidad) con otra entidad a través de una nueva relación.

## Simbología

La relación agregada se representa con un **rectángulo** (igual que cualquier entidad) que encierra la relación original.
![[screenshot-2026-03-24_16-01-22.png]]

## Ejemplo: Espectáculos y Facturas

Un espectáculo se presenta en un teatro en diferentes días. El precio puede variar según la presentación. Las facturas pueden incluir entradas para diferentes presentaciones.

Para vincular la relación `sePresenta` (entre Espectáculo y Teatro) con la entidad `Factura`, se necesita convertir `sePresenta` en una entidad mediante agregación. Luego, la relación `seVende` conecta esta agregación con `Factura`.

![[screenshot-2026-03-24_16-01-28.png]]
## Consideraciones

- Una agregación contiene una sola relación (la relación agregada/convertida en entidad)
- La relación agregada puede ser de cualquier grado (binaria, ternaria, etc.)
- Si la relación agregada es binaria, siempre será de multiplicidad **m-n**
- La relación que se vincula con la agregación puede ser de cualquier grado y multiplicidad

---
__TE SIENTES DETERMINADO__