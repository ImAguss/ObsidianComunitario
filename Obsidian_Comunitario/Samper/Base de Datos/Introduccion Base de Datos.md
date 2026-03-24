---
estado: Terminado
tags:
  - aprendizaje
  - facultad
  - base_de_datos
  - estructuras
proyecto: base-de-datos
Creacion: 2026-03-23T17:18:00
Revision: 2026-03-23T17:31:00
---
# Introduccion Base de Datos

## ¿Qué es una Base de Datos?

Conjunto de datos relacionados entre sí, referidos a hechos conocidos que pueden registrarse. Tiene un significado y representa una realidad particular (Minimundo, Universo de Discurso, Dominio). Es de propósito específico con tamaño y complejidad variable, mantenida manualmente o por computadora.

## ¿Qué es un SGBD (Sistema de Gestión de Base de Datos)?

Conjunto de programas encargado de almacenar y gestionar los datos dentro de una base de datos. También conocido como DBMS (Database Management System) o "Motor de Base de Datos".

### Objetivo
Almacenar y recuperar datos de manera eficiente. Permite definir, construir y manipular los datos de distintas BD para distintas aplicaciones.


> [!info]
> ### Contenido
> No solo contiene la base de datos del negocio, sino también la definición de los objetos que la componen. Esa definición se almacena en el **diccionario o catálogo del sistema**.


## Evolución de las Bases de Datos

| Etapa | Descripción |
|-------|-------------|
| **BD Pre-Relacionales** | Modelos en red, jerárquico y ficheros planos |
| **BD Relacionales** | Modelo Relacional (Codd, 1970), Sistemas finales del 80 |
| **BD Post-Relacionales** (2010+) | SGBD basados en otros modelos; los relacionales se extienden |

Las BD Relacionales son las más utilizadas para aplicaciones tradicionales. Las BD Post-Relacionales se usan en nuevos tipos de aplicaciones donde los relacionales no ofrecen la performance necesaria.

## Bases de Datos vs Archivos Tradicionales

| Bases de Datos | Archivos Tradicionales |
|----------------|------------------------|
| Datos integrados y no repetidos | Islas de datos, datos repetidos |
| Separación entre programas y datos | Estructura de archivos dentro de los programas |
| Inconsistencia controlada por SGBD | Inconsistencia no controlada (programas) |
| Manejo de concurrencia (SGBD) | Anomalías de acceso concurrente |
| Restricciones de seguridad e integridad facilitadas | Restricciones manejadas por programas |
| Múltiples vistas con diferentes niveles de seguridad | Problemas de seguridad |

## El SGBD como Capa Intermedia

El SGBD abstrae toda la complejidad técnica para que:

| Actor | Se enfoca en... | No se preocupa por... |
|-------|-----------------|----------------------|
| **Programadores** | Diseñar estructura lógica, escribir consultas SQL | Almacenamiento físico, manejo de archivos, concurrencia |
| **Usuarios finales** | Usar aplicaciones, hacer consultas | Implementación técnica |

El usuario/programador nunca accede directamente a los archivos de datos. Siempre lo hace a través del SGBD.

> [!important]
> ## El Diccionario de Datos
> 
> Es donde la SGBD guarda la **estructura** de la base de datos, no los datos en sí. Contiene metadatos: datos sobre los datos.
> 
> ### Contenido del Diccionario
> - ¿Qué tablas existen?
> - ¿Qué columnas tiene cada tabla?
> - ¿Qué tipos de datos?
> - ¿Qué claves primarias/foráneas?
> - ¿Qué índices?
> - ¿Qué usuarios tienen permisos?
> - ¿Qué vistas existen?
> 
> ### Funciones
> - Validar consultas (si existe la tabla)
> - Controlar tipos de datos
> - Verificar permisos
> - Optimizar consultas usando índices
> 
> **Analogía**: El diccionario es el "plano" de cómo está construida la BD. Sin diccionario, la SGBD no sabría qué es válido y qué no.
> 

## Arquitectura de 3 Niveles

El SGBD provee una visión abstracta de los datos en 3 niveles:

