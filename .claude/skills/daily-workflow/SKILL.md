---
name: daily-workflow
description: Inicia la sesión de estudio diaria de Mateo. Lee las materias activas desde la carpeta materias/, pregunta en cuál va a trabajar, carga el programa y cronograma de esa materia, muestra las próximas actividades según la fecha actual, y pregunta en qué tema o tarea quiere trabajar para cargar el contexto relevante. Usar al comienzo de cada sesión de estudio o cuando el usuario invoca /daily-workflow.
---

# Daily Workflow

Entrás en modo daily workflow. Tu rol es preparar el contexto de la sesión de estudio en tres pasos.

## Paso 1 — Elegir materia

Listá las carpetas dentro de `materias/` usando Glob. Mostrá los nombres como opciones numeradas y preguntale a Mateo cuál elige hoy.

## Paso 2 — Cargar contexto de la materia

Una vez que elige la materia:

1. Leé `materias/[materia]/meta/programa.md`
2. Leé `materias/[materia]/meta/cronograma.md`
3. Usá la fecha actual del contexto (`currentDate`) para filtrar solo las actividades que todavía no pasaron. Mostralas en orden cronológico, de forma breve y clara. No copies todo el cronograma.

## Paso 3 — Definir qué trabajar

Preguntale: "¿En qué estás trabajando o qué querés trabajar hoy?"

Según la respuesta, cargá el contexto relevante antes de continuar:

- Unidad o tema teórico → buscá en `materias/[materia]/teoria/` y `materias/[materia]/resumenes/`
- Ejercicio o TP → buscá en `materias/[materia]/ejercicios/`
- Parcial o examen → buscá en `materias/[materia]/examenes/` y revisá las fechas del cronograma
- Carpeta vacía → continuá sin contexto adicional, no rompas el flujo

Una vez cargado el contexto, confirmá en qué van a trabajar y arrancá. No hagas un resumen de todo lo que leíste.
