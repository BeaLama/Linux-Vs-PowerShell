# Auditoría y seguridad

## Introducción

La auditoría y la seguridad son elementos fundamentales en la administración de sistemas modernos.

## Índice

- [Auditoría de sistemas](#auditoria-de-sistemas)
- [Registros de seguridad](#registros-de-seguridad)
- [Control de acceso](#control-de-acceso)
- [Autenticación y autorización](#autenticacion-y-autorizacion)
- [Políticas de seguridad](#politicas-de-seguridad)
- [Hardening del sistema](#hardening-del-sistema)
- [Monitorización de seguridad](#monitorizacion-de-seguridad)
- [Respuesta ante incidentes](#respuesta-ante-incidentes)

---

## Auditoría de sistemas

*La auditoría de sistemas consiste en recopilar, revisar y analizar la actividad de un sistema operativo con el objetivo de comprobar que funciona de forma correcta, segura y conforme a las políticas establecidas.*

### Comparativa

| Linux | Windows |
|--------|----------|
| `journald` | Visor de eventos |
| `syslog` | Registro de Seguridad |
| `auditd` | Directivas de auditoría |
| Archivos de log | Eventos centralizados |

---

## Registros de seguridad

*Los registros de seguridad (*security logs*) son archivos o bases de datos donde el sistema operativo almacena los eventos relacionados con la seguridad.*

### Registros en Linux

*Linux dispone de varios registros relacionados con la seguridad.*

| Archivo | Contenido |
|----------|-----------|
| `/var/log/auth.log` | Autenticación (Debian/Ubuntu). |
| `/var/log/secure` | Autenticación (RHEL, Rocky, AlmaLinux). |
| `/var/log/syslog` | Eventos generales del sistema. |
| `/var/log/messages` | Eventos generales (según la distribución). |
| `journalctl` | Registro centralizado mediante systemd. |

### journalctl

*En sistemas con systemd, gran parte de la información puede consultarse mediante.*

```bash
journalctl
```

### Identificadores de evento (Event ID)

*Cada evento de Windows dispone de un identificador numérico.*

| Event ID | Descripción |
|-----------|-------------|
| 4624 | Inicio de sesión correcto |
| 4625 | Inicio de sesión fallido |
| 4634 | Cierre de sesión |
| 4720 | Creación de usuario |
| 4726 | Eliminación de usuario |
| 4732 | Usuario añadido a un grupo |

### Comparativa

| Linux | Windows |
|--------|----------|
| `journalctl` | Visor de eventos |
| `/var/log/auth.log` | Registro de Seguridad |
| `/var/log/secure` | Event ID |
| `syslog` | Registros del sistema |

---

## Control de acceso

*El control de acceso es el conjunto de mecanismos que determinan qué usuarios o procesos pueden acceder a un recurso y qué acciones están autorizados a realizar.*

### Comparativa

| Linux | Windows |
|--------|----------|
| Propietario | Usuario |
| Grupo | Grupo |
| Otros | Usuarios específicos |
| Permisos rwx | ACL |
| ACL opcionales | ACL integradas |

---

## Autenticación y autorización

*Aunque suelen utilizarse conjuntamente, autenticación y autorización son dos conceptos diferentes dentro de la seguridad informática.*

### Comparativa

| Autenticación | Autorización |
|---------------|--------------|
| Verifica la identidad | Determina los permisos |
| Se realiza primero | Se realiza después |
| Usuario y contraseña | Permisos y ACL |
| Claves SSH | Roles |
| MFA | Grupos |

---

## Políticas de seguridad

*Las políticas de seguridad son un conjunto de normas, procedimientos y directrices que establecen cómo deben protegerse los sistemas, los datos y los recursos de una organización.*

### Comparativa

| Política | Finalidad |
|-----------|-----------|
| Contraseñas | Proteger las credenciales |
| Cuentas | Gestionar identidades |
| Actualizaciones | Corregir vulnerabilidades |
| Copias de seguridad | Garantizar la recuperación de datos |
| Acceso remoto | Proteger conexiones externas |
| Uso aceptable | Regular el uso de los recursos |
| Respuesta ante incidentes | Actuar correctamente ante un incidente |

---

## Hardening del sistema

*El hardening consiste en aplicar un conjunto de medidas destinadas a reducir la superficie de ataque de un sistema operativo, un servidor o una aplicación.*

### Comparativa

| Sistema sin hardening | Sistema con hardening |
|------------------------|-----------------------|
| Muchos servicios activos | Solo los necesarios |
| Configuración por defecto | Configuración revisada |
| Puertos abiertos | Puertos mínimos |
| Permisos amplios | Mínimo privilegio |
| Actualizaciones pendientes | Sistema actualizado |
| Escasa auditoría | Auditoría configurada |

---

## Monitorización de seguridad

*La monitorización de seguridad consiste en supervisar de forma continua la actividad de un sistema para detectar comportamientos anómalos, intentos de intrusión o posibles incidentes de seguridad.*

### Comparativa

| Auditoría | Monitorización |
|------------|----------------|
| Registra eventos | Supervisa continuamente |
| Análisis posterior | Detección en tiempo real |
| Investigación | Prevención y respuesta |
| Registros | Alertas y supervisión |

---

## Respuesta ante incidentes

*Un incidente de seguridad es cualquier evento que compromete o puede comprometer la confidencialidad, integridad o disponibilidad de los sistemas o de la información.*

### Comparativa

| Fase | Objetivo |
|------|----------|
| Preparación | Estar preparado antes del incidente |
| Detección | Identificar el problema |
| Análisis | Comprender el incidente |
| Contención | Evitar su propagación |
| Erradicación | Eliminar la causa |
| Recuperación | Restaurar los servicios |
| Lecciones aprendidas | Mejorar la respuesta futura |

---

[⬆️ Volver al índice](#índice)
