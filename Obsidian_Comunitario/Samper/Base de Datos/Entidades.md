---
estado: Terminado
tags:
  - base_de_datos
  - modelo_er
  - diseño_conceptual
  - entidades
proyecto: base-de-datos
Creacion: 2026-03-23T23:07:00
Revision: 2026-03-23T23:30:00
---
# Entidades

## Definición
> [!important]
> Las entidades son elementos u objetos del minimundo que:
> - Son relevantes dentro del dominio que se está modelando
> - Necesitan registrarse en el sistema
> - **Existen por sí mismos** (independientes de otras entidades)
> - Pueden distinguirse unos de otros
> - Poseen propiedades propias (atributos) que los describen


## Tipos de Entidades

### Entidades Concretas

Representan objetos tangibles, físicos, que existen en el mundo real.

Ejemplos:
- Una persona (CUIL, nombre, dirección, fecha de nacimiento)
- Un vehículo (patente, marca, modelo)

### Entidades Abstractas

Representan conceptos o entidades que no son físicas pero existen conceptualmente.

Ejemplos:
- Una cuenta bancaria (número de cuenta, fecha de apertura, tipo de cuenta)
- Un pedido (número de pedido, fecha, cliente)
- Una factura (número de factura, fecha, monto total)

### Representacion
![[Representacion Entidad.png|358]]

## Atributos de las Entidades

Los atributos son las propiedades que describen a una entidad. Existen diferentes clasificaciones:

### Por su Composición

- **Simples**: No se pueden dividir en partes más pequeñas (ej: localidad, `CUIL`)
- **Compuestos**: Se pueden descomponer en atributos más simples (ej: `dirección` puede dividirse en `nombre Completo`,`código postal`)

### Por su Cardinalidad

- **Monovaluados**: Tienen un solo valor para cada entidad (ej: cada persona tiene un solo `CUIL`, una sola `fecha de nacimiento`)
- **Multivaluados**: Pueden tener múltiples valores para una misma entidad (ej: una persona puede tener varios `teléfonos`, varios `emails`)

### Por su Origen

- **Almacenados**: Se guardan directamente en la base de datos (ej: `nombre`, `dirección`)
- **Derivados/Calculados**: Se obtienen a partir de otros atributos almacenados (ej: `edad` se calcula a partir de la `fecha de nacimiento`, `subtotal` se calcula como `precio × cantidad`)

### Representacion
![[Representacion Atributos.png|338]]

> [!info]
> Los atributos derivados no necesariamente se almacenan, ya que pueden calcularse en tiempo de consulta. Sin embargo, en algunos casos se guardan por motivos de rendimiento.

## Entidad vs Conjunto de Entidades
> [!important]
> 
> Es importante distinguir:
> 
> - **Entidad**: Es la instancia individual, el objeto concreto (ej: "Miguel" como persona específica con CUIL 20-12345678-3)
> - **Conjunto de Entidades / Tipo de Entidad**: Es la "clase" o plantilla que define qué atributos comparten todas las entidades de ese tipo (ej: "Persona" como concepto abstracto)
> 
> En el diagrama ER, el rectángulo representa el **conjunto de entidades**, y cada fila de datos es una **entidad** (instancia).
> 
> ```
> Conjunto de Entidades: Persona
> Entidades (instancias):
>   - Persona con CUIL 20-12345678-3, nombre "Miguel"
>   - Persona con CUIL 27-34567890-1, nombre "Laura"
>   - Persona con CUIL 20-44665678-3, nombre "Hugo"
> ```
> 
> Los conjuntos de entidades pueden ser:
> 
> - **Disjuntos**: Una entidad solo puede pertenecer a un conjunto
> - **Solapados**: Una entidad puede pertenecer a varios conjuntos simultáneamente
> 
## Clave Primaria
> [!important]
> 
> Es el atributo o conjunto de atributos que identifican **unívocamente** una entidad dentro de su conjunto de entidades.
> 
> - **Clave Simple**: Un solo atributo identifica la entidad (ej: CUIL para una persona)
> - **Clave Compuesta**: Varios atributos combinados identifican la entidad (ej: código de área + número de teléfono)
> 
> La clave primaria debe garantizar:
> - Unicidad (cada entidad es única)
> - Minimalidad (no tiene atributos innecesarios)
> ![[Representacion clave primaria.png]]



---
__TE SIENTES DETERMINADO__