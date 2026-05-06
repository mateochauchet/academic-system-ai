# Resumen — Unidad 2: Diseño Lógico de Bases de Datos

## 1. Del relato del cliente al modelo

El diseñador se reúne con el cliente para entender el "mini-mundo" que se quiere modelar. El cliente habla en lenguaje natural; el diseñador tiene que hacer las preguntas correctas para extraer los datos y sus relaciones.

**Regla práctica para identificar los componentes:**
- Los **sustantivos importantes** del relato son las **entidades**.
- Los **sustantivos secundarios** (propiedades de esas entidades) son los **atributos**.
- Los **verbos de acción** entre entidades son las **relaciones**.

El producto de este proceso es el **Diagrama Entidad-Relación (DER)**, que representa el esquema conceptual de la base de datos antes de pasar a su implementación física.

---

## 2. Modelo Relacional

El modelo relacional es la forma en que se estructura la información dentro de una base de datos. Representa todo como un conjunto de **tablas** relacionadas entre sí.

| Concepto relacional | Equivalente en tabla |
|---|---|
| **Entidad** | Tabla |
| **Tupla** | Fila |
| **Atributo** | Columna |
| **Dominio** | Conjunto de valores posibles para un atributo |

El **dominio** está relacionado con el tipo de dato del atributo. Dos atributos de entidades distintas pueden compartir el mismo dominio: por ejemplo, la calle en la dirección de un cliente y la calle en la dirección de un empleado son del mismo dominio aunque pertenezcan a entidades distintas.

---

## 3. Entidades y tipos de entidades

Una **entidad** es cualquier objeto del mundo real sobre el que queremos guardar información. Puede ser una persona, un lugar, un evento, un concepto.

Se representa en el DER como un **rectángulo**.

Existen dos tipos de entidades relevantes en el diseño:

**Entidad fuerte:** tiene una clave propia que la identifica de forma unívoca, sin depender de ninguna otra entidad.

**Entidad débil:** no puede identificarse por sí sola. Depende de la existencia de otra entidad (su entidad padre o propietaria). Su clave se forma combinando la clave de la entidad padre con algún atributo discriminador propio. Ejemplo: una habitación no existe sin el hotel al que pertenece.

---

## 4. Atributos

Los atributos son las propiedades que describen a una entidad. Se representan en el DER como **óvalos** conectados al rectángulo de la entidad.

| Tipo | Descripción | Ejemplo |
|---|---|---|
| **Común** | Un solo valor, indivisible, no derivable de otro | Nombre, Color |
| **Multivaluado** | Puede tomar más de un valor para una misma tupla | Teléfono, Email |
| **Compuesto** | Se forma por la unión de varios atributos simples | Dirección = {Calle, Número, CP, Localidad} |
| **Calculado / Derivado** | Su valor se obtiene a partir de otro atributo, no se almacena directamente | Edad (calculada de FechaNacimiento), Monto = precio × cantidad × 1.21 |

**Grado de una entidad:** la cantidad de atributos que tiene. No confundir con la cardinalidad.

---

## 5. Claves

### Clave candidata
Es un atributo (o conjunto **mínimo** de atributos) que identifica unívocamente cada tupla de una entidad. Mínimo significa que no se puede quitar ningún atributo sin perder esa capacidad de identificación.

### Clave primaria (PK)
La clave candidata elegida para identificar las tuplas en la base de datos implementada. Se elige la más simple y estable posible (generalmente un código numérico corto).

### Clave alternativa
Toda clave candidata que no fue elegida como primaria. Sigue siendo única. Ejemplo: si se usa `Código` como PK, el `CUIT` es clave alternativa.

### Super-clave
Conjunto de atributos que incluye la clave candidata pero tiene atributos de más (es redundante). Ejemplo: `{CUIT, Apellido}` es super-clave porque con solo `CUIT` ya alcanza para identificar la tupla.

### Clave foránea (FK)
Atributo en una tabla que referencia la clave primaria de otra tabla. Es el mecanismo que "conecta" dos tablas y permite navegar la relación entre ellas.

---

## 6. Integridad

### Integridad de la entidad
Ningún atributo que forme parte de la clave primaria puede ser nulo. Una tupla sin clave no puede existir en la base.

### Integridad referencial
El DBMS garantiza que no pueda existir una clave foránea que apunte a una tupla inexistente en la tabla padre. Si la tabla `Préstamos` tiene una FK hacia `Socios`, no se puede cargar un préstamo con un código de socio que no existe en la tabla `Socios`. Tampoco se puede eliminar un socio que tenga préstamos asociados, a menos que se eliminen primero los préstamos.

