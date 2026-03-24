---
estado: Terminado
tags:
  - aprendizaje
  - base_de_datos
  - entidad/relacion
  - estructuras
proyecto: base-de-datos
Creacion: 2026-03-24T15:55:00
Revision: 2026-03-24T15:55:00
---
# Tabla de Contenidos

- [[#Definición|Definición]]
- [[#Clave Primaria de una Entidad Débil|Clave Primaria de una Entidad Débil]]
- [[#Simbología|Simbología]]
- [[#Ejemplo: Habitaciones de una Cadena de Hoteles|Ejemplo: Habitaciones de una Cadena de Hoteles]]
- [[#Relaciones con Otras Entidades|Relaciones con Otras Entidades]]
- [[#Dependencia de Existencia|Dependencia de Existencia]]
- [[#Relación con Entidades Fuertes|Relación con Entidades Fuertes]]
- [[#Conceptos Relacionados|Conceptos Relacionados]]
# Entidades Debiles

## Definición

> [!important]
> Una **Entidad Débil** es aquella cuyos atributos no son suficientes para identificarla unívocamente. Necesita de una **Entidad Fuerte** de la cual depende para conformar su [[Entidades#Clave Primaria|clave primaria]].


## Clave Primaria de una Entidad Débil


> [!important]
> La clave primaria de una entidad débil se compone de:
> 
> - Clave Primaria de la Entidad Fuerte de la cual depende
> - Discriminador de la Entidad Débil (clave parcial): distingue las entidades débiles que dependen de dicha entidad fuerte
> 
> ```
> Clave Primaria Entidad Débil = Clave Entidad Fuerte + Discriminador
>```

## Simbología

- **Doble línea** en el rectángulo: representa una entidad débil
- **Doble línea** en la relación: representa la relación fuerte-débil
- **Multiplicidad**: la relación fuerte-débil siempre es 1-n (la entidad fuerte es 1, la débil es n)
- **Participación**: la entidad débil tiene participación total en la relación

## Ejemplo: Habitaciones de una Cadena de Hoteles

Los números de habitaciones (101, 102, 201, etc.) se repiten para diferentes hoteles. El número de habitación por sí solo no identifica unívocamente una habitación, pero combinado con el CUIT del hotel sí.

- Entidad Fuerte: Hotel (clave: cuit)
- Entidad Débil: Habitación (clave: cuit + nroHab)

![[Ejemplo Hotel.png]]
![[Representacion Entidades debiles.png]]
## Relaciones con Otras Entidades

Una entidad débil puede estar relacionada con otras entidades además de la entidad fuerte de la que depende. Estas otras relaciones se representan con línea simple.
![[screenshot-2026-03-24_15-58-27.png]]

## Dependencia de Existencia

Si la existencia de una entidad X depende de la existencia de una entidad Y:

- X es una **entidad subordinada** (o dependiente)
- Y es una **entidad dominante**

Operativamente: si se suprime Y, se suprime X.

## Relación con Entidades Fuertes

Una **Entidad Débil SIEMPRE tiene dependencia de existencia** sobre la entidad fuerte relacionada. Esto significa que si se elimina la entidad fuerte, todas las entidades débiles asociadas también deben eliminarse.

## Conceptos Relacionados
- [[Programacion Orientada a Objetos#Composición|Composicion POO]]

---
__TE SIENTES DETERMINADO__