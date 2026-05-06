# Resumen — Unidad 2: Desafíos de Seguridad para los Usuarios

El eje central de esta unidad es que **el usuario es el eslabón más débil de la cadena de seguridad**, y al mismo tiempo, su primera línea de defensa. Los ataques que se estudian acá no explotan bugs en el código ni vulnerabilidades técnicas — explotan el comportamiento humano, la confianza y los errores cotidianos.

---

## 1. Privacidad en la Era Digital

### Tipos de datos

No toda la información es igual. Según su naturaleza y el nivel de protección que requieren, los datos se clasifican en:

| Tipo | Descripción | Ejemplos |
|------|-------------|---------|
| **Datos personales** | Identifican a una persona física | Nombre, DNI, email, dirección, teléfono |
| **Datos sensibles** | Categoría especial con mayor protección legal | Salud, religión, orientación sexual, datos biométricos |
| **Datos públicos** | Libremente accesibles sin restricción | Publicaciones en redes sociales, información de contacto publicada |
| **Metadatos** | Información sobre información | Fecha/hora de un email, ubicación GPS de una foto, duración de llamadas |

Los metadatos merecen atención especial: una foto publicada puede exponer ubicación exacta, dispositivo usado y hora del día sin que el usuario lo note conscientemente.

### Marco legal

La privacidad está respaldada por legislación en distintas jurisdicciones:

| Normativa | Alcance |
|-----------|---------|
| **GDPR** | Unión Europea — aplica a cualquier empresa que trate datos de ciudadanos europeos |
| **Ley 25.326** | Argentina — Ley de Protección de Datos Personales |
| **CCPA** | California, EE.UU. — derechos de privacidad para consumidores |

### La Web en capas: Surface, Deep y Dark Web

La web no es solo lo que aparece en Google. Tiene tres niveles bien diferenciados:

| Capa | Proporción | Descripción |
|------|-----------|-------------|
| **Surface Web** | ~4% | Lo que indexan los buscadores. Sitios públicos accesibles normalmente. |
| **Deep Web** | ~90% | Contenido no indexado: intranets corporativas, bases de datos académicas, correo privado, sistemas bancarios. No es ilegal — solo no está en los buscadores. |
| **Dark Web** | ~6% | Requiere software especial (TOR) para acceder. Anónima. Contiene tanto foros legítimos de activismo y privacidad como mercados ilegales (drogas, credenciales robadas, malware). |

**TOR (The Onion Router)** es una red de servidores voluntarios que cifra el tráfico en múltiples capas y lo enruta por distintos nodos, ocultando la IP del usuario. Las páginas `.onion` solo son accesibles desde esta red.

---

## 2. Ingeniería Social

La ingeniería social es el conjunto de técnicas de manipulación psicológica diseñadas para engañar a personas y lograr que realicen acciones o divulguen información confidencial. La diferencia clave con los ataques técnicos es que **no explota fallas en el software — explota fallas en el comportamiento humano**.

### Vulnerabilidades psicológicas

Los atacantes se apoyan en rasgos propios de la naturaleza humana:

| Vulnerabilidad | Cómo se explota |
|----------------|----------------|
| **Dificultad para decir no** | Las personas tienden a ceder ante pedidos aparentemente razonables o insistentes. |
| **Exceso de confianza** | Disposición a creer en la legitimidad de una solicitud sin verificarla. |
| **Necesidad de reconocimiento** | El deseo de ser útil o quedar bien lleva a compartir información innecesaria. |
| **Empatía** | La tendencia a ayudar cuando alguien parece estar en apuros facilita el engaño. |

### Técnicas de ingeniería social

| Técnica | Descripción |
|---------|-------------|
| **Phishing** | Email fraudulento que imita una entidad legítima para robar credenciales o datos. |
| **Vishing** | Voice phishing — llamada telefónica. El atacante se hace pasar por soporte técnico, banco o gobierno. |
| **Smishing** | SMS phishing — mensaje de texto con link malicioso o solicitud de datos. |
| **Pretexting** | Creación de un escenario falso elaborado para ganarse la confianza de la víctima y extraer información. |
| **Baiting** | Dejar dispositivos infectados (pendrives) en lugares públicos esperando que alguien los conecte. |
| **Quid pro quo** | Ofrecer algo a cambio de información: "Te ayudo con tu problema técnico, solo dame tu contraseña". |

### Caso real: Twitter Bitcoin Scam (2020)

En julio de 2020, atacantes usaron **vishing** contra empleados de Twitter con acceso a herramientas internas. Llamaron haciéndose pasar por soporte de TI, convencieron a empleados de entregar credenciales y tomaron control de cuentas verificadas de alto perfil: Barack Obama, Elon Musk, Apple, Uber, entre otros.

Publicaron desde esas cuentas una estafa de Bitcoin y recaudaron ~$120.000 en pocas horas.

La lección es directa: ni los sistemas más seguros del mundo protegen cuando un empleado es manipulado para entregar acceso.

---

## 3. Phishing: Anatomía y Variantes

El phishing es el ataque de ingeniería social más común. El **95% de las brechas de seguridad** comienza con un correo de phishing.

