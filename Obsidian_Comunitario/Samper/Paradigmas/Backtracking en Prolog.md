---
estado: Terminado
tags:
  - aprendizaje
  - prolog
  - backtracking
  - busqueda
proyecto: aprendizaje-prolog
Creacion: 2026-03-22T15:30:00
Revision: 2026-03-22T17:45:00
---
# Tabla de Contenidos

- [[#Concepto|Concepto]]
- [[#Orden de búsqueda|Orden de búsqueda]]
- [[#Funcionamiento paso a paso|Funcionamiento paso a paso]]
- [[#Patrón de búsqueda|Patrón de búsqueda]]
- [[#Ejemplo completo|Ejemplo completo]]
- [[#No determinismo|No determinismo]]
- [[#Puntos de elección|Puntos de elección]]
- [[#Control del backtracking|Control del backtracking]]
- [[#Relación con otros conceptos|Relación con otros conceptos]]
# Backtracking en Prolog

El backtracking es el mecanismo de búsqueda con retroceso que permite encontrar **todas las soluciones** de una consulta. Se deriva de [[Lenguaje de Programación Prolog#Lenguaje de Programación Prolog|Prolog]] como parte fundamental de su motor de inferencia.

## Concepto

Cuando Prolog busca una solución y encuentra un camino sin salida, **retrocede** al último punto donde había alternativas y prueba otra opción. Esto permite explorar todo el árbol de búsqueda.

## Orden de búsqueda

El motor busca:
1. **De arriba hacia abajo** — recorre cláusulas en orden
2. **De izquierda a derecha** — evalúa subobjetivos en secuencia

```
Objetivo: abuelo(A, N) :- padre(A, P), padre(P, N)
                                ↑           ↑
                            1er subobj   2do subobj
```

## Funcionamiento paso a paso

El motor:
1. Resuelve 1er subobjetivo → liga variables
2. Con esas ligaduras, resuelve 2do subobjetivo
3. ¿Encontró solución? → muestra resultado
4. Usuario pide más (`;`) → **backtracking en último subobjetivo**
5. ¿Agotó opciones en último? → **backtracking en anterior**
6. Repite hasta agotar todo

## Patrón de búsqueda

Es [**búsqueda en profundidad**](https://es.wikipedia.org/wiki/B%C3%BAsqueda_en_profundidad) (depth-first):
- El último subobjetivo agota sus opciones primero
- Luego retrocede al subobjetivo anterior
- Los subobjetivos anteriores "esperan" como puntos de elección

```
padre(A, P) ──────► prueba cláusulas
     │
     │    padre(P, N) ──► prueba cláusulas
     │         │
     │         ├── opción 1 → solución
     │         ├── opción 2 → solución (si ";")
     │         └── agotó → RETROCEDE
     │
     ├── RETROCEDE a padre(A, P) → siguiente cláusula
     │
     │    padre(P, N) ──► vuelve a probar todo
     │         │
     │         └── ...
```

## Ejemplo completo

```prolog
% Hechos
hombre(homero).
hombre(pericles).
hombre(tio_cosas).
hombre(lucas).
hombre(abuelo).
mujer(morticia).
mujer(merlina).
mujer(abuela).
padre(homero, pericles).
padre(abuelo, homero).
padre(abuelo, lucas).
padre(homero, merlina).
madre(morticia, pericles).

% Reglas
hijo(X, Y) :- hombre(X), padre(Y, X).
hijo(X, Y) :- hombre(X), madre(Y, X).
```

**Consulta:** `?- hijo(X, homero).`

**Traza paso a paso:**

```
1. hijo(X, homero) unifica con regla 1: hijo(X, Y) :- hombre(X), padre(Y, X)
   → Y = homero
   → Objetivos: hombre(X), padre(homero, X)

2. hombre(X) → X = homero (primera cláusula)
   [Punto de elección: más cláusulas hombre/1]

3. padre(homero, homero) → NO EXISTE → FALLA

4. BACKTRACKING en hombre(X)
   → X = pericles

5. padre(homero, pericles) → EXISTE ✓
   → SOLUCIÓN: X = pericles

6. Usuario presiona ";"
   → BACKTRACKING en padre(homero, X)
   → Busca siguiente padre(homero, ...) → padre(homero, merlina)
   → pericles ≠ merlina → NO UNIFICA → FALLA

7. BACKTRACKING en hombre(X)
   → X = tio_cosas
   → padre(homero, tio_cosas) → NO EXISTE → FALLA

8. Continúa probando: hombre(lucas), hombre(abuelo)...
   → Todos fallan con padre(homero, X)

9. Agotó regla 1 → BACKTRACKING a regla 2
   → hijo(X, Y) :- hombre(X), madre(Y, X)

10. Repite proceso con hombre(X) y madre(homero, X)...
```

**Solución:** `X = pericles`

## No determinismo

El backtracking permite que Prolog sea **no determinista**: una consulta puede tener múltiples soluciones. El usuario decide si quiere todas (`;`) o conformarse con la primera.

```prolog
?- padre(X, Y).
X = homero, Y = pericles ;
X = abuelo, Y = homero ;
X = abuelo, Y = lucas ;
...
```

## Puntos de elección

Cada vez que Prolog encuentra múltiples cláusulas que pueden unificar, crea un **punto de elección**. Si el camino actual falla, retrocede al punto de elección más reciente.

```prolog
% Hechos
color(rojo).
color(verde).
color(azul).

% Consulta
?- color(X).
X = rojo ;      % Primer punto de elección
X = verde ;     % Segundo punto de elección
X = azul.       % Último, no hay más opciones
```

## Control del backtracking

A veces se quiere **evitar** el backtracking. Se usa el **corte** (`!`):

```prolog
max(X, Y, X) :- X >= Y, !.    % Si X >= Y, corte: no buscar más
max(X, Y, Y) :- X < Y.
```

El corte congela las decisiones tomadas hasta ese punto, impidiendo retroceder.

## Relación con otros conceptos

- [[Lenguaje de Programación Prolog#Unificación|Unificación]]: Mecanismo base que permite el backtracking
- [[Programación Logica#Fundamentos|Programación Lógica]]: El backtracking es una característica del paradigma
- [[Recursion#¿Qué es la Recursión?|Recursión]]: Los predicados recursivos generan múltiples puntos de elección

---
__TE SIENTES DETERMINADO__