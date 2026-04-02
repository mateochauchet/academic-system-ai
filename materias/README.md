# Materias

Una carpeta por materia. Cada materia puede organizarse de dos formas según cómo se dicte.

---

## Opción A — Por tipo de contenido

Para materias sin una división clara en unidades.

```
[materia]/
├── meta/
│   ├── index.md        ← estado actual de la materia
│   ├── programa.md     ← unidades, temas, criterios de aprobación
│   └── cronograma.md   ← fechas de parciales y plan semanal
├── clases/             ← apuntes de clase
├── material/           ← PDFs oficiales de la cátedra
├── teoria/             ← conceptos y definiciones elaboradas
├── resumenes/          ← resúmenes por unidad
├── ejercicios/         ← TPs y ejercicios resueltos
└── examenes/           ← parciales anteriores y simulacros
```

---

## Opción B — Por unidades

Para materias con unidades bien definidas. Todo el contenido de una unidad vive junto.

```
[materia]/
├── meta/
│   ├── index.md
│   ├── programa.md
│   └── cronograma.md
└── unidades/
    └── unidad-1/
        ├── index.md        ← descripción y estructura de la unidad
        ├── material/       ← PDFs oficiales
        ├── guia/           ← guía de estudio
        ├── actividades/    ← ejercicios y actividades prácticas
        └── apuntes/        ← apuntes elaborados y resúmenes
```

---

## Materias activas (1er cuatrimestre 2026)

| Materia | Carpeta | Estructura |
|---------|---------|------------|
| Marketing | `marketing/` | Opción A |
| Fundamentos de Base de Datos | `base-de-datos/` | Opción A |
| Estructuras y Algoritmos de Datos II | `algoritmos-2/` | Opción B |
| Seguridad Informática | `seguridad-informatica/` | Opción A |
