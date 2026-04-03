# Actividad Unidad 2 — Resolución

## Consigna

Dado el algoritmo original, se solicita:
1. Modificarlo aplicando criterios de modularidad, definiendo funciones y procedimientos.
2. Explicar qué pruebas de verificación y validación se pueden realizar sobre el algoritmo modificado.

---

## Parte 1 — Algoritmo modularizado

### Análisis previo

El algoritmo original realiza tres tareas mezcladas en un único bloque: entrada de datos, procesamiento y salida. Para modularizarlo se identifican las siguientes responsabilidades, cada una asignada a un módulo independiente:

- `IngresarEdad`: Solicitar y validar una edad (>= 0)
- `IngresarSexo`: Solicitar y validar el sexo (F o M)
- `CalcularEstadisticas`: Calcular porcentajes sobre los totales acumulados
- `MostrarResultados`: Mostrar los resultados por pantalla

El algoritmo principal queda encargado únicamente de inicializar, coordinar el ingreso de datos y llamar a la salida.

---

### Algoritmo

```
VARIABLES GLOBALES
    TOTAL_ALU, TOTAL_F, TOTAL_M: ENTERO
    PORC_F, PORC_M: REAL


// Módulo 1: pide una edad válida (>= 0)
Función IngresarEdad(): ENTERO
    VARIABLES
        EDAD: ENTERO
    INICIO
        Repetir
            Mostrar("Ingrese la Edad (0 para finalizar)")
            Ingresar(EDAD)
        Hasta que (EDAD >= 0)
        Retornar EDAD
    FIN

// Módulo 2: pide un sexo válido (F o M)
Función IngresarSexo(): CARÁCTER
    VARIABLES
        SEXO: CARÁCTER
    INICIO
        Repetir
            Mostrar("Ingrese el Sexo (F o M)")
            Ingresar(SEXO)
        Hasta que (SEXO = 'F' O SEXO = 'M')
        Retornar SEXO
    FIN


// Módulo 3: calcula porcentajes
Procedimiento CalcularEstadisticas()
    INICIO
        PORC_F <- TOTAL_F / TOTAL_ALU * 100
        PORC_M <- TOTAL_M / TOTAL_ALU * 100
    FIN


// Módulo 4: muestra los resultados
Procedimiento MostrarResultados()
    INICIO
        Si (TOTAL_ALU = 0) Entonces
            Mostrar("No se ingresaron datos")
        Sino
            CalcularEstadisticas()
            Mostrar("Total de alumnos:", TOTAL_ALU)
            Mostrar("Total de mujeres:", TOTAL_F)
            Mostrar("Total de varones:", TOTAL_M)
            Mostrar("% de mujeres:", PORC_F)
            Mostrar("% de varones:", PORC_M)
        FinSi
    FIN


// Algoritmo principal
Algoritmo Principal
    VARIABLES
        EDAD: ENTERO
        SEXO: CARÁCTER
    INICIO
        TOTAL_ALU <- 0
        TOTAL_F   <- 0
        TOTAL_M   <- 0

        EDAD <- IngresarEdad()

        Mientras (EDAD <> 0) Hacer
            SEXO <- IngresarSexo()

            Si (SEXO = 'F') Entonces
                TOTAL_F <- TOTAL_F + 1
            Sino
                TOTAL_M <- TOTAL_M + 1
            FinSi

            TOTAL_ALU <- TOTAL_ALU + 1
            EDAD <- IngresarEdad()
        FinMientras

        MostrarResultados()
    FIN
```

---

## Parte 2 — Pruebas de verificación y validación

### Verificación

La verificación comprueba que el algoritmo cumple con los requerimientos funcionales especificados. Las pruebas que se pueden realizar son:

Pruebas unitarias: se prueba cada módulo de forma independiente:
- `IngresarEdad`: verificar que no acepta valores negativos y que acepta el 0 como fin.
- `IngresarSexo`: verificar que solo acepta 'F' o 'M' y rechaza cualquier otro carácter.
- `CalcularEstadisticas`: con valores conocidos (ej: 2 mujeres y 3 varones sobre 5 alumnos), verificar que los porcentajes calculados son correctos (40% y 60%).
- `MostrarResultados`: verificar que cuando TOTAL_ALU = 0 muestra el mensaje correspondiente y no intenta calcular porcentajes.

Prueba de integración, se prueba el funcionamiento conjunto:
- Ingresar una secuencia de alumnos y verificar que los totales acumulados en el principal coinciden con los resultados mostrados al final.

Técnica estática (inspección), sin ejecutar el programa, se puede revisar el código para detectar:
- Que ningún módulo realiza más de una tarea.
- Que `CalcularEstadisticas` no es llamado cuando `TOTAL_ALU = 0`, evitando una división por cero.

### Validación

La validación comprueba que el programa resuelve lo que el usuario realmente necesita. Las pruebas que se pueden realizar son:

**Prueba de sistema** — ejecutar el programa completo con datos reales y verificar que el comportamiento general es el esperado: carga varios alumnos, finaliza con 0, y muestra correctamente los totales y porcentajes.

**Prueba de aceptación** — un usuario real utiliza el programa e indica si los resultados que obtiene son los que esperaba. Por ejemplo, confirmar que los porcentajes mostrados tienen sentido para los datos ingresados.
