# Resumen — Unidad 2: División en Módulos y Verificación

## De qué trata la unidad

La unidad 1 te enseñó a *medir* qué tan bueno es un algoritmo. La unidad 2 te enseña a *construirlo bien*: cómo dividirlo en partes manejables y cómo verificar que funciona correctamente.

---

## 1. División en módulos

Cuando un problema es complejo, no lo resolvés de una sola vez. Lo partís en subproblemas más chicos, cada uno resuelto por un **módulo** (también llamado rutina, subprograma o subrutina — son todos sinónimos).

El algoritmo principal queda como una lista de llamadas a módulos:

```
Algoritmo Principal
    ObtenerNotas()
    CalcularPromedio()
    MostrarResultados()
FinAlgoritmo
```

Esto se llama **análisis descendente o Top-Down**: arrancás desde el problema general y vas bajando hasta llegar a tareas simples.

**¿Por qué modularizar?**
- El código es más fácil de leer y entender.
- Podés reutilizar un módulo en otros programas.
- Podés probar cada parte por separado.
- Si algo falla o hay que cambiar algo, el cambio queda aislado en un solo módulo.

---

## 2. Abstracción y ocultamiento de información

**Abstracción** es enfocarse en *qué hace* un módulo, sin preocuparte por *cómo lo hace*. Cuando llamás a `CalcularPromedio()`, te importa que te devuelva el promedio — no cómo lo calculó internamente.

**Ocultamiento de información** es que todo lo que pasa adentro de un módulo (variables intermedias, pasos de cálculo) es privado. El resto del programa no lo ve ni necesita verlo.

La imagen que usa la cátedra para esto es la **caja negra**: sabés qué entra y qué sale, pero no ves el interior.

```
Entrada → [ módulo ] → Salida
            (caja negra)
```

Cada módulo debe resolver **una sola tarea**. Si un módulo hace dos cosas, hay que partirlo.

---

## 3. Verificación vs. Validación

**Verificación** → ¿Lo construiste correctamente? Chequea que el software cumple con los requerimientos técnicos especificados.

**Validación** → ¿Construiste lo correcto? Chequea que el software cumple con lo que el cliente realmente necesita.

Son parecidos pero apuntan a cosas distintas. Podés verificar que el código hace lo que dice la especificación, pero si la especificación estaba mal desde el principio, la validación lo detecta.

---

## 4. Técnicas: estáticas vs. dinámicas

**Inspección de software (estática):** analizás el código, diagramas o documentación *sin ejecutar nada*. Se puede hacer en cualquier momento del desarrollo, incluso antes de tener código ejecutable.

**Pruebas de software (dinámica):** ejecutás el programa con datos de prueba y comparás el resultado con lo esperado. Necesitás una versión que corra.

---

## 5. Etapas de las pruebas

| Etapa | Qué se prueba |
|---|---|
| **Prueba de unidades** | Cada módulo por separado |
| **Prueba de integración** | Grupos de módulos juntos |
| **Prueba de sistema** | El sistema completo |
| **Prueba de aceptación** | El sistema en un entorno real con el usuario |

Primero probás las piezas, después el conjunto.

---

## 6. Caja negra vs. Caja blanca

**Caja negra** — probás la *funcionalidad* sin ver el código. Le das entradas y verificás que las salidas sean las correctas.

**Caja blanca** — tenés acceso al código y lo analizás por dentro. Buscás errores de lógica, bucles infinitos, ramas que nunca se ejecutan, etc.

Son complementarias: la caja negra detecta si el resultado es correcto, la caja blanca detecta por qué puede estar mal internamente.

---

## Lo que suele entrar en el parcial

- Diferencia entre verificación y validación (con las preguntas clave de cada una)
- Diferencia entre caja negra y caja blanca
- Diferencia entre técnicas estáticas y dinámicas
- Qué es la abstracción y el ocultamiento de información
- Dado un algoritmo monolítico, identificar cómo modularizarlo
- Las etapas de pruebas en orden

---

## Preguntas de autocontrol

1. ¿Cuál es la diferencia entre verificación y validación? Dá un ejemplo de cada una.
2. Un módulo que calcula el descuento de una factura Y además imprime el resultado, ¿está bien diseñado? ¿Por qué?
3. ¿En qué se diferencia una prueba de caja negra de una de caja blanca? ¿Cuándo usarías cada una?
4. ¿Qué ventaja tiene hacer prueba de unidades antes que prueba de sistema?
5. ¿Qué significa que una prueba es "estática"? ¿Podés hacerla sin tener el código terminado?