---

## 7. Relaciones y cardinalidad

### Tipos de relación según aridad (grado)

| Tipo | Participantes | Ejemplo |
|---|---|---|
| **Unaria** | La entidad se relaciona consigo misma | Empleado supervisa a Empleado (jefe-subordinado) |
| **Binaria** | Dos entidades distintas | Cliente compra Producto |
| **Ternaria** | Tres entidades | — |

Las relaciones se representan en el DER como un **rombo** con líneas hacia cada entidad participante.

### Cardinalidad

La cardinalidad define cuántas tuplas de una entidad pueden estar asociadas a cuántas tuplas de la otra en una relación.

| Cardinalidad | Descripción |
|---|---|
| **1-1** | Una tupla de A se relaciona con exactamente una tupla de B, y viceversa |
| **1-N** | Una tupla de A se relaciona con muchas tuplas de B, pero cada B se relaciona con solo una A |
| **N-M** | Muchas tuplas de A se relacionan con muchas tuplas de B |

**Ejemplo 1-N:** Un socio tiene muchos préstamos, pero cada préstamo pertenece a un solo socio.

**Ejemplo N-M:** Un cliente puede comprar muchos productos, y un producto puede ser comprado por muchos clientes.

### Atributos en relaciones N-M

Cuando una relación es N-M, puede tener atributos propios. Estos atributos pertenecen a la relación, no a ninguna de las entidades. Ejemplo: `cantidad` en la relación entre Cliente y Producto indica cuántas unidades de ese producto específico compró ese cliente específico. No tiene sentido poner `cantidad` en Cliente (¿cantidad de qué?) ni en Producto (¿para qué cliente?).

### Participación

La participación indica si la presencia de una entidad en una relación es obligatoria u opcional:

**Participación total:** todas las tuplas de la entidad deben participar en la relación. Ejemplo: todo préstamo debe estar asociado a un socio (no puede existir un préstamo sin socio).

**Participación parcial:** no todas las tuplas están obligadas a participar. Ejemplo: no todos los socios tienen préstamos activos.

---

## 8. DER — Notación Chen

El Diagrama Entidad-Relación en notación Chen usa la siguiente simbología:

```
ENTIDAD          → rectángulo
ATRIBUTO         → óvalo conectado al rectángulo
   └─ PK         → atributo subrayado
   └─ Multival.  → óvalo con doble borde
   └─ Derivado   → óvalo con borde punteado
   └─ Compuesto  → óvalo con sub-óvalos
RELACIÓN         → rombo con líneas hacia las entidades
CARDINALIDAD     → 1 o N en el extremo de cada línea
```

---

## 9. Diccionario de datos — Pasaje a tablas

El diccionario de datos es el resultado de traducir el DER (esquema conceptual) al conjunto de tablas que se van a implementar (esquema lógico/interno). Es la especificación formal de cada tabla: qué columnas tiene, cuáles son PK y cuáles son FK.

### Reglas de pasaje

**1 tabla por cada entidad.** Cada entidad del DER se convierte en una tabla. Sus atributos simples se convierten en columnas.

**1 tabla por cada atributo multivaluado.** Como un atributo multivaluado puede tener varios valores para una misma tupla, no puede representarse como una columna simple. Se crea una tabla separada con una FK hacia la entidad padre.
```
Email: {Código_PK, Dirección, CódSocio_FK → Socios}
```

**1 tabla por cada relación N-M.** La relación se convierte en una tabla cuya clave primaria es la combinación de las FK de ambas entidades. Los atributos propios de la relación también van en esta tabla.
```
Préstamo_Libro: {CodLibro_FK → Libros, CodPréstamo_FK → Préstamos}
```

**Para relaciones 1-N.** No se crea una tabla nueva. La FK va del lado "Muchos": la tabla del lado N recibe la PK de la tabla del lado 1 como clave foránea.
```
Préstamo: {ID_PK, Fecha, FechaDevolución, CódSocio_FK → Socios}
```

**Para relaciones 1-1.** La FK puede ir en cualquiera de las dos tablas. Convencionalmente se elige la entidad con participación total o la que conceptualmente "depende" de la otra.

### Fórmula de conteo de tablas

```
# tablas = entidades + atributos multivaluados + relaciones N-M
```

**Ejemplo biblioteca:**
- 4 entidades (Libro, Autor, Socio, Préstamo) → 4 tablas
- 1 atributo multivaluado (Email de Socios) → 1 tabla
- 2 relaciones N-M (Préstamo–Libro, Autor–Libro) → 2 tablas
- **Total: 7 tablas**

