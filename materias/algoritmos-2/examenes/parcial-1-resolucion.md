# Parcial 1 — Resolución
**Materia:** Estructuras y Algoritmos de Datos II  
**Fecha:** 4/5/2026 — 5/5/2026  
**Unidades:** I a III

---

## Punto 1

**Consigna:** Desarrolle una rutina recursiva que muestre los elementos de un arreglo en orden inverso (del último al primero).

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

**Llamada:** `MostrarInverso(A, n)` donde `n` es el tamaño del arreglo.

**Lógica:** imprime `A[n]`, luego `A[n-1]`, ..., hasta `A[1]`. Cuando `tope` llega a 0 no entra al `Si` y termina.

---

## Punto 2

**Consigna:** Dado el algoritmo iterativo de Búsqueda Secuencial, realizar una rutina equivalente de manera recursiva.

```
// PRE: CE >= 0, I >= 1
Función BusquedaSecuencialRec (ref A: TARR_ENTERO, val CE, DATO, I: ENTERO): BOOLEAN
    Si I > CE entonces
        BusquedaSecuencialRec ← FALSO
    sino
        Si A[I] = DATO entonces
            BusquedaSecuencialRec ← VERDADERO
        sino
            BusquedaSecuencialRec ← BusquedaSecuencialRec(A, CE, DATO, I + 1)
        fSi
    fSi
fFunc
```

**Llamada:** `BusquedaSecuencialRec(A, CE, DATO, 1)`

---

## Punto 3

**Consigna:** Verificar el correcto funcionamiento de la rutina `MostrarDigitos`. Indicar errores o especificaciones faltantes.

**Errores encontrados:**

1. **`N RESTO 10` debería ser `N DIV 10`** en la llamada recursiva. `N RESTO 10` devuelve el último dígito (un número de un solo dígito), por lo que la recursión termina ahí y solo muestra ese dígito. `N DIV 10` quita el último dígito y reduce el problema hacia el caso base.
2. **Falta `Mostrar(N RESTO 10)` después de la llamada recursiva.** Sin esto, solo se muestra el primer dígito.
3. **Tipo de retorno incorrecto:** declara `: ENTERO` pero nunca devuelve nada. Debe ser un `PROCEDIMIENTO`.
4. **`ref` debe ser `val`:** el parámetro N no se modifica.
5. **Falta PRE:** `// PRE: N >= 0`.

**Versión corregida:**

```
// PRE: N >= 0
PROCEDIMIENTO MostrarDigitos (val N: ENTERO)
INICIO
    Si N DIV 10 = 0 entonces
        Mostrar(N)
    Sino
        MostrarDigitos(N DIV 10)
        Mostrar(N RESTO 10)
    FinSi
FIN PROCEDIMIENTO
```

**Seguimiento con N = 123:**
```
MostrarDigitos(123) → MostrarDigitos(12) → MostrarDigitos(1) → Mostrar(1)
                                         ← Mostrar(2)
                   ← Mostrar(3)
Resultado: 1  2  3
```

---
