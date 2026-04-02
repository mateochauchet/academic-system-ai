Entrás en modo daily workflow. Tu rol es preparar el contexto de la sesión de estudio de Mateo en tres pasos.

## Paso 1 — Elegir materia

Listá las carpetas dentro de `materias/` usando Glob o Bash. Mostrá los nombres de las carpetas como opciones y preguntale a Mateo en cuál va a trabajar hoy.

## Paso 2 — Cargar contexto de la materia

Una vez que Mateo elige la materia:

1. Leé `materias/[materia]/meta/programa.md`
2. Leé `materias/[materia]/meta/cronograma.md`
3. Usá la fecha actual (disponible en el contexto como `currentDate`) para identificar las próximas actividades. Mostrá solo las fechas que todavía no pasaron, ordenadas de más cercana a más lejana. Presentalas de forma breve y clara — no copies todo el cronograma.

## Paso 3 — Definir qué trabajar

Preguntale: "¿En qué estás trabajando o qué querés trabajar hoy?"

Según lo que responda, cargá el contexto relevante antes de seguir:
- Si menciona una unidad o tema teórico → buscá archivos en `materias/[materia]/teoria/` y `materias/[materia]/resumenes/` que correspondan y leelos
- Si menciona un ejercicio o TP → leé los archivos relevantes en `materias/[materia]/ejercicios/`
- Si menciona un parcial o examen → leé `materias/[materia]/examenes/` y revisá las fechas del cronograma
- Si la carpeta correspondiente está vacía → no rompas el flujo, simplemente continuá sin contexto adicional

Una vez cargado el contexto, estás listo para ayudarlo. No hagas un resumen de todo lo que leíste — simplemente confirmá en qué van a trabajar y arrancá.
