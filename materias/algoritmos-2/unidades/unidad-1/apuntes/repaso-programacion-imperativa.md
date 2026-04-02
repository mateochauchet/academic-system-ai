# Repaso Programación Imperativa
**Algoritmos y Estructura de Datos I | CAECE**
Contenidista: Mg. Ing. Omar Gallo Haddad

---

## Objetivo

Repasar conceptos de tipos de datos básicos, estructuras de control, estructuras de datos fundamentales, arreglos, matrices, funciones, procedimientos, pasaje por valor y referencia, y registros.

---

## 1. Introducción

Al programar describimos una secuencia de pasos que la máquina debe ejecutar para resolver un problema. Usaremos **pseudocódigo** con características de la programación imperativa, independiente de lenguajes específicos.

Las instrucciones se ejecutan de arriba hacia abajo y siguen reglas léxicas, sintácticas y semánticas.

**Comentarios:**
```
// comentario de una línea
/* comentario
   de múltiples líneas */
```

---

## 2. Tipos de Datos

Un tipo de dato determina las operaciones posibles y cómo se almacena el valor en memoria.

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| `entero` | números enteros | 4, 123, -3, 0 |
| `real` | números reales | 3.14, 5.1, 123.7 |
| `carácter` | un solo símbolo | 'a', '&', 'H' |
| `cadena` | conjunto de caracteres | "hola", "123" |
| `lógico/booleano` | verdadero o falso | VERDADERO, FALSO |

---

## 3. Variables y Constantes

**Variable:** espacio en memoria con nombre, valor y tipo. Su valor puede cambiar durante la ejecución.

```
NOMBRE_DE_VARIABLE: TIPO_DE_DATO

// Ejemplos:
sueldo: real
titulo: cadena [20]   // el número indica el tamaño máximo
cantidad: entero
```

**Constante:** valor fijo durante toda la ejecución.

```
NOMBRE_DE_LA_CONSTANTE = VALOR

// Ejemplo:
PI = 3.141516
```

**Reglas para nombres de variables:**
- Solo letras, números y guion bajo
- No pueden empezar con números
- Sin espacios ni caracteres especiales
- Mayúsculas y minúsculas son distintas (`a` ≠ `A`)
- Estilo recomendado: `cantProdLimpieza` (camelCase) o `cant_prod_limpieza` (snake_case)
- Las constantes suelen escribirse en MAYÚSCULAS

---

## 4. Operaciones Aritméticas

| Operador | Descripción | Tipos |
|----------|-------------|-------|
| `+` | suma | entero, real |
| `-` | resta | entero, real |
| `*` | multiplicación | entero, real |
| `/` | división | entero, real |
| `DIV` | división entera | entero |
| `RESTO` | resto de la división | entero |

**Diferencia clave:**
- `7 / 5` = 1.4 (real)
- `7 DIV 5` = 1 (parte entera)
- `7 RESTO 5` = 2 (resto)

---

## 5. Operaciones de Relación

Devuelven `VERDADERO` o `FALSO`.

| Operador | Descripción | Tipos |
|----------|-------------|-------|
| `<` | menor | entero, real, carácter |
| `<=` | menor o igual | entero, real, carácter |
| `>` | mayor | entero, real, carácter |
| `>=` | mayor o igual | entero, real, carácter |
| `=` | igual | entero, real, carácter, cadena, lógico |
| `<>` o `≠` | distinto | entero, real, carácter, cadena, lógico |

---

## 6. Operaciones Lógicas

| Operador | Descripción |
|----------|-------------|
| `Y` | conjunción (AND) — verdadero si ambos son verdaderos |
| `O` | disyunción (OR) — falso solo si ambos son falsos |
| `NO` | negación (NOT) — invierte el valor lógico |

**Ejemplo:** `edad > 18 Y sexo = 'M'`

---

## 7. Entrada y Salida

```
Mostrar("texto")         // imprime por pantalla
Ingresar(variable)       // lee desde teclado
```

**Ejemplo completo:**
```
VARIABLES:
    cantidad: entero
    precio, total: real
    codigo: cadena[30]

INICIO
    Mostrar("Ingrese el código de producto")
    Ingresar(codigo)
    Mostrar("Ingrese cantidad")
    Ingresar(cantidad)
    Mostrar("Ingrese precio")
    Ingresar(precio)
    total <- cantidad * precio
    Mostrar("Del producto ", codigo, " total: ", total, " pesos")
FIN
```

