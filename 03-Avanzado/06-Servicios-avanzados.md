# Servicios avanzados

## Introducción

Los servicios son procesos especiales que se ejecutan en segundo plano para proporcionar funciones esenciales al sistema operativo o a las aplicaciones.

## Índice

- [Arquitectura de un servicio](#arquitectura-de-un-servicio)
- [Dependencias entre servicios](#dependencias-entre-servicios)
- [Tipos de inicio y estados](#tipos-de-inicio-y-estados)
- [Servicios críticos del sistema](#servicios-criticos-del-sistema)
- [Recuperación automática de servicios](#recuperacion-automatica-de-servicios)
- [Monitorización y diagnóstico](#monitorizacion-y-diagnostico)
- [Seguridad de los servicios](#seguridad-de-los-servicios)
- [Automatización](#automatizacion)

---

## Arquitectura de un servicio

*Un servicio es un tipo especial de proceso diseñado para ejecutarse en segundo plano y proporcionar funciones al sistema operativo o a otras aplicaciones.*

### Diferencia entre proceso y servicio

*Aunque ambos son procesos en ejecución, tienen finalidades distintas.*

| Proceso | Servicio |
|----------|-----------|
| Puede iniciarlo un usuario. | Normalmente lo inicia el sistema operativo. |
| Suele tener interfaz gráfica. | Normalmente no tiene interfaz. |
| Finaliza cuando termina su trabajo. | Permanece ejecutándose continuamente. |
| Depende del usuario. | Proporciona funciones al sistema o a otras aplicaciones. |

### Ejemplos de servicios habituales

| Servicio | Función |
|-----------|----------|
| SSH | Acceso remoto seguro |
| Apache / Nginx | Servidor web |
| MySQL / PostgreSQL | Base de datos |
| DNS | Resolución de nombres |
| DHCP | Asignación automática de IP |
| Print Spooler | Gestión de impresión |
| Windows Update | Actualizaciones del sistema |

### Comparativa Linux / Windows

| Linux | Windows |
|--------|----------|
| systemd | Service Control Manager |
| Unidades `.service` | Servicios registrados en el SCM |
| Archivos de configuración | Registro y archivos de configuración |
| Usuarios del sistema | Cuentas de servicio |
| `systemctl` | Consola Servicios / PowerShell |

---

## Dependencias entre servicios

*En la mayoría de los sistemas, los servicios no funcionan de forma aislada.*

### Dependencias en Linux

*En sistemas modernos, las dependencias son gestionadas por systemd.*

| Directiva | Función |
|------------|----------|
| `Requires=` | Dependencia obligatoria. |
| `Wants=` | Dependencia recomendada pero no obligatoria. |
| `After=` | Orden de inicio. |
| `Before=` | Indica que el servicio debe iniciarse antes que otro. |

### Consultar dependencias

*Mostrar dependencias de un servicio.*

```bash
systemctl list-dependencies sshd
```

### Consultar dependencias

*PowerShell.*

```powershell
Get-Service Spooler | Select-Object -ExpandProperty ServicesDependedOn
```

### Diagnóstico

*Cuando un servicio no inicia correctamente.*

```bash
systemctl status servicio
```
```powershell
Get-Service NombreServicio
```

### Comparativa

| Linux | Windows |
|--------|----------|
| `Requires=` | Dependencia obligatoria |
| `Wants=` | Dependencia opcional |
| `After=` | Orden de inicio |
| `Before=` | Orden previo |
| `systemctl list-dependencies` | `Get-Service` / `services.msc` |

---

## Tipos de inicio y estados

*Cada servicio dispone de una configuración de inicio y de un estado de ejecución.*

### Estados en Linux

*En sistemas con systemd, los estados más habituales son.*

| Estado | Significado |
|---------|-------------|
| active | Servicio funcionando. |
| inactive | Servicio detenido. |
| failed | Error durante el inicio o ejecución. |
| activating | Iniciándose. |
| deactivating | Deteniéndose. |

```bash
systemctl status servicio
```

---

## Servicios críticos del sistema

*No todos los servicios tienen la misma importancia.*

### Servicios críticos en Linux

*Algunos ejemplos habituales son.*

| Servicio | Función |
|----------|----------|
| `systemd` | Sistema de inicio y gestión de servicios. |
| `systemd-journald` | Registro de eventos. |
| `NetworkManager` | Gestión de la red. |
| `systemd-logind` | Gestión de sesiones de usuario. |
| `sshd` | Acceso remoto mediante SSH (en servidores). |
| `cron` o `crond` | Ejecución de tareas programadas. |

### Servicios críticos en Windows

*Entre los más importantes se encuentran.*

| Servicio | Función |
|----------|----------|
| Service Control Manager (SCM) | Administración de servicios. |
| Windows Event Log | Registro de eventos. |
| Remote Procedure Call (RPC) | Comunicación entre procesos. |
| Windows Update | Actualizaciones del sistema. |
| DHCP Client | Obtención automática de direcciones IP. |
| DNS Client | Resolución de nombres. |
| Print Spooler | Gestión de impresión. |

### Comparativa

| Servicio | Linux | Windows |
|----------|--------|----------|
| Gestión de servicios | `systemd` | Service Control Manager |
| Registro de eventos | `systemd-journald` | Windows Event Log |
| Gestión de red | `NetworkManager` | DHCP Client / DNS Client |
| Programación de tareas | `cron` | Task Scheduler |
| Acceso remoto | `sshd` | Remote Desktop Services (si está habilitado) |

---

## Recuperación automática de servicios

*Un servicio puede detenerse inesperadamente debido a errores de software, problemas de configuración, falta de recursos o fallos del sistema operativo.*

### Directiva Restart

*Las opciones más utilizadas son.*

| Valor | Comportamiento |
|--------|----------------|
| `no` | No reiniciar. |
| `always` | Reiniciar siempre. |
| `on-failure` | Reiniciar solo si falla. |
| `on-abnormal` | Reiniciar tras una finalización anómala. |
| `on-success` | Reiniciar tras finalizar correctamente. |

### Comparativa

| Linux | Windows |
|--------|----------|
| `Restart=` | Acciones de recuperación |
| `RestartSec=` | Tiempo antes del reinicio |
| systemd | Service Control Manager |
| Archivo `.service` | Propiedades del servicio |
| Reinicio automático | Reinicio automático |

---

## Monitorización y diagnóstico

*Supervisar el estado de los servicios es una tarea fundamental para garantizar la disponibilidad de un sistema.*

---

## Seguridad de los servicios

*Los servicios suelen ejecutarse de forma continua y, en muchos casos, están accesibles desde la red.*

### Comparativa

| Medida | Beneficio |
|---------|-----------|
| Mínimo privilegio | Reduce el impacto de un ataque |
| Cuentas dedicadas | Mejor aislamiento |
| Actualizaciones | Corrigen vulnerabilidades |
| Firewall | Reduce la exposición |
| Cifrado | Protege la información |
| Auditoría | Facilita investigaciones |
| Monitorización | Detecta incidencias rápidamente |
| Aislamiento | Limita la propagación de un compromiso |

---

## Automatización

*En entornos con numerosos equipos o servidores, administrar manualmente los servicios resulta poco práctico.*

### Automatización vs intervención manual

| Automatización | Administración manual |
|----------------|-----------------------|
| Rápida | Más lenta |
| Repetible | Depende del operador |
| Menos errores | Mayor riesgo de errores humanos |
| Escalable | Difícil de aplicar en muchos equipos |
| Requiere planificación | Útil para tareas puntuales |

---

[⬆️ Volver al índice](#índice)