# Unidad 3 — Recursividad

## Introducción

En esta unidad se presenta una nueva forma de resolver problemas: la **Recursividad**. A diferencia del proceso iterativo, el proceso recursivo encuentra la solución usando su propia definición.

---

## 1.1 El proceso autoreferencial

La recursividad es una rutina que **se invoca a sí misma**. El proceso mediante el cual se halla la solución deseada utiliza su propia definición para lograrlo.

---

## 1.2 Iteración vs Recursión

### 1.2.1 Proceso iterativo

Se utiliza un índice inicializado en cierto valor que se va modificando dentro de una estructura de control (`Mientras`, `Repetir`, `Para`) hasta que se cumple cierta condición.

Ejemplo — comer un paquete de galletas (iterativo):

```
// PRE: cant_galletas > 0
Procedimiento comer_paquete (val: cant_galletas entero)
    // supongamos que el paquete tiene 4 galletas, por lo que cant_galletas = 4
    VAR LOC: i: entero
    Para i ← 1 hasta cant_galletas hacer
        comer_galleta()
    fPara
    // cuando salimos del Para, se ejecutó comer_galleta() 4 veces
fProced
```

### 1.2.2 Proceso recursivo

"Comer un paquete de galletas" equivale a "comer una galleta + comer otro paquete más pequeño". Se repite hasta llegar al **caso base**: el paquete vacío.

Ejemplo — comer un paquete de galletas (recursivo):

```
// PRE: cant_galletas > 0 en la primera invocación
Procedimiento comer_paquete(val cant_galletas: entero)
    // supongamos que el paquete tiene 4 galletas, por lo que cant_galletas = 4
    Si cant_galletas >= 1 entonces
        comer_galleta()
        comer_paquete(cant_galletas-1) /* el procedimiento se llama a sí mismo
                                          pero decrementando el parámetro en 1 */
    fSi
fProced
```

Ejecución paso a paso para `comer_paquete(4)`:
```
comer_paquete(4) → comer_galleta() + comer_paquete(3)
                              → comer_galleta() + comer_paquete(2)
                                            → comer_galleta() + comer_paquete(1)
                                                          → comer_galleta() + comer_paquete(0)
                                                                        → [caso base: no hace nada]
```

A este proceso de subdividir el problema en instancias más pequeñas se lo conoce como **divide y vencerás**.

El punto irreducible (donde termina la recursión) se llama **caso base**.

### 1.2.2.1 Pasos de un algoritmo recursivo

1. **Identificar el o los casos base** (sabemos cómo resolverlos en forma concreta)
2. **Descomponer** el problema principal en versiones más pequeñas y simples de sí mismo hasta alcanzar el o los casos base
3. **Encadenar o combinar** los subproblemas que ya sabemos resolver para construir el resultado final

---

## 1.3 Ejemplos de recursividad

### 1.3.1 Factorial

Definición matemática:

```
n! = { 1           si n = 0
     { n * (n-1)!  si n > 0
```

Ejemplo: `5! = 5*4! = 5*4*3! = 5*4*3*2! = 5*4*3*2*1! = 5*4*3*2*1*0! = 5*4*3*2*1*1 = 120`

```
// PRE: n >= 0
Función fact (val n: entero): entero
    Si n > 0 entonces
        fact ← n * fact(n-1)    // recursión
    sino
        fact ← 1                // caso base: recordar que 0! = 1
    fSi
fFunc
```

Cadena de llamadas para `fact(5)`:
```
fact(5) ← 5 * fact(4)
               4 * fact(3)
                    3 * fact(2)
                         2 * fact(1)
                              1 * fact(0)
                                   1      ← caso base
```

Cuando se llega a `fact(0)`, se empieza a desapilar: `fact(1) = 1*1 = 1`, `fact(2) = 2*1 = 2`, ..., `fact(5) = 5*24 = 120`.

### 1.3.2 N-ésimo término de Fibonacci

Sucesión: `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...`

Definición:

```
f(n) = { f(n-1) + f(n-2)  si n >= 2
       { 1                 si n = 1
       { 0                 si n = 0
```

```
// PRE: n >= 0
Función Fibo (val n: entero): entero
    Si n >= 2 entonces
        Fibo ← Fibo(n-1) + Fibo(n-2)
    sino
        Fibo ← n
    fSi
fFunc
```

