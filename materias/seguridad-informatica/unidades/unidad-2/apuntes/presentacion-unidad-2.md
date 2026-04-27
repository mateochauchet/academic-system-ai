# Presentación — Unidad II: Desafíos de Seguridad para los Usuarios

Clase de la Unidad II. Cubre privacidad, dark web, ingeniería social, phishing avanzado, antimalware, contraseñas y 2FA, OSINT en redes sociales y recursos.

---

## Privacidad en la Era Digital

### Tipos de datos

| Tipo | Descripción | Ejemplos |
|------|-------------|---------|
| **Datos personales** | Identifican a una persona física | Nombre, DNI, email, dirección, teléfono |
| **Datos sensibles** | Categoría especial con mayor protección legal | Salud, religión, orientación sexual, datos biométricos |
| **Datos públicos** | Libremente accesibles sin restricción | Publicaciones en redes sociales, información de contacto publicada |
| **Metadatos** | Información sobre información | Fecha/hora de un email, ubicación GPS de una foto, duración de llamadas |

Los metadatos suelen ignorarse pero son extremadamente reveladores: una foto puede exponer ubicación exacta, dispositivo usado y hora del día sin que el usuario lo sepa.

### Marco legal

| Normativa | Alcance |
|-----------|---------|
| **GDPR** (Reglamento General de Protección de Datos) | Unión Europea — aplica a cualquier empresa que trate datos de ciudadanos europeos |
| **Ley 25.326** | Argentina — Ley de Protección de Datos Personales |
| **CCPA** (California Consumer Privacy Act) | California, EE.UU. — derechos de privacidad para consumidores |

---

## Dark Web

La web no es una sola capa. Se divide en tres niveles:

| Capa | Proporción | Descripción |
|------|-----------|-------------|
| **Surface Web** | ~4% | Lo que indexan los buscadores (Google, Bing). Sitios públicos accesibles normalmente. |
| **Deep Web** | ~90% | Contenido no indexado: intranets corporativas, bases de datos académicas, correo privado, sistemas bancarios. No es ilegal — solo no está en los buscadores. |
| **Dark Web** | ~6% | Requiere software especial (TOR) para acceder. Anónimo. Contiene tanto foros legítimos de activismo y privacidad como mercados ilegales (drogas, credenciales robadas, malware). |

**TOR (The Onion Router)**: red de servidores voluntarios que cifra el tráfico en capas y lo enruta por múltiples nodos, ocultando la IP del usuario. Las páginas `.onion` solo son accesibles desde la red TOR.

---

## Técnicas de Ingeniería Social

| Técnica | Descripción |
|---------|-------------|
| **Phishing** | Email fraudulento que imita una entidad legítima para robar credenciales o datos. |
| **Vishing** | Voice phishing — llamada telefónica. El atacante se hace pasar por soporte técnico, banco o gobierno. |
| **Smishing** | SMS phishing — mensaje de texto con link malicioso o solicitud de datos. |
| **Pretexting** | Creación de un escenario falso elaborado (pretexto) para ganarse la confianza de la víctima y extraer información. |
| **Baiting** | Dejar dispositivos infectados (pendrives) en lugares públicos esperando que alguien los conecte. |
| **Quid pro quo** | Ofrecer algo a cambio de información: "Te ayudo con tu problema técnico, solo necesito tu contraseña". |

### Caso real: Twitter Bitcoin Scam (2020)

En julio de 2020, el grupo de atacantes usó **vishing** contra empleados de Twitter con acceso a herramientas internas. Llamaron haciéndose pasar por soporte de TI, convencieron a empleados de entregar credenciales, y tomaron control de cuentas verificadas de alto perfil: Barack Obama, Joe Biden, Elon Musk, Apple, Uber, Kanye West.

Publicaron un mensaje de estafa de Bitcoin desde esas cuentas, recaudando ~$120.000 en pocas horas.

**Lección**: el factor humano es más vulnerable que la tecnología. Ni los sistemas más seguros protegen si un empleado es engañado para entregar acceso.

---

## Phishing: Anatomía y Variantes Avanzadas

### Anatomía de un ataque de phishing (5 pasos)

1. Atacante crea email falso imitando entidad conocida (banco, servicio, empresa).
2. Genera urgencia: "Tu cuenta se bloqueará en 24 hs", "Actividad sospechosa detectada".
3. Incluye link que parece legítimo (dominio similar: `bancogaliccia.com` vs `bancogalicia.com`).
4. Redirige a sitio clon visualmente idéntico al original.
5. Víctima ingresa credenciales → robadas.

**Estadística clave**: el 95% de las brechas de seguridad comienza con un correo de phishing.

### Variantes avanzadas

| Tipo | Descripción |
|------|-------------|
| **Spear Phishing** | Phishing dirigido y personalizado. El atacante investiga a la víctima (nombre, cargo, relaciones) para hacer el mensaje creíble. |
| **Whaling** | Spear phishing apuntado a directivos de alto nivel (CEO, CFO). Alta recompensa potencial. |
| **Clone Phishing** | Se clona un email legítimo que ya recibió la víctima, reemplazando links o adjuntos por versiones maliciosas. |
| **Quishing** | Phishing mediante códigos QR. El usuario escanea un QR y es redirigido a un sitio malicioso. |
| **BEC (Business Email Compromise)** | Compromiso del email corporativo. El atacante accede o suplanta la cuenta de un ejecutivo para solicitar transferencias o cambiar datos bancarios. |

