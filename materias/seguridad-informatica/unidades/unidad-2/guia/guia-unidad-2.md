# Guía de la Unidad II — Desafíos de Seguridad para los Usuarios

**Contenidista:** Germán Ariel Paradisi

---

## Objetivos

- Identificar los distintos tipos de ataques y amenazas orientadas a los usuarios.
- Comprender los mecanismos de autenticación y su relación con la seguridad.
- Reconocer las distintas categorías de malware y sus características.

**Palabras clave:** Ingeniería social — Autenticación — Malware — Phishing — Ransomware — Spyware — Troyano — Vulnerabilidades humanas.

---

## 1. Ingeniería Social

La ingeniería social es el conjunto de técnicas de manipulación psicológica orientadas a engañar personas para que realicen acciones o divulguen información confidencial. A diferencia de los ataques técnicos, explota vulnerabilidades humanas, no tecnológicas.

### 1.1 Vulnerabilidades psicológicas

Los atacantes se apoyan en rasgos inherentes al comportamiento humano:

| Vulnerabilidad | Descripción |
|----------------|-------------|
| **Dificultad para decir no** | Las personas tienden a ceder ante pedidos aparentemente razonables o insistentes. |
| **Exceso de confianza** | Disposición a creer en la legitimidad de una solicitud sin verificarla. |
| **Necesidad de reconocimiento** | El deseo de ser útil o de quedar bien lleva a compartir información innecesaria. |
| **Empatía** | La tendencia a ayudar cuando alguien parece estar en apuros facilita el engaño. |

### 1.2 Phishing

El phishing es un ataque de ingeniería social distribuido principalmente por correo electrónico. El atacante se hace pasar por una entidad legítima (banco, empresa, gobierno) para robar credenciales, datos personales o instalar malware.

**Anatomía de un ataque de phishing:**
1. El atacante crea un email falso imitando a una entidad conocida.
2. Genera urgencia: "Tu cuenta será bloqueada en 24 hs".
3. Incluye un link que parece legítimo pero apunta a un sitio bajo su control.
4. El sitio falso es visualmente idéntico al original.
5. La víctima ingresa sus credenciales → robadas.

### 1.3 Spear Phishing

Variante dirigida del phishing. El atacante investiga previamente a la víctima (nombre, cargo, relaciones, contexto laboral) para personalizar el mensaje y aumentar su credibilidad. Mucho más efectivo que el phishing genérico.

---

## 2. Autenticación

La autenticación es el proceso de verificar la identidad de un usuario o sistema antes de conceder acceso a un recurso. Existe una tensión permanente entre seguridad y usabilidad: a mayor seguridad, mayor fricción para el usuario legítimo.

### 2.1 Tipos de autenticación

| Tipo | Base | Ejemplos |
|------|------|---------|
| **Basada en conocimiento** | Algo que sabés | Contraseña, PIN, preguntas de seguridad |
| **Basada en posesión** | Algo que tenés | Token físico, tarjeta, teléfono (OTP/2FA) |
| **Biométrica** | Algo que sos | Huella dactilar, reconocimiento facial, iris |

### 2.2 Autenticación multifactor (MFA)

Combina dos o más tipos distintos de autenticación. Incluso si un factor es comprometido (ej: contraseña robada), el atacante necesita el segundo factor para acceder.

**Niveles de seguridad en 2FA (de menor a mayor):**
1. SMS / código por mensaje — vulnerable a SIM Swap
2. App TOTP (Google Authenticator, Authy) — más seguro, offline
3. Passkeys / FIDO2 — vinculadas al dispositivo, resistentes a phishing
4. Llave física (YubiKey) — el estándar más alto; requiere presencia física

---

## 3. Tipos de Malware

El malware (malicious software) es cualquier programa diseñado para dañar, comprometer o acceder de manera no autorizada a sistemas o datos.

### 3.1 Virus

Programa que se **replica insertándose en otros archivos ejecutables o documentos**. Necesita la intervención humana para propagarse (ejecutar el archivo infectado). Su objetivo puede ser destruir datos, consumir recursos o abrir puertas traseras.

Características:
- Requiere un archivo huésped.
- Se activa cuando el usuario ejecuta el archivo infectado.
- Puede modificar o destruir datos.

