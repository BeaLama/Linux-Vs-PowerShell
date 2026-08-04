# Copias de seguridad 

## Introducción

Las copias de seguridad constituyen uno de los pilares fundamentales de la administración de sistemas.

## Índice

- [Fundamentos de las copias de seguridad](#fundamentos-de-las-copias-de-seguridad)
- [Tipos de copias de seguridad](#tipos-de-copias-de-seguridad)
- [Estrategias y planificación](#estrategias-y-planificacion)
- [Almacenamiento de las copias](#almacenamiento-de-las-copias)
- [Automatización y herramientas](#automatizacion-y-herramientas)
- [Restauración y recuperación](#restauracion-y-recuperacion)
- [Seguridad de las copias](#seguridad-de-las-copias)

---

## Fundamentos de las copias de seguridad

*Las copias de seguridad (backup) son duplicados de la información almacenados en un medio distinto al original con el objetivo de poder recuperarla en caso de pérdida, corrupción o eliminación.*

### Frecuencia de las copias

*La periodicidad depende de la importancia de la información.*

| Tipo de información | Frecuencia habitual |
|----------------------|--------------------|
| Bases de datos críticas | Varias veces al día |
| Servidores | Diaria |
| Documentación | Diaria |
| Equipos personales | Semanal |
| Archivos históricos | Mensual |

### Comparativa

| Concepto | Finalidad |
|----------|-----------|
| Backup | Recuperar información |
| Sincronización | Mantener datos iguales |
| Replicación | Alta disponibilidad |
| RAID | Redundancia frente a fallos de disco |

---

## Tipos de copias de seguridad

*Existen diferentes tipos de copias de seguridad, cada uno con ventajas e inconvenientes en cuanto al tiempo necesario para realizarlas, el espacio de almacenamiento requerido y la velocidad de recuperación.*

### Comparativa

*Ejemplo.*

| Día | Completa | Incremental | Diferencial |
|-----|----------|-------------|-------------|
| Lunes | Todo | Todo | Todo |
| Martes | Todo | Cambios martes | Cambios martes |
| Miércoles | Todo | Cambios miércoles | Cambios martes + miércoles |
| Jueves | Todo | Cambios jueves | Cambios martes + miércoles + jueves |

### Comparativa

| Tipo | Espacio | Tiempo de copia | Tiempo de restauración |
|------|----------|-----------------|------------------------|
| Completa | Alto | Alto | Muy rápido |
| Incremental | Bajo | Muy rápido | Más lento |
| Diferencial | Medio | Medio | Rápido |
| Espejo | Igual que el origen | Rápido | Muy rápido |
| Snapshot | Muy bajo inicialmente | Muy rápido | Muy rápido |
| Sintética | Medio | Rápido | Muy rápido |

---

## Estrategias y planificación

*Disponer de copias de seguridad no garantiza por sí solo la recuperación de la información.*

### Clasificación de la información

*No todos los datos tienen la misma importancia.*

| Nivel | Ejemplos |
|--------|----------|
| Crítico | Bases de datos, ERP, Active Directory |
| Alto | Documentación de la empresa |
| Medio | Equipos de usuarios |
| Bajo | Archivos temporales |

### Frecuencia de las copias

*La planificación debe establecer cada cuánto tiempo se ejecutarán los backups.*

| Información | Frecuencia |
|--------------|-----------|
| Bases de datos | Cada hora o varias veces al día |
| Servidores | Diaria |
| Equipos de usuario | Semanal |
| Archivos históricos | Mensual |

### Política de retención

*La política de retención determina cuánto tiempo deben conservarse las copias.*

| Tipo | Conservación |
|------|--------------|
| Diarias | 30 días |
| Semanales | 3 meses |
| Mensuales | 1 año |
| Anuales | 5 años |

### Relación entre RPO y RTO

*Ambos conceptos son fundamentales en cualquier plan de continuidad.*

| Concepto | Significado |
|----------|-------------|
| RPO | Cantidad máxima de datos que pueden perderse |
| RTO | Tiempo máximo permitido para recuperar el servicio |

### Comparativa

| Estrategia | Objetivo |
|------------|----------|
| GFS | Rotación de copias |
| 3-2-1 | Protección frente a pérdidas |
| 3-2-1-1-0 | Protección avanzada contra ransomware |
| RPO | Limitar la pérdida de datos |
| RTO | Reducir el tiempo de recuperación |

---

## Almacenamiento de las copias

*La ubicación donde se almacenan las copias de seguridad es tan importante como la propia copia.*

### Comparativa

| Almacenamiento | Ventajas | Inconvenientes |
|----------------|----------|----------------|
| Disco externo | Económico | Riesgo de pérdida |
| NAS | Centralizado | Requiere red |
| SAN | Alto rendimiento | Coste elevado |
| Servidor Backup | Gestión centralizada | Necesita mantenimiento |
| Cinta | Muy económica a largo plazo | Restauración lenta |
| Cloud | Escalable y externa | Dependencia de Internet |
| Híbrido | Combina rapidez y seguridad | Mayor complejidad |

---

## Automatización y herramientas

*En infraestructuras profesionales, las copias de seguridad rara vez se realizan de forma manual.*

### Automatización en Linux

*En sistemas Linux la herramienta más utilizada es cron.*

```bash
0 2 * * * /usr/local/scripts/backup.sh
```

### Scripts de backup

*Muchas organizaciones desarrollan scripts propios.*

```bash
rsync -av /datos /backup
```
```powershell
Robocopy C:\Datos D:\Backup /MIR
```

### Robocopy

*En Windows destaca Robocopy.*

```powershell
robocopy C:\Datos D:\Backup /MIR /R:2 /W:5
```

- Copia incremental.
- Reanudación automática.
- Gran rendimiento.
- Muy utilizado en servidores Windows.

### Comparativa

| Herramienta | Sistema | Características |
|-------------|----------|-----------------|
| Windows Server Backup | Windows | Integrada |
| rsync | Linux | Sincronización eficiente |
| Robocopy | Windows | Copias avanzadas |
| Restic | Multiplataforma | Cifrado y deduplicación |
| BorgBackup | Linux | Deduplicación y compresión |
| Duplicati | Multiplataforma | Interfaz web y nube |
| Veeam | Empresarial | Backup y replicación |
| Nakivo | Empresarial | Virtualización y cloud |

---

## Restauración y recuperación

*El objetivo principal de una copia de seguridad es permitir la recuperación de la información cuando se produce una incidencia.*

### Comparativa

| Tipo de restauración | Uso habitual |
|-----------------------|--------------|
| Archivo | Recuperar documentos eliminados |
| Carpeta | Recuperar directorios completos |
| Base de datos | Restaurar información crítica |
| Aplicación | Recuperar software y configuración |
| Máquina virtual | Recuperación rápida de servidores virtuales |
| Bare Metal | Reconstrucción completa del sistema |

---

## Seguridad de las copias

*Las copias de seguridad contienen, en muchas ocasiones, la misma información crítica que los sistemas originales.*

### Comparativa

| Medida | Objetivo |
|---------|----------|
| Cifrado | Proteger la confidencialidad |
| MFA | Evitar accesos no autorizados |
| Copia offline | Proteger frente al ransomware |
| Copia inmutable | Evitar modificaciones o borrados |
| Offsite | Protección ante desastres |
| Auditoría | Registrar actividades |
| Hashes | Verificar integridad |

---

[⬆️ Volver al índice](#índice)