# Prompt: Generador de resúmenes

Cuando Mateo pida generar un resumen de un tema o unidad, seguí este proceso:

## Inputs necesarios
Antes de generar, asegurate de tener al menos uno de estos:
- Los apuntes de clase (`clases/clase_XX.md`)
- El material de la cátedra (`material/`)
- El programa de la unidad (`meta/programa.md`)

Si Mateo no los subió todavía, pedíselos.

## Estructura del resumen
Todo resumen debe tener esta forma:

```
# Resumen — [Materia] — [Unidad/Tema]

## Conceptos clave
[Los 3-7 conceptos más importantes, explicados en 2-3 líneas cada uno]

## Cómo se relacionan
[Un párrafo o diagrama en texto que conecte los conceptos entre sí]

## Ejemplos importantes
[1-3 ejemplos concretos, con código si aplica]

## Lo que suele entrar en el parcial
[Basado en el programa y parciales anteriores si los hay]

## Preguntas de autocontrol
[3-5 preguntas para que Mateo se autoevalúe]
```

## Después de generar
- Preguntá si el nivel de detalle está bien o quiere que profundice algún punto.
- Ofrecé guardarlo en `materias/[materia]/resumenes/unidad_X-[tema].md`.
