# Apuntes sobre el cálculo de la eficiencia de los algoritmos
**Autor:** José L. Balcázar — Dept. Llenguatges i Sistemes Informàtics

---

## Contenido

1. Introducción y motivación
2. El tamaño de los datos
3. Las notaciones asintóticas y sus propiedades
4. Formas de crecimiento frecuentes
5. Algunas precauciones a tomar
6. Cálculo del coste
7. Ecuaciones recurrentes

---

## 1. Introducción y motivación

El objetivo al desarrollar un programa es minimizar el consumo de recursos. La **eficiencia es un concepto relativo**: un algoritmo es más eficiente que otro si realiza las mismas tareas con menos recursos.

Medir la eficiencia implica medir los recursos necesarios para la ejecución, principalmente:
- **Tiempo de cálculo** (el más importante)
- Memoria interna
- Memoria secundaria (en algunos casos)

El análisis se basa en las instrucciones del algoritmo, no en ejecutarlo, para poder predecir su comportamiento ante datos futuros.

### El problema de las dependencias

Los recursos consumidos dependen de:
- La **máquina** y el **compilador** → varían por factores constantes
- El **tamaño de los datos** → puede cambiar drásticamente (duplicar, elevar al cuadrado)

Por eso se expresa la eficiencia en función del tamaño de datos y se hace independiente de factores multiplicativos constantes.

---

## 2. El tamaño de los datos

Antes de analizar un algoritmo hay que definir qué se entiende por "tamaño de los datos":

- Para enteros: puede ser el **valor** en sí, o el **tamaño de su representación binaria** (logarítmico en el valor). Importante especificarlo porque difieren en una exponencial.
- Para vectores o archivos: generalmente es la **cantidad de elementos**, si estos no alcanzan tamaños considerables.

### Análisis del caso peor vs. caso medio

- **Caso peor:** el más usado. Es pesimista pero siempre válido.
- **Caso mejor:** demasiado optimista, poco útil en la práctica.
- **Caso medio:** requiere una distribución de probabilidad sobre las entradas. Más informativo pero más complejo.

---

## 3. Las notaciones asintóticas

Clasifican funciones por su **velocidad de crecimiento** (orden de magnitud). Se basan en el comportamiento límite → definen el **coste asintótico**.

### 3.1 O mayúscula (cota superior)

`O(f)` = conjunto de funciones g que crecen **a lo más tan rápido** como f.

```
O(f) = { g | ∃c₀ ∈ ℝ⁺, ∃n₀ ∈ ℕ, ∀n ≥ n₀ : g(n) ≤ c₀ · f(n) }
```

Propiedades:
1. **Invariancia multiplicativa:** `g ∈ O(f) ⟺ c·g ∈ O(f)`
2. **Reflexividad:** `f ∈ O(f)`
3. **Transitividad:** si `h ∈ O(g)` y `g ∈ O(f)` → `h ∈ O(f)`
4. **Criterio de caracterización:** `g ∈ O(f) ⟺ O(g) ⊆ O(f)`
5. **Regla de la suma:** `O(f + g) = O(max(f, g))`
6. **Regla del producto:** si `g₁ ∈ O(f₁)` y `g₂ ∈ O(f₂)` → `g₁·g₂ ∈ O(f₁·f₂)`
7. **Invariancia aditiva:** `g ∈ O(f) ⟺ c + g ∈ O(f)`

### 3.2 o minúscula (cota superior estricta)

`o(f)` = funciones g que crecen **estrictamente más lento** que f.

```
o(f) = { g | ∀c₀ ∈ ℝ⁺, ∃n₀ ∈ ℕ, ∀n ≥ n₀ : g(n) ≤ c₀ · f(n) }
```

Diferencia con O: el cuantificador sobre c₀ es universal (∀) en lugar de existencial (∃).

Propiedades:
1. **Invariancia multiplicativa:** `g ∈ o(f) ⟺ c·g ∈ o(f)`
2. **Invariancia aditiva:** `g ∈ o(f) ⟺ c + g ∈ o(f)`
3. **Antirreflexividad:** `f ∉ o(f)`
4. **Caracterización en términos de O:** `g ∈ o(f)` si y solo si `g ∈ O(f)` pero `f ∉ O(g)`. En particular: `o(f) ⊂ O(f)` (inclusión propia)
5. **Otra relación con O:** `g ∈ o(f) ⟺ O(g) ⊆ o(f)`
6. **Transitividad:** si `h ∈ o(g)` y `g ∈ o(f)` → `h ∈ o(f)`
7. **Caracterización por límites:** `g ∈ o(f) ⟺ lim(n→∞) g(n)/f(n) = 0`

### 3.3 Omega Ω (cota inferior)

Existen dos versiones:

**ΩK(f)** (Knuth): g crece por encima de f **desde algún punto en adelante**.
```
ΩK(f) = { g | ∃c₀ ∈ ℝ⁺, ∃n₀ ∈ ℕ, ∀n ≥ n₀ : g(n) ≥ c₀ · f(n) }
```

**Ω∞(f)**: g supera a f en **infinitas ocasiones** (útil cuando g oscila fuertemente).
```
Ω∞(f) = { g | ∃c₀ ∈ ℝ⁺, ∀n₀ ∈ ℕ, ∃n ≥ n₀ : g(n) ≥ c₀ · f(n) }
```

