# Guía de la Unidad III — Seguridad Ofensiva

**Contenidista:** Germán Ariel Paradisi

---

## Objetivos

- Comprender las diferencias entre vulnerabilidades físicas y lógicas y su impacto en la seguridad de los sistemas.
- Identificar tipos de vulnerabilidades: buffer overflow, errores de configuración, errores web, errores de protocolo.
- Analizar los estándares CVE, CWE y CAPEC, y comprender el uso de CVSS para valorar vulnerabilidades.
- Explorar herramientas y técnicas de detección de vulnerabilidades.
- Conocer los tipos de pruebas de seguridad: análisis interno, externo, sondeo de red, pentesting.
- Dominar el ciclo de vida de las vulnerabilidades (análisis → clasificación → parcheo → aplicación).
- Explorar los enfoques de análisis: escaneo, evaluación, pentesting, Red Team, Purple Team, emulación de adversarios.
- Comprender OSINT: concepto, aplicación en ciberseguridad, legalidad, ciclo y herramientas.

**Palabras clave:** Vulnerabilidad – CVE – CWE – CAPEC – OSINT – CVSS – Red Team – Blue Team – Purple Team – OWASP – Riesgo – Pruebas de Penetración – Emulación de Adversarios

---

## 1. Introducción al Análisis de Vulnerabilidades

Una **vulnerabilidad** es una brecha o punto débil presente en un sistema, aplicación o medida de seguridad que podría ser aprovechada por amenazas externas o internas. Su explotación puede comprometer la integridad, confidencialidad o disponibilidad de la información.

### 1.1 Vulnerabilidades físicas

Afectan directamente la infraestructura física de una organización. Incluyen:

- **Desastres naturales**: terremotos, inundaciones, fallos eléctricos que interrumpen servicios o dañan equipos.
- **Controles de acceso inadecuados**: si cualquier persona puede acceder físicamente a las instalaciones, un individuo malintencionado puede conectar un USB infectado, robar equipos o introducir malware directamente en los sistemas.

### 1.2 Vulnerabilidades lógicas

Afectan la infraestructura y el funcionamiento operativo de los sistemas. Se clasifican en:

- **Vulnerabilidades de configuración**: configuraciones incorrectas o inseguras en SO, aplicaciones, firewalls. Ejemplos: contraseñas predeterminadas no cambiadas, configuraciones por defecto, permisos excesivos.
- **Vulnerabilidades de actualización**: sistemas sin parches al día. Cuando un fabricante termina el soporte (ej: Windows XP), los sistemas dejan de recibir actualizaciones de seguridad y quedan expuestos indefinidamente.
- **Vulnerabilidades de desarrollo**: errores de programación explotables. Ejemplos: SQL Injection, Cross-Site Scripting (XSS), falta de validación de entradas.

---

## 2. Tipos de Vulnerabilidades

### 2.1 Desbordamiento de buffer (Buffer Overflow)

El programa no controla adecuadamente el espacio de memoria asignado a un búfer, lo que permite a un atacante sobreescribir áreas de memoria adyacentes con código malicioso. Este código puede ejecutarse antes que otras tareas previstas del sistema.

Se aprovecha mediante **payloads** (datos diseñados específicamente para explotar la vulnerabilidad) o para inyectar **backdoors** directamente en RAM. Prevención: validación de entradas y gestión correcta de memoria.

### 2.2 Errores de configuración

Abarcan desde contraseñas predeterminadas o débiles hasta privilegios excesivos y protocolos de encriptación obsoletos. Ejemplos:

- Uso de contraseñas predeterminadas → acceso no autorizado trivial.
- Protocolos de encriptación inseguros → comunicaciones interceptables.
- SSH sin parches → explotable de forma remota.
- Falta de actualizaciones → exposición a vulnerabilidades conocidas.

### 2.3 Errores WEB

Vulnerabilidades en aplicaciones web:

- **SQL Injection**: inserción de comandos SQL maliciosos en campos de entrada. El atacante puede acceder, modificar o eliminar datos de la base de datos, incluyendo credenciales.
- **Cross-Site Scripting (XSS)**: inserción de scripts maliciosos en páginas web que se ejecutan en el navegador de la víctima. Permite robar cookies de sesión, redirigir a sitios falsos o tomar control de la sesión.

