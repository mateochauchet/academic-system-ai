---
name: resumir-unidad
description: Genera un resumen completo de estudio para una unidad de una materia universitaria. Lee los markdowns disponibles (guía, apuntes) cruzados con el programa oficial, y produce un documento con todos los temas y conceptos necesarios para la unidad, explicados en detalle. Guarda el resultado en resumenes/ dentro de la unidad. Usar cuando Mateo pide un resumen de una unidad, quiere repasar una unidad completa, o se prepara para un parcial.
---

# Resumir Unidad

## Paso 1 — Determinar materia y unidad

Si el usuario no especificó materia o número de unidad en los argumentos, preguntale. Ambos datos son necesarios antes de continuar.

Rutas base:
- Materia: `materias/[materia]/`
- Unidad: `materias/[materia]/unidades/unidad-[N]/`

## Paso 2 — Leer el programa de la materia

Leé `materias/[materia]/meta/programa.md`.

Identificá los temas listados para la unidad solicitada. Estos son el índice de lo que debe cubrir el resumen.

## Paso 3 — Leer el material disponible

En `materias/[materia]/unidades/unidad-[N]/`:

1. Leé todos los `.md` en `guia/` (si existen).
2. Leé todos los `.md` en `apuntes/` (si existen).
3. Si hay temas del programa que no están cubiertos por los markdowns, leé los PDFs en `material/`.

No leas PDFs si ya existe un markdown que los cubre.

## Paso 4 — Generar el resumen

Generá un documento de estudio con estas características:

- **Título**: `# Resumen — Unidad [N]: [Nombre de la Unidad]`
- **Cubre todos los temas** listados en el programa para esta unidad, sin excepción.
- **Cada tema tiene una explicación completa**: definición, desarrollo conceptual, ejemplos donde corresponda.
- **No es una lista de bullets**: explicá los conceptos en profundidad, como si la persona no tuviera otro material para estudiar.
- **Incluye tablas, pseudocódigo o diagramas** si el tema lo requiere.
- Al final, una sección `## Conceptos clave` con los términos más importantes y su definición en una línea.

## Paso 5 — Guardar y confirmar

1. Creá la carpeta `resumenes/` si no existe dentro de la unidad.
2. Guardá el resumen en `materias/[materia]/unidades/unidad-[N]/resumenes/resumen-unidad-[N].md`.
3. Mostrá el resumen completo en el chat.
4. Confirmá al final: `Guardado en resumenes/resumen-unidad-[N].md`.