### Herramientas de defensa anti-phishing

| Herramienta | Función |
|-------------|---------|
| **SPF** (Sender Policy Framework) | Define qué servidores pueden enviar emails en nombre de un dominio. |
| **DKIM** (DomainKeys Identified Mail) | Firma criptográfica en el email que verifica que no fue alterado. |
| **DMARC** | Política sobre qué hacer con emails que fallan SPF/DKIM (rechazar, poner en cuarentena, reportar). |
| **KnowBe4** | Plataforma de entrenamiento en seguridad: simula ataques de phishing para educar empleados. |

---

## Antimalware: Detección y Soluciones

### Métodos de detección

| Método | Cómo funciona | Limitación |
|--------|--------------|------------|
| **Firmas (signatures)** | Compara archivos contra una base de datos de malware conocido. | No detecta malware nuevo (zero-day). |
| **Heurístico** | Analiza el comportamiento o código del archivo buscando patrones sospechosos. | Puede generar falsos positivos. |
| **Sandboxing** | Ejecuta el archivo en un entorno aislado para observar su comportamiento real. | Requiere más recursos; el malware puede detectar el sandbox. |
| **ML / IA** | Modelos entrenados para clasificar archivos o comportamientos como maliciosos. | Depende de la calidad del entrenamiento; puede ser engañado. |

### Soluciones populares

- **Windows Defender** — integrado en Windows, cubre la mayoría de amenazas cotidianas.
- **Malwarebytes** — especializado en detección post-infección y limpieza.
- **CrowdStrike Falcon** — EDR (Endpoint Detection & Response) empresarial, basado en IA.
- **Kaspersky**, **ESET**, **Bitdefender** — soluciones comerciales con alta tasa de detección.

---

## Contraseñas y Autenticación de Dos Factores

### Contraseñas seguras

- Mínimo 12 caracteres.
- Combinación de mayúsculas, minúsculas, números y símbolos.
- Única por servicio — nunca reutilizar.
- Usar un gestor de contraseñas: **Bitwarden** (open source), **1Password**, **KeePass**.

**Por qué no reutilizar**: si un servicio es brecheado, el atacante prueba las mismas credenciales en otros servicios (credential stuffing). Con contraseñas únicas, el daño queda contenido.

### 2FA / MFA — Jerarquía de seguridad

| Método | Seguridad | Notas |
|--------|----------|-------|
| SMS / código por mensaje | Baja | Vulnerable a SIM Swap (el atacante convence a la operadora de transferir tu número a su SIM) |
| App TOTP (Google Authenticator, Authy) | Media-Alta | Código de 6 dígitos que cambia cada 30s, generado localmente — no depende de red |
| Passkeys / FIDO2 | Alta | Clave criptográfica vinculada al dispositivo; resistente a phishing por diseño |
| Llave física (YubiKey) | Muy Alta | Hardware token; requiere presencia física; el estándar más alto disponible |

---

## OSINT y Redes Sociales

Las redes sociales son una fuente masiva de información para atacantes. Con **OSINT** (Open Source Intelligence) y datos públicos, un atacante puede:

- Identificar relaciones laborales y estructura organizacional (LinkedIn).
- Conocer rutinas, ubicaciones habituales y horarios (Instagram, Twitter).
- Encontrar respuestas a preguntas de seguridad (nombre de mascota, ciudad natal).
- Construir un pretexto convincente para un ataque de spear phishing.

**Regla práctica**: revisar periódicamente qué información está pública en los perfiles. Asumir que cualquier dato publicado puede usarse contra vos.

---

## Decálogo de Seguridad para Usuarios

1. **Contraseñas únicas y fuertes** — gestor de contraseñas para cada cuenta.
2. **Activar 2FA en todos los servicios importantes** — preferir app o llave física sobre SMS.
3. **Desconfiar de lo urgente** — el phishing abusa de la urgencia y el miedo.
4. **Verificar el remitente y la URL antes de hacer clic** — hover sobre el link para ver el destino real.
5. **Actualizar siempre** — sistemas, apps, firmware y drivers.
6. **No conectar dispositivos desconocidos** — pendrives abandonados pueden ser baiting.
7. **Proteger la privacidad en redes sociales** — revisar qué información es pública.
8. **Usar VPN en redes públicas** — el tráfico en Wi-Fi abierta puede interceptarse.
9. **Backups 3-2-1** — 3 copias, 2 medios distintos, 1 offsite.
10. **Educación continua** — las amenazas evolucionan; el conocimiento es la mejor defensa.

---

## Recursos

| Plataforma | Qué ofrece |
|------------|-----------|
| **CyberInt** | Inteligencia de amenazas y monitoreo de dark web |
| **Fortinet** | Soluciones de seguridad empresarial; blog con threat intelligence |
| **KnowBe4** | Entrenamiento en concienciación de seguridad y simulaciones de phishing |
| **Whalemate** | Recursos de ciberseguridad y comunidad |
| **Beygoo** | Recursos educativos de seguridad informática |
| **Have I Been Pwned (HIBP)** | Verificá si tu email o contraseña aparece en brechas de datos conocidas |
