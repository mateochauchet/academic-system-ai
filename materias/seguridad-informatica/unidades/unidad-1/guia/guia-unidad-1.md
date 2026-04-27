# Guía de la Unidad I — Fundamentos de la Seguridad de la Información

**Contenidista:** Germán Ariel Paradisi

---

## Objetivos

- Reconocer y clasificar amenazas, vulnerabilidades y ataques en entornos digitales.
- Comprender los principios básicos de seguridad informática y sus componentes.
- Analizar y aplicar los pilares fundamentales de seguridad informática en la protección de sistemas y datos.

**Palabras clave:** Amenazas informáticas — Controles de seguridad — Integridad — Disponibilidad — Confidencialidad — Superficie de ataque — Vulnerabilidades Informáticas — Seguridad de la información — Seguridad informática.

---

## 1. Riesgos, Amenazas, Vulnerabilidades

Para mejorar la seguridad de una empresa es necesario considerar cuatro factores:

- **Recursos**: activos tangibles (servidores, computadoras, equipos de red, vehículos, inmuebles) e intangibles (bases de datos de clientes, manuales, patentes, información en general) usados para las operaciones.
- **Amenazas**: eventos con potencial de perjudicar procesos o recursos.
- **Vulnerabilidades**: debilidades en los sistemas o procedimientos que podrían permitir que una amenaza tenga éxito.
- **Riesgos**: probabilidad de que ocurra un evento adverso que cause daño. Se define como **Riesgo = probabilidad de que una amenaza específica explote una vulnerabilidad particular**.

La función principal del responsable de seguridad es realizar una **evaluación de riesgos** que identifique vulnerabilidades y amenazas, y determine el grado de exposición.

### Evaluación de riesgos

En una evaluación básica se asigna un valor numérico al impacto (0 = ningún daño, 3 = gran daño) y otro a la probabilidad (0 = nula, 3 = alta). El **riesgo** se obtiene multiplicando ambos valores.

| Amenaza | Impacto | Probabilidad | Riesgo |
|---------|---------|--------------|--------|
| Robo de credenciales de un sistema biométrico | 3 | 0 | 0 |
| Infección con un código malicioso | 2 | 3 | 6 |
| Pérdida de suministro eléctrico | 3 | 1 | 3 |

Esto permite priorizar los riesgos más graves y tomar medidas en consecuencia.

### 1.1 Tipos de amenazas

**Amenazas naturales** — surgen por causas no intencionales:
- Errores humanos involuntarios (borrar información, enviar un correo a un destinatario equivocado).
- Daños al hardware por uso constante, inundaciones o fallos eléctricos.

**Amenazas deliberadas** — originadas por agentes internos o externos con intención maliciosa:
- **Agentes internos**: empleados descontentos, ex empleados con credenciales no revocadas.
- **Agentes externos**: competidores desleales, activistas, terroristas, cibercriminales.

Para mitigarlas: seguridad física y lógica, capacitación del personal, políticas de acceso y control de datos, tecnologías de detección y respuesta ante incidentes.

### 1.2 Vulnerabilidades

Las vulnerabilidades son **fallos de diseño en procedimientos o recursos** que pueden ser explotados por amenazas. No se crean intencionalmente; surgen como resultado de errores en el diseño, la implementación o la configuración de sistemas.

Ejemplos: sistema desactualizado, mala configuración, permisos incorrectos. Para identificarlas: bases de datos de vulnerabilidades, boletines de seguridad, comunidades de profesionales.

---

## 2. La Seguridad en Términos Generales

La seguridad implica un estado de bienestar caracterizado por la **ausencia de riesgos**. Desde una perspectiva disciplinaria, es un campo interdisciplinario dedicado a evaluar y gestionar los riesgos que afectan a personas, activos o entornos.

La seguridad siempre busca la **gestión de riesgos**. Cualquier intento de mejorar la seguridad involucra cuatro acciones:

1. **Prevención del riesgo** — evitar que ocurra.
2. **Transferir el riesgo** — delegarlo (ej: contratar un seguro).
3. **Mitigar el riesgo** — reducir su impacto.
4. **Aceptar el riesgo** — asumir que puede ocurrir y sus consecuencias.

---

## 3. Concepto de Seguridad Informática

**Seguridad informática** vs **seguridad de la información**: aunque suenan similares, difieren en alcance.

- La **seguridad informática** se centra en la protección del entorno informático: procesos, técnicas y métodos para procesar, almacenar y transmitir información.
- La **seguridad de la información** abarca todo aquello que pueda contener datos sensibles, sin limitarse al entorno informático.

La seguridad informática busca establecer normas, procedimientos, métodos y técnicas para garantizar la **seguridad, confiabilidad y disponibilidad** de un sistema de información. Su función principal es **minimizar los riesgos** provenientes de la entrada de datos, medios de transporte, hardware, usuarios y protocolos.

