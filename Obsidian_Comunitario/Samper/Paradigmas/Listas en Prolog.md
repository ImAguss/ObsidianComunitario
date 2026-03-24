---
estado: Terminado
tags:
  - aprendizaje
  - prolog
  - listas
  - estructuras
proyecto: aprendizaje-prolog
Creacion: 2026-03-22T14:00:00
Revision: 2026-03-22T15:46:00
---
# Tabla de Contenido

- [[#Sintaxis|Sintaxis]]
	- [[#Sintaxis#Cabeza y Cola|Cabeza y Cola]]
	- [[#Sintaxis#Estructura interna|Estructura interna]]
	- [[#Sintaxis#Notaciones válidas|Notaciones válidas]]
- [[#Predicados predefinidos|Predicados predefinidos]]
	- [[#Predicados predefinidos#Ejemplos|Ejemplos]]
- [[#Predicados personalizados|Predicados personalizados]]
	- [[#Predicados personalizados#Longitud de una lista|Longitud de una lista]]
	- [[#Predicados personalizados#Suma de elementos positivos|Suma de elementos positivos]]
	- [[#Predicados personalizados#Constructor (cons)|Constructor (cons)]]
- [[#Patrón de recursión con listas|Patrón de recursión con listas]]
- [[#Relación con otros conceptos|Relación con otros conceptos]]
# Listas en Prolog

Las listas son la estructura que permite representar un **conjunto de elementos** en Prolog. Se derivan de [[Lenguaje de Programación Prolog#Lenguaje de Programación Prolog|Prolog]] como estructura fundamental para manejo de colecciones.

## Sintaxis

Una lista se representa entre corchetes:

```prolog
[1, 2, 3]       % Lista con 3 elementos
[]              % Lista vacía
[[a, b], [c]]   % Lista de listas
```

### Cabeza y Cola

Para operar con listas, se separa en **cabeza** (primer elemento) y **cola** (resto de la lista):

```prolog
[Cabeza | Cola]
```

El operador `|` se comporta como **analizador y constructor**:

```prolog
?- [H|T] = [1, 2, 3, 4].
H = 1,
T = [2, 3, 4].

?- [X, Y | Z] = [a, b, c, d].
X = a,
Y = b,
Z = [c, d].
```

### Estructura interna

Una lista es una **estructura anidada**. `[1, 2, 3]` equivale a:

```
[1 | [2 | [3 | []]]]
```

La cola **siempre es una sublista**:
- `[1, 2, 3]` → cola `[2, 3]`
- `[2, 3]` → cola `[3]`
- `[3]` → cola `[]`

Esto permite procesar listas recursivamente: operar sobre la cabeza y delegar el resto a la sublista (cola).

### Notaciones válidas

**Con constantes:**
```prolog
[3, 5, 7]           % Lista con 3 elementos
[3 | [5, 7]]        % Equivalente a [3, 5, 7]
[a, b, [c, d, e]]   % Lista con sublista
```

**Con variables:**
```prolog
[X | Y]             % Cabeza en X, cola en Y
[X, Y | Z]          % Dos primeras en X e Y, resto en Z
[X | [Y | Z]]       % Cabeza en X, segunda en Y, resto en Z
```

## Predicados predefinidos

SWI-Prolog proporciona predicados para el manejo de listas:

| Predicado | Descripción |
|-----------|-------------|
| `is_list(Term)` | Verifica si `Term` es una lista |
| `length(List, Len)` | `Len` es la longitud de `List` |
| `sort(List, Sorted)` | `Sorted` es `List` ordenada sin duplicados |
| `append(L1, L2, L3)` | `L3` es la concatenación de `L1` y `L2` |
| `member(Elem, List)` | `Elem` es elemento de `List` |
| `nextto(X, Y, List)` | `Y` está después de `X` en `List` |
| `delete(L1, Elem, L2)` | `L2` es `L1` sin `Elem` |
| `nth0(Index, List, Elem)` | `Elem` es el elemento en posición `Index` (desde 0) |
| `reverse(L1, L2)` | `L2` es `L1` invertida |

### Ejemplos

```prolog
?- is_list([1, 2, 3]).
true.

?- is_list(X).
false.              % Variable libre no es lista

?- length([a, b, c], N).
N = 3.

?- append([1, 2], [3, 4], L).
L = [1, 2, 3, 4].

?- member(X, [a, b, c]).
X = a ;
X = b ;
X = c.

?- nth0(1, [a, b, c], X).
X = b.              % Índice comienza en 0
```

## Predicados personalizados

### Longitud de una lista

```prolog
longitud([], 0).
longitud([_|T], R) :- longitud(T, R1), R is R1 + 1.
```

```prolog
?- longitud([2, 4, 3, 7, 1], X).
X = 5.
```

### Suma de elementos positivos

```prolog
suma_positivos([], 0).
suma_positivos([H|T], R) :-
    H > 0,
    suma_positivos(T, R1),
    R is R1 + H.
suma_positivos([H|T], R) :-
    H =< 0,
    suma_positivos(T, R).
```

### Constructor (cons)

Agrega un elemento al inicio de una lista:

```prolog
cons(X, L, Z) :- Z = [X|L].
```

```prolog
?- cons(1, [2, 3], Z).
Z = [1, 2, 3].

?- cons(a, [b, c], Z).
Z = [a, b, c].
```

## Patrón de recursión con listas

El patrón típico para procesar listas en Prolog:

```prolog
mi_predicado([], ...).              % Caso base: lista vacía
mi_predicado([H|T], ...) :-        % Caso recursivo
    % procesar H
    mi_predicado(T, ...).           % llamada recursiva con cola
```

1. **Caso base**: Definir qué pasa con la lista vacía
2. **Caso recursivo**: Procesar la cabeza y llamar recursivamente con la cola

## Relación con otros conceptos

- [[Lenguaje de Programación Prolog#Backtracking|Backtracking]]: Al buscar elementos, Prolog puede encontrar todas las soluciones
- [[Recursion#¿Qué es la Recursión?|Recursión]]: El procesamiento de listas en Prolog es inherentemente recursivo

---
__TE SIENTES DETERMINADO__