Mitigación: validación y sanitización de entradas, firewalls de aplicaciones web (WAF), auditorías regulares.

### 2.4 Errores de protocolo

Muchos protocolos fueron diseñados sin contemplar la seguridad. Ejemplo: **HTTP** carece de encriptación — es adecuado para navegación general pero insuficiente para transacciones sensibles (bancarias, credenciales). Se requiere HTTPS con certificados SSL/TLS para garantizar confidencialidad e integridad.

### 2.5 Aprovechamiento de las vulnerabilidades

Las vulnerabilidades se explotan principalmente de dos formas:

| Forma | Descripción |
|-------|-------------|
| **Aprovechamiento remoto** | El atacante usa una computadora para analizar y atacar un servidor con un puerto abierto vulnerable. Si logra acceso no autorizado, la explotación fue exitosa. |
| **Ingeniería social** | El atacante manipula a personas dentro de la organización para que abran archivos infectados, entreguen credenciales o faciliten acceso a sistemas críticos. |

---

## 3. Estándares para Valorar Vulnerabilidades

Para estandarizar la comunicación sobre vulnerabilidades, la industria utiliza tres estándares complementarios: CVE, CWE y CAPEC.

### 3.1 CVE — Common Vulnerabilities and Exposures

Lista estandarizada de identificadores para vulnerabilidades conocidas públicamente. Cada registro CVE tiene el formato **CVE-YYYY-NNNN** (año + número único). Su propósito es facilitar la identificación y el intercambio automático de datos entre herramientas de seguridad.

Ejemplo: Log4Shell → `CVE-2021-44228`.

**CVE Details** es una plataforma que ofrece una interfaz gráfica para consultar la base de datos CVE. Permite buscar por proveedor, producto, fecha y tipo de fallo. Es invaluable para mantenerse al tanto de vulnerabilidades recientes y evaluar su impacto potencial.

### 3.2 CWE — Common Weakness Enumeration

Catálogo de **debilidades comunes** en software y hardware. A diferencia del CVE (que identifica vulnerabilidades específicas), el CWE aborda categorías generales de debilidades.

Relación: un CVE es una instancia concreta de una debilidad listada en el CWE. El CWE proporciona un enfoque más holístico — permite entender las raíces de las vulnerabilidades y tomar medidas preventivas más efectivas.

### 3.3 CAPEC — Common Attack Pattern Enumeration and Classification

Diccionario y sistema de clasificación de **patrones de ataque conocidos**. Documenta cómo los adversarios explotan las debilidades identificadas en el CWE. Sirve como guía para analistas, desarrolladores y educadores.

Su valor: permite diseñar estrategias de defensa más efectivas al comprender las tácticas y motivaciones de los atacantes.

### 3.4 Valoración de vulnerabilidades — CVSS

#### ¿Qué es CVSS?

El **Common Vulnerability Scoring System (CVSS)** es un sistema de puntuación estándar para evaluar la gravedad de las vulnerabilidades en tecnologías de la información. Está bajo supervisión del **FIRST** (Forum of Incident Response and Security Teams) y es de uso libre.

Su objetivo: cuantificar la gravedad de las vulnerabilidades para que las organizaciones puedan priorizar sus esfuerzos de seguridad.

#### ¿Cómo se calcula?

CVSS utiliza una escala del **0 al 10**:

| Rango | Severidad |
|-------|-----------|
| 0.0 – 3.9 | Baja |
| 4.0 – 6.9 | Media |
| 7.0 – 10.0 | Alta / Crítica |

Se usan tres grupos de métricas:

- **Métricas base**: características intrínsecas de la vulnerabilidad (vector de acceso, complejidad, autenticación requerida). Miden el impacto directo en confidencialidad, integridad y disponibilidad.
- **Métricas temporales** (opcionales): cambios en el tiempo — confirmación técnica, nivel de remediación disponible, nivel de confianza en el reporte.
- **Métricas de entorno** (opcionales): características del entorno específico del usuario — daño colateral potencial, requisitos de CIA en ese entorno particular.

La fórmula genera una puntuación + un vector de texto que describe cómo se calculó (ej: `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H`).

