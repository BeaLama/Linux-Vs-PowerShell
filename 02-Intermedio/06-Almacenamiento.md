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

---

## Ver los discos del sistema

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `lsblk` | `Get-Disk` |
| **Ejemplo** | `lsblk -f` | `Get-Volume` |

> 💡 **Diferencia clave** — 🐧 `lsblk` muestra discos, particiones y puntos de montaje. · 🪟 `Get-Disk` muestra únicamente los discos físicos.

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

### Comandos relacionados

- [Consultar el espacio disponible](#consultar-el-espacio-disponible)
- [Consultar información de un volumen](#consultar-información-de-un-volumen)
- [Ver los discos del sistema](#ver-los-discos-del-sistema)

---

[⬆️ Volver al índice](#índice)