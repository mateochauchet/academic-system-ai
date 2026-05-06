# Resumen — Unidad 1: Introducción a los Sistemas de Base de Datos

## 1. Datos e información

Aunque se usan como sinónimos en el lenguaje cotidiano, en el contexto de bases de datos tienen significados distintos. Los **datos** son hechos en bruto: números, nombres, fechas, que por sí solos no dicen nada. La **información** es el resultado de procesar esos datos y darles un significado en un contexto determinado.

Una **base de datos** es una colección de hechos con un significado relevante para el mundo que nos interesa modelar, organizados con un propósito específico. Dos condiciones son clave: los datos deben tener coherencia interna (representar correctamente el mini-mundo que modelan) y deben actualizarse tan pronto como cambia la realidad que describen.

---

## 2. Del procesamiento de archivos al DBMS

Antes de las bases de datos, las aplicaciones manejaban sus propios archivos. Cada programa definía sus registros, sus rutas, su formato. Este enfoque generaba dos problemas graves:

**Dependencia física aplicación-archivo.** Si un archivo se movía de carpeta o se renombraba, todos los programas que lo usaban rompían. No había ninguna capa de abstracción entre el programa y el lugar físico donde vivían los datos.

**Acceso monousuario.** Si un programa tenía abierto un archivo para generar un reporte, ningún otro programa podía escribir sobre él al mismo tiempo. El acceso era exclusivo.

Estos problemas motivaron la creación del DBMS: un sistema que actúa como intermediario entre las aplicaciones y los datos físicos, y que resuelve ambas limitaciones.

---

## 3. DBMS — Definición, funciones y ventajas

Un **DBMS (Database Management System)** es una colección de programas que permite crear y mantener una base de datos. Sus funciones principales son cuatro:

- **Definir** la base: especificar tipos de datos, estructuras y restricciones.
- **Construir** la base: almacenar los datos en algún medio controlado por el DBMS.
- **Manipular** la base: consultar, actualizar, generar reportes.
- **Compartir** la base: permitir acceso concurrente a múltiples usuarios y aplicaciones.

### Ventajas sobre el procesamiento de archivos

| Problema anterior | Solución del DBMS |
|---|---|
| Dependencia física entre programa y archivo | **Aislamiento programa-datos:** el programa no sabe ni le importa dónde viven físicamente los datos |
| Una sola vista posible de los datos | **Múltiples vistas:** cada usuario ve solo la parte que le corresponde |
| Acceso exclusivo por un solo proceso | **Procesamiento multiusuario** con control de concurrencia |
| Sin autodescripción | **Meta-data:** la base se describe a sí misma en el catálogo del sistema |

El **catálogo del sistema** (o diccionario de datos) es donde el DBMS guarda los metadatos: la estructura de las tablas, los tipos de datos, las restricciones, los índices. Es la "base de datos de la base de datos". Gracias al catálogo, el DBMS puede entender la estructura de los datos sin que los programas tengan que conocerla.

---

## 4. Tipos de usuarios

Cuatro perfiles interactúan con una base de datos, con distintos niveles de acceso y responsabilidades:

**DBA (Administrador de Base de Datos).** Tiene los máximos privilegios. Se encarga de gestionar permisos de acceso, rendimiento, uso de recursos, backups y la definición del esquema interno (cómo se almacenan físicamente los datos). Es el responsable de que la base funcione de manera eficiente y segura.

**Diseñador.** Trabaja antes de que la base exista. Relevando las necesidades de los usuarios y el negocio, diseña el modelo conceptual: qué entidades existen, qué relaciones tienen, qué atributos importan. También define qué vistas verá cada tipo de usuario.

**Analistas y Programadores.** Los analistas traducen los requerimientos del negocio en especificaciones técnicas. Los programadores crean las aplicaciones que interactúan con la base de datos a través del DML embebido en el código.

**Usuarios Finales.** Interactúan con la base indirectamente, a través de interfaces o vistas construidas para ellos. No conocen el esquema completo ni necesitan hacerlo.

---

## 5. Arquitectura de tres esquemas

La arquitectura de tres esquemas (o arquitectura ANSI/SPARC) es el modelo que describe cómo se organiza internamente un DBMS. Tiene tres niveles que se apilan uno sobre el otro, y cada nivel oculta al nivel superior los detalles del inferior.

```
┌─────────────────────────────────────────────┐
│   NIVEL EXTERNO (vistas de usuario)         │  ← Usuarios finales
│   Cada usuario ve solo lo que le corresponde│
├─────────────────────────────────────────────┤
│   NIVEL CONCEPTUAL (esquema lógico)         │  ← Diseñadores y desarrolladores
│   Estructura completa, sin detalle físico   │
├─────────────────────────────────────────────┤
│   NIVEL INTERNO (esquema físico)            │  ← DBA
│   Archivos en disco, índices, rutas físicas │
└─────────────────────────────────────────────┘
```

**Nivel interno:** describe cómo se almacenan físicamente los datos. Archivos, índices, rutas de acceso. Solo el DBA trabaja a este nivel.

**Nivel conceptual:** describe la estructura lógica completa de la base: qué entidades existen, qué atributos tienen, qué restricciones se aplican, qué relaciones hay entre ellas. Es independiente de cómo se almacena físicamente.

**Nivel externo:** son las vistas que se construyen para los distintos grupos de usuarios. Cada vista es un subconjunto del esquema conceptual, adaptado a lo que ese usuario necesita ver.

---

## 6. Independencia de datos