Relación con O: `g ∈ ΩK(f) ⟺ f ∈ O(g)`

### 3.4 Theta Θ (cota ajustada)

Funciones con la **misma tasa de crecimiento** que f.

```
Θ(f) = O(f) ∩ ΩK(f)
```

Propiedades clave:
- `g ∈ Θ(f) ⟺ (g ∈ O(f) y f ∈ O(g)) ⟺ O(f) = O(g)`
- **Condición de límite:** si `lim(n→∞) g(n)/f(n)` existe, es finito y no cero → `g ∈ Θ(f)`
- **Simetría:** `g ∈ Θ(f) ⟺ f ∈ Θ(g)`
- **Regla de la suma:** `Θ(f + g) = Θ(max(f, g))`

---

## 4. Formas de crecimiento frecuentes

| Orden | Nombre |
|-------|--------|
| Θ(log n) | Logarítmico |
| Θ(n) | Lineal |
| Θ(n · log n) | Cuasilineal |
| Θ(n²) | Cuadrático |
| Θ(n³) | Cúbico |
| Θ(nᵏ) con k fijo | Polinómico |
| Θ(kⁿ) con k fijo | Exponencial |

Jerarquía: `O(1) ⊂ O(log n) ⊂ O(n) ⊂ O(n log n) ⊂ O(n²) ⊂ O(n³) ⊂ O(kⁿ) ⊂ O(n!) ⊂ O(nⁿ)`

Se considera **eficiente** un algoritmo que alcanza coste cuasilineal. Cualquier coste superior a polinómico (y polinómicos de grado alto) son **intratables** en la práctica.

---

## 5. Precauciones a tomar

Las notaciones asintóticas **ocultan constantes multiplicativas**. Esto puede llevar a errores de interpretación:

Un algoritmo con mejor orden asintótico pero **constante oculta alta** puede ser más lento en la práctica que uno con peor orden pero constante pequeña, especialmente para datos de tamaño moderado.

Sin embargo, esto es la excepción. Para tamaños de datos prácticos, los algoritmos con mejor crecimiento asintótico suelen ser preferibles.

Otro factor a considerar: el **tiempo de desarrollo** del programa. Un algoritmo muy eficiente pero complejo puede no justificarse si el programa solo va a ejecutarse pocas veces.

---

## 6. Cálculo del coste

Para calcular el coste de un algoritmo se combinan los costes de todas sus instrucciones. Por la **regla de la suma**, el coste de una secuencia de instrucciones coincide con el **máximo** de los costes individuales.

### Reglas prácticas

- **Instrucciones simples** (asignación, operaciones booleanas, aritméticas sobre datos pequeños): coste constante.
- **Secuencia de instrucciones:** coste = máximo de los costes individuales.
- **Alternativa (if-else):** coste = máximo de las ramas (análisis del caso peor).
- **Bucle:** coste = suma de los costes de cada iteración. Si el número de vueltas depende del tamaño de datos, no se puede aplicar directamente la regla de la suma.
- **Llamada a función/procedimiento:** requiere analizar la rutina previamente. Si es recursiva, aparece una ecuación de recurrencia.

---

## 7. Ecuaciones recurrentes

El análisis de algoritmos recursivos produce una función T(n) definida en términos de sí misma → **ecuación de recurrencia**.

### Teorema general

Dadas las recurrencias:

```
T1(n) = { f(n)              si 0 ≤ n < c
         { a·T1(n-c) + b·nᵏ  si n ≥ c

T2(n) = { g(n)              si 0 ≤ n < c
         { a·T2(n/c) + b·nᵏ  si n ≥ c
```

Sus órdenes de magnitud son:

**T1 — datos decrecen aritméticamente (n - c):**

| Condición | Resultado |
|-----------|-----------|
| a < 1 | Θ(nᵏ) |
| a = 1 | Θ(nᵏ⁺¹) |
| a > 1 | Θ(aⁿ/ᶜ) |

**T2 — datos decrecen geométricamente (n/c):**

| Condición | Resultado |
|-----------|-----------|
| a < cᵏ | Θ(nᵏ) |
| a = cᵏ | Θ(nᵏ · log n) |
| a > cᵏ | Θ(n^log_c(a)) |

> Este es el **Teorema Maestro** en su forma general.

### Observación importante

Un decrecimiento **geométrico** (n/c) es casi siempre preferible a uno **aritmético** (n-c), ya que produce costes sustancialmente menores (puede significar pasar de exponencial a polinómico).

Los valores más frecuentes de k son:
- **k = 0:** el trabajo adicional es constante (solo llamadas recursivas)
- **k = 1:** el trabajo adicional es lineal

---

## Referencias

- Aho, Hopcroft, Ullman (1983). *Data structures and algorithms.* Addison-Wesley.
- Brassard, Bratley (1987). *Algorithmique: conception et analyse.* Masson.
- Knuth (1973). *The art of computer programming 1.* Addison-Wesley.
- Mehlhorn (1984). *Data structures and algorithms 1.* Springer-Verlag.
- Wirth (1986). *Algorithms and data structures.* Prentice-Hall.
