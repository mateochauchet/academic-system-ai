# Práctica — Unidad 3: Recursividad

28 ejercicios de programación recursiva.

---

## Recursión básica

**Problema 1** — Escribir una función recursiva que emita el n-ésimo término de la sucesión de Fibonacci.

**Problema 2** — Escribir una función recursiva que emita la suma `1+2+3+...+(n-1)+n`.

**Problema 3** — Escribir una función recursiva para calcular el término n-ésimo de la secuencia de Lucas: `1, 3, 4, 7, 11, 18, 29, 47, ...`

**Problema 4** — Escribir una función recursiva que devuelva la cantidad de dígitos de un número entero.

**Problema 5** — Escribir una función recursiva que calcule `w^k` mediante multiplicaciones sucesivas, siendo `k` un número natural.

**Problema 6** — Escribir un procedimiento recursivo que calcule `z*v` mediante sumas sucesivas, con `z`, `v` enteros.

**Problema 7** — Escribir un procedimiento recursivo para calcular el cociente y el resto entre dos números a partir de restas sucesivas.

**Problema 8** — Desarrollar un procedimiento recursivo que liste todos los pares de números positivos que son suma de un número dado.
> Ej: 5 = (1, 4) ; (2, 3)

**Problema 9** — Proponer un procedimiento recursivo tal que, dado un arreglo de números reales, permita calcular el mínimo elemento del vector y su posición.

**Problema 10** — Proponer una rutina recursiva tal que, dado un arreglo de números reales, permita calcular el promedio de sus elementos.

**Problema 11** — Escribir una función recursiva que dado un número entero positivo calcule su imagen especular.
> Ej: f(345) = 543

**Problema 12** — Función de Ackermann. Definida como:

```
A(M, N) = N+1              si M = 0
          A(M-1, 1)        si N = 0
          A(M-1, A(M,N-1)) si M≠0, N≠0
```

Desarrollar un algoritmo y una función recursiva que calculen A(M,N) para M≥0 y N≥0.

---

## Arreglos

**Problema 13** — Escribir un procedimiento recursivo que imprima el contenido de las posiciones pares de un arreglo de enteros.

**Problema 14** — La raíz cuadrada de un número positivo A puede calcularse con la fórmula iterativa:

```
R₁ = 1
Rᵢ = 1/2 * (Rᵢ₋₁ + A/Rᵢ₋₁)
```

Desarrollar una función recursiva que devuelva la raíz aproximada de un número X.

**Problema 15** — Escribir una función recursiva que calcule el producto escalar de dos vectores que recibe como parámetros.

**Problema 16** —
- a) Escribir una función que realice una búsqueda secuencial (lineal) de un elemento dentro de un arreglo de enteros.
- b) Ídem, pero para búsqueda binaria.

**Problema 17** — Escribir una función recursiva para calcular la suma de los elementos de un arreglo de enteros de dimensión N.

**Problema 18** — Escribir un procedimiento recursivo que emita los elementos de un vector.

**Problema 19** — Ídem anterior emitiendo los elementos en orden inverso.

**Problema 20** — Escribir una función recursiva que determine si una cadena de caracteres es un palíndromo.

**Problema 21** — Sea A un vector de N elementos. Programar los procesos recursivos que permitan:
- a) Hallar el producto de los elementos del arreglo (función y procedimiento)
- b) Verificar que un determinado elemento se encuentre en el arreglo (función)
- c) Calcular la posición de un determinado elemento, 0 si no se encuentra (función)
- d) Contar la cantidad de ocurrencias de un valor X en el arreglo (función)
- e) Imprimir los elementos de la siguiente forma:
  ```
  A1, A2, ..., AN
  A2, ..., AN
  ...
  AN
  ```
- f) Verificar si es igual a un arreglo B de N elementos (función)
- g) Calcular el promedio

---

## Matrices

**Problema 22** — Hacer una función recursiva que busque el elemento mínimo de una matriz cuadrada.

**Problema 23** — Hacer un procedimiento recursivo que devuelva los máximos de cada fila de una matriz de M×N.

**Problema 24** — Hacer una función lógica recursiva que determine si una matriz cuadrada de dimensión N es simétrica con respecto a su diagonal.

**Problema 25** — Desarrollar una función recursiva para determinar el elemento máximo de la triangular inferior de una matriz cuadrada de elementos reales. **No debe recorrer elementos innecesarios de la matriz.**

**Problema 26** — Definir un procedimiento recursivo que, dada una matriz cuadrada, genere un arreglo con los dobles de los elementos de la diagonal principal.

---

## Algoritmos matemáticos

**Problema 27** — Dados x y Tol, desarrollar una función recursiva que calcule el polinomio de Taylor para sen(x), generando términos sucesivos hasta encontrar uno menor a la tolerancia (en valor absoluto):

```
x - x³/3! + x⁵/5! - x⁷/7! + ... + (-1)ⁿ * x^(2n+1) / (2n+1)!
```

**Problema 28** — Dada una matriz de N×N (N positivo, N≤50) que contiene caracteres, construir un procedimiento recursivo que devuelva un arreglo de enteros indicando, por cada columna, la cantidad de veces que se repite el carácter ubicado en la diagonal principal de la matriz.

Ejemplo (N=4):
```
Matriz:            Resultado:
A  B  H  P         3
A  I  J  P         2
K  I  H  L         3
A  N  H  O         1
```
Los caracteres de la diagonal son A, I, H, O. Se cuenta cuántas veces aparece cada uno en su columna.