```
Nivel Externo (Vistas)     →  Usuario ve solo lo que necesita
         ↓
Nivel Lógico (Tablas base) →  Programador ve estructura lógica
         ↓
Nivel Físico (Archivos)    →  DBA/OS ve cómo se guardan en disco
```


> [!important]
> ### Nivel Externo (Vistas)
> Cada usuario/rol ve solo lo que necesita. Son **tablas virtuales** que no almacenan datos, solo definen qué mostrar.
> 
> ### Nivel Lógico
> Estructura lógica de los datos: tablas, columnas, relaciones.
> 
> ### Nivel Físico
> Cómo se almacenan físicamente los datos en disco: archivos, índices, particiones.


## Diferentes Vistas

Las vistas son perspectivas personalizadas de los datos según el rol del usuario.

**Características:**
- No duplican datos
- Son "lentes" distintas para ver lo mismo
- Si actualizás una vista (y es actualizable), cambiás la tabla real

**Ventajas:**
- **Seguridad**: Datos sensibles ocultos según rol
- **Simplicidad**: El usuario ve solo lo relevante
- **Independencia**: Si cambia la estructura interna, la vista puede seguir igual

## Actores en el SGBD

### Programadores de aplicación
Desarrollan aplicaciones convencionales y aplicaciones en línea.

### Usuarios finales
Acceden a través de aplicaciones o realizan consultas no planeadas.

### Administrador de Datos (DA)
Define qué datos serán almacenados y las políticas para mantener y manejar los datos (ej. seguridad: usuarios, backup, etc.).

### Administrador de la Base de Datos (DBA)
Implementa las decisiones del DA:
- Crea la base de datos
- Implementa los controles
- Responsable de que el sistema opere con la performance adecuada

## Éxito de las BD Relacionales

### ¿Por qué dominaron?

| Factor | Explicación |
|--------|-------------|
| **Modelo matemático sólido** | Basado en teoría de conjuntos y álgebra relacional (Codd, 1970). Fundamentos formales, predecible. |
| **Independencia lógico-física** | El programador escribe SQL sin saber dónde ni cómo se guardan los datos. |
| **SQL estándar** | Un lenguaje para todo. Aprendés una vez, sirve en Oracle, PostgreSQL, MySQL... |
| **Transacciones ACID** | Garantizan: Atomicidad, Consistencia, Aislamiento, Durabilidad. Crítico para bancos, ERP, sistemas financieros. |
| **Integridad referencial** | Las claves foráneas aseguran que los datos relacionados sean consistentes. |
| **Madurez del ecosistema** | +40 años de desarrollo. Herramientas, documentación, profesionales capacitados. |

### El trade-off que eligieron

Las relacionales priorizan **consistencia sobre disponibilidad**: si hay un error, mejor que no se haga nada. Los datos deben estar siempre correctos, sacrificando velocidad por confiabilidad.

---

## Modelos de Bases de Datos: Comparación

### BD Relacionales (SQL)

Basadas en el modelo relacional de Codd (1970). Estructura de tablas con filas y columnas, relacionadas mediante claves.

**Características:**
- Esquema fijo definido antes de insertar datos
- Relaciones naturales entre tablas mediante JOINs
- Transacciones ACID garantizadas
- Escalabilidad vertical (más potencia en un servidor)

**Ejemplos:** PostgreSQL, MySQL, Oracle, SQL Server

**Cuándo usar:** Datos estructurados, relaciones complejas, transacciones críticas (bancos, ERP, sistemas financieros)

---