#### Beneficios de CVSS

- Estandarización de puntuaciones → criterios coherentes para comparar vulnerabilidades.
- Marco abierto y transparente → decisiones fundamentadas.
- Priorización consciente → enfocar recursos en las vulnerabilidades de mayor riesgo para el entorno específico.

---

## 4. Detección de Vulnerabilidades

Detectar vulnerabilidades requiere combinar tres enfoques:

| Enfoque | Descripción |
|---------|-------------|
| **Escaneo automatizado** | Herramientas como Nikto, Nessus, Nmap exploran rangos de IP buscando vulnerabilidades conocidas. Rápido y eficiente, pero puede no detectar vulnerabilidades nuevas. |
| **Análisis manual** | Revisión humana que permite descubrir vulnerabilidades sutiles que los escáneres pasan por alto. Más completo, más lento. |
| **Consulta de información** | Técnicas de búsqueda como *Google Hacking* (dorks) para encontrar información expuesta involuntariamente. |

### 4.1 Herramientas para escanear vulnerabilidades

| Herramienta | Tipo | Especialidad |
|-------------|------|-------------|
| **Acunetix** | Pago | Aplicaciones web — detecta y verifica explotación real |
| **Netsparker** | Pago | SQL Injection, XSS |
| **ProxyStrike** | Gratuita | SQL Injection, XSS |
| **Nessus** | Pago | Sistemas operativos, redes, integración con Android |
| **Nexpose** | Pago | Vinculado a Metasploit, exporta vectores de ataque |
| **OpenVAS** | Gratuita | Escaneo con/sin credenciales |
| **LanGuard** | Pago | Políticas de seguridad y gestión de equipos |

Los escáneres operan actualizando **firmas** de vulnerabilidades conocidas. Cuando se identifica una nueva vulnerabilidad, se desarrollan firmas y se actualizan en los escáneres.

### 4.2 Establecimiento de las reglas del juego

Antes de iniciar cualquier análisis, es fundamental definir:
- Tareas a realizar y límites a respetar.
- Permisos y obligaciones del analista.
- Si se pueden interrumpir servicios o no.

Además, se debe mantener el análisis confidencial para el menor número de personas posible. Si los usuarios saben que están siendo monitoreados, modifican su comportamiento, alterando los resultados reales.

### 4.3 Recolección de información — Metodologías de escaneo

| Metodología | Acceso disponible | Tipo de análisis |
|-------------|------------------|-----------------|
| **Caja Blanca** | Visión completa + acceso de superusuario | Actúa como usuario legítimo con privilegios; verifica qué acciones adicionales son posibles |
| **Caja Negra** | Solo información mínima (ej: IP o nombre de empresa) | Recopila todo lo posible desde afuera sin ejecutar acciones; solo detecta y documenta |
| **Caja Gris** | Acceso parcial | Combina ambos enfoques; información limitada pero no tan restringida como caja negra |

En un análisis de **caja blanca** se obtiene: IPs de servidores, usuarios, contraseñas, servicios, esquemas de red, niveles de privilegio.
En un análisis de **caja negra** se obtiene: IPs, nombres de dominio, emails.

### 4.4 Tipos de pruebas de seguridad

#### 4.4.1 Análisis interno
Simula hasta dónde puede llegar un usuario típico dentro de la organización. La organización provee una computadora con credenciales normales. Incluye:
- Revisión de privacidad (manejo ético/legal de información).
- Pruebas de contingencia (efectividad de medidas ante accesos no autorizados).
- Descifrado de contraseñas (robustez de contraseñas y algoritmos criptográficos).
- Evaluación de políticas de seguridad (coherencia con objetivos del negocio).

#### 4.4.2 Análisis externo
Busca obtener acceso remoto a servidores de la organización desde fuera de la red interna. Puede comenzar con ingeniería social. Incluye:
- Revisión de inteligencia competitiva (OSINT desde fuentes públicas).
- Revisión de privacidad.
- Análisis de solicitudes (ingeniería social por teléfono/email/chat).
- Análisis de ingeniería social (manipular empleados para instalar malware o crear sesiones desde el exterior).

