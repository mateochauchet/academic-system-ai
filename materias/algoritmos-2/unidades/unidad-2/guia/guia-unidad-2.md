# Guía Unidad 2 — División en Módulos y Verificación
**Estructuras y Algoritmos de Datos II | CAECE**
Contenidista: Maximiliano López

---

## 1. Introducción

Continuando desde la Unidad 1 (complejidad algorítmica), ahora se presenta una estrategia para construir programas más complejos y verificarlos: la **división por módulos**, que permite dividir el problema en subproblemas y simplificar el desarrollo.

---

## 2. Estrategia para Resolver Problemas

La estrategia es pensar en el problema general e ir descomponiéndolo en subproblemas. Estos subproblemas se siguen dividiendo hasta llegar a uno lo suficientemente simple como para resolverse de forma sencilla.

Se construye así un **algoritmo principal** y **subalgoritmos** para cada subproblema.

> En la bibliografía estos subalgoritmos aparecen con distintos nombres: **módulos, subprogramas, rutinas, subrutinas** — todos son sinónimos del mismo concepto.

---

### 2.1 Razones para Definir Rutinas

- **Simplifica la programación.** Una rutina es simple de programar.
- **Permite la reutilización de código.** Un módulo ya resuelto puede usarse en cualquier otro algoritmo que lo necesite, sin "reinventar la rueda".
- **El algoritmo resulta más simple y claro.** El algoritmo principal queda como una lista de llamadas a módulos — se entiende qué hace sin necesidad de conocer los detalles internos.
- **El programa es más simple para verificar.** Las pruebas se pueden realizar en cada módulo de forma independiente.
- **Reduce los tiempos de mantenimiento.** Los cambios quedan aislados al módulo correspondiente.

---

### 2.2 Abstracción

La abstracción se produce al crear módulos. Ejemplo: un algoritmo principal dividido en tres módulos:

```
Algoritmo Principal
    Obtener Notas de Un alumno
    Calcular Promedio De Notas
    Mostrar Promedio de Notas
Fin AlgoritmoPrincipal
```

El módulo "Calcular Promedio De Notas" solo se ocupa de calcular el promedio — no pide las notas ni muestra resultados. Está **abstraído** del resto. No sabemos cómo lo resuelve internamente: es la idea de una **"caja negra"** — sabemos qué necesita y qué hace, pero no cómo lo realiza.

Los módulos son independientes entre sí (aunque pueden colaborar), y es ideal que cada uno realice **una sola tarea**.

> **Abstracción:** aislamiento de un elemento de su contexto. En programación, la abstracción está relacionada con **"qué hace"**.

---

### 2.3 Ocultamiento de la Información

Concepto derivado de la abstracción. Las operaciones internas de un módulo (variables intermedias, pasos de cálculo) no son de interés para el resto del sistema — quedan **"ocultas"**.

Ejemplo: el módulo que calcula el promedio necesita sumar todos los números y contar la cantidad. Esa información es interna al módulo, no la expone hacia afuera.

> Un módulo resuelve un único problema dejando "oculto" el cómo lo realiza.

El ocultamiento también aplica en el **análisis previo** del problema: se define qué datos necesita el programa y qué resultados genera, sin especificar cómo se resolverá.

---

### 2.4 División en Módulos (Análisis Descendente — Top-Down)

Proceso para separar el problema en módulos:

1. **Analizar el problema** (Análisis Previo).
2. **Plantear el algoritmo principal** como una lista de acciones genéricas, divididas en las etapas de todo programa:
   - Entrada de datos
   - Proceso
   - Salida de datos
3. **Analizar cada módulo** y dividirlo en submódulos hasta llegar a una funcionalidad mínima, donde cada módulo realice **una sola tarea**.

> Este proceso permite ir descendiendo en la complejidad para tener módulos, o lo que luego serán las rutinas, cada vez más simples.

---

## 3. Verificación y Validación

Una vez finalizado el algoritmo, se debe comprobar si está bien o tiene errores. Para eso existen dos procesos diferenciados:

### 3.1 Verificación

Comprobar que el software **cumple con los requerimientos funcionales y no funcionales** (cumple la especificación).

> Pregunta clave: **¿Se está construyendo el producto correctamente?**

### 3.2 Validación

Comprobar que el software **cumple con las expectativas del cliente**, no solo con lo especificado.

> Pregunta clave: **¿Se está construyendo el producto concreto?**

> La Verificación y Validación son los procesos de análisis que aseguran que el software cumple con la especificación de requerimientos y las expectativas del usuario.

---

### 3.3 Técnicas de Verificación y Validación

| Técnica | Descripción | Tipo | Momento |
|---------|-------------|------|---------|
| **Inspección de Software** | Se analizan representaciones del sistema (diagramas, documentos, código fuente) en búsqueda de errores. No requiere que el programa esté terminado. | ESTÁTICO | Durante TODO el proceso de desarrollo |
| **Pruebas de Software** | Se constata dinámicamente el resultado de la ejecución contra lo esperable. Se definen datos de prueba, se ejecuta el software y se contrastan los resultados. Requiere versión ejecutable. | DINÁMICO | Luego del desarrollo |

---

### 3.4 Etapas del Proceso de Pruebas

| Etapa | Descripción | Cuándo |
|-------|-------------|--------|
| **Prueba de unidades** | Se prueban métodos, rutinas y clases de manera independiente. | Al finalizar el desarrollo de cada rutina |
| **Prueba de integración** | Se prueban agrupaciones de elementos del sistema ya validados individualmente. | Luego de las pruebas de unidades |
| **Prueba de sistema** | Se prueba el sistema completo. | Una vez desarrollados todos los componentes |
| **Prueba de aceptación** | Se prueba el sistema en un entorno real con participación del usuario. | Al final |

---

### 3.5 Caja Negra vs. Caja Blanca

#### Caja Negra (pruebas funcionales)
- Se enfoca en la **funcionalidad** del software.
- Se realiza **sin conocer la estructura interna** del código fuente.
- Evalúa el comportamiento del software desde el punto de vista del **usuario**.
- Detecta errores o comportamientos inesperados en las entradas/salidas.

```
Entrada → [ Funciones ] → Salida
           (caja negra)
```

#### Caja Blanca (pruebas estructurales)
- Se enfoca en la **estructura interna** del software.
- Requiere **acceso al código fuente** y conocimiento de la arquitectura y diseño.
- Busca errores en el código: bucles infinitos, problemas de lógica, redundancias, etc.

```
Entrada → [ lógica interna visible ] → Salida
           (caja blanca)
```

> Las pruebas de caja negra se enfocan en funcionalidad y resultados esperados. Las de caja blanca, en la estructura interna. **Ambas son complementarias** y necesarias para asegurar la calidad del software.

---

## 4. Conclusiones

En esta unidad se presentaron las técnicas para **validación de programas**:

- **División en módulos**: estrategia para resolver problemas complejos.
- **Verificación y Validación**: procesos para evaluar si se cumplen los requerimientos funcionales, no funcionales y las expectativas del cliente.
- **Caja negra y caja blanca**: técnicas de pruebas funcionales y estructurales.

---

## Bibliografía

- Bisbal Riera, J. (2013). *Manual de algorítmica: recursividad, complejidad y diseño de algoritmos.* Editorial UOC.
- Sedgewick, R. y Wayne, K. (2011). *Algorithms.* 4th Edition. Addison-Wesley.
- Cormen, T. et al. (2022). *Introduction to algorithms.* 4th Edition. The MIT Press.
