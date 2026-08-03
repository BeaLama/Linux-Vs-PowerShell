# Almacenamiento

## Introducción

El almacenamiento es uno de los componentes fundamentales de cualquier sistema. Una correcta administración de discos, particiones y sistemas de archivos permite garantizar el rendimiento, la disponibilidad de los datos y el correcto funcionamiento del equipo.

---

## Índice

- [Ver los discos del sistema](#ver-los-discos-del-sistema)
- [Consultar el espacio disponible](#consultar-el-espacio-disponible)
- [Listar particiones](#listar-particiones)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Montar y desmontar sistemas de archivos](#montar-y-desmontar-sistemas-de-archivos)
- [Crear una partición](#crear-una-partición)
- [Formatear una partición](#formatear-una-partición)
- [Cambiar la etiqueta de un volumen](#cambiar-la-etiqueta-de-un-volumen)
- [Comprobar el uso del disco por directorios](#comprobar-el-uso-del-disco-por-directorios)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Ver los discos del sistema

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `lsblk` | `Get-Disk` |
| **Ejemplo** | `lsblk -f` | `Get-Volume` |

> 💡 **Diferencia clave** — 🐧 `lsblk` muestra discos, particiones y puntos de montaje. · 🪟 `Get-Disk` muestra únicamente los discos físicos.

---

### Buenas prácticas

- Comprueba que todos los discos esperados son detectados por el sistema.
- Verifica el tamaño del disco antes de crear particiones o formatearlo.
- Identifica correctamente el disco sobre el que vas a trabajar para evitar pérdidas de información.
- Revisa el estado de los discos cuando se detecten problemas de almacenamiento.

---

### Comandos relacionados

- [Consultar el espacio disponible](#consultar-el-espacio-disponible)
- [Listar particiones](#listar-particiones)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)

---

[⬆️ Volver al índice](#índice)

## Consultar el espacio disponible

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `df -h` | `Get-Volume` |

**Ejemplo**
```bash
df -Th
```
```powershell
Get-Volume |
Select-Object DriveLetter,
              FileSystemType,
              Size,
              SizeRemaining
```

> 💡 **Diferencia clave** — 🐧 `df` muestra el uso de los sistemas de archivos montados. · 🪟 `Get-Volume` muestra información de los volúmenes de Windows.

---

### Buenas prácticas

- Revisa periódicamente el espacio libre de los discos.
- Mantén un margen de espacio disponible para evitar problemas de rendimiento.
- Investiga las unidades cuyo porcentaje de uso sea elevado.
- Comprueba el crecimiento del almacenamiento antes de que el disco llegue al 100 % de ocupación.

---

### Comandos relacionados

- [Ver los discos del sistema](#ver-los-discos-del-sistema)
- [Listar particiones](#listar-particiones)
- [Comprobar el uso del disco por directorios](#comprobar-el-uso-del-disco-por-directorios)

---

[⬆️ Volver al índice](#índice)

## Listar particiones

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo fdisk -l` | `Get-Partition` |
| **Ejemplo** | `sudo fdisk -l /dev/sda` | `Get-Partition -DiskNumber 0` |

> 💡 **Diferencia clave** — 🐧 `fdisk -l` muestra información de discos y particiones. · 🪟 `Get-Partition` muestra únicamente las particiones.

---

### Buenas prácticas

- Comprueba siempre el disco sobre el que vas a trabajar antes de modificar particiones.
- Verifica el tamaño de las particiones antes de ampliarlas o eliminarlas.
- Identifica si el disco utiliza GPT o MBR antes de realizar cambios.
- Realiza una copia de seguridad antes de modificar el esquema de particiones.

---

### Comandos relacionados

- [Ver los discos del sistema](#ver-los-discos-del-sistema)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Crear una partición](#crear-una-partición)

---

[⬆️ Volver al índice](#índice)

## Consultar información de un volumen

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `lsblk -f` | `Get-Volume` |

**Ejemplo**
```bash
blkid
```
```powershell
Get-Volume |
Select-Object DriveLetter,
              FileSystemLabel,
              FileSystem,
              HealthStatus
```

> 💡 **Diferencia clave** — 🐧 `lsblk -f` muestra sistemas de archivos, UUID y puntos de montaje. · 🪟 `Get-Volume` muestra información del volumen administrado por Windows.


---

### Buenas prácticas

- Comprueba el sistema de archivos antes de realizar tareas de mantenimiento.
- Utiliza el UUID en Linux para evitar problemas cuando cambie el nombre del dispositivo.
- Verifica que el volumen se encuentre en buen estado antes de almacenar información crítica.
- Mantén etiquetas descriptivas para identificar fácilmente los distintos volúmenes.

---

### Comandos relacionados

- [Ver los discos del sistema](#ver-los-discos-del-sistema)
- [Listar particiones](#listar-particiones)
- [Montar y desmontar sistemas de archivos](#montar-y-desmontar-sistemas-de-archivos)

---

[⬆️ Volver al índice](#índice)

## Montar y desmontar sistemas de archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo mount <dispositivo> <punto_de_montaje>` | `Mount-DiskImage -ImagePath "<ruta>"` |

**Ejemplo**
```bash
sudo umount /mnt
```
```powershell
Dismount-DiskImage `
-ImagePath "C:\ISO\Windows.iso"
```

> 💡 **Diferencia clave** — 🐧 Cualquier sistema de archivos debe montarse en un directorio antes de utilizarse. · 🪟 Las unidades físicas suelen montarse automáticamente; `Mount-DiskImage` se utiliza principalmente para imágenes ISO y VHD/VHDX.

---

### Buenas prácticas

- Comprueba que el punto de montaje existe antes de montar una partición.
- Desmonta siempre un sistema de archivos antes de retirar un disco externo.
- Evita desmontar unidades que estén siendo utilizadas por otros procesos.
- Verifica que no haya archivos abiertos antes de ejecutar `umount`.

---

### Comandos relacionados

- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Crear una partición](#crear-una-partición)
- [Formatear una partición](#formatear-una-partición)

---

[⬆️ Volver al índice](#índice)

## Crear una partición

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo fdisk <disco>` | `New-Partition` |

**Ejemplo**
```bash

```
```powershell
New-Partition `
-DiskNumber 1 `
-UseMaximumSize `
-DriveLetter D
```

> 💡 **Diferencia clave** — 🐧 `fdisk` y `parted` son herramientas interactivas. · 🪟 `New-Partition` crea la partición directamente mediante parámetros.

---

### Buenas prácticas

- Verifica cuidadosamente el disco antes de crear una partición.
- Comprueba si el disco utiliza GPT o MBR antes de modificarlo.
- Deja espacio libre si prevés ampliar particiones en el futuro.
- Formatea siempre la nueva partición antes de utilizarla.

---

### Comandos relacionados

- [Listar particiones](#listar-particiones)
- [Formatear una partición](#formatear-una-partición)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)

---

[⬆️ Volver al índice](#índice)

## Formatear una partición

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo mkfs.ext4 <partición>` | `Format-Volume` |
| **Ejemplo** | `sudo mkfs.xfs /dev/sdb1` | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 El sistema de archivos se especifica mediante el comando (`mkfs.ext4`, `mkfs.xfs`, etc.). · 🪟 El sistema de archivos se indica mediante el parámetro `-FileSystem`.

---

### Buenas prácticas

- Comprueba dos veces la partición antes de formatearla.
- Selecciona el sistema de archivos más adecuado para el uso previsto.
- Asigna una etiqueta descriptiva para identificar fácilmente el volumen.
- Realiza una copia de seguridad antes de formatear cualquier partición.

---

### Comandos relacionados

- [Crear una partición](#crear-una-partición)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Cambiar la etiqueta de un volumen](#cambiar-la-etiqueta-de-un-volumen)

---

[⬆️ Volver al índice](#índice)

## Cambiar la etiqueta de un volumen

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo e2label <partición> <etiqueta>` | `Set-Volume` |

**Ejemplo**
```bash
sudo xfs_admin `
-L Datos `
/dev/sdb1
```
```powershell
Set-Volume `
-DriveLetter D `
-NewFileSystemLabel "Datos"
```

> 💡 **Diferencia clave** — 🐧 La utilidad depende del sistema de archivos utilizado. · 🪟 `Set-Volume` funciona con los sistemas de archivos compatibles con Windows.

---

### Buenas prácticas

- Utiliza etiquetas descriptivas para identificar fácilmente los volúmenes.
- Mantén una nomenclatura coherente entre los distintos discos del sistema.
- Comprueba la etiqueta después de modificarla para verificar que el cambio se ha aplicado correctamente.
- Evita utilizar caracteres especiales o nombres excesivamente largos.

---

### Comandos relacionados

- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Formatear una partición](#formatear-una-partición)
- [Ver los discos del sistema](#ver-los-discos-del-sistema)

---

[⬆️ Volver al índice](#índice)

## Comprobar el uso del disco por directorios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `du -sh <directorio>` | `Get-ChildItem` |

**Ejemplo**
```bash
du -h --max-depth=1 /home
```
```powershell
Get-ChildItem C:\Users -Directory |
ForEach-Object {

    $size = (
        Get-ChildItem $_.FullName `
        -Recurse -File `
        -ErrorAction SilentlyContinue |
        Measure-Object Length -Sum
    ).Sum

    [PSCustomObject]@{
        Directorio = $_.Name
        TamañoGB   = "{0:N2}" -f ($size / 1GB)
    }

}
```

> 💡 **Diferencia clave** — 🐧 `du` calcula directamente el tamaño de los directorios. · 🪟 Es necesario combinar varios cmdlets para obtener un resultado similar.

---

### Buenas prácticas

- Revisa periódicamente los directorios de mayor tamaño para evitar quedarte sin espacio.
- Analiza especialmente carpetas de copias de seguridad, registros (`logs`) y archivos temporales.
- Elimina únicamente archivos cuya función conozcas.
- Utiliza este comando antes de ampliar un disco o una partición para identificar qué está consumiendo el almacenamiento.

---

### Comandos relacionados

- [Consultar el espacio disponible](#consultar-el-espacio-disponible)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Ver los discos del sistema](#ver-los-discos-del-sistema)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Ver los discos del sistema | `lsblk` | `Get-Disk` |
| Consultar el espacio disponible | `df -h` | `Get-Volume` |
| Listar particiones | `fdisk -l` / `parted -l` | `Get-Partition` |
| Consultar información de un volumen | `lsblk -f` / `blkid` | `Get-Volume` |
| Montar un sistema de archivos | `mount` | `Mount-DiskImage` |
| Desmontar un sistema de archivos | `umount` | `Dismount-DiskImage` |
| Crear una partición | `fdisk` / `parted` | `New-Partition` |
| Formatear una partición | `mkfs.ext4`, `mkfs.xfs`, `mkfs.ntfs` | `Format-Volume` |
| Cambiar la etiqueta de un volumen | `e2label`, `xfs_admin`, `ntfslabel` | `Set-Volume` |
| Consultar el uso del disco por directorios | `du -sh` | `Get-ChildItem` + `Measure-Object` |

---

### Buenas prácticas generales

- Comprueba siempre el disco correcto antes de crear, eliminar o formatear particiones.
- Mantén suficiente espacio libre en las unidades para evitar problemas de rendimiento.
- Utiliza etiquetas descriptivas para identificar fácilmente los distintos volúmenes.
- Realiza copias de seguridad antes de modificar particiones o sistemas de archivos.
- Verifica el sistema de archivos utilizado antes de ejecutar tareas de mantenimiento.
- Supervisa periódicamente el crecimiento del almacenamiento para detectar posibles problemas antes de que el disco se llene.

---

[⬆️ Volver al índice](#índice)