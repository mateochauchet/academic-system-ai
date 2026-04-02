# Guía Unidad 1 — Complejidad Algorítmica
**Estructuras y Algoritmos de Datos II | CAECE**
Contenidista: Maximiliano López

---

## 1. Introducción

El tema central de esta unidad es la **eficiencia** de los algoritmos. Para eso, primero se repasan las características de todo algoritmo y luego se introduce la complejidad algorítmica como herramienta para medirla.

---

## 2. Análisis de Algoritmos

Un algoritmo es una **lista finita de instrucciones** que describe paso a paso y de manera precisa un proceso que, al finalizar, resuelve un problema perteneciente a una familia de problemas.

Todo algoritmo debe ser:

- **Finito**: tiene un inicio y un final definidos.
- **Preciso**: sin ambigüedades. Se usa pseudocódigo para garantizarlo.
- **Finaliza**: siempre termina su ejecución (no puede ser infinito).
- **Efectivo**: resuelve correctamente el problema para el que fue diseñado.
- **Eficiente**: consume la menor cantidad posible de espacio y tiempo.

---

### 2.1 Complejidad Algorítmica

La **complejidad algorítmica** es la medida de la cantidad de recursos temporales que necesita un algoritmo. Permite:

- Comprender el tiempo y el espacio que se utiliza para ejecutar un algoritmo.
- Determinar la eficiencia de un algoritmo.

---

### 2.2 Criterios

- La complejidad es **relativa al tamaño de los datos de entrada**, no es una medida absoluta.
- El **tiempo es independiente del hardware o software** donde se ejecute. Se mide en **pasos del algoritmo**.
- A la hora de evaluar el costo, se distinguen tres casos:
  - El **mejor caso**
  - El **peor caso**
  - El **caso promedio**

---

### 2.3 Tiempo de Ejecución

La complejidad temporal se expresa como **T(n)**, donde `n` representa el tamaño de los datos de entrada. Según el algoritmo, `n` puede ser:

- El dato en sí (por ejemplo, un número entero).
- La cantidad de elementos que lo componen (por ejemplo, el tamaño de un arreglo).

**Ejemplo:**

```
1  Suma <- 0
2  Mientras (A > 0) Hacer
3      Suma <- Suma + A
4      A <- A - 1
5  FinMientras
```

La cantidad de iteraciones depende del valor de `A`. Si A = 10 → 10 iteraciones; si A = 500 → 500 iteraciones. Por lo tanto: **T(A)**.

---

### 2.4 Análisis de Casos

Ejemplo con la **Búsqueda Secuencial Ordenada**:

```
1  POS <- -1
2  ESTA <- FALSO
3  Mientras (POS <= CE) Y (NO ESTA) Y (A[POS] <= DATO) Hacer
4      Si (A[POS] = DATO) entonces
5          ESTA <- VERDADERO
6      sino
7          POS <- POS + 1
8      finsi
9  FinMientras
```

- **Mejor caso**: DATO está en la primera posición.
- **Peor caso**: DATO es mayor que el último elemento, o está en la última posición.
- **Caso promedio**: DATO está o no está en una posición equiprobable (cualquier posición intermedia).

---

## 3. Funciones de Complejidad

El **orden de la función T(n)** expresa el comportamiento dominante del algoritmo para datos de gran tamaño. Este comportamiento se llama **comportamiento asintótico** y se expresa con las siguientes notaciones.

---

### 3.1 O Mayúscula — Cota Superior

El conjunto **O(g(n))** está formado por las funciones f(n) que crecen a un ritmo **menor o igual** que g(n).

```
O(g(n)) = { f: N → R⁺ | ∃ c constante positiva y n₀ ∈ N : f(n) ≤ c·g(n), ∀ n ≥ n₀ }
```

Significa que **f no crece más rápido que g**. Se llama Cota Superior porque limita superiormente el comportamiento asintótico.

---

### 3.2 Omega Ω — Cota Inferior

El conjunto **Ω(g(n))** está formado por las funciones f(n) que crecen a un ritmo **mayor o igual** que g(n).

```
Ω(g(n)) = { f: N → R⁺ | ∃ c constante positiva y n₀ ∈ N : 0 < c·g(n) ≤ f(n), ∀ n ≥ n₀ }
```

Significa que **f crece más rápido que g**. Se llama Cota Inferior porque limita inferiormente el comportamiento asintótico.

---

### 3.3 Theta Θ — Cota Ajustada

