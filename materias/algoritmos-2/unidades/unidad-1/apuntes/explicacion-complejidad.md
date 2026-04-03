# Diferencia entre O, Ω y Θ — Algoritmos II Unidad 1

## La analogía

Imaginá que tenés que llegar de tu casa a la facultad y querés saber cuánto tardás.

- **O (cota superior):** "Nunca tardo más de 1 hora." — es el **techo**. El peor escenario posible.
- **Ω (cota inferior):** "Nunca tardo menos de 10 minutos." — es el **piso**. El mejor escenario posible.
- **Θ (cota ajustada):** "Siempre tardo entre 25 y 35 minutos." — es el **rango real**. Techo y piso coinciden en el mismo orden.

## Aplicado a algoritmos

Tomá la búsqueda secuencial sobre un arreglo de n elementos:

- **O(n):** en el peor caso recorro todo el arreglo. El costo nunca supera n pasos.
- **Ω(1):** en el mejor caso encuentro el dato en la primera posición. El costo nunca baja de 1 paso.
- **Θ(?):** acá no podés poner un Θ único porque el mejor y el peor caso son órdenes distintos (1 vs n). Θ solo aplica cuando ambos coinciden.

Tomá el recorrido de una matriz cuadrada (dos for anidados):

- Siempre recorre exactamente n² celdas, sin importar qué haya adentro.
- Mejor caso = peor caso = n².
- Entonces sí podés decir **Θ(n²)** — el costo es exactamente ese orden, siempre.

## Cuándo usás cada una

**O** es la que más vas a usar. Cuando analizás un algoritmo, lo que querés saber es el peor caso: ¿cuánto puede tardar a lo sumo?

**Ω** aparece cuando querés demostrar que un problema *no puede* resolverse más rápido de cierto límite. Por ejemplo, ordenar n elementos requiere como mínimo Ω(n log n) comparaciones.

**Θ** solo la podés usar cuando el mejor y el peor caso son del mismo orden. Cuando podés afirmar Θ, estás diciendo que el algoritmo *siempre* se comporta así, sin importar los datos.

## Resumen en una línea cada una

- **O(g):** el algoritmo nunca tarda *más* que g. (techo)
- **Ω(g):** el algoritmo nunca tarda *menos* que g. (piso)
- **Θ(g):** el algoritmo siempre tarda *exactamente* en el orden de g. (piso = techo)
