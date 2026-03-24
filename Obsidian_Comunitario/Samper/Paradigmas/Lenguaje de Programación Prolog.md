---
estado: Terminado
tags:
  - aprendizaje
  - logico
  - prolog
  - programacion
proyecto: aprendizaje-prolog
Creacion: 2026-03-21T22:37:00
Revision: 2026-03-21T23:15:00
---
# Tabla de Contenidos

- [[#Propósito|Propósito]]
- [[#Filosofía|Filosofía]]
- [[#Sintaxis Básica|Sintaxis Básica]]
	- [[#Sintaxis Básica#Aridad|Aridad]]
	- [[#Sintaxis Básica#Hechos|Hechos]]
	- [[#Sintaxis Básica#Reglas|Reglas]]
	- [[#Sintaxis Básica#Consultas (Goals)|Consultas (Goals)]]
- [[#Unificación|Unificación]]
	- [[#Unificación#Reglas de unificación|Reglas de unificación]]
	- [[#Unificación#Ejemplo|Ejemplo]]
	- [[#Unificación#Propagación de ligaduras|Propagación de ligaduras]]
- [[#Backtracking|Backtracking]]
- [[#Predicados de Entrada/Salida|Predicados de Entrada/Salida]]
- [[#Para tener en cuenta|Para tener en cuenta]]
- [[#Derivaciones|Derivaciones]]
# Lenguaje de Programación Prolog

**PROgrammation en LOGique** — implementación más extendida del paradigma de [[Programación Logica#Programación Logica|programación lógica]]. Desarrollado en 1972 en la Universidad de Aix-Marseille por Alain Colmerauer y Philippe Roussel.

## Propósito

Fue diseñado originalmente para:
- Procesamiento de lenguaje natural
- Demostración automática de teoremas

Hoy se usa para: sistemas expertos, procesamiento de lenguaje natural, bases de datos deductivas, verificación de software, planificación (IA clásica).

## Filosofía

El programador declara **relaciones**, no procedimientos. No se indica "cómo" resolver algo, sino "qué" es verdad. El motor de inferencia se encarga del resto.

## Sintaxis Básica

| Elemento | Convención | Ejemplo |
|----------|------------|---------|
| Átomos | Minúsculas | `maria`, `homero`, `x` |
| Variables | Mayúsculas o `_` | `X`, `Persona`, `_` |
| Predicados | `nombre/aridad` | `padre/2`, `hijo/1` |

### Aridad

El número de argumentos de un predicado. `padre/2` significa que `padre` toma 2 argumentos. Puede tomar valores de 0 a n.

### Hechos

Cláusulas sin cuerpo — verdades absolutas:

```prolog
hombre(homero).
hombre(pericles).
mujer(morticia).
padre(abuelo, homero).
madre(morticia, pericles).
```

### Reglas

Cláusulas con cabeza y cuerpo — verdades condicionales:

```prolog
hijo(X, Y) :- hombre(X), padre(Y, X).
hijo(X, Y) :- hombre(X), madre(Y, X).
```

Traducción: "X es hijo de Y SI X es hombre Y Y es padre de X"

### Consultas (Goals)

Preguntas al sistema:

```prolog
?- hijo(X, homero).
X = pericles ;
X = ...
```

## Unificación
 
El motor no "compara" variables con cláusulas, ni tampoco usa el "Pasaje por parametros" conocido en otros lenguajes. **Unifica** el objetivo con la cabeza de cada cláusula.

> [!question] Consulta Sobre Unificacion
> Si bien "entiendo" mas o menos que es unificar, no logro comprender esta definicion en su totalidad. Seria ligar literalmente? El hecho de que este para el scope de la regla solamente hace que basicamente el backtracking no interfiera en esa ligadura?


### Reglas de unificación

| Lado izquierdo | Lado derecho | ¿Unifica? | Resultado |
|----------------|--------------|-----------|-----------|
| Variable libre | Cualquier cosa | **Sí** | Variable se liga |
| Valor concreto | Mismo valor | **Sí** | Sin cambios |
| Valor concreto | Valor distinto | **No** | Falla |
| Variable ligada | Su valor | **Sí** | Ya está ligada |
| Variable ligada | Otro valor | **Depende** | Si coincide sí, si no no |

### Ejemplo

```prolog
?- padre(X, bart).
% X está libre → unifica con padre(homero, bart)
% Resultado: X = homero

?- padre(homero, X).
% X libre → unifica con cualquier padre(homero, ...)
% Resultado: X = bart ; X = lisa ; ...

?- padre(homero, bart).
% Sin variables → solo verifica existencia
% Resultado: true
```

### Propagación de ligaduras

Cuando una variable se liga, el valor se propaga a toda la regla, perteneciendo al scope(alcance) de la misma:

```prolog
hijo(X, Y) :- padre(Y, X).
```

Consulta: `?- hijo(bart, Y).`

1. `hijo(bart, Y)` unifica con `hijo(X, Y)`
2. `X = bart` (se liga)
3. Ahora evalúa `padre(Y, bart)` con `X` ya ligado
4. `Y` se liga cuando encuentra un hecho que unifique

## Backtracking

Mecanismo de búsqueda con retroceso que permite encontrar **todas las soluciones** de una consulta. Cuando Prolog encuentra un camino sin salida, retrocede al último punto donde había alternativas y prueba otra opción. Ver [[Backtracking en Prolog]] para detalles completos.

El motor busca **de arriba hacia abajo** y **de izquierda a derecha**, creando puntos de elección en cada bifurcación.

## Predicados de Entrada/Salida

| Predicado | Descripción |
|-----------|--------------|
| `read(X)` | Lee un término del canal de entrada (teclado) |
| `write(X)` | Escribe el término X en el canal de salida (display) |
| `write_ln(X)` | Escribe X y salta línea |
| `nl` | Genera nueva línea |
| `tab(X)` | Escribe X espacios |

## Para tener en cuenta

- El nombre del predicado debe ser representativo de la realidad
- Todos los predicados de igual nombre deben ir juntos en el código
- Los argumentos se escriben con minúsculas (átomos)
- Solo las variables van con mayúsculas
- No existe pasaje de parámetros tradicional — trabaja con unificación
- Los argumentos pueden funcionar como entrada o salida, pero no ambos simultáneamente

## Derivaciones

- [[Aritmética en Prolog]] — evaluación de expresiones y operadores aritméticos
- [[Backtracking en Prolog]] — mecanismo de búsqueda con retroceso
- [[Listas en Prolog]] — estructura fundamental para manejo de colecciones
- [[Recursividad en Prolog]] — técnica para predicados sobre estructuras variables

---
__TE SIENTES DETERMINADO__