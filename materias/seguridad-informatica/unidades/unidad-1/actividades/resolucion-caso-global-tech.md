# Resolución — Caso de Estudio GlobalTech

## Confidencialidad

**¿Qué información fue comprometida?**
Datos personales de clientes (nombres, contactos, posiblemente datos bancarios), datos de empleados (información personal, credenciales) y propiedad intelectual (código fuente, patentes, secretos comerciales).

**¿Cuáles son las consecuencias?**
Para los clientes y empleados: riesgo de robo de identidad, fraude, suplantación. Para la empresa: pérdida de ventaja competitiva si se expuso propiedad intelectual, daño reputacional, multas regulatorias por no proteger datos personales.

**¿Cómo mitigar el impacto?**
Notificar a los afectados para que tomen medidas (cambiar contraseñas, monitorear cuentas). Revocar credenciales comprometidas. Cifrar los datos sensibles que quedaron en los sistemas para evitar futuros accesos. Contratar servicios de monitoreo de identidad para los afectados.

---

## Integridad

**¿Cómo afectó el ataque a la integridad?**
Los atacantes tuvieron acceso a la red interna durante días. En ese tiempo pudieron modificar registros, alterar configuraciones o introducir malware persistente. Los datos que quedaron en los sistemas no pueden considerarse confiables hasta verificarlos.

**¿Cómo restaurar la integridad?**
Comparar el estado actual de los sistemas contra backups previos al ataque. Usar checksums y firmas digitales para verificar que los archivos no fueron modificados. Reinstalar sistemas comprometidos desde cero si es necesario.

**¿Cómo prevenir futuros ataques?**
Implementar auditorías continuas que registren cada acceso y cambio. Activar alertas ante modificaciones no autorizadas. Mantener backups frecuentes e inmutables (que el atacante no pueda modificar).

---

## Disponibilidad

**¿Cómo impactó la disponibilidad?**
El 27 de febrero GlobalTech suspendió servicios voluntariamente para contener el ataque. Aunque fue una decisión correcta, los usuarios quedaron sin acceso. Esto genera pérdidas económicas directas y daño a la confianza de los clientes.

**¿Cómo restaurar la disponibilidad?**
Aislar los sistemas comprometidos y levantar los servicios no afectados lo antes posible. Restaurar los sistemas dañados desde backups verificados. Comunicar plazos claros a los usuarios para gestionar expectativas.

**¿Cómo prevenir futuros ataques?**
Implementar balanceo de carga y redundancia para que un ataque a un servidor no tire toda la infraestructura. Definir un plan de respuesta a incidentes que permita contener el daño sin suspender todo. Parchear vulnerabilidades en servidores web de forma inmediata cuando se detectan.
