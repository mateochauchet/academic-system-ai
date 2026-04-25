# QuickSort

Desarrollado por **Charles Hoare en 1960**.

**Objetivo**: ordenar un array de n elementos en orden ascendente.

---

## Ordenamiento

1. Partir el array `A[INICIO...FIN]` en dos subarrays reorganizando los elementos:
   - `A[INICIO...q-1]` → todos menores o iguales a `A[q]`
   - `A[q+1...FIN]` → todos mayores a `A[q]`
2. Ordenar los dos subarrays mediante llamados recursivos a QuickSort.
3. El array `A[INICIO...FIN]` termina ordenado.

---

## Ejemplo paso a paso

Array inicial: `[9, -3, 5, 2, 6, 8, -6, 1, 3]` — pivote = 3 (último elemento)

```
                              Pivot
         9  -3   5   2   6   8  -6   1  [3]

            <=3                  >=3
    -3   2  -6  [1]   3    8   5   9  [6]

  <=1          >=1        <=6         >=6
-3  -6  [1]    2      5  [6]      9  [8]
                6          8
  >= -6
[-6]  -3             [8]   9
   4     5                    11
```

Los elementos en corchetes son los pivotes de cada partición.

---

## Funciones auxiliares

**particion**: reorganiza los elementos alrededor del pivote. Coloca el pivote en su posición final (menores a la izquierda, mayores a la derecha). Devuelve la posición final del pivote.

**intercambiar**: intercambia dos elementos en el arreglo.

---

## Pseudocódigo completo

```
PROCEDIMIENTO quickSort (ref A: TARREGLO, val INICIO, FIN: ENTERO)
VAR LOC
    Q: ENTERO
INICIO
    Si (INICIO < FIN) entonces
        Q ← particion(A, INICIO, FIN)
        quickSort(A, INICIO, q-1)
        quickSort(A, q+1, FIN)
    fSi
FIN PROCEDIMIENTO

FUNCIÓN particion (ref A: TARREGLO, val INICIO, FIN: ENTERO); ENTERO
VAR LOC
    I, J, pivot: entero
INICIO
    pivot ← A[FIN]
    I ← INICIO - 1
    para J ← INICIO hasta FIN-1 hacer
        si A[J] <= pivot entonces
            I ← I + 1
            intercambiar(A[I], A[J])
        fSi
    fPara
    intercambiar(A[I+1], A[FIN])
    particion ← I + 1
FIN FUNCIÓN

PROCEDIMIENTO intercambiar (reg A, B: ENTERO)
VAR LOC
    AUX: ENTERO
INICIO
    AUX ← A
    A ← B
    B ← AUX
FIN PROCEDIMIENTO
```

---

## Ventajas

- Muy eficiente para arreglos con muchos elementos
- Algoritmo *in situ*: ordena sin requerir memoria adicional
- La elección del pivote es clave: un mal pivote puede degradar la performance. El pivote ideal es el elemento con valor cercano al promedio del arreglo.
