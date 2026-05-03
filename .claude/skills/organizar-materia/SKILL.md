---
name: organizar-materia
description: Organiza el material descargado del campus en la estructura de carpetas del proyecto. Recibe archivos sueltos (PDFs, markdowns, txts) en la carpeta de una materia, los clasifica por nivel (materia o unidad) y tipo (guia, actividad, apuntes, meta), los mueve al lugar correcto, convierte PDFs de guías a markdown, y crea los index.md por unidad. Usar cuando el usuario descargó material nuevo del campus y quiere organizarlo.
---

# Organizar Materia

## Paso 1 — Determinar materia

Si el usuario no especificó la materia, listá las carpetas en `materias/` y preguntale cuál quiere organizar.

## Paso 2 — Escanear archivos a organizar

Buscá todos los archivos sueltos en la materia:
- Archivos en la raíz de `materias/[materia]/`
- Archivos en `materias/[materia]/unidades/unidad-N/` que no estén dentro de ninguna subcarpeta (`material/`, `guia/`, `apuntes/`, `actividades/`, `resumenes/`)

Listá lo que encontraste antes de continuar.

## Paso 3 — Clasificar cada archivo

Para cada archivo, determiná dos cosas: **¿a qué nivel pertenece?** y **¿qué tipo es?**

### Regla fundamental sobre PDFs y markdown

**El PDF original siempre queda en `material/`. El markdown generado va en otro lado.**
Nunca reemplaces un PDF por su conversión — son dos artefactos distintos que coexisten.

### ¿Nivel materia o nivel unidad?

| Señal en el nombre o ubicación | Destino del PDF | Markdown generado |
|-------------------------------|-----------------|-------------------|
| Contiene "programa" | `material/` (queda ahí) | `meta/programa.md` |
| Contiene "cronograma" | `material/` (queda ahí) | `meta/cronograma.md` |
| Contiene "parcial", "examen", "final" | `examenes/` | — |
| Contiene "unidad" + número | `unidades/unidad-N/material/` | `unidades/unidad-N/guia/guia-unidad-N.md` |
| Ya está en carpeta `unidad-N/` | `unidades/unidad-N/material/` | `unidades/unidad-N/guia/guia-unidad-N.md` |
| Sin señal clara | Leé las primeras líneas y cruzalas contra `meta/programa.md`. Si sigue siendo ambiguo, preguntale al usuario. | |

### ¿Qué tipo dentro de la unidad?

| Señal | Destino |
|-------|---------|
| PDF con "guia" en el nombre, o contenido teórico de la cátedra | `material/` + convertir a `guia/guia-unidad-N.md` |
| Nombre contiene "TP", "tp", "actividad", "obligatorio", "entregable" | `actividades/` |
| Archivo `.md` o `.txt` con notas personales | `apuntes/` |
| Archivo `.docx` | Pedirle al usuario que lo convierta a `.txt` o `.pdf` primero |
| Resto | `material/` |

## Paso 4 — Confirmar plan antes de ejecutar

Mostrá al usuario la clasificación completa antes de mover nada:

```
archivo.pdf        → unidades/unidad-2/material/ + convertir a guia/
TP_01.md           → unidades/unidad-3/actividades/
programa.pdf       → meta/programa.md
caso-ejemplo.docx  → ⚠ necesita conversión manual (.txt o .pdf)
```

Pedí confirmación. No muevas nada hasta que el usuario apruebe.

## Paso 5 — Crear estructura de carpetas

Para cada unidad involucrada, creá las subcarpetas que falten:
`material/`, `guia/`, `apuntes/`, `actividades/`, `resumenes/`

## Paso 6 — Mover archivos

Mové cada archivo a su lugar según la clasificación aprobada.

## Paso 7 — Convertir PDFs de guías a markdown

Para cada PDF clasificado como guía:
1. Extraé el texto con `pdftotext`
2. Formatealo en markdown con secciones, tablas y listas según el contenido
3. Guardalo en `unidades/unidad-N/guia/guia-unidad-N.md`

No conviertas si ya existe el archivo markdown correspondiente.

## Paso 8 — Crear index.md por unidad

Para cada unidad procesada, creá o actualizá `unidades/unidad-N/index.md` con:
- Título y descripción breve de la unidad (inferida del programa o del contenido)
- Árbol de la estructura de carpetas
- Lista de archivos disponibles con descripción de una línea cada uno

## Paso 9 — Confirmar

Mostrá un resumen de todo lo que se organizó y los archivos generados.
