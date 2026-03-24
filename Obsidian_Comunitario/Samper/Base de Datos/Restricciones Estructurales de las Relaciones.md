---
estado: Terminado
tags:
  - base_de_datos
  - modelo_er
  - diseño_conceptual
  - restricciones
  - relaciones
proyecto: base-de-datos
Creacion: 2026-03-23T23:34:00
Revision: 2026-03-23T23:50:00
---
# Restricciones Estructurales de las Relaciones

Existen dos tipos de restricciones estructurales en los conjuntos de relaciones:

## Cardinalidad/Multiplicidad

> [!important]
> Indica la **cantidad de instancias** de una entidad que pueden estar asociadas con instancias de otra entidad dentro de una relación determinada. Al modelarla siempre especifica el maximo, no el minimo.
> 

### En Relaciones Binarias

El análisis se realiza en **ambos sentidos** de la relación:

#### Cardinalidad 1:1 (Uno a Uno)

- Una entidad A se relaciona con **a lo sumo una** entidad B
- Una entidad B se relaciona con **a lo sumo una** entidad A

Ejemplo: Persona — POSEE —> Vehículo
- Una persona tiene un solo vehículo
- Un vehículo tiene solo un dueño

![[Cardinalidad 1-1.png]]

#### Cardinalidad 1:N (Uno a Muchos)

- Una entidad A puede relacionarse con **varias** entidades B
- Una entidad B se relaciona con **a lo sumo una** entidad A

Ejemplo: Persona — POSEE —> Vehículo
- Una persona puede tener varios vehículos
- Un vehículo tiene solo un dueño

![[Cardinalidad 1-N.png]]

#### Cardinalidad M:N (Muchos a Muchos)

- Una entidad A puede relacionarse con **varias** entidades B
- Una entidad B puede relacionarse con **varias** entidades A

Ejemplo: Persona — POSEE —> Vehículo
- Una persona puede tener varios vehículos
- Un vehículo puede tener varios dueños

![[Cardinalidad M-N.png]]

### En Relaciones Ternarias

El análisis considera **pares de entidades**:

#### Cardinalidad N:1:1

Cada par de entidades (A,B) se relaciona con una sola entidad C.

#### Cardinalidad N:M:1

Cada par de entidades (A,B) se relaciona con una sola entidad C, pero otros pares pueden relacionarse con varias entidades.

#### Cardinalidad N:M:P

Cada par de entidades puede relacionarse con varias entidades de la tercera.

> [!important]
> Para analizar una relación ternaria, tomar **pares de entidades** y preguntar: ¿cuántas entidades del tercer tipo pueden estar asociadas con este par?

![[Cardinalidad Ternaria.png]]

## Tipo de Participación

Indica si una entidad **siempre debe estar relacionada** con otra entidad dentro de una relación dada, o si su presencia es **opcional**.

### Participación Total (Doble línea)

Cada entidad del conjunto **debe estar presente** en al menos una instancia de la relación.

Ejemplo: Un vehículo **siempre** tiene un dueño (no puede existir sin dueño registrado).

### Participación Parcial (Línea simple)

Cada entidad del conjunto **puede o no estar presente** en la relación.

Ejemplo: Un vehículo **puede** tener un dueño (puede no tenerlo registrado).

> [!note] Nota 
> Por simplicidad, se utiliza línea simple en todas las participaciones, excepto en relaciones que vinculan entidades fuertes y débiles (ver [[Entidades Debiles#Entidades Debiles|entidades débiles]]).

![[Participacion Total vs Parcial.png]]

![[screenshot-2026-03-23_23-37-16.png]]

---
__TE SIENTES DETERMINADO__