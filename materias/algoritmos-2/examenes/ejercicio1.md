## Punto 1

Consigna: Desarrolle una rutina recursiva que muestre los elementos de un arreglo en orden inverso (del último al primero).

```
// PRE: tope >= 0
PROCEDIMIENTO MostrarInverso (ref A: arreglo[CMAX] de entero, val tope: entero)
INICIO
    Si tope >= 1 entonces
        Mostrar(A[tope])
        MostrarInverso(A, tope - 1)
    fSi
FIN PROCEDIMIENTO
```