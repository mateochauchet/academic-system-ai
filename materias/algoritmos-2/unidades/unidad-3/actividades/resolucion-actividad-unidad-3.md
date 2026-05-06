# Actividad Unidad 3 — Resolución

## Consigna

Desarrollar un procedimiento recursivo tal que, dado un arreglo de números reales, permita calcular el mínimo elemento del vector y su posición.

---

## Resolución

```
Procedimiento MinRecursivo(val A: arreglo de REAL, val i: ENTERO, val n: ENTERO,
                           ref minVal: REAL, ref minPos: ENTERO)
INICIO
    Si i = n - 1 Entonces
        minVal <- A[i]
        minPos <- i
    Sino
        MinRecursivo(A, i + 1, n, minVal, minPos)
        Si A[i] < minVal Entonces
            minVal <- A[i]
            minPos <- i
        FinSi
    FinSi
FIN
```