Lo que debe contemplar la seguridad se clasifica en tres partes:

- **Usuarios**: el eslabón más débil. Es imposible controlar a las personas; un error puede echar a perder el trabajo de mucho tiempo. En muchos casos el sistema debe protegerse del propio usuario.
- **Información**: el principal activo. Es lo que se desea proteger; "el oro de la seguridad informática".
- **Infraestructura**: aunque es uno de los medios más controlados, no está exento de riesgos. Abarca desde accesos no permitidos y robo de identidad hasta daños físicos por robos, inundaciones e incendios.

**Conclusión**: la seguridad informática es el conjunto de métodos y herramientas para proteger el principal activo de una organización (la información o los sistemas) ante eventuales amenazas.

---

## 4. Controles Preventivos

Los controles preventivos son medidas que actúan **antes de que ocurra un incidente**. Se perciben a menudo como costos adicionales, pero constituyen una inversión necesaria.

Son de naturaleza a largo plazo: no proporcionan beneficios inmediatos, pero pueden prevenir una amplia gama de ataques o mitigar su impacto. La barrera principal para su adopción es la falta de compromiso de todas las partes.

Ejemplos:
- Actualización de sistemas
- Soluciones de detección de códigos maliciosos (antivirus, antimalware)
- Firewall
- Contraseñas

La organización puede personalizar qué incluir en sus mecanismos preventivos.

---

## 5. Controles Correctivos

Los controles correctivos se implementan **después de que ocurre un incidente**, con el propósito de corregir el impacto.

Características:
- **Alto costo**: se aplican cuando el problema ya ocurrió y no puede prolongarse. Puede requerirse contratar expertos externos, adquirir soluciones comerciales, comprar parches.
- **Limitación temporal**: el tiempo es un recurso extremadamente escaso en estas situaciones. Incluso con recursos financieros, el tiempo disponible suele ser insuficiente.

---

## 6. Controles Detectivos

Los controles detectivos son los **más complejos** y requieren un alto grado de conocimientos técnicos. Parten del supuesto de que un atacante pudo haber comprometido la seguridad, total o parcialmente.

Dos objetivos principales:
1. **Identificar el punto exacto del ataque** para tomar medidas correctivas y recuperarse de la intrusión (no siempre es posible).
2. **Detectar actividades sospechosas y comprender lo sucedido**, incluso si no se puede determinar el punto exacto.

**Intrusión**: serie de acciones realizadas de manera deshonesta con el objetivo de obtener acceso no autorizado.

**Detección de intrusiones**: proceso de identificación y respuesta ante actividades ilícitas observadas en los recursos de una red, sistema, plataforma o empresa.

---

## 7. Los Pilares de la Seguridad (Tríada CIA)

La seguridad de la información se sustenta en tres pilares esenciales que constituyen la base de las estrategias y medidas de seguridad:

```
         Integridad
            |
   Pilares de la SI
            |
    Disponibilidad — Confidencialidad
```

La debilidad en cualquiera de estos pilares compromete tanto la seguridad como la usabilidad del sistema.

### 7.1 Integridad

Garantiza que **los datos no se pierdan ni se vean comprometidos** de manera intencional o accidental. Trabajar con información incorrecta puede ser tan perjudicial como perderla: la manipulación sutil desencadena errores en cascada y decisiones equivocadas.

Medidas para asegurar la integridad:
1. Monitoreo del tráfico de red para detectar intrusiones y actividades sospechosas.
2. Políticas de auditoría que registren quién accede a qué información, cuándo y con qué propósito.
3. Sistemas de control de cambios con comparación de resúmenes o firmas digitales para detectar modificaciones no autorizadas.
4. Copias de seguridad para restaurar la información en su estado original ante manipulación o pérdida.

### 7.2 Disponibilidad

Asegura que **los datos estén accesibles cuando se necesiten**, de manera rápida y eficiente. La falta de disponibilidad hace que la información pierda su utilidad y valor.

Políticas para garantizarla:
- **SLA** (Acuerdos de nivel de servicio): establecen tiempos de disponibilidad y respuesta ante incidentes.
- **Balanceadores de carga** de tráfico para mitigar impactos de ataques DDoS.
- **Copias de seguridad** para restaurar datos ante pérdida o corrupción.
- **Recursos alternativos** en caso de fallos en los sistemas primarios.

También implica elaborar políticas claras, definir acciones ante incidentes y delimitar el perímetro de afectación.

### 7.3 Confidencialidad

Garantiza que **solo las personas autorizadas accedan a los datos**. Se implementa mediante tres recursos principales:

