# MergeSort

Desarrollado por **John von Neumann en 1948**.

**Objetivo**: ordenar un array de n elementos en orden ascendente.

---

## Ordenamiento

1. Tomar la secuencia de n elementos desordenados y dividirla en 2 subsecuencias de n/2 elementos cada una.
2. Ordenar las dos subsecuencias recursivamente utilizando MergeSort.
3. Mezclar las dos subsecuencias ordenadas obteniendo una secuencia ordenada.

---

## Ejemplo paso a paso

Array inicial: `[38, 27, 43, 3, 9, 82, 10]`

```
[38, 27, 43, 3, 9, 82, 10]
        ↙               ↘
[38, 27, 43, 3]     [9, 82, 10]
    ↙       ↘         ↙      ↘
[38, 27]  [43, 3]  [9, 82]  [10]
  ↙   ↘    ↙   ↘    ↙   ↘
[38] [27] [43] [3] [9] [82]
  ↘   ↙    ↘   ↙    ↘   ↙
[27, 38]  [3, 43]  [9, 82]  [10]
        ↘           ↙
    [3, 27, 38, 43]   [9, 10, 82]
                ↘       ↙
         [3, 9, 10, 27, 38, 43, 82]
```

---

## Etapas principales

1. `mergeSort` se inicia con el rango completo del arreglo.
2. Se divide en dos mitades: izquierda (`izq` a `med`) y derecha (`med+1` a `der`).
3. Se aplica `mergeSort` recursivamente a ambas mitades.
4. Se fusionan las dos mitades ordenadas con el procedimiento `merge`.

## Función de mezcla (`merge`)

Combina dos segmentos ordenados en uno solo. Usa dos arreglos auxiliares (`arrIzq` y `arrDer`) para almacenar temporalmente los elementos de cada mitad. Compara y mezcla los elementos de vuelta en el arreglo original.

---

## Pseudocódigo completo

```
PROCEDIMIENTO mergeSort (ref A: TARREGLO, val izq, der: ENTERO)
    VAR LOC: med: entero
    INICIO
        Si (izq < der) entonces
            med ← (izq + der) DIV 2
            mergeSort(A, izq, med)
            mergeSort(A, med+1, der)
            merge(A, izq, med, der)
        fSi
    FIN PROCED


PROCEDIMIENTO merge (ref A: TARREGLO, val izq, med, der: ENTERO)
VAR LOC
    I, J, K, aux1, aux2: entero
    arrIzq: arreglo de aux1 enteros     // array auxiliar izquierdo
    arrDer: arreglo de aux2 enteros     // array auxiliar derecho

INICIO
    aux1 ← med - izq + 1
    aux2 ← der - med

    Para I desde 1 hasta aux1 hacer    // copiando datos a arrays auxiliares
        arrIzq[I] ← A[izq + I - 1]
    fPara
    Para J desde 1 hasta aux2 hacer
        arrDer[J] ← A[med + J]
    fPara

    I ← 1                              // uniendo los datos de vuelta en A[izq...der]
    J ← 1
    K ← izq
    Mientras (I <= aux1) y (J <= aux2) hacer
        Si arrIzq[I] <= arrDer[J] entonces
            A[K] ← arrIzq[I]
            I ← I + 1
        sino
            A[K] ← arrDer[J]
            J ← J + 1
        fSi
        K ← K + 1
    fMientras

    Mientras I <= aux1 hacer           // copiando elementos remanentes de arrIzq, si quedan
        A[K] ← arrIzq[I]
        I ← I + 1
        k ← k + 1
    fMientras
    Mientras J <= aux2 hacer           // copiando elementos remanentes de arrDer, si quedan
        A[K] ← arrDer[J]
        J ← J + 1
        K ← K + 1
    fMientras
FIN PROCED
```

---

## Ventajas y desventajas

**Ventajas:**
- Eficiente para arreglos con muchos elementos
- Performance estable
- Conserva el orden relativo de elementos con claves iguales (*estable*)

**Desventajas:**
- Requiere espacio adicional en memoria para los arreglos auxiliares durante la mezcla