### 3.2 Gusano (Worm)

Similar al virus pero **se propaga de forma autónoma** a través de redes, sin necesidad de intervención humana. Explota vulnerabilidades en protocolos o servicios de red para replicarse en otros sistemas.

Diferencia clave respecto al virus: el gusano no necesita un archivo huésped; se replica por sí solo y puede saturar redes con su tráfico.

### 3.3 Troyano

Programa que **aparenta ser legítimo** (juego, utilidad, actualización) pero ejecuta código malicioso en segundo plano. No se replica solo; depende de que el usuario lo instale voluntariamente.

Componentes típicos:
- **C&C (Command & Control)**: servidor remoto desde el que el atacante envía instrucciones al troyano instalado.
- **Backdoor (puerta trasera)**: acceso remoto persistente al sistema comprometido.

El atacante puede usar el troyano para robar datos, desplegar más malware, o incorporar el equipo a una botnet.

### 3.4 Adware

Software que **muestra publicidad no solicitada**. Puede instalarse junto con software legítimo (bundleware). Suele ser clasificado como **grayware** o **PUA** (Potentially Unwanted Application): no es explícitamente malicioso pero es indeseable.

Impacto principal: degrada la experiencia del usuario y puede redirigir tráfico web o recopilar datos de navegación.

### 3.5 Spyware

Software que **espía al usuario** y recopila información sensible sin su consentimiento. Transmite los datos a un servidor externo.

Variantes:
- **Keylogger**: registra todo lo que el usuario escribe (contraseñas, mensajes, números de tarjeta).
- **RAT (Remote Access Trojan)**: combinación de troyano y spyware que permite al atacante controlar el equipo de forma remota y observar la pantalla en tiempo real.

### 3.6 Rogue (Rogueware / Scareware)

Software que **simula ser un antivirus legítimo**. Muestra alertas falsas de infección para asustar al usuario y llevarlo a pagar por una "solución" que en realidad no existe (o que es el propio malware).

Mecanismo: genera pop-ups alarmantes → el usuario entra en pánico → paga para "desinfectar" → el atacante obtiene dinero y/o datos de tarjeta.

### 3.7 Ransomware

El ransomware **cifra los archivos de la víctima y exige un rescate** (generalmente en criptomonedas) a cambio de la clave de descifrado. Es uno de los ataques más rentables para los cibercriminales.

**Dos variantes principales:**

| Tipo | Comportamiento |
|------|---------------|
| **Criptoransomware** | Cifra archivos y datos; el sistema puede funcionar pero los datos son inaccesibles. |
| **Lockscreen ransomware** | Bloquea el acceso al sistema operativo completo; no necesariamente cifra datos. |

**Estrategia de defensa — Regla 3-2-1:**
- **3** copias de los datos.
- **2** medios de almacenamiento distintos (ej: disco externo + nube).
- **1** copia offsite (fuera del lugar físico).

Esta estrategia garantiza que, ante un ataque de ransomware, siempre exista una copia limpia de los datos para restaurar.

---

## Síntesis de la Unidad

La Unidad II aborda los desafíos de seguridad desde la perspectiva del usuario. La **ingeniería social** explota vulnerabilidades psicológicas (confianza, empatía, dificultad para decir no) para robar información o engañar a las personas. La **autenticación** es la primera línea de defensa: cuantos más factores se combinan (contraseña + OTP + biometría), menor la probabilidad de acceso no autorizado. Los **tipos de malware** cubren un espectro amplio: desde virus y gusanos que se propagan solos, hasta ransomware que extorsiona organizaciones enteras.

El denominador común de esta unidad es que **el usuario es tanto el vector de ataque más explotado como la primera línea de defensa**: la educación y la conciencia son fundamentales.

---

## Bibliografía

**Obligatoria:**
- Grubb, S. (2021). *How Cybersecurity Really Works: A Hands-On Guide for Total Beginners*. No Starch Press.
- Romero, M. et al. (2018). *Introducción a la Seguridad Informática y el Análisis de Vulnerabilidades*. Área de Innovación y Desarrollo, S.L.

**Optativa:**
- Diogenes, Y; Ozkaya, E. (2018). *Ciberseguridad: Estrategias de ataque y defensa*. Packt.