- **Autenticación de usuarios**: identifica y verifica la identidad de quienes intentan acceder.
- **Gestión de privilegios**: permite que los usuarios accedan y operen únicamente con la información autorizada (permisos de lectura, escritura, etc.).
- **Cifrado de información (encriptación)**: transforma la información en un formato ilegible para quienes no están autorizados. Se aplica tanto a información en tránsito como almacenada.

La confidencialidad puede estar respaldada por legislación de protección de datos personales. Las filtraciones de entidades bancarias, empresas y gobiernos son ejemplos de violaciones de este pilar.

---

## 8. Principio de Mínimos Privilegios

Establece que **cada usuario o sistema debe tener acceso únicamente a los recursos necesarios para llevar a cabo sus funciones**, sin privilegios innecesarios ni permanentes.

**Privilegios**: permisos que un usuario o sistema tiene para actuar sobre otros recursos. En sistemas operativos (Windows, Mac, Linux), las cuentas se dividen en:
- **Usuarios normales**: acceso a herramientas instaladas y a su directorio de usuario.
- **Administradores**: privilegios adicionales para configurar el sistema, instalar/eliminar software.

El principio establece que cada usuario debe disponer solo de los privilegios mínimos necesarios:
- Para una tarea específica.
- Durante el tiempo imprescindible.
- Con alcance limitado a lo que exija la tarea.

Ejemplo práctico: usar un usuario normal para navegar o gestionar correo; usar el administrador solo para instalar software o cambiar configuración del sistema.

Este enfoque **minimiza el riesgo** de códigos maliciosos, espionaje o corrupción de archivos del sistema.

---

## 9. Superficie de Ataque

La superficie de ataque de una infraestructura IT es el **conjunto de elementos que pueden ser vulnerables y susceptibles de ser explotados** por incidentes naturales o ataques deliberados.

A mayor superficie de ataque (más elementos expuestos), mayores probabilidades de que existan vulnerabilidades explotables. **Minimizar la superficie implica reducir los riesgos potenciales**.

### Tipos de ataque

**Ataque pasivo**: monitorear al sujeto atacado sin afectar directamente la infraestructura. No es invasivo pero permite observar lo que la infraestructura almacena o transmite. Se usan técnicas de monitorización de tráfico y fuentes abiertas (OSINT). Su objetivo es obtener información para usarla en ataques posteriores.

**Ataque activo**: acciones directas que buscan penetrar la infraestructura y establecerse de manera permanente. Objetivos: sabotaje, robo de información, despliegue de malware para espionaje o secuestro de equipos.

### Componentes de la superficie de ataque

**Software**: aplicaciones, servicios, ejecutables, páginas web. Las vulnerabilidades son fallos en la programación o compilación. Para reducir esta superficie: minimizar el software instalado, mantenerlo actualizado con parches, configurarlo con mínimos privilegios, evitar software pirata, analizar bases de datos de vulnerabilidades periódicamente.

**Hardware**: dispositivos de red (routers, switches, firewalls), computadoras, servidores, sistemas de almacenamiento. Amenazas: envejecimiento de equipos, robos, incendios, inundaciones, perturbadores de señal. Para reducir: proteger físicamente los equipos, cerrar puertos innecesarios, deshabilitar protocolos no pertinentes, desplegar firewalls y sistemas de detección de intrusos, mantener el firmware actualizado.

**Recursos Humanos**: las personas pueden actuar contra los intereses de la organización. Para reducir: sistemas de registro y auditoría (evita el anonimato), educación y concienciación sobre seguridad.

---

## Síntesis de la Unidad

La Unidad I establece los conceptos base de la seguridad informática: recursos (tangibles e intangibles), amenazas (naturales y deliberadas), vulnerabilidades (fallos de diseño) y riesgos (probabilidad × impacto). La evaluación de riesgos permite priorizar amenazas y aplicar controles preventivos (antes del incidente), correctivos (después) y detectivos (para identificar intrusiones).

Los tres pilares de la seguridad — **Integridad, Disponibilidad y Confidencialidad** (tríada CIA) — son la base de toda estrategia de protección. Complementan estos pilares el **Principio de Mínimos Privilegios** (acceso solo a lo necesario) y el concepto de **Superficie de Ataque** (software, hardware, recursos humanos).

---

## Bibliografía

**Obligatoria:**
- Grubb, S. (2021). *How Cybersecurity Really Works: A Hands-On Guide for Total Beginners*. No Starch Press.
- Romero, M. et al. (2018). *Introducción a la Seguridad Informática y el Análisis de Vulnerabilidades*. Área de Innovación y Desarrollo, S.L.

**Optativa:**
- Diogenes, Y; Ozkaya, E. (2018). *Ciberseguridad: Estrategias de ataque y defensa*. Packt.
