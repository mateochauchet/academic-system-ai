# Actividad Unidad 2 — División en Módulos y Verificación
**Estructuras y Algoritmos de Datos II | CAECE**
Contenidista: Maximiliano López

---

## Consigna

Dado el siguiente algoritmo, analice el código para comprender qué es lo que realiza y cuál es su objetivo. Realice las siguientes tareas:

1. Modificar el algoritmo aplicando los criterios de modularidad, definiendo funciones y procedimientos.
2. Explicar con sus palabras qué pruebas de verificación y validación puede realizar en su algoritmo modificado.

---

## Algoritmo original

```
VARIABLES
    EDAD, TOTAL_ALU, TOTAL_F, TOTAL_M: ENTERO
    SEXO: CARÁCTER
    PORC_F, PORC_M: REAL

INICIO
    TOTAL_ALU <- 0
    TOTAL_F <- 0
    TOTAL_M <- 0

    Repetir
        Mostrar ("Ingrese la Edad (0 para finalizar)")
        Ingresar (EDAD)
    Hasta que (EDAD >= 0)

    Mientras (EDAD <> 0) Hacer
        Repetir
            Mostrar ("Ingrese el Sexo (F o M)")
            Ingresar (SEXO)
        Hasta que (SEXO = 'F' O SEXO = 'M')

        Si (SEXO = 'F') entonces
            TOTAL_F <- TOTAL_F + 1
        Sino
            TOTAL_M <- TOTAL_M + 1
        Fin si

        TOTAL_ALU <- TOTAL_ALU + 1

        Repetir
            Mostrar ("Ingrese la Edad (0 para finalizar)")
            Ingresar (EDAD)
        Hasta que (EDAD >= 0)
    Fin Mientras

    Si (TOTAL_ALU = 0) entonces
        Mostrar ("No se ingresaron datos")
    Sino
        Mostrar ("El total de alumnos es:", TOTAL_ALU)
        Mostrar ("El total de mujeres es:", TOTAL_F)
        Mostrar ("El total de varones es:", TOTAL_M)
        PORC_F <- TOTAL_F / TOTAL_ALU * 100
        PORC_M <- TOTAL_M / TOTAL_ALU * 100
        Mostrar ("El % de mujeres es:", PORC_F)
        Mostrar ("El % de varones es:", PORC_M)
    Fin Si
FIN
```
