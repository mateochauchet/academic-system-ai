# Guía del sistema universitario con Claude

## ¿Cómo funciona?

Este sistema está pensado para que Claude te conozca como estudiante y te ayude a lo largo de toda la carrera. Cuanto más lo uses y más completes los archivos, mejor va a ser la ayuda.

---

## Estructura de carpetas

```
universidad-os/
├── CLAUDE.md          ← Tu contexto académico (Claude lo lee siempre)
├── TASKS.md           ← Tareas pendientes y fechas importantes
├── GUIA.md            ← Este archivo
├── materias/
│   ├── _plantilla/    ← Copiar esta carpeta para cada nueva materia
│   ├── analisis/
│   ├── fisica/
│   └── [otras materias]/
│       ├── info.md    ← Datos, programa, criterios de aprobación
│       ├── apuntes/   ← Apuntes de clase
│       ├── parciales/ ← Exámenes pasados, resúmenes para estudiar
│       └── tps/       ← Trabajos prácticos
├── memory/            ← Conceptos y conocimiento acumulado entre cuatrimestres
└── historial/         ← Materias ya aprobadas
```

---

## Primer paso: completar CLAUDE.md

Abrí el archivo `CLAUDE.md` y completá:
- Tu facultad y carrera exacta
- Las materias que estás cursando este cuatrimestre
- Las fechas aproximadas de parciales
- Cómo preferís estudiar

Esto le da a Claude el contexto para ayudarte bien desde el principio.

---

## Cómo pedirle ayuda a Claude

### Para organización
- *"¿Qué tengo pendiente esta semana?"* → Claude revisa TASKS.md
- *"Tengo parcial de Álgebra el 15 de abril, agregalo"* → Claude actualiza TASKS.md
- *"Arranqué a cursar Termodinámica, ayudame a configurarla"* → Claude crea la carpeta con info.md

### Para estudiar
- *"Tengo parcial de Análisis en una semana, ¿cómo arrancamos?"* → Claude lee el programa en info.md y arma un plan
- *"Explicame transformadas de Laplace"* → Claude explica el tema
- *"Haceme un resumen de la Unidad 3 de Física"* → Claude genera el resumen y lo guarda en parciales/
- *"Tomate de examinador y haceme preguntas de Estructuras de Datos"* → Claude te toma práctica oral

### Para trabajos prácticos
- *"Tengo que hacer el TP2 de Programación, es sobre punteros en C"* → Claude te ayuda a entender, diseñar y resolver
- *"Revisá mi código y decime qué está mal"* → Claude hace code review

### Para el día a día
- *"¿Qué debería estudiar hoy?"* → Claude te sugiere según fechas en TASKS.md
- *"No entendí nada de la clase de hoy sobre integrales dobles"* → Claude explica desde cero

---

## Flujo para una materia nueva

1. Copiá la carpeta `materias/_plantilla/` y renombrala con el nombre de la materia
2. Completá `info.md` con los datos del curso
3. Actualizá `CLAUDE.md` agregando la materia a la tabla
4. Agregá las fechas de parciales a `TASKS.md`
5. ¡Listo! Ya podés pedirle ayuda a Claude con esa materia

---

## Tips para sacarle el jugo

- **Subí los apuntes y PDFs** a la carpeta de la materia para que Claude los pueda leer
- **Después de cada clase**, pedile a Claude que te ayude a organizar los apuntes
- **Antes de cada parcial**, pedile un plan de estudio basado en el programa
- **Guardá los resúmenes** que Claude genera en `parciales/` para no tener que repetirlos
- **Al terminar el cuatrimestre**, mové la materia a `historial/` con la nota final

---

## Sistema de memoria entre sesiones

Claude lee `CLAUDE.md` al principio de cada conversación para recordar quién sos y qué estás cursando. Cuanto más completo esté ese archivo, mejor.

La carpeta `memory/` guarda conocimiento más permanente (conceptos que ya dominás, materias que ya aprobaste, etc.).