> La asignación `<-` se lee de derecha a izquierda: el valor de la derecha se guarda en la variable de la izquierda.

---

## 8. Estructuras de Control

### Condicional Simple
Si una condición es verdadera, se ejecuta lo que está dentro del condicional y luego se continúa desde donde este termina.
```
Si edad > 18 entonces
    Mostrar("Usted es mayor de edad")
fSi
// y luego se continua desde aquí
```

### Condicional Alternativo (if-else)
Si la condición es verdadera se ejecuta el primer bloque; si es falsa, el bloque alternativo. Finalizado uno u otro, el flujo continúa desde donde termina todo el condicional — no se pasa de un bloque al otro.
```
Si estado = "activo" entonces
    Mostrar("Puede acceder")
sino
    Mostrar("No puede acceder")
fSi
```

### Condicional Anidado
```
Si resultado = "victoria" entonces
    puntos <- 3
Sino
    Si resultado = "empate" entonces
        puntos <- 1
    Sino
        puntos <- 0
    fSi
fSi
```

### Mientras (while)
Se ejecuta mientras la condición sea verdadera. Puede no ejecutarse ninguna vez. Es importante que dentro del bucle algo cambie para que la condición eventualmente se vuelva falsa, de lo contrario se produce un loop infinito.
```
Ingresar(edad)
Mientras edad < 18 entonces
    Mostrar("Por favor, ingrese una edad mayor a 18")
    Ingresar(edad)
fMientras
```

### Repetir (do-while)
Se ejecuta al menos una vez. Termina cuando la condición del `Hasta que` es verdadera.
```
Repetir
    Mostrar("Ingrese edad mayor a 18")
    Ingresar(edad)
Hasta que edad > 18
```

### Para (for)
Itera desde un valor inicial hasta uno final, incrementando de 1 en 1 por defecto.
```
Para num <- 1 hasta 10 hacer
    Mostrar(num)
fPara
```

---

## 9. Registros

Permiten agrupar varios campos de distintos tipos bajo un mismo nombre.

```
T_REG_EMPLEADO = Registro
    Nombre: cadena
    Apellido: cadena
    Legajo: cadena
    Sueldo: real
fReg

empleado: T_REG_EMPLEADO
```

Para acceder a un campo se usa el **operador punto** `.`:
```
Mostrar(empleado.nombre)
```

---

## 10. Arreglos

Conjunto finito de elementos del **mismo tipo**, dispuestos consecutivamente, con un nombre en común. Se accede por posición con corchetes `[]`. Las posiciones van de **1 al máximo**.

```
MAX = 5
arr: arreglo de MAX enteros

Arr[1] = 64
Arr[2] = 32
Arr[3] = 11
Arr[4] = 5
Arr[5] = 97
```

Resultado:
```
| 64 | 32 | 11 | 5 | 97 |
   1    2    3   4    5
```

> Acceder fuera del rango (ej: posición 6) provoca error de desbordamiento.

---

## 11. Matrices

Arreglo de dos dimensiones: filas y columnas. Se accede con `[fila, columna]`.

```
MAX = 3
mat: matriz de [MAX, MAX] enteros

mat[1, 1] = 23    mat[1, 2] = 88    mat[1, 3] = 17
mat[2, 1] = 4     mat[2, 2] = 6     mat[2, 3] = 11
mat[3, 1] = 41    mat[3, 2] = 8     mat[3, 3] = 5
```

Resultado:
```
| 23 | 88 | 17 |
|  4 |  6 | 11 |
| 41 |  8 |  5 |
```

---

## 12. Rutinas

### Pasaje de parámetros

- **Por valor (`val`):** se trabaja con una copia. Los cambios NO afectan al original.
- **Por referencia (`ref`):** se trabaja con la dirección de memoria original. Los cambios SÍ persisten.

### Función
Devuelve un único valor. Por lo general usa parámetros por valor.

```
Función esPar (val num: entero): lógico
    Devolver (num RESTO 2 = 0)
fFunc

// Uso:
resp1 <- esPar(4)   // verdadero
resp2 <- esPar(3)   // falso
```

### Procedimiento
No devuelve valor. Puede tener parámetros por valor y por referencia.

```
Proced ingresarNum (ref num: entero)
    Repetir
        Mostrar("Ingrese un entero positivo")
        Ingresar(num)
    Hasta que num > 0
fFunc

// Uso:
a: entero
ingresarNum(a)
Mostrar(a)
```
