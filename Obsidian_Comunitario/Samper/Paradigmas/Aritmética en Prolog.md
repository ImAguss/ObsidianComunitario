---
estado: Terminado
tags:
  - aprendizaje
  - prolog
  - aritmetica
  - evaluacion
proyecto: aprendizaje-prolog
Creacion: 2026-03-22T15:00:00
Revision: 2026-03-22T15:00:00
---
# Tabla de Contenidos

- [[#El problema|El problema]]
- [[#`=` vs `is`|`=` vs `is`]]
- [[#El predicado `is`|El predicado `is`]]
	- [[#El predicado `is`#Variables libres vs ligadas|Variables libres vs ligadas]]
- [[#Operadores aritméticos|Operadores aritméticos]]
- [[#Predicados aritméticos predefinidos|Predicados aritméticos predefinidos]]
	- [[#Predicados aritméticos predefinidos#`succ/2` — Sucesor|`succ/2` — Sucesor]]
	- [[#Predicados aritméticos predefinidos#`plus/3` — Suma|`plus/3` — Suma]]
	- [[#Predicados aritméticos predefinidos#`abs/1` — Valor absoluto|`abs/1` — Valor absoluto]]
- [[#Notación de argumentos|Notación de argumentos]]
- [[#Comparaciones aritméticas|Comparaciones aritméticas]]
- [[#Errores comunes|Errores comunes]]
	- [[#Errores comunes#Confundir `=` con `is`|Confundir `=` con `is`]]
	- [[#Errores comunes#Olvidar que `is` requiere variables ligadas|Olvidar que `is` requiere variables ligadas]]
	- [[#Errores comunes#Usar `=` para comparar resultados|Usar `=` para comparar resultados]]
# Aritmética en Prolog

Prolog no evalúa expresiones aritméticas automáticamente. Se deriva de [[Lenguaje de Programación Prolog#Lenguaje de Programación Prolog|Prolog]] como mecanismo para realizar cálculos.

## El problema

En la mayoría de los lenguajes, `6 = 4 + 2` evalúa a `true`. En Prolog:

```prolog
?- 6 = 4 + 2.
false.
```

El `=` **no evalúa**, solo unifica. `6` no es igual al término `4 + 2`.

## `=` vs `is`

| Operador | Qué hace | Ejemplo | Resultado |
|----------|----------|---------|-----------|
| `=` | Unifica (sin evaluar) | `N = 4 + 2` | `N = 4+2` (expresión sin evaluar) |
| `is` | Evalúa y unifica | `N is 4 + 2` | `N = 6` |

**Ejemplos:**

```prolog
?- 6 = 6.
true.                    % Unifica 6 con 6

?- 6 = 4 + 2.
false.                   % 6 no es igual al término (4 + 2)

?- N = 4 + 2.
N = 4+2.                 % N se liga a la expresión sin evaluar

?- 6 is 4 + 2.
true.                    % Evalúa 4+2=6, luego 6=6

?- N is 4 + 2.
N = 6.                   % Evalúa primero, luego liga N
```

## El predicado `is`

`is` funciona en dos pasos:
1. **Evalúa** la expresión del lado derecho
2. **Unifica** el resultado con el lado izquierdo

### Variables libres vs ligadas

```prolog
?- N is 4 + 2.
N = 6.                   % N estaba libre, se liga

?- N is N + 1.
ERROR: Arguments are not sufficiently instantiated
```

Si `N` está libre, `is` no puede evaluar `N + 1`. La expresión debe tener **todas sus variables ligadas** para poder evaluarse.

```prolog
?- N = 4, N is N + 1.
false.                   % N=4 ligada, evalúa 4+1=5, luego 4=5 → false
```

## Operadores aritméticos

| Operador | Operación |
|----------|-----------|
| `+` | Suma |
| `-` | Resta |
| `*` | Multiplicación |
| `/` | División |
| `mod` | Módulo (resto) |
| `//` | División entera |
| `**` | Potencia |

## Predicados aritméticos predefinidos

### `succ/2` — Sucesor

Para números naturales:

```prolog
?- succ(3, X).
X = 4.

?- succ(X, 5).
X = 4.

?- succ(X, 0).
false.                   % No existe natural anterior a 0

?- succ(X, -1).
ERROR: Domain error     % Solo funciona con naturales
```

### `plus/3` — Suma

```prolog
?- plus(2, 3, X).
X = 5.

?- plus(2, X, 7).
X = 5.

?- plus(X, 3, 7).
X = 4.
```

Al menos dos de los tres argumentos deben estar instanciados a enteros.

### `abs/1` — Valor absoluto

```prolog
?- X is abs(-5).
X = 5.

?- X is abs(5).
X = 5.
```

## Notación de argumentos

En la documentación de Prolog se usa:

| Símbolo | Significado |
|---------|-------------|
| `+` | Parámetro de entrada (debe estar instanciado) |
| `-` | Parámetro de salida (debe estar libre) |
| `?` | Parámetro de entrada o salida |

Ejemplo: `succ(?Int1, ?Int2)` — ambos pueden ser entrada o salida.

## Comparaciones aritméticas

Para comparar resultados de expresiones:

| Operador | Significado |
|----------|-------------|
| `=:=` | Igualdad aritmética |
| `=\=` | Desigualdad aritmética |
| `<` | Menor que |
| `>` | Mayor que |
| `=<` | Menor o igual |
| `>=` | Mayor o igual |

**Importante:** `=<` (menor o igual), no `<=` (ese es otro operador en Prolog).

```prolog
?- 3 + 2 =:= 5.
true.                    % Evalúa ambos lados y compara

?- 3 + 2 =:= 6.
false.

?- X = 3, X + 2 > 4.
true.                    % X debe estar ligada para evaluar
```

## Errores comunes

### Confundir `=` con `is`

```prolog
% MAL: intenta unificar N con la expresión
factorial(0, N) :- N = 1.

% BIEN: evalúa y unifica
factorial(0, N) :- N is 1.
```

### Olvidar que `is` requiere variables ligadas

```prolog
% ERROR: N está libre, no se puede evaluar N + 1
?- N is N + 1.
ERROR: Arguments are not sufficiently instantiated

% BIEN: primero ligar, luego evaluar
?- N = 4, M is N + 1.
N = 4, M = 5.
```

### Usar `=` para comparar resultados

```prolog
% MAL: unifica, no compara
?- X = 3, X = 2 + 1.
false.                   % X=3 y 2+1 son términos distintos

% BIEN: comparar aritméticamente
?- X = 3, X =:= 2 + 1.
true.
```

---
__TE SIENTES DETERMINADO__