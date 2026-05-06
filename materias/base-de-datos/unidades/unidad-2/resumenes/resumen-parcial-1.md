# Resumen Parcial 1 — Unidad 2: Diseño Lógico de Bases de Datos

## El modelo relacional

Una base de datos relacional organiza la información en **tablas**. Dentro de cada tabla:

- Cada **fila** es una *tupla* — un registro concreto (ej: un cliente específico)
- Cada **columna** es un *atributo* — una propiedad de esa entidad (ej: nombre, edad, DNI)
- El **dominio** de un atributo es el conjunto de valores que puede tomar (ej: el dominio de "edad" son enteros positivos)

---

## Entidades

Una **entidad** es cualquier cosa del mundo real sobre la que querés guardar información. Puede ser un objeto físico (un libro, un auto) o abstracto (un préstamo, una venta).

En el diagrama E-R se representa con un **rectángulo**.

---

## Atributos

Son las propiedades de una entidad. Hay cuatro tipos:

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Común (simple)** | Un solo valor, indivisible | `Nombre`, `Color` |
| **Multivaluado** | Puede tener más de un valor | `Teléfono` (varias líneas) |
| **Compuesto** | Se forma uniendo varios atributos | `Dirección = {Calle, Número, CP, Localidad}` |
| **Calculado/Derivado** | Se calcula a partir de otro atributo, no se guarda | `Edad` (de FechaNacimiento), `MontoTotal` |

El **grado** de una entidad es cuántos atributos tiene.

> Los atributos multivaluados generan su propia tabla en el pasaje a tablas.
> Los atributos derivados se representan con óvalo punteado y no se almacenan.

---

## Claves

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Candidata** | Atributo (o conjunto mínimo) que identifica unívocamente cada tupla | `DNI`, `CUIL` |
| **Primaria (PK)** | La clave candidata elegida como identificador oficial | Se elige la más simple |
| **Alternativa** | Clave candidata no elegida como primaria | Si PK = DNI, entonces CUIL es alternativa |
| **Super-clave** | Conjunto que incluye la PK más atributos extra (redundante) | `{DNI, Apellido}` |
| **Foránea (FK)** | Atributo que apunta a la PK de otra tabla | `CódSocio` en tabla Préstamos |

---

## Integridad referencial

El DBMS garantiza que **no puede existir una FK que apunte a una tupla inexistente** en la tabla padre.

Ejemplo: si en `Préstamos` hay un registro con `CódSocio = 14`, entonces el socio 14 tiene que existir en la tabla `Socios`. Si no existe, el DBMS rechaza el registro.

---

## Relaciones

Asociación entre dos o más entidades. Se representa con un **rombo** en el diagrama E-R.

### Aridad (cuántas entidades participan)

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Unaria** | La entidad se relaciona consigo misma | Empleado supervisa a Empleado |
| **Binaria** | Dos entidades distintas | Cliente compra Producto |
| **Ternaria** | Tres entidades | — |

### Cardinalidad (cuántas tuplas participan de cada lado)

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **1-1** | Una tupla de A con exactamente una de B | Empleado ↔ Legajo |
| **1-N** | Una tupla de A con muchas de B | Socio → Préstamos |
| **N-M** | Muchas de A con muchas de B | Clientes ↔ Productos |

> Si una relación N-M tiene atributos propios (como `Cantidad`), esos atributos pertenecen a la relación, no a ninguna entidad.

---

## Pasaje a tablas (Diccionario de datos)

| Regla | Acción |
|-------|--------|
| Por cada **entidad** | 1 tabla |
| Por cada **atributo multivaluado** | 1 tabla con FK a la entidad padre |
| Por cada **relación N-M** | 1 tabla cuya PK = combinación de FK de ambas entidades |
| Por cada **relación 1-N** | No se crea tabla nueva; la FK va en el lado "muchos" |
| Por cada **relación 1-1** | No se crea tabla nueva; la FK va en cualquiera de las dos |

**Fórmula para contar tablas:**
```
Total = entidades + atributos multivaluados + relaciones N-M
```

**Ejemplo biblioteca:**
- 4 entidades (Libro, Autor, Socio, Préstamo) → 4 tablas
- 1 atributo multivaluado (Email de Socios) → 1 tabla
- 2 relaciones N-M (Préstamo-Libro, Autor-Libro) → 2 tablas
- **Total: 7 tablas**

---

## Especialización (herencia)

Cuando una entidad tiene subtipos con atributos propios.

- La entidad padre se llama **superclase**
- Las derivadas se llaman **subclases**
- Las subclases heredan la PK de la superclase como su FK

```
Libro:   {Código (PK), Título, Edición}
Físico:  {Código (FK → Libro), NúmeroEjemplar}
Digital: {Código (FK → Libro), URL}
```

Si un libro existe en `Físico`, también debe existir en `Libro`.

---

## Agregación

Se usa cuando una relación N-M entre dos entidades necesita relacionarse con una tercera como si fuera una unidad, y **solo son válidas las combinaciones pre-definidas**.

Ejemplo: el menú de un restaurante define combinaciones válidas de Comida-Ingrediente. Un comensal solo puede pedir combinaciones que ya existen en el menú, no cualquier par.

```
Comida_Ingrediente: {CódComida (FK), CódIngrediente (FK), Cantidad}

Pedido: {CódComensal (FK), CódComida (FK → Comida_Ingrediente), CódIngrediente (FK → Comida_Ingrediente)}
```

> Diferencia con relación ternaria: en la ternaria cualquier combinación es válida; en la agregación, solo las que ya están definidas en la tabla intermedia.

---

## Checklist para el parcial

- [ ] Leer el enunciado e identificar entidades, atributos y relaciones
- [ ] Determinar la cardinalidad de cada relación (1-1, 1-N, N-M)
- [ ] Dibujar o describir el DER con la notación correcta
- [ ] Hacer el pasaje a tablas aplicando las cuatro reglas
- [ ] Identificar PK y FK en cada tabla resultante
- [ ] Reconocer cuándo usar especialización y cuándo usar agregación
