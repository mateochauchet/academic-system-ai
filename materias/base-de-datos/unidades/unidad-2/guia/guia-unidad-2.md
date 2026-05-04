# Guía Unidad 2 — Diseño Lógico de Bases de Datos

## Introducción

El diseñador comienza reuniéndose con el cliente para entender el "mini-mundo" a modelar. El cliente habla en lenguaje natural de su negocio; el diseñador debe hacer las preguntas correctas para extraer los datos relevantes y sus relaciones.

**Regla práctica:** los sustantivos importantes del relato del cliente son las **entidades**; los sustantivos secundarios (propiedades de esas entidades) son los **atributos**; los verbos de acción entre entidades son las **relaciones**.

---

## 1. Modelo Relacional

> El modelo relacional representa la base de datos como una colección de **entidades** relacionadas entre sí, donde cada entidad se puede ver como una **tabla**.

| Concepto relacional | Equivalente en tabla |
|---|---|
| Entidad | Tabla |
| T-upla (tupla) | Fila |
| Atributo | Columna |
| Dominio | Conjunto de valores posibles de un atributo |

El dominio de un atributo está relacionado con su tipo de dato. Dos atributos de entidades distintas pueden compartir el mismo dominio (ej: la calle en la dirección de clientes y empleados).

---

## 2. Modelo Entidad-Relación (E-R)

Notación gráfica del esquema conceptual:

```
ENTIDAD          → rectángulo
ATRIBUTO         → óvalo
RELACIÓN         → rombo con líneas a las entidades
CARDINALIDAD     → símbolo en el extremo de cada línea (1 o N)
```

### Tipos de atributos

| Tipo | Descripción | Ejemplo |
|---|---|---|
| **Común** | Un solo valor, indivisible, no derivable | Nombre, Color |
| **Multivaluado** | Puede tomar más de un valor | Teléfono, Email |
| **Compuesto** | Se forma por la unión de varios atributos | Dirección = {Calle, Número, CP, Localidad} |
| **Calculado/Derivado** | Se calcula a partir de otro atributo | Edad (de fecha de nacimiento), Monto = precio × cantidad × 1.21 |

**Grado** de una entidad: la cantidad de atributos que tiene.

---

## 3. Claves

### Tipos de claves

**Clave candidata:** atributo (o conjunto mínimo de atributos) que identifica unívocamente cada t-upla de una entidad.

**Clave primaria (PK):** la clave candidata elegida para identificar las t-uplas. Se elige la más simple (generalmente un número corto).

**Clave alternativa:** otra clave candidata que no fue elegida como primaria. En el ejemplo: si se usa `código` como PK, el `CUIT` es clave alternativa.

**Super-clave:** conjunto de atributos que incluye la clave pero tiene atributos de más. Ejemplo: `{CUIT, Apellido}` es super-clave porque solo el CUIT ya alcanza.

**Clave foránea (FK):** atributo en una tabla que referencia la clave primaria de otra tabla. Sirve para "atar" t-uplas entre tablas relacionadas.

### Integridad Referencial

El DBMS garantiza que no pueda existir una clave foránea que apunte a una t-upla inexistente en la tabla padre. Ejemplo: no se puede crear un email para el socio código=14 si ese socio no existe en la tabla Socios.

---

## 4. Relaciones y Cardinalidad

### Tipos de relaciones según aridad

| Tipo | Participantes | Ejemplo |
|---|---|---|
| **Unaria** | La entidad se relaciona consigo misma | Empleado supervisa a Empleado (jefe-subordinado) |
| **Binaria** | Dos entidades | Cliente compra Producto |
| **Ternaria** | Tres entidades | — |

### Cardinalidad

Indica cuántas t-uplas de cada entidad participan en la relación:

| Cardinalidad | Descripción | Ejemplo |
|---|---|---|
| **1-1** | Una t-upla se relaciona con exactamente una de la otra | — |
| **1-N** | Una t-upla se relaciona con muchas de la otra | Un socio tiene muchos préstamos |
| **N-M** | Muchas t-uplas de cada lado | Clientes compran muchos productos; productos son comprados por muchos clientes |

Un atributo en una relación N-M pertenece a la relación, no a las entidades. Ejemplo: `cantidad` en la relación Clientes-Productos indica cuántas unidades de un producto específico compró un cliente específico.

---

## 5. Diccionario de Datos — Pasaje a Tablas

El diccionario de datos es el resultado de convertir el esquema conceptual (DER) al esquema interno (tablas).

### Reglas de pasaje

**1 tabla por cada entidad**

**1 tabla por cada atributo multivaluado** — con FK a la entidad padre
```
Email: {Código, Dirección, CódSocio (FK Socios)}
```

**1 tabla por cada relación N-M** — su clave es la combinación de las FK de ambas entidades
```
Préstamo_Libro: {CodLibro (FK Libros), CodPréstamo (FK Préstamos)}
```

**Para relaciones 1-N** — la FK va en la tabla del lado "Muchos"
```
Préstamo: {ID, Fecha, FechaDevolución, CódSocio (FK Socios)}
```

### Fórmula de conteo de tablas
```
# tablas = entidades + atributos multivaluados + relaciones N-M
```

**Ejemplo biblioteca:**
- 4 entidades (Libro, Autor, Socio, Préstamo) → 4 tablas
- 1 atributo multivaluado (Email de Socios) → 1 tabla
- 2 relaciones N-M (Préstamo-Libro, Autor-Libro) → 2 tablas
- **Total: 7 tablas**

---

## 6. Refinamiento del Modelo

### Especialización (herencia)

Cuando una entidad tiene subtipos con atributos propios se usa especialización:

```
         Libro
        /     \
    Físico   Digital
```

- **Superclase** (Libro): tiene la PK y todos los atributos comunes (título, edición)
- **Subclases** heredan la PK de la superclase como FK

```
Libro:   {Código, Título, Edición}
Digital: {ID (FK Libro), URL}
Físico:  {ID (FK Libro), NúmeroEjemplar}
```

No tiene sentido que un libro físico tenga URL ni que un libro digital tenga número de ejemplar.

### Agregación (menú)

Se usa cuando una relación N-M entre dos entidades actúa como una sola entidad para relacionarse con una tercera. El "menú" es una tabla de combinaciones válidas pre-definidas, y solo se pueden elegir combinaciones que ya existan en esa tabla.

**Pasaje a tablas de la agregación:**
```
Comida-Ingrediente: {CodComida (FK Comida), CodIngrediente (FK Ingrediente), Cant}
```

La relación del comensal con la agregación:
```
Comensal-Comida-Ingrediente: {
  CodComensal (FK Comensal),
  CodComida (FK Comida-Ingrediente),
  CodIngrediente (FK Comida-Ingrediente)
}
```

Las FK de Comida e Ingrediente solo pueden tomar combinaciones que ya existen en la tabla de la agregación. No son válidas todas las combinaciones posibles.

---

## Síntesis

```
Relato del cliente
        ↓
Diagrama E-R (esquema conceptual)
  → entidades, atributos, relaciones, cardinalidades
        ↓
Diccionario de datos (pasaje a tablas)
  → 1 tabla/entidad + 1 tabla/multivaluado + 1 tabla/N-M
  → claves primarias, claves foráneas, integridad referencial
        ↓
Base de datos implementada
```