#### 4.4.3 Sondeo de red
Fase inicial: recopilación de información preliminar sobre los sistemas. Examina nombres de dominio, servidores, IPs, mapas de red, ISP, propietarios y servicios activos.

#### 4.4.4 Identificación de servicios de sistemas
Enumeración de servicios de Internet activos. Se usa **Fingerprinting** para identificar sistema operativo y versión.

#### 4.4.5 Búsqueda y verificación de vulnerabilidades
Uso de herramientas automáticas para detectar agujeros de seguridad y errores de configuración. Se complementa con monitoreo de vulnerabilidades recientemente publicadas (que pueden no estar aún en los escáneres).

#### 4.4.6 Testeo de aplicaciones web
Pruebas de caja negra sobre aplicaciones web: evalúa la seguridad desde la perspectiva de un atacante externo sin conocer el código fuente.

#### 4.4.7 Testeo de relaciones de confianza
Evalúa mecanismos de enrutamiento y políticas de acceso para verificar que solo dispositivos y usuarios autorizados puedan comunicarse dentro de la red.

#### 4.4.8 Verificación de redes inalámbricas
Verificación del estándar 802.11 (Wi-Fi): protocolos de seguridad, configuración de puntos de acceso, robustez de contraseñas, detección de intrusiones, resistencia a sniffing y suplantación de identidad.

### 4.5 Documentación e Informes

Al concluir, se debe presentar un informe detallado que incluya:
- Lista de vulnerabilidades examinadas y detectadas.
- Servicios y dispositivos vulnerables identificados.
- Clasificación del nivel de riesgo por vulnerabilidad.
- Programas y herramientas utilizados con sus configuraciones.
- Recomendaciones específicas para mitigar cada vulnerabilidad.

### 4.6 Ciclo de vulnerabilidades

Una vez detectadas las vulnerabilidades, el ciclo de remediación comprende 4 pasos:

**1. Análisis de activos**: inventariar y categorizar todos los activos de la organización (IPs, servidores, dispositivos de red, aplicaciones, bases de datos). El inventario debe mantenerse actualizado.

**2. Clasificar y priorizar riesgos**: el escáner genera un informe con todas las vulnerabilidades. Como no es posible remediarlas todas simultáneamente (limitaciones de tiempo y recursos), se prioriza combinando **severidad de la vulnerabilidad × importancia del sistema afectado**. Primero se abordan las más graves en sistemas críticos.

**3. Probar parches y configuraciones**: los parches deben instalarse primero en una única máquina de prueba para verificar que no introducen nuevos errores. Los parches solo deben descargarse de sitios oficiales del fabricante (un parche de fuente no confiable puede introducir malware).

**4. Aplicar parches y configuraciones**: una vez verificados, aplicar en todos los sistemas de la red. Pueden usarse soluciones automáticas de despliegue. Algunos escáneres generan tickets automáticamente asignados a ingenieros responsables de la remediación.

---

## 5. Tipos de Análisis de Vulnerabilidades

Según el modelo de madurez SCYTHE, los enfoques van de menor a mayor complejidad:

```
Vulnerability Scanning → Vulnerability Assessment → Penetration Testing → Red Team → Purple Team Exercise → Adversary Emulation
```

### 5.1 Escaneo de vulnerabilidades

El más básico. Usa escáneres automatizados para **identificar y catalogar vulnerabilidades conocidas**. Requiere un esfuerzo mínimo con las herramientas adecuadas.

**Análisis de GAP**: evalúa el nivel de cumplimiento de una organización respecto a legislaciones, normativas sectoriales o estándares internacionales (ej: GDPR, ISO 27001). Identifica la brecha entre los requisitos de seguridad y el estado actual.

### 5.2 Evaluación de Vulnerabilidades

Análisis más exhaustivo. Una vulnerabilidad es cualquier error que permite acciones no autorizadas (interrupción del servicio, acceso no autorizado, escalada de privilegios, ejecución de código).

Las vulnerabilidades en aplicaciones suelen estar en el código fuente; las de sistemas, en configuraciones inseguras.

**Puede ser**:
- **Interna**: desde dentro de la organización.
- **Externa**: simula el enfoque de un atacante externo evaluando la seguridad perimetral.

