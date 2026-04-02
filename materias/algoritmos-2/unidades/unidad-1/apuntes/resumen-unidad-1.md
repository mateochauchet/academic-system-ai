# Resumen — Algoritmos II — Unidad 1: Complejidad Algorítmica

## Conceptos clave

**1. Análisis de algoritmos**
Todo algoritmo debe ser finito, preciso, efectivo y eficiente. La eficiencia se mide en recursos: principalmente **tiempo** (pasos del algoritmo, no segundos reales) y memoria. El análisis se hace sobre el código, no ejecutándolo, para predecir el comportamiento con datos futuros.

**2. T(n) — Función de costo**
El tiempo de ejecución se expresa como T(n), donde n es el **tamaño de los datos de entrada** (puede ser el valor de un número, la longitud de un arreglo, etc.). Se analizan tres escenarios:
- **Mejor caso:** optimista, poco útil.
- **Peor caso:** el más usado. Garantiza que nunca va a ser peor que eso.
- **Caso promedio:** más informativo pero requiere asumir distribuciones de probabilidad.

**3. Notación O — Cota superior**
O(g(n)) es el conjunto de funciones que crecen *a lo más tan rápido* como g(n). Formalmente: existe una constante c y un n₀ tal que para todo n ≥ n₀, f(n) ≤ c·g(n). Es la notación más usada en la práctica porque describe el **peor caso**.

**4. Notación Ω — Cota inferior**
Ω(g(n)) contiene las funciones que crecen *al menos tan rápido* como g(n). Es la imagen espejo de O: g ∈ Ω(f) si y solo si f ∈ O(g). Describe el **mejor caso o mínimo garantizado**.

**5. Notación Θ — Cota ajustada**
Θ(g(n)) = O(g(n)) ∩ Ω(g(n)). Una función está en Θ(g) si crece **exactamente al mismo ritmo** que g — ni más rápido ni más lento. Es la notación más precisa: cuando podés usarla, sabés exactamente el orden.

**6. Órdenes de complejidad**
Las funciones se agrupan en clases de crecimiento. De menor a mayor costo:

| Notación | Nombre |
|---|---|
| O(1) | Constante |
| O(log n) | Logarítmica |
| O(n) | Lineal |
| O(n log n) | Casi lineal |
| O(n²) | Cuadrática |
| O(n³) | Cúbica |
| O(aⁿ) | Exponencial |

**7. Reglas de cálculo**
Para analizar un algoritmo instrucción por instrucción:
- Instrucción simple (asignación, comparación): O(1)
- Secuencia de instrucciones: O(máximo de los costos individuales)
- If-else: O(máximo entre las ramas)
- Bucle: O(iteraciones × costo del cuerpo)
- Bucles anidados: se multiplican los costos

---

## Cómo se relacionan

El análisis de algoritmos parte de contar los **pasos reales** que ejecuta el código (T(n)), pero eso produce funciones complicadas como 3n² + 5n - 7. Las notaciones asintóticas (O, Ω, Θ) permiten simplificar eso a lo que importa: el **término dominante**, ignorando constantes y términos menores. O da el techo (nunca peor que esto), Ω da el piso (nunca mejor que esto), y Θ los combina cuando ambos coinciden. En la práctica casi siempre se trabaja con O del peor caso, que es la garantía más útil.

---

## Ejemplos importantes

**Búsqueda secuencial → O(n)**
Si buscás un elemento en un arreglo recorriéndolo de a uno, en el peor caso revisás todos. El costo crece linealmente con n.

**Búsqueda binaria → O(log n)**
Cada paso descarta la mitad del arreglo. Con n = 1.000.000 elementos, solo necesitás ~20 pasos. Mucho más eficiente que la búsqueda secuencial.

**Recorrido de matriz cuadrada → O(n²)**
```
Para C <- 1 hasta N Hacer
    Para F <- 1 hasta N Hacer
        Mostrar M[F, C]
    FinPara
FinPara
```
Dos bucles anidados = n × n = n² pasos. Una matriz 100×100 implica 10.000 operaciones.

**Efecto práctico de duplicar n:**

| T(n) | n=100 | n=200 |
|---|---|---|
| log n | 1 h | 1.15 h |
| n | 1 h | 2 h |
| n² | 1 h | 4 h |
| 2ⁿ | 1 h | 1.27 × 10³⁰ h |

El exponencial hace que duplicar el input sea prácticamente imposible de manejar.

---

## Lo que suele entrar en el parcial

- **Definición formal de O, Ω y Θ** (saber escribirla con la fórmula)
- **Identificar el orden de un algoritmo** dado en pseudocódigo (aplicar las reglas de cálculo)
- **Comparar dos algoritmos** y decir cuál es más eficiente
- **Análisis de casos** (mejor, peor y promedio) para un algoritmo dado
- **Jerarquía de complejidades**: saber ordenarlas y entender qué significa que O(n²) ⊂ O(n³)
- Posiblemente: **ecuaciones de recurrencia** simples

---

## Preguntas de autocontrol

1. ¿Cuál es la diferencia entre O, Ω y Θ? ¿En qué situación usarías cada una?
2. Dado un pseudocódigo con dos bucles anidados (el externo va de 1 a n, el interno de 1 a n²), ¿cuál es su complejidad?
3. ¿Por qué se ignoran las constantes multiplicativas en el análisis asintótico? ¿Cuándo podría ser un problema ignorarlas?
4. ¿Qué diferencia hay entre T(n) = n y T(n) = 2n en términos de notación O? ¿Son del mismo orden?
5. Un algoritmo A tiene O(n log n) y otro B tiene O(n²). Para n = 10, ¿cuál ejecuta más pasos? ¿Y para n = 10.000?
