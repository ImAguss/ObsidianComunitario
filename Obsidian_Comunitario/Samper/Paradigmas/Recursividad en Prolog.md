---
estado: Terminado
tags:
  - aprendizaje
  - prolog
  - recursion
  - algoritmos
proyecto: aprendizaje-prolog
Creacion: 2026-03-22T16:00:00
Revision: 2026-03-22T16:00:00
---
# Tabla de Contenidos

- [[#Principios básicos|Principios básicos]]
- [[#Ejemplo: Factorial|Ejemplo: Factorial]]
- [[#Errores comunes de diseño|Errores comunes de diseño]]
	- [[#Errores comunes de diseño#Recursión circular|Recursión circular]]
	- [[#Errores comunes de diseño#Recursión a izquierda|Recursión a izquierda]]
- [[#Ejemplo: Caminos en un grafo|Ejemplo: Caminos en un grafo]]
- [[#Patrón general|Patrón general]]
- [[#Diferencias con recursión en Python|Diferencias con recursión en Python]]
- [[#Relación con otros conceptos|Relación con otros conceptos]]
# Recursividad en Prolog

La recursividad en Prolog sigue principios diferentes a lenguajes imperativos. Se deriva de [[Lenguaje de Programación Prolog#Lenguaje de Programación Prolog|Prolog]] como técnica fundamental para definir predicados que operan sobre estructuras de tamaño variable.

## Principios básicos

Todo predicado recursivo en Prolog necesita:

1. **Caso base (parada)**: Una cláusula que termina la recursión
2. **Caso recursivo**: Al menos un argumento debe **crecer o decrecer** hacia el caso base

```prolog
% Caso base: termina la recursión
factorial(0, 1).

% Caso recursivo: N decrece hacia 0
factorial(N, R) :-
    N > 0,
    N1 is N - 1,
    factorial(N1, R1),
    R is N * R1.
```

Sin caso base, la recursión nunca termina. Sin decrecimiento, nunca alcanza el caso base.

## Ejemplo: Factorial

```prolog
factorial(0, 1).
factorial(N, R) :-
    N > 0,
    N1 is N - 1,
    factorial(N1, R1),
    R is N * R1.
```

**Consulta:** `?- factorial(3, K).`

**Traza paso a paso:**

```
factorial(3, K)
│
├─ ¿factorial(0, 1)? → No, N=3 ≠ 0
│
├─ factorial(3, R):
│   N > 0 ✓
│   N1 is 3 - 1 → N1 = 2
│   factorial(2, R1)
│   │
│   ├─ ¿factorial(0, 1)? → No, N=2 ≠ 0
│   │
│   ├─ factorial(2, R1):
│   │   N > 0 ✓
│   │   N1 is 2 - 1 → N1 = 1
│   │   factorial(1, R2)
│   │   │
│   │   ├─ ¿factorial(0, 1)? → No, N=1 ≠ 0
│   │   │
│   │   ├─ factorial(1, R2):
│   │   │   N > 0 ✓
│   │   │   N1 is 1 - 1 → N1 = 0
│   │   │   factorial(0, R3)
│   │   │   │
│   │   │   └─ factorial(0, 1) → R3 = 1 ✓ (CASO BASE)
│   │   │
│   │   │   R2 is 1 * 1 → R2 = 1
│   │   │
│   │   └─ R1 is 2 * 1 → R1 = 2
│   │
│   └─ R is 3 * 2 → R = 6
│
└─ K = 6
```

**Resultado:** `K = 6`

## Errores comunes de diseño

### Recursión circular

Una regla que se llama a sí misma sin avanzar hacia el caso base:

```prolog
% MAL: nunca termina
 ancestro(X, Y) :- ancestro(X, Z), ancestro(Z, Y).
```

No hay caso base, y no hay argumento que decrezca. El motor entra en bucle infinito.

**Corrección:**

```prolog
% BIEN: caso base + caso recursivo
ancestro(X, Y) :- padre(X, Y).           % Caso base
ancestro(X, Y) :- padre(X, Z), ancestro(Z, Y).  % Recursivo
```

### Recursión a izquierda

El predicado recursivo aparece **antes** de que se liguen las variables necesarias:

```prolog
% MAL: Recursión a izquierda
camino(Co, Cd, [X|Y]) :-
    camino(Ci, Cd, Y),      % Llamada recursiva ANTES de ligar Ci
    ruta(X, Co, Ci),
    Co \= Cd.
```

Prolog evalúa de izquierda a derecha. Si `Ci` no está ligado, `camino(Ci, Cd, Y)` genera soluciones infinitas.

**Corrección:**

```prolog
% BIEN: ligar variables ANTES de la llamada recursiva
camino(C, C, []).                      % Caso base
camino(Co, Cd, [X|Y]) :-
    Co \= Cd,
    ruta(X, Co, Ci),                   % Liga Ci primero
    camino(Ci, Cd, Y).                  % Luego recursión
```

## Ejemplo: Caminos en un grafo

Dados hechos de rutas entre ciudades:

```prolog
ruta(1, a, b).
ruta(2, a, c).
ruta(8, b, c).
ruta(3, b, d).
ruta(4, c, d).
```

**Predicado para encontrar caminos:**

```prolog
% Caso base: origen y destino coinciden
camino(C, C, []).

% Caso recursivo: buscar ruta intermedia
camino(Co, Cd, [X|Y]) :-
    Co \= Cd,
    ruta(X, Co, Ci),
    camino(Ci, Cd, Y).
```

**Consultas:**

```prolog
?- camino(a, c, X).
X = [2] ;           % Ruta directa: a → c
X = [1, 8].         % Ruta indirecta: a → b → c

?- camino(d, b, X).
false.              % No hay camino de d a b (grafo dirigido)
```

**Traza de `camino(a, c, X)`:**

```
1. camino(a, c, X)
   Co \= Cd ✓ (a ≠ c)
   ruta(X, a, Ci) → X=1, Ci=b (primera ruta desde a)
   camino(b, c, Y)
   │
   ├─ ¿camino(b, b, Y)? → No, Co=b, Cd=c, b ≠ c
   │
   └─ camino(b, c, Y)
       Co \= Cd ✓
       ruta(X, b, Ci) → X=8, Ci=c
       camino(c, c, Y)
       │
       └─ camino(c, c, []) ✓ (CASO BASE)

   Y = []
   X = [1, 8]      % Primera solución

Usuario presiona ";":

2. BACKTRACKING en ruta(X, a, Ci)
   → X=2, Ci=c (segunda ruta desde a)
   camino(c, c, Y)
   │
   └─ camino(c, c, []) ✓

   Y = []
   X = [2]          % Segunda solución
```

## Patrón general

```prolog
% Caso base: condición de terminación
predicado(Base, ...).

% Caso recursivo: acercarse al caso base
predicado(Recursivo, ...) :-
    condicion,
    acercar_a_base,
    predicado(MasCercanoABase, ...).
```

## Diferencias con recursión en Python

| Aspecto              | Python                    | Prolog                         |
| -------------------- | ------------------------- | ------------------------------ |
| Caso base            | `if` + `return`           | Cláusula separada              |
| Llamada recursiva    | Función que retorna valor | Predicado que unifica          |
| Variables            | Se reasignan              | Se ligan (no hay reasignación) |
| Múltiples soluciones | Una                       | Varias (backtracking)          |

## Relación con otros conceptos

- [[Backtracking en Prolog#Backtracking en Prolog|Backtracking en Prolog]]: Cada llamada recursiva crea puntos de elección
- [[Listas en Prolog#Listas en Prolog|Listas en Prolog]]: El procesamiento de listas es inherentemente recursivo
- [[Aritmética en Prolog#Aritmética en Prolog|Aritmética en Prolog]]: Necesario para decrementar contadores en recursión
- [[Recursion#¿Qué es la Recursión?|Recursion]]: Que es la recurison y comparacion con python

---
__TE SIENTES DETERMINADO__