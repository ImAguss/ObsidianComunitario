---
estado: EnProceso
tags:
  - aprendizaje
  - base_de_datos
  - entidad/relacion
  - estructuras
proyecto: base-de-datos
Creacion: 2026-03-23T22:52:00
Revision: 2026-03-23T22:52:00
---
# Modelo Entidad Relacion Extendido

## Introducción al Proceso de Diseño

El diseño de una base de datos atraviesa diferentes etapas que dependen de los requisitos del usuario. Estos requisitos se clasifican en dos tipos complementarios:

- **Requisitos de Datos**: Qué datos guardar, cómo estructurarlos, qué relaciones existen entre ellos.
- **Requisitos Funcionales**: Qué debe hacer el sistema (ej: "buscar clientes por nombre", "generar reportes mensuales", "validar CUIL de 11 dígitos").
- **Requisitos No Funcionales**: Cómo debe comportarse el sistema (ej: "tiempo de respuesta < 2 segundos", "soportar 1000 usuarios concurrentes", "cifrar datos sensibles"). Incluyen accesibilidad, usabilidad, seguridad, rendimiento, escalabilidad.

### Flujo de Diseño según Requisitos de Datos

![[Diagrama de etapas de diseño.png|553]]

Cuando los requisitos son de datos, el proceso sigue este camino:

```
Requisitos de Datos → Diseño Conceptual → Esquema Conceptual → Diseño Lógico → Esquema Lógico → Elección de SGBD → Diseño Físico
```

1. **Diseño Conceptual**: Se modela el minimundo usando el Modelo Entidad/Relación Extendido.
2. **Esquema Conceptual**: Resultado del diseño conceptual en forma de diagrama ER.
3. **Diseño Lógico**: Mapeo del esquema conceptual al modelo relacional (tablas).
4. **Esquema Lógico**: Resultado del diseño lógico.
5. **Elección de SGBD**: Se analiza qué Sistema de Gestión de Base de Datos utilizar.
6. **Diseño Físico**: Implementación final considerando el SGBD elegido.

## Deriva a las notas
[[Entidades]]
[[Relaciones]]
[[Restricciones Estructurales de las Relaciones]]
[[Atributos vs Entidades]]
[[SuperClases - SubClases]]
[[Entidades Debiles]]
[[Agregacion]]

---
__TE SIENTES DETERMINADO__