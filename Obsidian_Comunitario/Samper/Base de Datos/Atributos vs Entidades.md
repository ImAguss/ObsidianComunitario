---
estado: Terminado
tags:
  - base_de_datos
  - modelo_er
  - diseño_conceptual
  - entidades
  - atributos
proyecto: base-de-datos
Creacion: 2026-03-23T23:42:00
Revision: 2026-03-23T23:44:00
---
# Atributos vs Entidades

En el modelado conceptual, puede surgir la duda de si un elemento debe representarse como un atributo o como una entidad.

## Criterio de Decisión

Para decidir si algo es atributo o entidad, considerar:

> [!important]
> ### Representar como Atributo cuando:
> 
> - No necesita otros atributos más allá del nombre o valor
> - No puede ser referenciado en otro lugar del modelo
> - No tiene comportamiento propio ni relaciones independientes
> - No posee atributos PROPIOS
> 
> Ejemplo: `localidad` como atributo de `Persona`
> - Solo interesa el nombre de la localidad
> - No se necesita guardar más información sobre ella


> [!important]
> ### Representar como Entidad cuando:
> 
> - Necesita tener otros atributos propios (además del nombre)
> - Puede existir en otros lugares del modelo y ser referenciado
> - Tiene relaciones con otras entidades
> - Requiere identificación propia (clave primaria)
> 
> Ejemplo: `Localidad` como entidad
> - Puede tener atributos: código postal, provincia, país
> - Puede relacionarse con otras entidades: `Dirección`, `Sucursal`
> - Otras entidades pueden referenciarla


## Ejemplo Comparativo
![[screenshot-2026-03-23_23-44-23.png]]
## Depende del Contexto

La decisión depende de:

- **Necesidades de información del minimundo**: ¿Qué datos se necesitan realmente?
- **Semántica de la realidad**: ¿Tiene sentido que el elemento exista por sí mismo?
- **Flexibilidad ante cambios**: ¿Puede evolucionar y necesitar más atributos en el futuro?

---
__TE SIENTES DETERMINADO__