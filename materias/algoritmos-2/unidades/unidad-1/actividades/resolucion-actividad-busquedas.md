# Actividad Unidad 1 — Búsqueda Secuencial y Binaria
**Estructuras y Algoritmos de Datos II | CAECE**

---

## Consigna

Realizar el algoritmo y analizar la complejidad algorítmica para:
- Búsqueda secuencial
- Búsqueda binaria

---

## Búsqueda Secuencial

### Algoritmo

```
Función BusquedaSecuencial(A, n, dato)
    POS <- 0
    ENCONTRADO <- FALSO

    Mientras (POS < n) Y (NO ENCONTRADO) Hacer
        Si A[POS] = dato Entonces
            ENCONTRADO <- VERDADERO
        Sino
            POS <- POS + 1
        FinSi
    FinMientras

    Si ENCONTRADO Entonces
        Retornar POS
    Sino
        Retornar -1
    FinSi
FinFunción
```

### Análisis de complejidad

Recorre el arreglo elemento por elemento hasta encontrar el dato o llegar al final.

- **Mejor caso — Ω(1):** el dato está en la primera posición. Una sola comparación.
- **Peor caso — O(n):** el dato no está, o está al final. Se recorren los n elementos.
- **Caso promedio — Θ(n):** en promedio el dato está en el medio (n/2 comparaciones), lo que sigue siendo orden lineal.

**Complejidad: O(n)**

---

## Búsqueda Binaria

> Requiere que el arreglo esté **ordenado**.

### Algoritmo

```
Función BusquedaBinaria(A, n, dato)
    IZQ <- 0
    DER <- n - 1
    ENCONTRADO <- FALSO

    Mientras (IZQ <= DER) Y (NO ENCONTRADO) Hacer
        MEDIO <- (IZQ + DER) DIV 2

        Si A[MEDIO] = dato Entonces
            ENCONTRADO <- VERDADERO
        Sino
            Si dato < A[MEDIO] Entonces
                DER <- MEDIO - 1
            Sino
                IZQ <- MEDIO + 1
            FinSi
        FinSi
    FinMientras

    Si ENCONTRADO Entonces
        Retornar MEDIO
    Sino
        Retornar -1
    FinSi
FinFunción
```

### Análisis de complejidad

En cada iteración se descarta la mitad del arreglo. La pregunta clave es: ¿cuántas veces puedo dividir n entre 2 hasta llegar a 1? La respuesta es log₂(n).

- **Mejor caso — Ω(1):** el dato está justo en el medio. Una sola iteración.
- **Peor caso — O(log n):** se divide el arreglo hasta que queda un solo elemento.

Con n = 1.000.000: log₂(1.000.000) ≈ 20 pasos (vs 1.000.000 de la secuencial).

**Complejidad: O(log n)**

---

## Comparación

| | Mejor caso | Peor caso | Requisito |
|---|---|---|---|
| Secuencial | Ω(1) | O(n) | Ninguno |
| Binaria | Ω(1) | O(log n) | Arreglo ordenado |

La binaria es mucho más eficiente en el peor caso. El trade-off es que necesita el arreglo ordenado previamente.