Etapas: identificación temprana de debilidades → mapeo de superficies de ataque → descubrimiento de vulnerabilidades → visualización desde perspectiva de atacante.

### 5.3 Pruebas de penetración (Pentesting)

Va más allá de la evaluación: **no solo identifica vulnerabilidades, sino que también las explota**. Se realiza de forma profesional y controlada con alcance y reglas de compromiso definidas.

Las pruebas abarcan dispositivos físicos, digitales y el factor humano (ingeniería social).

**Fases del pentesting:**

| Fase | Objetivo | Acciones |
|------|---------|---------|
| **1. Reconocimiento** | Recopilar información sobre el objetivo | Emails, IPs, SO, servicios, topología de red — puede ser la más prolongada |
| **2. Escaneo** | Identificar puntos de entrada | Escaneo de puertos y servicios activos, detección de vectores de ataque potenciales |
| **3. Enumeración** | Obtener datos específicos | Conexiones activas a sistemas objetivo; usuarios, grupos de seguridad, políticas de acceso |
| **4. Acceso** | Explotar vulnerabilidades | Usar las vulnerabilidades confirmadas para ingresar al sistema, simular ataque real |
| **5. Mantenimiento de acceso** | Persistencia discreta | Instalar backdoors, crear cuentas adicionales, modificar permisos para mantener acceso sin ser detectado |

Al finalizar, se genera documentación detallada: vulnerabilidades encontradas, brechas de seguridad, recomendaciones.

### 5.4 Ejercicios de Red Team

El Red Team **emula las tácticas de adversarios reales** para probar integralmente la postura de seguridad de la organización (personas, procesos y tecnologías).

Diferencias clave vs pentesting:
- Solo la alta dirección sabe que se está realizando; el equipo de IT no es informado.
- Simula una **amenaza persistente avanzada (APT)**, no solo vulnerabilidades puntuales.
- Incluye ingeniería social y evaluación de seguridad física.

Los clientes principales del Red Team son los **defensores** (responsables de los controles de detección y alerta).

### 5.5 Ejercicios de Purple Team

Colaboración entre Red Team (ofensivo) y Blue Team (defensivo). Ambos trabajan juntos con comunicación abierta y transparente:
- Red Team ejecuta ataques simulados.
- Blue Team monitorea y responde.
- Se comparten técnicas de ataque, estrategias de defensa y lecciones aprendidas.

Objetivo: mejora continua de las capacidades de detección, respuesta y mitigación **en tiempo real**, identificando debilidades en procesos, tecnología y capacitación del personal.

### 5.6 Emulaciones de adversarios

El enfoque más avanzado. El Red Team simula las **tácticas y procedimientos de un atacante real específico** (identificado mediante inteligencia) contra la organización objetivo.

Se recrea el escenario basado en el marco de trabajo del atacante (ej: MITRE ATT&CK). Evalúa no solo la tecnología sino la **madurez de los procesos y roles de seguridad** (analistas, respondientes a incidentes, cazadores de amenazas, CISO, administradores).

---

## 6. OWASP

**OWASP** (Open Web Application Security Project) es una organización internacional sin fines de lucro dedicada a la seguridad de aplicaciones web. Todos sus materiales (documentación, herramientas, vídeos, foros) son gratuitos.

Su proyecto más conocido es el **OWASP Top 10**: lista de los 10 riesgos de seguridad más importantes en aplicaciones web, actualizada periódicamente por expertos globales. Es un "documento de concienciación" recomendado para incorporar en todos los procesos de desarrollo.

### 6.1 OWASP Top 10 (2021)

