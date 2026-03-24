---
estado: Terminado
tags:
  - aprendizaje
  - base_de_datos
  - entidad/relacion
  - estructuras
proyecto: base-de-datos
Creacion: 2026-03-24T15:32:00
Revision: 2026-03-24T15:43:00
---
# SuperClases - SubClases

## Definición

> [!important]
> Un conjunto de entidades (tipo de entidad) puede poseer subgrupos de entidades que comparten características pero también tienen particularidades propias. Esto da origen a:
> 
> - **[[Programacion Orientada a Objetos#Herencia|SuperClases]] (Supertipo)**: Conjunto de entidades que contiene características comunes (atributos y relaciones) y una clave primaria compartida por todas las subclases.
> - **[[Programacion Orientada a Objetos#Herencia|SubClases]] (Subtipo)**: Subgrupos de entidades que heredan las características de la superclase y además poseen atributos y relaciones propias.

## Proceso de Generalización y Especialización

- **Especialización**: Proceso descendente donde se identifican subgrupos dentro de una entidad existente, definiendo sus características particulares.
- **Generalización**: Proceso ascendente donde se agrupan entidades similares en una superclase compartida, identificando características comunes.

## Restricciones y Características


> [!important]
> ### Según cobertura (cobertura de participación)
> 
> - **Completa**: Cada entidad de la superclase debe ser miembro de al menos una subclase. Se representa con línea doble.
> - **Parcial**: Cada entidad de la superclase puede ser miembro de una subclase (no es obligatorio). Se representa con línea simple.
> 
> ### Según solapamiento
> 
> - **Disjunta**: Cada entidad de la superclase puede ser miembro de máximo una subclase. Se representa con letra **D**.
> - **Solapada**: Una entidad puede ser miembro de varias subclases simultáneamente. Se representa con letra **O** (overlap).


## Combinaciones Posibles

Las restricciones pueden combinarse de cualquier forma:

- Completa, disjunta
- Completa, solapada
- Parcial, disjunta
- Parcial, solapada

## Criterios Múltiples

Una especialización puede basarse en más de un criterio simultáneamente. Por ejemplo, vehículos pueden clasificarse por tipo de vehículo Y por tipo de combustible, generando subclases diferentes según cada criterio.

## Ejemplos
![[Herencia.png]]
![[screenshot-2026-03-24_15-49-43.png]]
![[screenshot-2026-03-24_15-50-40.png|697]]

## Conceptos Relacionados
[[Programacion Orientada a Objetos#Herencia|Herencia POO]]

---
__TE SIENTES DETERMINADO__