---

## 10. Refinamiento del modelo

### Especialización (herencia)

Cuando una entidad tiene subtipos con atributos propios que no aplican a todos los miembros, se usa especialización. Es el equivalente a la herencia en programación orientada a objetos.

```
         Libro
        /     \
    Físico   Digital
```

- La **superclase** (Libro) tiene la PK y los atributos comunes a todos los libros.
- Las **subclases** heredan la PK de la superclase y la usan como FK. Solo tienen sus atributos específicos.

```
Libro:   {Código_PK, Título, Edición}
Digital: {ID_PK_FK → Libro, URL}
Físico:  {ID_PK_FK → Libro, NúmeroEjemplar}
```

No tiene sentido que un libro físico tenga URL, ni que un libro digital tenga número de ejemplar.

### Agregación (menú)

Se usa cuando una relación N-M entre dos entidades actúa como una unidad para relacionarse con una tercera entidad. La relación N-M se "trata como una entidad" y se le agrega otra relación.

El caso típico es el menú de un restaurante: un menú es la combinación de una comida con sus ingredientes. Un comensal no puede pedir "pizza con cualquier ingrediente" — solo puede pedir combinaciones que ya existen en el menú.

```
Comida-Ingrediente: {CodComida_FK, CodIngrediente_FK, Cant}
```

La relación del comensal:
```
Pedido: {
  CodComensal_FK → Comensal,
  CodComida_FK → Comida-Ingrediente,
  CodIngrediente_FK → Comida-Ingrediente
}
```

Las FK de Comida e Ingrediente en el pedido solo pueden tomar combinaciones que ya existen en la tabla de la agregación. No son válidas todas las combinaciones posibles de comidas e ingredientes.

---

## 11. Diseños de calidad

Un buen diseño de base de datos evita:

**Redundancia:** no repetir la misma información en varios lugares. Si el nombre de un socio aparece en la tabla de Socios y también en cada préstamo, cualquier cambio hay que hacerlo en múltiples filas con riesgo de inconsistencia.

**Anomalías de actualización:** si un dato está repetido, modificarlo en un lugar y no en otro genera inconsistencia.

**Anomalías de inserción:** no debería ser necesario conocer toda la información para poder ingresar un registro parcial.

**Anomalías de eliminación:** borrar un registro no debería implicar perder información que corresponde a otra entidad.

La solución a estos problemas es la **normalización**: un conjunto de reglas que garantizan que cada dato esté en un solo lugar y que las dependencias entre atributos sean coherentes.

---

## Flujo completo de diseño

```
Relato del cliente (lenguaje natural)
        ↓
Identificar entidades, atributos y relaciones
        ↓
Diagrama E-R — esquema conceptual
  (entidades, atributos tipificados, relaciones, cardinalidades)
        ↓
Diccionario de datos — pasaje a tablas
  (1 tabla/entidad + 1 tabla/multivaluado + 1 tabla/N-M)
  (PK, FK, integridad referencial)
        ↓
Refinamiento del modelo
  (especialización, agregación)
        ↓
Base de datos implementada
```

---

## Conceptos clave

| Término | Definición |
|---|---|
| **Entidad** | Objeto del mundo real sobre el que se guarda información; se representa como tabla |
| **Tupla** | Una fila de una tabla; una instancia de la entidad |
| **Atributo** | Propiedad de una entidad; se representa como columna |
| **Dominio** | Conjunto de valores posibles para un atributo |
| **Grado** | Cantidad de atributos de una entidad |
| **Clave candidata** | Conjunto mínimo de atributos que identifica unívocamente una tupla |
| **Clave primaria (PK)** | La clave candidata elegida como identificador oficial |
| **Clave alternativa** | Clave candidata no elegida como PK |
| **Super-clave** | Conjunto de atributos que incluye la clave pero tiene atributos de más |
| **Clave foránea (FK)** | Atributo que referencia la PK de otra tabla |
| **Integridad referencial** | Garantía de que toda FK apunta a una tupla que existe en la tabla padre |
| **Cardinalidad** | Cuántas tuplas de cada lado participan en una relación (1-1, 1-N, N-M) |
| **Participación total** | Todas las tuplas de la entidad deben estar en la relación |
| **Participación parcial** | No todas las tuplas están obligadas a participar |
| **Especialización** | Subtipos de una entidad con atributos propios (herencia) |
| **Agregación** | Relación N-M que actúa como entidad para relacionarse con una tercera |
| **Diccionario de datos** | Especificación formal de las tablas que resultan del pasaje del DER |
