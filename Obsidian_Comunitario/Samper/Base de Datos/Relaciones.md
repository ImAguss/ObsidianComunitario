---
estado: Terminado
tags:
  - base_de_datos
  - modelo_er
  - diseño_conceptual
  - relaciones
proyecto: base-de-datos
Creacion: 2026-03-23T23:22:00
Revision: 2026-03-23T23:45:00
---
# Relaciones

## Definición

> [!important]
> Las relaciones (o vinculaciones) representan una **asociación o vinculación entre dos o más entidades**.
> 
> Ejemplos:
> - Médico **ATIENDE** a Paciente
> - Persona **TRABAJA** en Empresa
> - Estudiante **CURSA** Materia
> 
> A diferencia de las entidades, las relaciones **dependen de la existencia de las entidades** que vinculan. No pueden existir por sí mismas.


## Conjuntos de Relaciones

Un conjunto de relaciones agrupa todas las relaciones del mismo tipo. Cada instancia de una relación conecta entidades específicas entre sí.

### Representacion
![[Representacion Relaciones.png]]

## Atributos en Relaciones


> [!important]
> Las relaciones pueden tener atributos descriptivos propios, al igual que las entidades.
> 
> Ver [[Entidades#Atributos de las Entidades|tipos de atributos]] para clasificación (simples/compuestos, monovaluados/multivaluados, almacenados/derivados).

### Representacion
![[Atributos en Relaciones.png]]

## Clave Primaria en Relaciones

> [!important]
> Cuando una relación contiene atributos, puede necesitar distinguir instancias dentro del conjunto de relaciones. En ese caso, se subrayan los atributos que forman parte de la clave primaria.
> 
> Para más detalle sobre claves primarias, ver [[Entidades#Clave Primaria|clave primaria en entidades]].
> 

## Grado de las Relaciones

El grado refiere a la **cantidad de entidades vinculadas** por la relación.

### Relaciones Binarias

Vinculan **dos entidades**. Es el tipo más común.

Ejemplo: Persona — TRABAJA —> Empresa

### Relaciones Ternarias

Vinculan **tres entidades**.

Ejemplo: Empleado — TRABAJA_EN —> Proyecto —> Departamento
![[Representacion Ternaria.png]]

### Relaciones N-arias

Vinculan **n entidades**. Pueden ser más complejas y menos frecuentes.


> [!info]
> En el diseño de bases de datos, las relaciones binarias son las más utilizadas. Las ternarias y n-arias suelen representarse como entidades intermedias en el modelo relacional.


---
__TE SIENTES DETERMINADO__