### 1.3.3 Suma de N números naturales

`SumaNat(5) = 1+2+3+4+5 = 15`

La suma hasta N es igual a la suma hasta N-1 más N. Caso base: cuando N = 1.

```
// PRE n >= 1
Funcion SumaNat (val n: entero): entero
    Si n > 1 entonces
        SumaNat ← n + SumaNat(n-1)
    sino
        SumaNat ← 1
    fSi
fFunc
```

### 1.3.4 Cantidad de dígitos de un número entero

Se usa `DIV 10` para ir quitando dígitos. Caso base: cuando `x DIV 10 = 0` queda un solo dígito.

```
// PRE n >= 0
Funcion Digitos (val x: entero): entero
    Si x DIV 10 > 0 entonces
        Digitos ← 1 + Digitos(x DIV 10)
    sino
        Digitos ← 1
    fSi
fFunc
```

### 1.3.5 Máximo elemento de un arreglo

Se reduce el arreglo quitando un elemento en cada llamada. Caso base: arreglo con 1 elemento.

```
// PRE {tope > 0}
Funcion max (ref x: arreglo[CMAX] de enteros, val tope: entero): entero
    VAR LOC: maximo: entero
    Si tope > 1 entonces
        maximo ← max(x, tope-1)
        Si x[tope] > maximo entonces
            max ← x[tope]
        sino
            max ← maximo
        fSi
    sino
        max ← x[1]
    fSi
fFunc
```

### 1.3.6 Suma de los elementos de un arreglo

Mismo criterio que 1.3.5: arreglo con un elemento menos en cada llamada. Caso base: 1 elemento.

```
// PRE {tope > 0}
Funcion Suma (ref x: arreglo[CMAX] de enteros, val tope: entero): entero
    Si tope > 1 entonces
        Suma ← x[tope] + Suma(x, tope-1)
    sino
        Suma ← x[1]
    fSi
fFunc
```

### 1.3.7 Buscar un elemento en un arreglo

Devuelve `verdadero` si `elem` está en el arreglo, `falso` si no. Caso base: `tope = 0` (arreglo vacío → no está).

```
// PRE {tope >= 0}
Funcion Existe (ref x: arreglo[CMAX] de entero, val tope, val elem: entero): lógico
    Si tope > 0 entonces
        Si x[tope] = elem entonces
            existe ← verdadero
        sino
            existe ← existe(x, tope-1, elem)
        fSi
    sino
        existe ← falso
    fSi
fFunc
```

---

## 1.4 Métodos de ordenamiento recursivos

Los métodos simples (Inserción, Selección, Burbujeo) son iterativos. QuickSort y MergeSort son métodos más eficientes que usan recursividad.

### 1.4.1 QuickSort

Ver apunte dedicado: `quicksort.md`

Resumen:
- Estrategia divide y vencerás
- Elige un **pivote** (el último elemento en esta implementación)
- Reorganiza: menores o iguales al pivote a la izquierda, mayores a la derecha
- Aplica quickSort recursivamente a ambas partes
- **Ventaja**: eficiente para arreglos grandes, ordenamiento *in situ* (sin memoria adicional)
- **Clave**: la elección del pivote afecta el rendimiento

### 1.4.2 MergeSort

Ver apunte dedicado: `mergesort.md`

Resumen:
- Divide el arreglo en dos mitades
- Ordena cada mitad recursivamente
- Fusiona las dos mitades ordenadas con el procedimiento `merge`
- **Ventaja**: performance estable, conserva el orden relativo de elementos con claves iguales
- **Desventaja**: requiere espacio adicional para los arreglos auxiliares

---

## Conclusiones

La recursividad es una forma de resolver algoritmos que divide el problema en subproblemas más pequeños hasta encontrar el **caso base**. Se implementa mediante una rutina que se invoca a sí misma. En esta unidad se comparó con el proceso iterativo y se aplicó a ejemplos como Factorial, y a los métodos de ordenamiento QuickSort y MergeSort.

---

## Bibliografía

- Bisbal Riera, J. (2013). *Manual de algorítmica: recursividad, complejidad y diseño de algoritmos.* Editorial UOC.
- Sedgewick, R. y Wayne, K. (2011). *Algorithms.* 4th Edition. Addison-Wesley.
- Cormen, T. et al. (2022). *Introduction to algorithms.* 4th Edition. The MIT Press.