| ID | Vulnerabilidad | Descripción |
|----|---------------|-------------|
| **A01** | Pérdida de control de acceso | Controles de acceso defectuosos permiten a atacantes actuar como usuarios privilegiados. Mitigación: tokens de autorización con controles estrictos. |
| **A02** | Fallas criptográficas | Datos confidenciales (contraseñas, info financiera) sin protección adecuada. Susceptibles a ataques en ruta (man-in-the-middle). Mitigación: encriptar todos los datos sensibles, no cachear información confidencial. |
| **A03** | Inyección | Envío de datos no confiables a intérpretes de código (SQL, OS, LDAP). Ejemplo clásico: SQL Injection. Mitigación: validación + sanitización de entradas. |
| **A04** | Diseño inseguro | Fallas en el diseño mismo — no pueden corregirse con implementación perfecta porque los controles necesarios nunca fueron creados. Requiere modelado de amenazas desde el inicio. |
| **A05** | Configuración de seguridad incorrecta | La más común. Configuraciones por defecto, mensajes de error excesivamente descriptivos. Mitigación: eliminar funciones no usadas, mensajes de error genéricos. |
| **A06** | Componentes vulnerables y desactualizados | Bibliotecas y frameworks con vulnerabilidades conocidas. Un componente comprometido puede afectar cientos de miles de sitios. Mitigación: eliminar componentes no usados, mantenerlos actualizados. |
| **A07** | Fallas de identificación y autenticación | Vulnerabilidades en sistemas de login. Ataques de credential stuffing (probar listas de credenciales filtradas). Mitigación: 2FA, limitación de intentos de login. |
| **A08** | Fallas en software e integridad de datos | Suposiciones no verificadas sobre actualizaciones de software, datos críticos y pipelines CI/CD. Uno de los mayores impactos según CVSS. |
| **A09** | Fallas en registro y monitoreo | Promedio: 200 días para detectar una fuga. Sin logging adecuado, los atacantes tienen tiempo ilimitado. Mitigación: implementar planes de registro, supervisión y respuesta a incidentes. |
| **A10** | SSRF — Falsificación de solicitudes del lado del servidor | La app obtiene recursos remotos sin validar la URL del usuario. El atacante puede hacer que el servidor envíe solicitudes a destinos inesperados, incluso tras firewall/VPN. |

---

## 7. OSINT: Inteligencia de Fuentes Abiertas

**OSINT** (Open Source Intelligence) consiste en la recopilación, análisis y utilización de información pública disponible en diversas fuentes en línea para obtener conocimientos sobre personas, organizaciones, eventos u otros aspectos relevantes.

### 7.1 Investigación defensiva

Aplicación de OSINT sobre uno mismo: entender qué datos personales están disponibles en la web para anticipar qué podría recopilar un investigador externo. Permite mitigar riesgos de robo de información o suplantación de identidad.

### 7.2 Conceptos básicos

- **Dato**: cualquier información relacionada con la persona investigada (fotografías, textos, grabaciones, historial de navegación).
- **Big Data**: recopilación masiva de datos por empresas o sistemas automatizados, de diversas fuentes, procesable a alta velocidad.
- **Metadatos**: información sobre otros datos. Una foto puede revelar fecha, hora y ubicación GPS del dispositivo sin que el usuario lo sepa.

### 7.3 Por qué usar OSINT

La mayoría de las personas comparten información personal en línea (redes sociales, foros) sin ser conscientes de que puede ser pública y accesible para cualquier propósito — desde planificar un ataque hasta resolver un crimen. OSINT es fundamental en la gestión de riesgos digitales.

### 7.4 Aplicación en ciberseguridad

- **Investigaciones privadas**: obtener información sobre individuos sospechosos de participar en ciberataques.
- **Investigaciones públicas**: recabar datos verificados para casos legales (delitos cibernéticos, personas desaparecidas).
- **Pentesting**: investigación OSINT previa al ejercicio de penetración para conocer mejor el objetivo y encontrar puntos de vulnerabilidad (ej: ataques de ingeniería social basados en datos públicos).

### 7.5 OSINT ¿Legal o Ilegal?

OSINT se basa en recopilación de datos de **fuentes públicas o abiertas** — esto es legal en sí mismo.

Sin embargo, la **divulgación de información sensible con intenciones dañinas** constituye un delito llamado **doxxing**, tipificado en la legislación de la mayoría de los países. Es crucial actuar siempre en conformidad con la legislación del país donde se realiza la investigación.

### 7.6 Ciclo OSINT