El conjunto **Θ(g(n))** está formado por las funciones f(n) que crecen **exactamente al mismo ritmo** que g(n).

```
Θ(g(n)) = { f: N → R⁺ | ∃ c₁, c₂ constantes positivas y n₀ ∈ N : 0 < c₁·g(n) ≤ f(n) ≤ c₂·g(n), ∀ n ≥ n₀ }
```

Significa que **f crece al mismo ritmo que g**. Se llama Cota Ajustada porque mantiene el mismo crecimiento asintótico.

---

## 4. Orden de Complejidad

La familia O(f(n)), Ω(f(n)), Θ(f(n)) define un **orden de complejidad** representado por la función f(n) más sencilla.

### Principales órdenes

| Orden      | Nombre      |
|------------|-------------|
| O(1)       | constante   |
| O(log n)   | logarítmica |
| O(n)       | lineal      |
| O(n log n) | casi lineal |
| O(n²)      | cuadrática  |
| O(n³)      | cúbica      |
| O(aⁿ)      | exponencial |

Jerarquía: `O(1) ⊂ O(log n) ⊂ O(n) ⊂ O(n log n) ⊂ O(n²) ⊂ O(n³) ⊂ O(aⁿ)`

---

### 4.1 Reglas de Cálculo

- **Instrucciones simples** (asignaciones, comparaciones, lectura/escritura, acceso a arreglos): `O(1)`

- **Secuencia de instrucciones**:
  ```
  T(S1; S2) = T(S1) + T(S2)
  O(T(S1; S2)) = max(O(T(S1)), O(T(S2)))
  ```

- **Condicional (if-then-else)**:
  ```
  O(T(IF-THEN-ELSE)) = max(O(T(condición)), max(O(T(rama THEN)), O(T(rama ELSE))))
  ```

- **Según (switch-case)**:
  ```
  O(T(SWITCH)) = max(O(T(condición), T(S1), ... T(Sn)))
  ```

- **Ciclos (while / do-while / for)**:
  ```
  O(T(BUCLE)) = (#iteraciones) * max(O(T(condición), T(cuerpo)))
  ```

- **Rutinas no recursivas**:
  ```
  O(T(RUTINA)) = max(O(T(S1), ... T(Sn)))
  ```

---

## 5. Ejemplos

### 5.1 Búsqueda Secuencial Ordenada → O(n)

El peor caso ocurre cuando el dato no está en el arreglo o está en la última posición. El número de pasos depende del tamaño del arreglo, por lo tanto:

**Complejidad: O(n)**

---

### 5.2 Búsqueda Binaria → O(log n)

En cada paso se descarta la mitad del arreglo. La complejidad crece, pero mucho más lento que n — crece de forma logarítmica.

```
1   IZQ <- -1
2   DER <- CE
3   ESTA <- FALSO
4   Mientras (IZQ <= DER) Y (NO ESTA) Hacer
5       MEDIO = (IZQ + DER) DIV 2
6       Si (A[MEDIO] < DATO) entonces
7           IZQ <- MEDIO + 1
8       Sino
9           Si (A[MEDIO] > DATO) entonces
10              DER <- MEDIO - 1
11          Sino
12              ESTA <- VERDADERO
13              POS <- MEDIO
14          Finsi
15      finsi
16  FinMientras
```

**Complejidad: O(log n)**

---

### 5.3 Recorrido de Matriz Cuadrada → O(n²)

Dos ciclos anidados que recorren `CANT` filas y `CANT` columnas. En una matriz 2×2 se recorren 4 elementos; en una 3×3, 9 elementos. El crecimiento es cuadrático.

```
1  Para C <- 1 hasta CANT Hacer
2      Para F <- 1 hasta CANT Hacer
3          Mostrar M[F, C]
4      FinPara
5  FinPara
```

**Complejidad: O(n²)**

---

## 6. Conclusiones

Un algoritmo es **eficiente** cuando utiliza la menor cantidad de espacio y tiempo. La **complejidad algorítmica** permite medirlo, analizando el **mejor, peor y caso promedio**, y expresando el resultado con el **orden de complejidad** correspondiente.

---

## Bibliografía

- Bisbal Riera, J. (2013). *Manual de algorítmica: recursividad, complejidad y diseño de algoritmos.* Editorial UOC.
- Sedgewick, R. y Wayne, K. (2011). *Algorithms.* 4th Edition. Addison-Wesley.
- Cormen, T. et al. (2022). *Introduction to algorithms.* 4th Edition. The MIT Press.