La independencia de datos es la capacidad de modificar un nivel del esquema sin impactar a los niveles superiores. Hay dos tipos:

### Independencia física
La capacidad de cambiar el **esquema interno** (cómo se almacenan los datos en disco) sin necesidad de modificar el esquema conceptual ni los programas de aplicación.

Ejemplo: el DBA agrega un disco nuevo y reorganiza los archivos físicos. Ningún usuario, ninguna aplicación, ni el esquema lógico se ven afectados. Esta operación puede hacerse incluso con la base en funcionamiento.

### Independencia lógica
La capacidad de cambiar el **esquema conceptual** sin necesidad de modificar los esquemas externos ni los programas de aplicación.

Ejemplo: se agrega un nuevo atributo a la tabla de clientes (un score de crédito). Las vistas existentes, que no usan ese atributo, siguen funcionando sin cambios.

La independencia lógica es más difícil de lograr que la física, porque los programas de aplicación suelen depender más de la estructura lógica que de la física.

---

## 7. Lenguajes del DBMS (Data Sublanguages)

El término **Data Sublanguage** hace referencia a que los lenguajes de bases de datos son sublengajes especializados, diseñados para operar sobre datos. En los DBMS modernos, SQL cumple todos estos roles, pero conceptualmente se distinguen tres lenguajes:

| Lenguaje | Nombre completo | Propósito |
|---|---|---|
| **DDL** | Data Definition Language | Define la base de datos a nivel conceptual: crea tablas, restricciones, relaciones |
| **SDL** | Storage Definition Language | Define el nivel interno: cómo y dónde se almacenan físicamente los datos |
| **DML** | Data Manipulation Language | Define vistas de usuarios y permite consultar y manipular los datos |

**Orden de implementación:** primero se define el esquema conceptual e interno con DDL y SDL. Solo después se puede definir el esquema externo con DML. No puede hacerse al revés, porque el esquema externo depende de que el conceptual ya exista.

### Tablas y manipulación de datos

En el modelo relacional, los datos se organizan en **tablas** (también llamadas relaciones). Cada tabla tiene columnas (atributos) y filas (registros o tuplas). El DML permite realizar cuatro operaciones fundamentales sobre estas tablas:

- **SELECT** — Consultar datos
- **INSERT** — Insertar nuevas filas
- **UPDATE** — Modificar filas existentes
- **DELETE** — Eliminar filas

---

## 8. Módulos componentes del DBMS

El DBMS internamente está compuesto por módulos que procesan los distintos tipos de pedidos:

```
DBA                    Programadores              Usuarios Finales
(DDL + comandos        (DML embebido en           (consultas
 privilegiados)         aplicaciones)              interactivas)
       ↓                      ↓                         ↓
Compilador DDL      Compilador DML           Compilador de consultas
       ↓                      ↓                         ↓
                    Catálogo del sistema
               (metadatos: estructura de la BD)
                              ↓
               Administrador de datos almacenados
                              ↓
               Base de datos (archivos en disco)
```

**Compilador DDL:** interpreta las definiciones de estructura (CREATE TABLE, etc.) y guarda los metadatos en el catálogo.

**Compilador DML:** transforma los comandos de manipulación escritos en el código de las aplicaciones en instrucciones que el motor puede ejecutar.

**Compilador de consultas:** verifica que la sintaxis sea correcta, que los objetos referenciados existan en el catálogo, y que la consulta esté bien formada antes de ejecutarla.

**Control de concurrencia:** garantiza que múltiples usuarios puedan operar simultáneamente sin interferir entre sí (por ejemplo, que dos usuarios no puedan modificar el mismo registro al mismo tiempo de forma inconsistente).

---

## 9. Ambientes de bases de datos

Los DBMS pueden desplegarse en distintos ambientes según las necesidades:

**Centralizado:** un único servidor concentra todo el procesamiento. Simple de administrar, pero puede ser un cuello de botella.

**Cliente-servidor:** el servidor corre el motor de base de datos y los clientes envían consultas. Es el modelo más común en aplicaciones empresariales.

**Distribuido:** los datos están repartidos en múltiples nodos físicos pero se acceden como si fueran una base única. Permite mayor disponibilidad y escalabilidad, pero añade complejidad en la consistencia.

**En la nube:** el DBMS corre en infraestructura de un proveedor externo (AWS RDS, Google Cloud SQL, etc.). El proveedor gestiona la disponibilidad, los backups y el hardware.

---

## Conceptos clave

| Término | Definición |
|---|---|
| **Base de datos** | Colección de hechos con significado relevante para un mini-mundo, con un propósito específico |
| **DBMS** | Software que permite definir, construir, manipular y compartir una base de datos |
| **Meta-data / Catálogo** | Datos sobre la estructura de la base, guardados por el propio DBMS |
| **Aislamiento programa-datos** | La aplicación no conoce ni depende de la ubicación física de los datos |
| **Arquitectura tres esquemas** | Separación en niveles externo, conceptual e interno para lograr independencia de datos |
| **Independencia física** | Cambiar el almacenamiento físico sin afectar el esquema conceptual |
| **Independencia lógica** | Cambiar el esquema conceptual sin afectar las vistas ni los programas |
| **DDL** | Lenguaje para definir estructuras de la base (nivel conceptual) |
| **SDL** | Lenguaje para definir el almacenamiento físico (nivel interno) |
| **DML** | Lenguaje para definir vistas y manipular datos |
| **DBA** | Administrador de la base de datos, máximos privilegios |
| **Control de concurrencia** | Mecanismo que permite acceso simultáneo sin inconsistencias |