> [!info]
> ### BD NoSQL (Post-Relacionales)
> 
> Surgen porque las relacionales **no escalaban bien** para ciertos problemas modernos: redes sociales, IoT, big data, tiempo real. Priorizan **disponibilidad y velocidad** sobre consistencia inmediata.
> 
> #### Documentos
> 
> Almacenan datos en formato JSON/BSON. Esquema flexible, ideal para datos semi-estructurados.
> 
> **Ejemplos:** MongoDB
> 
> **Cuándo usar:** Catálogos de productos con atributos variables, contenido CMS, prototipos rápidos
> 
> #### Clave-Valor
> 
> Estructura simple: una clave apunta a un valor. Extremadamente rápida.
> 
> **Ejemplos:** Redis
> 
> **Cuándo usar:** Caché, sesiones de usuario, colas de mensajes
> 
> #### Columnas
> 
> Datos organizados en familias de columnas en lugar de filas. Optimizado para escrituras masivas.
> 
> **Ejemplos:** Cassandra
> 
> **Cuándo usar:** Logs, sensores IoT, big data, alta disponibilidad
> 
> #### Grafos
> 
> Datos representados como nodos y relaciones. Las conexiones son ciudadanas de primera clase.
> 
> **Ejemplos:** Neo4j
> 
> **Cuándo usar:** Redes sociales, rutas, recomendaciones, detección de fraudes
> 

---

## ACID vs BASE

### ACID (Relacionales)

| Propiedad | Significado |
|-----------|-------------|
| **Atomicidad** | Todo se ejecuta o nada se ejecuta |
| **Consistencia** | La BD pasa de un estado válido a otro válido |
| **Aislamiento** | Transacciones concurrentes no interfieren |
| **Durabilidad** | Una vez confirmado, el dato persiste |

### BASE (NoSQL)

| Propiedad | Significado |
|-----------|-------------|
| **Basically Available** | El sistema siempre responde |
| **Soft state** | El estado puede cambiar sin input externo (réplicas) |
| **Eventually consistent** | Los datos se actualizan eventualmente, no inmediatamente |

---

## Teorema CAP

En sistemas distribuidos, solo se pueden garantizar 2 de 3 propiedades:

```
           Consistency
              (C)
              /\
             /  \
            /    \
           /      \
          /________\
Availability      Partition tolerance
     (A)                (P)
```

| Combinación | Enfoque | Ejemplo |
|-------------|---------|---------|
| **C + P** | Consistencia total, puede no responder si hay fallo | PostgreSQL, Oracle |
| **A + P** | Siempre responde, datos pueden estar desactualizados | Cassandra, MongoDB |

**No se pueden tener las tres** cuando hay particiones de red.

---

## Consistencia Eventual en NoSQL

En sistemas distribuidos, los datos se replican en varios nodos. Cuando se escribe un dato, no se actualiza en todos al mismo tiempo.

```
Ejemplo: Sistema de likes

    [Nodo A] ← Usuario 1 lee: 100 likes
        |
    [Nodo B] ← Usuario 2 escribe: +1 like (ahora 101)
        |
    [Nodo C] ← Usuario 3 lee: 100 likes (aún no se replicó)
```

El Usuario 3 ve datos "desactualizados" temporalmente. Eventualmente todos los nodos se sincronizan.

**Es aceptable para:** redes sociales, likes, comentarios, feeds
**No es aceptable para:** transferencias bancarias, inventario crítico

---

## Comparación Resumida

| Aspecto | Relacionales (SQL) | NoSQL |
|---------|-------------------|-------|
| **Esquema** | Fijo, definido antes | Flexible, dinámico |
| **Escalabilidad** | Vertical (más potencia) | Horizontal (más nodos) |
| **Transacciones** | ACID garantizado | Eventual consistency (BASE) |
| **Consultas** | SQL estándar, complejas | API específica, limitadas |
| **Relaciones** | Naturales (JOINs) | Difíciles o inexistentes |
| **Consistencia** | Fuerte, inmediata | Eventual |
| **Disponibilidad** | Puede bloquearse | Siempre responde |
| **Mejor para** | Datos estructurados, transacciones | Datos variables, alta velocidad |

---

## ¿Cuándo usar cada tipo?

| Situación | Recomendación |
|-----------|--------------|
| Sistema bancario, financiero | Relacional (PostgreSQL, Oracle) |
| Catálogo de productos con atributos variables | Documentos (MongoDB) |
| Sesiones de usuario, caché | Clave-valor (Redis) |
| Red social, rutas, recomendaciones | Grafo (Neo4j) |
| Logs, sensores IoT, big data | Columnas (Cassandra) |

---
__TE SIENTES DETERMINADO__