### Anatomía de un ataque (5 pasos)

1. El atacante crea un email falso imitando una entidad conocida (banco, empresa, gobierno).
2. Genera urgencia: "Tu cuenta será bloqueada en 24 hs", "Actividad sospechosa detectada".
3. Incluye un link que parece legítimo pero apunta a un dominio bajo su control (`bancogaliccia.com` vs `bancogalicia.com`).
4. El sitio falso es visualmente idéntico al original.
5. La víctima ingresa sus credenciales → robadas.

### Variantes avanzadas

| Tipo | Descripción |
|------|-------------|
| **Spear Phishing** | Phishing dirigido y personalizado. El atacante investiga a la víctima (nombre, cargo, relaciones) para hacer el mensaje altamente creíble. |
| **Whaling** | Spear phishing apuntado a directivos de alto nivel (CEO, CFO). Alta recompensa potencial. |
| **Clone Phishing** | Se clona un email legítimo que la víctima ya recibió, reemplazando links o adjuntos por versiones maliciosas. |
| **Quishing** | Phishing mediante códigos QR. El usuario escanea un QR y es redirigido a un sitio malicioso. |
| **BEC** (Business Email Compromise) | El atacante accede o suplanta la cuenta de un ejecutivo para solicitar transferencias o cambiar datos bancarios. |

### Herramientas de defensa anti-phishing

| Herramienta | Función |
|-------------|---------|
| **SPF** (Sender Policy Framework) | Define qué servidores pueden enviar emails en nombre de un dominio. |
| **DKIM** (DomainKeys Identified Mail) | Firma criptográfica en el email que verifica que no fue alterado en tránsito. |
| **DMARC** | Política sobre qué hacer con emails que fallan SPF/DKIM: rechazar, poner en cuarentena o reportar. |

---

## 4. Autenticación

La autenticación es el proceso de verificar la identidad de un usuario antes de conceder acceso a un recurso. Existe una tensión permanente entre seguridad y usabilidad: a mayor seguridad, mayor fricción para el usuario legítimo.

### Tipos de autenticación

| Tipo | Base | Ejemplos |
|------|------|---------|
| **Basada en conocimiento** | Algo que sabés | Contraseña, PIN, preguntas de seguridad |
| **Basada en posesión** | Algo que tenés | Token físico, tarjeta, teléfono (OTP/2FA) |
| **Biométrica** | Algo que sos | Huella dactilar, reconocimiento facial, iris |

### Autenticación Multifactor (MFA)

Combina dos o más tipos distintos de autenticación. Si un factor es comprometido (ej: contraseña robada), el atacante necesita el segundo factor para acceder. Jerarquía de seguridad de menor a mayor:

| Método | Seguridad | Nota |
|--------|----------|------|
| SMS / código por mensaje | Baja | Vulnerable a SIM Swap: el atacante convence a la operadora de transferir tu número a su SIM. |
| App TOTP (Google Authenticator, Authy) | Media-Alta | Código de 6 dígitos que cambia cada 30s, generado localmente sin depender de red. |
| Passkeys / FIDO2 | Alta | Clave criptográfica vinculada al dispositivo; resistente a phishing por diseño. |
| Llave física (YubiKey) | Muy Alta | Hardware token; requiere presencia física; el estándar más alto disponible. |

### Contraseñas seguras

- Mínimo 12 caracteres, combinando mayúsculas, minúsculas, números y símbolos.
- Única por servicio — nunca reutilizar. Si un servicio es brecheado, el atacante prueba las mismas credenciales en otros (credential stuffing). Con contraseñas únicas, el daño queda contenido.
- Usar un gestor de contraseñas: **Bitwarden** (open source), **1Password**, **KeePass**.

---

## 5. Tipos de Malware

El malware (malicious software) es cualquier programa diseñado para dañar, comprometer o acceder de manera no autorizada a sistemas o datos. Cada tipo tiene una forma de propagarse y un objetivo distinto.

### Virus
Se replica insertándose en otros archivos ejecutables o documentos. **Necesita intervención humana para propagarse**: el usuario debe ejecutar el archivo infectado. Puede destruir datos, consumir recursos o abrir puertas traseras.

### Gusano (Worm)
Similar al virus pero **se propaga de forma autónoma** por redes, sin necesidad de que el usuario haga nada. Explota vulnerabilidades en protocolos o servicios para replicarse en otros sistemas. Puede saturar redes con su propio tráfico.

### Troyano
**Aparenta ser legítimo** (juego, utilidad, actualización falsa) pero ejecuta código malicioso en segundo plano. No se replica solo; depende de que el usuario lo instale voluntariamente. Típicamente incluye:
- **C&C (Command & Control)**: servidor remoto desde el que el atacante envía instrucciones.
- **Backdoor**: acceso remoto persistente al sistema comprometido.

### Adware
Software que **muestra publicidad no solicitada**. Suele instalarse junto con software legítimo. Se clasifica como **grayware** o **PUA** (Potentially Unwanted Application): no es explícitamente destructivo pero degrada la experiencia y puede recopilar datos de navegación.

