# Guía Unidad 1 — Introducción a los Sistemas de Base de Datos

## 1. Un poco de historia: del procesamiento de archivos a las BBDD

Antes de las bases de datos, las aplicaciones usaban **procesamiento de archivos**: cada programa definía sus propios archivos con sus propios registros. Esto generaba dos problemas críticos:

**Dependencia entre aplicaciones y archivos físicos:** si un programa movía un archivo a otra carpeta, todos los demás programas que lo usaban fallaban con "archivo no encontrado". No había separación entre dónde estaban los datos y quién los usaba.

**Procesamiento monousuario:** dos programas no podían acceder al mismo archivo al mismo tiempo. Si uno estaba leyendo para generar un reporte, el otro no podía escribir.

Estos dos problemas —la dependencia física y el acceso exclusivo— fueron la motivación principal para crear los DBMS.

---

## 2. ¿Qué es un DBMS?

> **Base de datos:** colección de hechos con un significado relevante para el mundo con el que nos interesa trabajar, con un propósito específico. Su contenido debe reflejar los cambios en los datos tan pronto como sea posible.

> **DBMS (Database Management System):** colección de programas que permite a los usuarios crear y mantener una base de datos. Facilita la definición, construcción, manipulación y compartición de datos entre usuarios y aplicaciones.

### Ventajas del DBMS sobre el procesamiento de archivos

| Problema anterior | Solución del DBMS |
|---|---|
| Dependencia aplicación-archivo | **Aislamiento programa-datos:** la aplicación no sabe dónde están los archivos físicos |
| Solo una vista de los datos | **Múltiples vistas:** cada usuario ve solo lo que necesita |
| Acceso monousuario | **Procesamiento multiusuario** con control de concurrencia |
| Sin autodescripción | **Meta-data:** la base se describe a sí misma en el catálogo |

---

## 3. Tipos de usuarios

| Tipo | Rol |
|---|---|
| **DBA (Administrador)** | Máximos permisos. Gestiona permisos, rendimiento, recursos y el esquema interno |
| **Diseñador** | Crea los modelos de datos antes de que exista la base. Define las vistas de cada usuario |
| **Analistas y Programadores** | Los analistas relevan necesidades; los programadores crean las aplicaciones que acceden a los datos |
| **Usuarios Finales** | Interactúan con las vistas construidas para ellos |

---

## 4. Arquitectura de tres esquemas

La arquitectura de tres niveles permite el **aislamiento** entre usuarios y datos físicos:

```
┌─────────────────────────────────────────┐
│   NIVEL EXTERNO (vistas de usuario)     │  ← Usuarios finales
│   Solo ven lo que les corresponde       │
├─────────────────────────────────────────┤
│   NIVEL CONCEPTUAL (esquema lógico)     │  ← Diseñadores, desarrolladores
│   Estructura completa, sin detalle físico│
├─────────────────────────────────────────┤
│   NIVEL INTERNO (esquema físico)        │  ← DBA
│   Archivos en disco, rutas de acceso    │
└─────────────────────────────────────────┘
```

Cada nivel oculta hacia arriba los detalles del nivel inferior.

---

## 5. Independencia de datos

### Independencia lógica
> Capacidad de cambiar el **esquema conceptual** sin tener que cambiar los esquemas externos ni los programas de aplicación.

Ejemplo: agregar un nuevo campo a los clientes (métrica de scoring) sin tocar los archivos físicos ni las vistas existentes.

### Independencia física
> Capacidad de cambiar el **esquema interno** (cómo se almacenan los datos) sin cambiar el esquema conceptual.

Ejemplo: el DBA agrega un disco nuevo y mueve archivos — ningún usuario ni aplicación se ve afectado. Esto puede hacerse mientras la base está operando.

---

## 6. Lenguajes del DBMS

| Lenguaje | Nombre completo | Para qué sirve |
|---|---|---|
| **DDL** | Data Definition Language | Crear la base de datos, sus estructuras y objetos (nivel conceptual) |
| **SDL** | Storage Definition Language | Especificar el nivel interno: archivos físicos y dónde se guardan los datos |
| **DML** | Data Manipulation Language | Especificar vistas de usuarios finales y mapeos entre niveles |

En los DBMS actuales se usa el mismo lenguaje para todo (SQL), y las sentencias se clasifican internamente en DDL, DML y SDL.

**Orden de implementación:** primero se define el esquema conceptual e interno (DDL/SDL), luego recién se puede definir el esquema externo (DML). No puede hacerse en otro orden.

---

## 7. Módulos componentes del DBMS

```
DBA                          Programadores            Usuarios Finales
(DDL + comandos              (DML embebido en          (consultas
 privilegiados)               aplicaciones)             interactivas)
       ↓                            ↓                        ↓
Compilador DDL            Compilador DML           Compilador de consultas
       ↓                            ↓                        ↓
                         Catálogo del sistema
                    (metadatos: estructuras de la BD)
                                   ↓
                    Administrador de datos almacenados
                                   ↓
                    Base de datos (archivos en disco)
```

- **Compilador DDL:** interpreta definiciones y guarda metadatos en el catálogo
- **Compilador DML:** transforma comandos en código objeto que accede a la base
- **Compilador de consultas:** verifica sintaxis, que los objetos existan en el catálogo y que las sentencias estén bien formadas
- **Control de concurrencia:** garantiza que múltiples usuarios puedan operar simultáneamente sin interferir

---

## Síntesis

El flujo completo de construcción de una base de datos:

1. El **cliente** solicita modelar un mini-mundo de su interés
2. El **diseñador** crea la base y el esquema conceptual → usa DDL
3. El **desarrollador** crea programas y el esquema externo → usa DML
4. El **DBA** administra el esquema interno → usa comandos privilegiados
5. Los **usuarios finales** acceden a través de las vistas que se construyeron para ellos
