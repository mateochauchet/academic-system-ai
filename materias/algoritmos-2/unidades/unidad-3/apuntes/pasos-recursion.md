# Pasos para diseñar una recursión

Ante cualquier ejercicio recursivo, hacete estas tres preguntas en orden:

1. **Caso base** — ¿cuándo el problema es tan chico que lo resolvés directo, sin llamarte de nuevo?
2. **Reducir** — ¿cómo achicás el problema para acercarte al caso base? (decrementar, quitar elemento, dividir a la mitad...)
3. **Combinar** — ¿qué hacés con el resultado de la llamada recursiva para armar la respuesta final?

---

## Ejemplo: Fibonacci

- **Caso base**: `n = 0` → 0, `n = 1` → 1 (los sé de memoria)
- **Reducir**: necesito `fibo(n-1)` y `fibo(n-2)`
- **Combinar**: sumo los dos → `fibo(n-1) + fibo(n-2)`

```
// PRE: n >= 0
Función Fibo(val n: entero): entero
    Si n >= 2 entonces
        Fibo ← Fibo(n-1) + Fibo(n-2)
    sino
        Fibo ← n
    fSi
fFunc
```