| Fase | Descripción |
|------|-------------|
| **Planteamiento de requisitos** | Definir formalmente los objetivos, formato requerido, nivel de formalidad, veracidad de fuentes aceptadas. |
| **Identificación de fuentes** | Enumerar posibles fuentes de información. La lista puede ampliarse durante el proceso. |
| **Adquisición y procesamiento** | Recopilar y analizar la información. Durante el procesamiento puede surgir nueva información (ej: extracción de metadatos de imágenes) que lleve a revisar las fuentes. |
| **Presentación y formalización** | Estructurar los resultados conforme a los requisitos establecidos al inicio. La información cruda sin presentación adecuada carece de utilidad. |

### 7.7 Obtención de la información

#### 7.7.1 Tipos de fuentes

| Fuente | Características |
|--------|----------------|
| **Redes sociales** (Instagram, Facebook, Twitter) | Gran cantidad de información personal pública (fotos, nombres, conexiones personales y laborales, opiniones) |
| **Internet profunda** | Sitios no indexados por buscadores, cuentas privadas, sitios .onion — más difícil de acceder |
| **Literatura gris** | Publicaciones y noticias de tiradas limitadas, no archivadas — veracidad variable |
| **Medios tradicionales** | TV, radio, cine, periódicos — fáciles de encontrar en archivos, generalmente confiables |

#### 7.7.2 Métodos de obtención

| Método | Descripción | Trade-off |
|--------|-------------|-----------|
| **Obtención activa** | El investigador establece contacto directo con el objetivo (solicitud de amistad, escaneo de red, conversación con cuenta anónima) | Alta veracidad, pero el objetivo puede darse cuenta de la investigación |
| **Obtención pasiva** | Sin contacto directo — buscadores, archivos de medios, perfiles públicos | Menor riesgo de detección, pero información potencialmente menos valiosa |

La combinación de ambos enfoques permite obtener la diversidad de información necesaria para análisis completos.

#### 7.7.3 Dorks en buscadores

Los motores de búsqueda (Google, Bing, DuckDuckGo, Yandex) ofrecen **operadores de búsqueda** (dorks) que permiten filtrar y precisar resultados. La sintaxis es consistente en la mayoría de los buscadores, heredada de Google.

Ejemplos de operadores:
- `site:empresa.com` — resultados de un dominio específico
- `filetype:pdf "confidencial"` — archivos PDF con la palabra "confidencial"
- `inurl:admin` — URLs que contienen "admin"

La **investigación defensiva** aplica dorks sobre uno mismo (nombre, email, usuario) para descubrir información expuesta en filtraciones de datos o motores de búsqueda de personas.

---

## Síntesis de la Unidad

La Unidad III aborda la **Seguridad Ofensiva** desde el análisis de vulnerabilidades hasta las técnicas avanzadas de prueba. Los fundamentos son los tipos de vulnerabilidades (físicas y lógicas, con sus variantes: buffer overflow, config errors, web errors, protocol errors) y los estándares de la industria para clasificarlas (CVE como identificador específico, CWE como catálogo de debilidades, CAPEC como clasificación de patrones de ataque, y CVSS como sistema de puntuación).

La detección combina escaneo automatizado, análisis manual y OSINT, y se organiza según tres metodologías (caja blanca, negra y gris). El ciclo de remediación sigue: análisis de activos → clasificación y priorización → prueba de parches → aplicación. Los tipos de análisis van desde el escaneo básico hasta la emulación de adversarios, pasando por el pentesting con sus 5 fases y los ejercicios de Red/Purple Team.

OWASP Top 10 (2021) y OSINT completan la unidad: el primero como marco de referencia para vulnerabilidades web; el segundo como metodología de recopilación de inteligencia desde fuentes abiertas, con su ciclo de 4 fases y distinción entre obtención activa y pasiva.

---

## Bibliografía

**Obligatoria:**
- Grubb, S. (2021). *How Cybersecurity Really Works: A Hands-On Guide for Total Beginners*. No Starch Press.
- OWASP (2021). *OWASP Top Ten*. https://owasp.org/www-project-top-ten/
- Romero, M. et al. (2018). *Introducción a la Seguridad Informática y el Análisis de Vulnerabilidades*. Área de Innovación y Desarrollo, S.L.

**Optativa:**
- Kiser, Q. (2020). *Ciberseguridad: Una Simple Guía para Principiantes sobre Ciberseguridad, Redes Informáticas y Cómo Protegerse del Hacking*. No Starch Press.
