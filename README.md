# facultad-ai — Sistema académico de Mateo

Sistema local para centralizar todo el conocimiento académico y trabajar con LLMs de forma organizada.

## Estructura

```
facultad-ai/
├── CLAUDE.md              ← System prompt: cómo debe comportarse Claude
├── TASKS.md               ← Fechas importantes y tareas pendientes (vista global)
├── README.md              ← Este archivo
├── context/               ← Contexto del estudiante
│   ├── perfil.md          ← Quién es Mateo, fortalezas, historial
│   ├── objetivos.md       ← Qué quiere lograr este cuatrimestre y en la carrera
│   └── metodologia.md     ← Cómo estudia, cómo usa el sistema
├── materias/              ← Una carpeta por materia
│   └── [materia]/
│       ├── meta/
│       │   ├── index.md       ← Estado actual de la materia (leer primero)
│       │   ├── programa.md    ← Unidades, temas, criterios de aprobación
│       │   └── cronograma.md  ← Fechas de parciales, plan semana a semana
│       ├── clases/            ← Apuntes de clase (clase_01-[tema].md)
│       ├── material/          ← PDFs y material de la cátedra
│       ├── teoria/            ← Conceptos y definiciones elaboradas
│       ├── resumenes/         ← Resúmenes por unidad (material de estudio)
│       ├── ejercicios/        ← TPs y ejercicios resueltos
│       └── examenes/          ← Parciales anteriores y simulacros
├── archive/               ← Materias cerradas (aprobadas o pausadas)
└── prompts/               ← Prompts reutilizables para Claude
    ├── tutor.md               ← Cómo explicar temas
    ├── simulador_parcial.md   ← Cómo tomar un examen simulado
    ├── generador_resumen.md   ← Cómo generar resúmenes estructurados
    └── corrector.md           ← Cómo corregir ejercicios y código
```

## Materias cursando (1er cuatrimestre 2026)
- Marketing → `materias/marketing/`
- Fundamentos de Base de Datos → `materias/base-de-datos/`
- Estructuras y Algoritmos de Datos II → `materias/algoritmos-2/`
- Seguridad Informática → `materias/seguridad-informatica/`

## Usos típicos

**Estudiar un tema** → Decile a Claude el tema y la materia. Él lee el programa y te pregunta cómo querés la explicación.

**Simular un parcial** → "Simulame un parcial de [materia]". Claude lee el programa y los parciales anteriores, y actúa de examinador.

**Generar un resumen** → "Generá un resumen de la Unidad 2 de Base de Datos". Claude lo estructura y ofrece guardarlo.

**Corregir un TP** → Pegá el código o ejercicio y pedí corrección. Claude explica los errores sin darte la solución directo.

**Ver qué tenés pendiente** → "¿Qué tengo para esta semana?" Claude revisa TASKS.md.