### Spyware
**Espía al usuario** y recopila información sensible sin su consentimiento, transmitiéndola a un servidor externo. Variantes:
- **Keylogger**: registra todo lo que el usuario escribe (contraseñas, mensajes, datos de tarjeta).
- **RAT (Remote Access Trojan)**: combina troyano y spyware; permite al atacante controlar el equipo de forma remota y ver la pantalla en tiempo real.

### Rogue (Scareware)
**Simula ser un antivirus legítimo**. Genera pop-ups alarmantes de infecciones falsas para asustar al usuario y llevarlo a pagar por una "solución" que en realidad no existe. El atacante obtiene dinero y/o datos de tarjeta.

### Ransomware
**Cifra los archivos de la víctima y exige un rescate** (generalmente en criptomonedas) a cambio de la clave de descifrado. Es uno de los ataques más rentables para los cibercriminales.

| Tipo | Comportamiento |
|------|---------------|
| **Criptoransomware** | Cifra archivos; el sistema puede funcionar pero los datos son inaccesibles. |
| **Lockscreen ransomware** | Bloquea el acceso al sistema operativo completo. |

**Defensa: Regla 3-2-1**
- **3** copias de los datos.
- **2** medios de almacenamiento distintos (ej: disco externo + nube).
- **1** copia offsite (fuera del lugar físico).

Esta regla garantiza que siempre exista una copia limpia para restaurar ante un ataque de ransomware.

---

## 6. Antimalware: Detección y Soluciones

### Métodos de detección

| Método | Cómo funciona | Limitación |
|--------|--------------|------------|
| **Firmas (signatures)** | Compara archivos contra una base de datos de malware conocido. | No detecta malware nuevo (zero-day). |
| **Heurístico** | Analiza comportamiento o código buscando patrones sospechosos. | Puede generar falsos positivos. |
| **Sandboxing** | Ejecuta el archivo en un entorno aislado para observar su comportamiento real. | El malware puede detectar el sandbox. |
| **ML / IA** | Modelos entrenados para clasificar archivos o comportamientos como maliciosos. | Puede ser engañado con muestras adversariales. |

### Soluciones populares

- **Windows Defender** — integrado en Windows, cubre la mayoría de amenazas cotidianas.
- **Malwarebytes** — especializado en detección post-infección y limpieza.
- **CrowdStrike Falcon** — EDR (Endpoint Detection & Response) empresarial, basado en IA.

---

## 7. OSINT y Redes Sociales

Las redes sociales son una fuente masiva de información para atacantes. Con **OSINT** (Open Source Intelligence), un atacante puede:

- Identificar relaciones laborales y estructura organizacional (LinkedIn).
- Conocer rutinas, ubicaciones y horarios (Instagram, Twitter).
- Encontrar respuestas a preguntas de seguridad (nombre de mascota, ciudad natal).
- Construir un pretexto convincente para un ataque de spear phishing.

Regla práctica: asumir que cualquier dato publicado puede usarse en un ataque. Revisar periódicamente qué información es pública en los perfiles.

---

## Conceptos clave

| Término | Definición |
|---------|-----------|
| **Ingeniería social** | Manipulación psicológica para obtener acceso o información de una persona. |
| **Phishing** | Email fraudulento que suplanta una entidad legítima para robar datos. |
| **Spear phishing** | Phishing dirigido y personalizado a una víctima específica. |
| **Whaling** | Spear phishing apuntado a directivos de alto nivel. |
| **Vishing** | Phishing por llamada telefónica. |
| **Smishing** | Phishing por SMS. |
| **Baiting** | Dejar dispositivos infectados en lugares públicos para que alguien los conecte. |
| **Pretexting** | Crear un escenario falso para ganarse la confianza de la víctima. |
| **MFA / 2FA** | Autenticación que combina dos o más factores distintos para verificar identidad. |
| **SIM Swap** | Ataque donde el atacante transfiere el número de teléfono de la víctima a su SIM. |
| **Virus** | Malware que se replica insertándose en archivos; requiere acción del usuario para propagarse. |
| **Gusano** | Malware que se propaga de forma autónoma por redes sin intervención humana. |
| **Troyano** | Malware disfrazado de software legítimo; no se replica solo. |
| **Ransomware** | Malware que cifra archivos y exige rescate para recuperarlos. |
| **Spyware** | Malware que recopila información del usuario sin su conocimiento. |
| **Keylogger** | Variante de spyware que registra todo lo que el usuario escribe. |
| **RAT** | Remote Access Trojan — control remoto del equipo comprometido. |
| **Rogue / Scareware** | Falso antivirus que asusta al usuario para que pague por una solución inexistente. |
| **Regla 3-2-1** | 3 copias de datos, en 2 medios distintos, con 1 copia offsite. |
| **OSINT** | Open Source Intelligence — recolección de información desde fuentes públicas. |
| **Dark Web** | Capa de internet que requiere TOR para acceder; anónima y no indexada. |
| **SPF / DKIM / DMARC** | Protocolos de autenticación de email para prevenir spoofing y phishing. |
| **Credential stuffing** | Usar credenciales robadas de un servicio para intentar acceder a otros. |
