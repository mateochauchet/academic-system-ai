# Unidad 1 — Fundamentos de la Seguridad de la Información

## El punto de partida: ¿qué protege la seguridad informática?

Toda organización tiene **recursos**: servidores, computadoras, redes (tangibles) y bases de datos, contratos, patentes (intangibles). El objetivo de la seguridad informática es proteger esos recursos, especialmente **la información**, que es el activo más valioso.

---

## 1. Amenazas, Vulnerabilidades y Riesgo

**Amenaza** — cualquier evento que puede causar daño. Hay dos tipos:
- *Naturales*: no son intencionales. Error humano (borrar un archivo sin querer), fallo de hardware, inundación, corte de luz.
- *Deliberadas*: alguien actúa con intención maliciosa. Puede ser interno (empleado descontento, ex-empleado con acceso no revocado) o externo (hackers, cibercriminales, competidores).

**Vulnerabilidad** — una debilidad en el sistema que permite que una amenaza tenga éxito. No se crea a propósito; aparece por errores de diseño, mala configuración o falta de actualización.

**Riesgo** — la probabilidad de que una amenaza explote una vulnerabilidad y cause daño.

> **Riesgo = Probabilidad × Impacto**

Ejemplo de evaluación:

| Amenaza | Impacto (0–3) | Probabilidad (0–3) | Riesgo |
|---------|--------------|-------------------|--------|
| Robo de sistema biométrico | 3 | 0 | **0** |
| Infección con malware | 2 | 3 | **6** |
| Pérdida de suministro eléctrico | 3 | 1 | **3** |

---

## 2. Qué hacer con un riesgo

Cuando identificás un riesgo, tenés cuatro opciones:

1. **Prevenir** — eliminar la causa para que no ocurra.
2. **Transferir** — delegarlo a otro (ej: contratar un seguro).
3. **Mitigar** — reducir su impacto si ocurre.
4. **Aceptar** — reconocés que puede pasar y asumís las consecuencias.

---

## 3. Seguridad Informática vs. Seguridad de la Información

- **Seguridad de la información**: abarca cualquier soporte con datos sensibles (papel, conversaciones, digital).
- **Seguridad informática**: se enfoca en sistemas digitales — cómo procesar, almacenar y transmitir información de forma segura.

Tres elementos que debe proteger:
- **Usuarios**: el eslabón más débil.
- **Información**: el activo principal, "el oro" a cuidar.
- **Infraestructura**: hardware, redes, servidores.

---

## 4. Los tres tipos de controles

**Preventivos** — actúan *antes* del incidente. Inversión a largo plazo. Ejemplos: antivirus, firewall, contraseñas fuertes, actualizaciones.

**Correctivos** — actúan *después* del incidente. Son caros y urgentes: el tiempo es el recurso más escaso. Ejemplos: parches de emergencia, restaurar backups, contratar expertos.

**Detectivos** — los más complejos. Parten del supuesto de que algo ya pasó. Su objetivo es identificar el punto exacto del ataque y entender qué sucedió. Requieren alto conocimiento técnico.

---

## 5. La Tríada CIA — Los tres pilares de la seguridad

```
        Integridad
           |
  Disponibilidad — Confidencialidad
```

Si cualquiera de los tres falla, el sistema no es seguro.

### Confidencialidad
Solo las personas autorizadas pueden acceder a la información. Se implementa con:
- **Autenticación**: verificar que el usuario es quien dice ser.
- **Gestión de privilegios**: cada usuario accede solo a lo que necesita.
- **Cifrado**: la información se vuelve ilegible para quienes no tienen la clave.

### Integridad
Los datos no fueron modificados de forma no autorizada. Trabajar con datos incorrectos puede ser tan dañino como perderlos.

Se garantiza con:
- Monitoreo del tráfico de red.
- Auditorías que registren quién accedió y cambió qué.
- Firmas digitales y checksums para detectar modificaciones.
- Backups para restaurar el estado original.

### Disponibilidad
La información tiene que estar accesible cuando se necesita.

Se garantiza con:
- **SLAs**: acuerdos de nivel de servicio con tiempos garantizados.
- **Balanceo de carga**: distribuye tráfico para aguantar ataques DDoS.
- **Redundancia y backups**: si falla un sistema, otro toma el relevo.

---

## 6. Principio de Mínimos Privilegios

Cada usuario o sistema debe tener acceso *únicamente* a lo que necesita para su función, nada más.

La regla tiene tres dimensiones:
- **Qué** puede hacer: solo los permisos necesarios para la tarea.
- **Por cuánto tiempo**: solo mientras dure la tarea.
- **Sobre qué**: solo los recursos que requiere esa tarea.

Si un malware infecta una sesión de usuario normal, tiene acceso limitado. Si infecta una sesión de administrador, puede hacer lo que quiera.

---

## 7. Superficie de Ataque

El conjunto de todos los puntos por donde alguien podría atacar un sistema. Cuanto más grande, más oportunidades tiene el atacante.

Tres componentes:

**Software**: aplicaciones, servicios, páginas web. Para reducirla: instalar solo lo necesario, mantener todo actualizado, configurar con mínimos privilegios.

**Hardware**: routers, switches, servidores, computadoras. Para reducirla: protección física, cerrar puertos innecesarios, actualizar firmware.

**Recursos Humanos**: el componente más impredecible. Para reducirla: auditorías y registros (eliminan el anonimato), capacitación en seguridad.

### Tipos de ataque

**Pasivo**: el atacante observa sin interferir. Recolecta información con OSINT y monitoreo de tráfico. Prepara el terreno para ataques posteriores.

**Activo**: intervención directa sobre la infraestructura. Busca entrar, instalarse y persistir. Objetivos: robar datos, desplegar malware, sabotear.

---

## Mapa mental

```
Seguridad Informática
├── Conceptos base
│   ├── Recurso
│   ├── Amenaza (natural / deliberada)
│   ├── Vulnerabilidad
│   └── Riesgo = Probabilidad × Impacto
│
├── Respuesta al riesgo
│   ├── Prevenir / Transferir / Mitigar / Aceptar
│   └── Controles: Preventivo | Correctivo | Detectivo
│
├── Tríada CIA
│   ├── Confidencialidad (autenticación, cifrado, privilegios)
│   ├── Integridad (auditorías, firmas digitales, backups)
│   └── Disponibilidad (SLA, redundancia, balanceo)
│
└── Principios clave
    ├── Mínimos Privilegios
    └── Superficie de Ataque (software / hardware / personas)
```
