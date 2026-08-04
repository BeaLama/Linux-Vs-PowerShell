# 11 - Recuperación del sistema 

## Introducción

La recuperación del sistema comprende el conjunto de procedimientos y herramientas destinados a restaurar el funcionamiento de un equipo o servidor tras un fallo grave.

## Índice

- [Fundamentos de la recuperación del sistema](#fundamentos-de-la-recuperación-del-sistema)
- [Recuperación del arranque](#recuperación-del-arranque)
- [Herramientas de recuperación en Windows](#herramientas-de-recuperación-en-windows)
- [Herramientas de recuperación en Linux](#herramientas-de-recuperación-en-linux)
- [Recuperación de servicios y aplicaciones](#recuperación-de-servicios-y-aplicaciones)
- [Recuperación desde copias de seguridad](#recuperación-desde-copias-de-seguridad)
- [Recuperación ante desastres (Disaster Recovery)](#recuperación-ante-desastres-disaster-recovery)
- [Pruebas y validación de la recuperación](#pruebas-y-validación-de-la-recuperación)

---

## Fundamentos de la recuperación del sistema

*La recuperación del sistema comprende el conjunto de procedimientos, herramientas y técnicas destinados a restaurar el funcionamiento normal de un equipo o servidor tras un fallo que impide su uso total o parcial.*

### Prioridad de los sistemas

*No todos los sistemas tienen la misma importancia.*

| Prioridad | Sistemas |
|-----------|----------|
| Crítica | Active Directory, ERP, Bases de datos |
| Alta | Servidores de archivos |
| Media | Aplicaciones internas |
| Baja | Equipos de usuario |

### Comparativa

| Concepto | Objetivo |
|----------|----------|
| Recuperación | Restaurar el funcionamiento del sistema |
| Diagnóstico | Identificar la causa del fallo |
| Backup | Recuperar datos perdidos |
| Continuidad del negocio | Mantener los servicios disponibles |
| Disaster Recovery | Recuperar la infraestructura tras un desastre |

---

## Recuperación del arranque

*El proceso de arranque es el conjunto de etapas que permiten cargar el sistema operativo desde que el equipo recibe alimentación hasta que el usuario puede iniciar sesión.*

### Comparativa

| Problema | Posible solución |
|-----------|------------------|
| Disco no detectado | Revisar BIOS/UEFI |
| Orden de arranque incorrecto | Configurar Boot Order |
| Bootloader dañado | Reconstruir gestor de arranque |
| Partición EFI corrupta | Reparar o recrear la partición |
| Sistema de archivos corrupto | Reparar el sistema de archivos |
| Archivos del sistema dañados | Restaurar archivos del sistema |

---

## Herramientas de recuperación en Windows

*Windows incorpora un amplio conjunto de herramientas destinadas a diagnosticar y reparar problemas que impiden el funcionamiento normal del sistema operativo.*

### Comparativa

| Herramienta | Función |
|-------------|----------|
| WinRE | Entorno de recuperación |
| Reparación de inicio | Reparar el arranque automáticamente |
| Restaurar sistema | Volver a un estado anterior |
| CHKDSK | Reparar errores del disco |
| SFC | Restaurar archivos del sistema |
| DISM | Reparar la imagen de Windows |
| Bootrec | Reparar el gestor de arranque |
| BCDBoot | Reconstruir archivos de arranque |
| Visor de eventos | Analizar errores del sistema |

---

## Herramientas de recuperación en Linux

*Linux dispone de numerosas herramientas para diagnosticar y recuperar sistemas dañados sin necesidad de reinstalar el sistema operativo.*

### Reinstalar GRUB

*Desde un entorno Live es posible reinstalar el gestor de arranque.*

```bash
sudo grub-install /dev/sda
```

### FSCK

*fsck (File System Check) comprueba y repara errores en los sistemas de archivos.*

```bash
sudo fsck /dev/sda1
```

- Inodos dañados.
- Errores de bloques.
- Corrupción del sistema de archivos.

### Journalctl

*journalctl permite consultar los registros generados por systemd.*

```bash
journalctl -xb
```

### Systemctl

*Cuando el sistema consigue arrancar parcialmente, systemctl permite comprobar el estado de los servicios.*

```bash
systemctl status apache2
```

### Reparación de paquetes

*En sistemas basados en Debian es posible reparar instalaciones incompletas.*

```bash
sudo apt --fix-broken install
```

### Comparativa

| Herramienta | Función |
|-------------|----------|
| Recovery Mode | Recuperación básica |
| Rescue Mode | Diagnóstico con servicios mínimos |
| Emergency Mode | Recuperación mínima |
| Live USB | Reparación desde un sistema externo |
| GRUB | Gestor de arranque |
| fsck | Reparar sistemas de archivos |
| journalctl | Consultar registros |
| chroot | Acceder al sistema instalado |
| systemctl | Gestionar servicios |

---

## Recuperación de servicios y aplicaciones

*No todas las incidencias afectan al sistema operativo completo.*

### Comprobación del estado del servicio

*En Windows.*

```bash
systemctl status apache2
```
```powershell
Get-Service
```

### Revisión de registros

*Los registros suelen proporcionar información muy valiosa.*

```bash
journalctl
```

- Visor de eventos.
- Registros de aplicaciones.
- Registros del sistema.

### Reinicio controlado

*En muchas ocasiones basta con reiniciar el servicio.*

```bash
sudo systemctl restart apache2
```
```powershell
Restart-Service DNS
```

### Comparativa

| Incidencia | Actuación habitual |
|------------|--------------------|
| Servicio detenido | Reiniciar servicio |
| Configuración incorrecta | Restaurar configuración |
| Base de datos dañada | Reparar o restaurar backup |
| Certificado caducado | Renovar certificado |
| Dependencia detenida | Iniciar servicio dependiente |
| Corrupción grave | Restaurar desde copia de seguridad |

---

## Recuperación desde copias de seguridad

*La recuperación desde copias de seguridad es uno de los métodos más importantes para restaurar sistemas después de una incidencia grave.*

### Comparativa

| Tipo de recuperación | Uso |
|----------------------|-----|
| Archivo individual | Recuperar documentos eliminados |
| Carpeta completa | Restaurar recursos compartidos |
| Base de datos | Recuperar información estructurada |
| Máquina virtual | Recuperar servidores rápidamente |
| Bare Metal Recovery | Reconstrucción completa |
| Restauración granular | Recuperar elementos concretos |

---

## Recuperación ante desastres (Disaster Recovery)

### Diferencia entre Backup y Disaster Recovery

*Aunque están relacionados, no son lo mismo.*

| Backup | Disaster Recovery |
|--------|-------------------|
| Protege datos | Recupera servicios completos |
| Guarda información | Define procedimientos |
| Permite restaurar archivos | Permite recuperar operaciones |
| Es una parte del DR | Incluye backup, sistemas y procesos |

### Análisis de impacto del negocio (BIA)

*Antes de crear un plan DR es necesario realizar un análisis de impacto.*

| Servicio | Prioridad |
|----------|-----------|
| Active Directory | Crítica |
| ERP | Crítica |
| Correo | Alta |
| Archivos compartidos | Alta |
| Aplicaciones internas | Media |

- Servicios críticos.
- Dependencias.
- Coste de una interrupción.
- Tiempo máximo sin servicio.
- Prioridad de recuperación.

### Equipo de respuesta

*Un plan DR debe definir responsables.*

| Rol | Función |
|-----|---------|
| Responsable IT | Coordinar recuperación |
| Administrador sistemas | Recuperar servidores |
| Administrador redes | Recuperar comunicaciones |
| Responsable negocio | Validar servicios |

### Comparativa

| Estrategia | Tiempo recuperación | Coste |
|------------|--------------------|-------|
| Backup tradicional | Alto | Bajo |
| Cold Site | Alto | Bajo |
| Warm Site | Medio | Medio |
| Hot Site | Muy bajo | Alto |
| Cloud DR | Bajo | Variable |
| Replicación | Muy bajo | Alto |

---

## Pruebas y validación de la recuperación

*Una recuperación del sistema no puede considerarse completada simplemente porque el equipo o servicio vuelva a arrancar.*

### Frecuencia de las pruebas

*La periodicidad depende de la criticidad del sistema.*

| Sistema | Frecuencia |
|---------|------------|
| Sistemas críticos | Mensual |
| Servidores importantes | Trimestral |
| Sistemas secundarios | Semestral |
| Documentación | Revisión continua |

### Comparativa

| Prueba | Objetivo |
|--------|----------|
| Documental | Revisar procedimientos |
| Parcial | Validar componentes concretos |
| Completa | Comprobar recuperación total |
| Simulación desastre | Evaluar respuesta global |

---

[⬆️ Volver al índice](#índice)