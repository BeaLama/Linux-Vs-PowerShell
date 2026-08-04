# Almacenamiento avanzado

## Introducción

El almacenamiento es uno de los componentes más importantes de cualquier sistema informático.

## Índice

- [Tipos de almacenamiento](#tipos-de-almacenamiento)
- [RAID](#raid)
- [LVM y administración de volúmenes](#lvm-y-administracion-de-volumenes)
- [Sistemas de archivos avanzados](#sistemas-de-archivos-avanzados)
- [Almacenamiento en red](#almacenamiento-en-red)
- [Cuotas de disco](#cuotas-de-disco)
- [Monitorización y mantenimiento](#monitorizacion-y-mantenimiento)
- [Recuperación de almacenamiento](#recuperacion-de-almacenamiento)

---

## Tipos de almacenamiento

*El almacenamiento es el componente encargado de guardar de forma permanente la información de un sistema informático.*

### Comparativa HDD, SSD y NVMe

| Característica | HDD | SSD SATA | SSD NVMe |
|---------------|------|----------|-----------|
| Tecnología | Magnética | Memoria flash | Memoria flash |
| Velocidad | Baja | Alta | Muy alta |
| Latencia | Alta | Baja | Muy baja |
| Partes móviles | Sí | No | No |
| Consumo | Alto | Bajo | Bajo |
| Precio por GB | Bajo | Medio | Superior |

### Comparativa

| Tipo | Uso habitual |
|------|--------------|
| HDD | Almacenamiento masivo |
| SSD SATA | Equipos y servidores |
| SSD NVMe | Alto rendimiento |
| NAS | Compartición de archivos |
| SAN | Virtualización y centros de datos |
| Nube | Escalabilidad y acceso remoto |

---

## RAID

*El RAID (Redundant Array of Independent Disks) es una tecnología que permite combinar varios discos físicos para que el sistema operativo los utilice como una única unidad lógica.*

### Comparativa de niveles RAID

| RAID | Discos mínimos | Rendimiento | Redundancia | Capacidad útil |
|------|----------------|-------------|-------------|----------------|
| RAID 0 | 2 | Muy alta | No | 100 % |
| RAID 1 | 2 | Alta | Sí (1 disco) | 50 % |
| RAID 5 | 3 | Alta | Sí (1 disco) | n−1 |
| RAID 6 | 4 | Alta | Sí (2 discos) | n−2 |
| RAID 10 | 4 | Muy alta | Sí | 50 % |

### Comparativa de uso

| Escenario | RAID recomendado |
|-----------|------------------|
| Máximo rendimiento | RAID 0 |
| Sistema operativo | RAID 1 |
| Servidor de archivos | RAID 5 |
| Datos críticos | RAID 6 |
| Virtualización y bases de datos | RAID 10 |

---

## LVM y administración de volúmenes

*La gestión tradicional de particiones presenta diversas limitaciones.*

### Consultar la configuración

*Linux proporciona diferentes comandos para consultar la información de LVM.*

```bash
pvs
```

### Ampliar un volumen lógico

*Una de las principales ventajas de LVM consiste en ampliar fácilmente un volumen lógico.*

```bash
lvextend -L +20G /dev/vgdatos/lvdatos
```

### Comparativa

| Linux | Windows |
|--------|----------|
| Physical Volume (PV) | Disco físico |
| Volume Group (VG) | Storage Pool |
| Logical Volume (LV) | Disco virtual |
| LVM | Storage Spaces |

---

## Sistemas de archivos avanzados

*El sistema de archivos es el componente encargado de organizar y gestionar la información almacenada en un dispositivo de almacenamiento.*

### Compatibilidad

*No todos los sistemas operativos admiten los mismos sistemas de archivos.*

| Sistema operativo | Sistemas habituales |
|-------------------|---------------------|
| Linux | ext4, XFS, Btrfs, ZFS |
| Windows | NTFS, ReFS |
| macOS | APFS |

### ¿Qué sistema de archivos elegir?

*La elección depende del escenario.*

| Escenario | Sistema recomendado |
|-----------|---------------------|
| Linux general | ext4 |
| Grandes servidores Linux | XFS |
| Snapshots y administración avanzada | Btrfs |
| Máxima integridad | ZFS |
| Windows general | NTFS |
| Grandes servidores Windows | ReFS |

### Comparativa

| Sistema | Plataforma | Ventaja principal |
|----------|------------|-------------------|
| ext4 | Linux | Estabilidad |
| XFS | Linux | Alto rendimiento |
| Btrfs | Linux | Snapshots y funciones avanzadas |
| ZFS | Linux/BSD | Máxima integridad |
| NTFS | Windows | Compatibilidad y seguridad |
| ReFS | Windows Server | Alta resiliencia |

---

## Almacenamiento en red

*En entornos empresariales es habitual que la información no se almacene únicamente en los discos internos de cada equipo o servidor, sino en dispositivos accesibles a través de la red.*

### Diferencias entre NAS y SAN

*Aunque ambos permiten compartir almacenamiento, funcionan de forma diferente.*

| NAS | SAN |
|------|-----|
| Comparte archivos | Comparte bloques |
| Acceso mediante SMB o NFS | Acceso mediante iSCSI o Fibre Channel |
| Fácil de administrar | Más complejo |
| Menor coste | Mayor coste |
| Ideal para documentos | Ideal para servidores y virtualización |

### Comparativa SMB y NFS

| SMB | NFS |
|------|-----|
| Principalmente Windows | Principalmente Linux |
| Utiliza Samba en Linux | Integrado en Linux |
| Muy habitual en oficinas | Muy habitual en servidores |

### Comparativa

| Tecnología | Nivel de acceso | Uso habitual |
|------------|-----------------|--------------|
| NAS | Archivos | Compartición de documentos |
| SAN | Bloques | Virtualización y bases de datos |
| SMB | Archivos | Redes Windows |
| NFS | Archivos | Redes Linux |
| iSCSI | Bloques | Servidores sobre Ethernet |
| Fibre Channel | Bloques | Centros de datos |

---

## Cuotas de disco

*Las cuotas de disco permiten limitar la cantidad de espacio de almacenamiento que pueden utilizar los usuarios o grupos dentro de un sistema de archivos.*

### Consultar cuotas en Linux

*Algunos comandos habituales son.*

```bash
quota
```

### Comparativa

| Tipo | Característica |
|------|----------------|
| Cuota por usuario | Límite individual |
| Cuota por grupo | Límite compartido |
| Soft Limit | Genera avisos |
| Hard Limit | Bloquea la escritura |

---

## Monitorización y mantenimiento

*La monitorización y el mantenimiento del almacenamiento permiten garantizar el correcto funcionamiento de discos, sistemas de archivos y dispositivos de almacenamiento a lo largo del tiempo.*

### Consultar SMART en Linux

*La herramienta más utilizada es smartctl, incluida en el paquete smartmontools.*

```bash
smartctl -H /dev/sda
```

### Consultar SMART en Windows

*Windows permite consultar parte de esta información mediante PowerShell o herramientas específicas del fabricante.*

```powershell
Get-PhysicalDisk
```

- CrystalDiskInfo.
- Dell OpenManage.
- HPE Smart Storage Administrator.
- Samsung Magician (SSD Samsung).

### Estado del sistema de archivos

*Además del hardware, también debe supervisarse el sistema de archivos.*

```bash
fsck
```
```powershell
chkdsk
```

- Errores.
- Corrupciones.
- Espacio libre.
- Integridad.
- Journaling.

### Comparativa

| Elemento | Qué supervisa |
|----------|---------------|
| SMART | Estado físico del disco |
| Espacio libre | Capacidad disponible |
| IOPS | Operaciones por segundo |
| Latencia | Tiempo de respuesta |
| RAID | Estado de redundancia |
| Sistema de archivos | Integridad de los datos |

---

## Recuperación de almacenamiento

*A pesar de aplicar medidas como RAID, copias de seguridad o monitorización, pueden producirse incidencias que afecten al almacenamiento de un sistema.*

### Recuperación del sistema de archivos

*Cuando un sistema de archivos presenta errores puede ser necesario repararlo.*

```bash
fsck
```
```powershell
chkdsk
```

---

[⬆️ Volver al índice](#índice)
