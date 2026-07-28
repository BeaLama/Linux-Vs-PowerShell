# Almacenamiento

## Introducción

El almacenamiento es uno de los componentes fundamentales de cualquier sistema. Una correcta administración de discos, particiones y sistemas de archivos permite garantizar el rendimiento, la disponibilidad de los datos y el correcto funcionamiento del equipo.

En este capítulo aprenderás a consultar la información de los discos, administrar particiones, montar sistemas de archivos, comprobar el espacio disponible y realizar tareas básicas de mantenimiento tanto en Linux como en PowerShell.

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

### Linux

```bash
lsblk
```

También puede utilizarse:

```bash
lsblk -f
```

**Descripción**

Permite mostrar todos los dispositivos de almacenamiento conectados al sistema.

La información incluye:

- Nombre del disco.
- Particiones.
- Tamaño.
- Tipo de dispositivo.
- Punto de montaje.
- Sistema de archivos (con `-f`).

---

### PowerShell

```powershell
Get-Disk
```

También puede utilizarse:

```powershell
Get-PhysicalDisk
```

**Descripción**

Permite consultar los discos físicos conectados al equipo.

La información mostrada puede incluir:

- Número de disco.
- Estado.
- Tamaño.
- Tipo de bus (SATA, NVMe, USB, etc.).
- Estilo de partición (GPT o MBR).

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver los discos del sistema | `lsblk` | `Get-Disk` |
| Ver información física del disco | `lsblk -f` | `Get-PhysicalDisk` |

---

### Ejemplos

**Mostrar todos los discos y particiones**

Linux

```bash
lsblk
```

PowerShell

```powershell
Get-Disk
```

---

**Mostrar discos con el sistema de archivos**

Linux

```bash
lsblk -f
```

PowerShell

```powershell
Get-Volume
```

---

**Mostrar únicamente los discos físicos**

Linux

```bash
lsblk -d
```

PowerShell

```powershell
Get-PhysicalDisk
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `lsblk` muestra discos, particiones y puntos de montaje. | `Get-Disk` muestra únicamente los discos físicos. |
| `lsblk -f` añade información del sistema de archivos. | Para consultar los volúmenes debe utilizarse `Get-Volume`. |
| La salida es texto estructurado en forma de árbol. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

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

> **⚠️ Advertencia:** Antes de crear, eliminar o formatear particiones, asegúrate de identificar correctamente el disco. Un error al seleccionar el dispositivo puede provocar la pérdida permanente de datos.

---

[⬆️ Volver al índice](#índice)

## Consultar el espacio disponible

### Linux

```bash
df -h
```

También puede utilizarse:

```bash
df -Th
```

**Descripción**

Permite mostrar el espacio utilizado y disponible de los sistemas de archivos montados.

La información incluye:

- Sistema de archivos.
- Tamaño total.
- Espacio utilizado.
- Espacio libre.
- Porcentaje de uso.
- Punto de montaje.
- Tipo de sistema de archivos (con `-T`).

La opción `-h` muestra los tamaños en un formato legible (MB, GB, TB).

---

### PowerShell

```powershell
Get-Volume
```

También puede utilizarse:

```powershell
Get-PSDrive -PSProvider FileSystem
```

**Descripción**

Permite consultar el espacio disponible de los volúmenes del equipo.

La información puede incluir:

- Letra de unidad.
- Etiqueta del volumen.
- Sistema de archivos.
- Espacio libre.
- Tamaño total.
- Estado del volumen.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar el espacio disponible | `df -h` | `Get-Volume` |
| Ver espacio de las unidades | `df -Th` | `Get-PSDrive -PSProvider FileSystem` |

---

### Ejemplos

**Mostrar el espacio disponible de todos los sistemas de archivos**

Linux

```bash
df -h
```

PowerShell

```powershell
Get-Volume
```

---

**Mostrar también el tipo de sistema de archivos**

Linux

```bash
df -Th
```

PowerShell

```powershell
Get-Volume |
Select-Object DriveLetter,
              FileSystemType,
              Size,
              SizeRemaining
```

---

**Consultar una ubicación concreta**

Linux

```bash
df -h /home
```

PowerShell

```powershell
Get-Volume -DriveLetter C
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `df` muestra el uso de los sistemas de archivos montados. | `Get-Volume` muestra información de los volúmenes de Windows. |
| Puede consultarse una ruta específica. | Puede filtrarse por letra de unidad. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

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

> **💡 Consejo:** Si una unidad tiene muy poco espacio libre, utiliza herramientas como `du` (Linux) o revisa las carpetas de mayor tamaño en Windows para localizar rápidamente qué está ocupando el almacenamiento.

---

[⬆️ Volver al índice](#índice)

## Listar particiones

### Linux

```bash
sudo fdisk -l
```

También puede utilizarse:

```bash
parted -l
```

**Descripción**

Permite mostrar todas las particiones detectadas en el sistema junto con información detallada de los discos.

La información incluye:

- Disco.
- Tamaño.
- Tipo de tabla de particiones (MBR o GPT).
- Particiones existentes.
- Tamaño de cada partición.
- Tipo de partición.

---

### PowerShell

```powershell
Get-Partition
```

**Descripción**

Muestra todas las particiones existentes en los discos del equipo.

La información incluye:

- Número de disco.
- Número de partición.
- Letra de unidad.
- Tamaño.
- Tipo de partición.
- Estado.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar particiones | `fdisk -l` / `parted -l` | `Get-Partition` |

---

### Ejemplos

**Mostrar todas las particiones del sistema**

Linux

```bash
sudo fdisk -l
```

PowerShell

```powershell
Get-Partition
```

---

**Mostrar las particiones de un disco concreto**

Linux

```bash
sudo fdisk -l /dev/sda
```

PowerShell

```powershell
Get-Partition -DiskNumber 0
```

---

**Mostrar únicamente el número y el tamaño de las particiones**

Linux

```bash
lsblk
```

PowerShell

```powershell
Get-Partition |
Select-Object DiskNumber,
              PartitionNumber,
              DriveLetter,
              Size
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `fdisk -l` muestra información de discos y particiones. | `Get-Partition` muestra únicamente las particiones. |
| `parted -l` también identifica el tipo de tabla de particiones (GPT o MBR). | El estilo de partición puede consultarse mediante `Get-Disk`. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

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

> **⚠️ Advertencia:** Los comandos utilizados para listar particiones son seguros, pero los programas `fdisk` y `parted` también permiten modificarlas. Antes de realizar cualquier cambio, asegúrate de haber seleccionado el disco correcto y de disponer de una copia de seguridad.

---

[⬆️ Volver al índice](#índice)

## Consultar información de un volumen

### Linux

```bash
lsblk -f
```

También puede utilizarse:

```bash
blkid
```

**Descripción**

Permite consultar información detallada de los sistemas de archivos y volúmenes existentes.

La información puede incluir:

- Nombre del dispositivo.
- Sistema de archivos.
- Etiqueta (Label).
- UUID.
- Punto de montaje.

`blkid` resulta especialmente útil para obtener el UUID de una partición, utilizado habitualmente en el archivo `/etc/fstab`.

---

### PowerShell

```powershell
Get-Volume
```

**Descripción**

Muestra información detallada sobre los volúmenes del sistema.

La información incluye:

- Letra de unidad.
- Etiqueta del volumen.
- Sistema de archivos.
- Estado.
- Tamaño total.
- Espacio libre.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar información de un volumen | `lsblk -f` / `blkid` | `Get-Volume` |

---

### Ejemplos

**Mostrar todos los volúmenes**

Linux

```bash
lsblk -f
```

PowerShell

```powershell
Get-Volume
```

---

**Mostrar el UUID de las particiones**

Linux

```bash
blkid
```

PowerShell

```powershell
Get-Volume |
Select-Object DriveLetter,
              FileSystemLabel,
              FileSystem,
              HealthStatus
```

---

**Consultar un volumen concreto**

Linux

```bash
lsblk -f /dev/sda1
```

PowerShell

```powershell
Get-Volume -DriveLetter C
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `lsblk -f` muestra sistemas de archivos, UUID y puntos de montaje. | `Get-Volume` muestra información del volumen administrado por Windows. |
| `blkid` está orientado a identificar dispositivos mediante UUID y etiquetas. | Windows identifica principalmente los volúmenes mediante letras de unidad y GUID internos. |
| La salida es texto estructurado. | La salida son objetos que pueden filtrarse y procesarse mediante la tubería. |

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

> **💡 Consejo:** En Linux es recomendable utilizar el **UUID** para montar sistemas de archivos de forma permanente en `/etc/fstab`, ya que nombres como `/dev/sda1` pueden cambiar al añadir o retirar discos del equipo.

---

[⬆️ Volver al índice](#índice)

## Montar y desmontar sistemas de archivos

### Linux

```bash
sudo mount <dispositivo> <punto_de_montaje>
```

Para desmontar:

```bash
sudo umount <dispositivo>
```

o

```bash
sudo umount <punto_de_montaje>
```

**Descripción**

Permite montar o desmontar sistemas de archivos para acceder a su contenido.

- `mount` asocia un dispositivo a un directorio del sistema.
- `umount` elimina esa asociación sin borrar los datos.

> **Importante:** Antes de desmontar un sistema de archivos, asegúrate de que ningún proceso lo está utilizando.

---

### PowerShell

```powershell
Mount-DiskImage -ImagePath "<ruta>"
```

Para desmontar:

```powershell
Dismount-DiskImage -ImagePath "<ruta>"
```

**Descripción**

Permite montar y desmontar imágenes de disco (ISO, VHD o VHDX).

Una vez montada, Windows asignará automáticamente una letra de unidad para acceder a su contenido.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Montar un sistema de archivos | `mount` | `Mount-DiskImage` |
| Desmontar un sistema de archivos | `umount` | `Dismount-DiskImage` |

---

### Ejemplos

**Montar una partición**

Linux

```bash
sudo mount /dev/sdb1 /mnt
```

PowerShell

```powershell
Mount-DiskImage `
-ImagePath "C:\ISO\Windows.iso"
```

---

**Desmontar una partición o imagen**

Linux

```bash
sudo umount /mnt
```

PowerShell

```powershell
Dismount-DiskImage `
-ImagePath "C:\ISO\Windows.iso"
```

---

**Ver los sistemas de archivos montados**

Linux

```bash
mount
```

o

```bash
findmnt
```

PowerShell

```powershell
Get-Volume
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Cualquier sistema de archivos debe montarse en un directorio antes de utilizarse. | Las unidades físicas suelen montarse automáticamente; `Mount-DiskImage` se utiliza principalmente para imágenes ISO y VHD/VHDX. |
| El punto de montaje puede ser cualquier directorio del sistema. | Windows asigna normalmente una letra de unidad automáticamente. |
| `umount` desmonta el sistema de archivos sin eliminar los datos. | `Dismount-DiskImage` únicamente desmonta la imagen virtual. |

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

> **⚠️ Advertencia:** Desmontar un sistema de archivos mientras existen archivos abiertos o procesos utilizándolo puede provocar pérdida de datos o corrupción del sistema de archivos. En Linux puedes comprobar qué procesos lo están utilizando mediante `lsof` o `fuser`.

---

[⬆️ Volver al índice](#índice)

## Crear una partición

### Linux

```bash
sudo fdisk <disco>
```

También puede utilizarse:

```bash
sudo parted <disco>
```

**Descripción**

Permite crear, modificar o eliminar particiones en un disco.

- `fdisk` está orientado a discos con tabla de particiones **MBR** y **GPT**.
- `parted` ofrece una interfaz más flexible y permite trabajar fácilmente con discos de gran tamaño y particiones GPT.

> **Importante:** Crear una partición modifica la estructura del disco. Antes de realizar cualquier cambio, asegúrate de disponer de una copia de seguridad.

---

### PowerShell

```powershell
New-Partition
```

**Descripción**

Permite crear una nueva partición en un disco.

Puede especificarse:

- Disco.
- Tamaño.
- Letra de unidad.
- Uso del espacio restante del disco.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear una partición | `fdisk` / `parted` | `New-Partition` |

---

### Ejemplos

**Crear una partición utilizando `fdisk`**

Linux

```bash
sudo fdisk /dev/sdb
```

Una vez dentro del programa:

```text
n    -> Nueva partición
p    -> Partición primaria (si procede)
Enter
Enter
w    -> Guardar cambios
```

---

**Crear una partición utilizando todo el espacio libre**

PowerShell

```powershell
New-Partition `
-DiskNumber 1 `
-UseMaximumSize `
-DriveLetter D
```

---

**Crear una partición de 50 GB**

Linux

```bash
sudo parted /dev/sdb
```

Dentro de `parted`:

```text
mkpart primary ext4 1MiB 50GiB
quit
```

PowerShell

```powershell
New-Partition `
-DiskNumber 1 `
-Size 50GB `
-DriveLetter D
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `fdisk` y `parted` son herramientas interactivas. | `New-Partition` crea la partición directamente mediante parámetros. |
| La partición normalmente deberá formatearse posteriormente con `mkfs`. | La partición suele formatearse posteriormente con `Format-Volume`. |
| Es necesario indicar el dispositivo (`/dev/sdX`, `/dev/nvme...`). | Se trabaja mediante el número de disco (`DiskNumber`). |

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

> **⚠️ Advertencia:** Crear una partición puede provocar la pérdida de información si se realiza sobre un disco con datos existentes. Comprueba siempre el dispositivo seleccionado (`/dev/sdb`, `/dev/nvme0n1`, etc. o `DiskNumber`) antes de guardar los cambios.

---

[⬆️ Volver al índice](#índice)

## Formatear una partición

### Linux

```bash
sudo mkfs.ext4 <partición>
```

También puede utilizarse:

```bash
sudo mkfs.xfs <partición>
```

o

```bash
sudo mkfs.ntfs <partición>
```

(según el sistema de archivos deseado)

**Descripción**

Permite crear un sistema de archivos sobre una partición para que pueda almacenar información.

Algunos de los sistemas de archivos más utilizados son:

- **ext4** → Sistema de archivos estándar en la mayoría de distribuciones Linux.
- **XFS** → Muy utilizado en servidores y almacenamiento de gran capacidad.
- **NTFS** → Compatible con Windows.

> **Importante:** Formatear una partición elimina toda la información almacenada en ella.

---

### PowerShell

```powershell
Format-Volume
```

**Descripción**

Permite formatear un volumen utilizando el sistema de archivos deseado.

Los sistemas de archivos más habituales son:

- NTFS
- FAT32
- exFAT
- ReFS

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Formatear una partición | `mkfs` | `Format-Volume` |

---

### Ejemplos

**Formatear una partición en ext4**

Linux

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

**Formatear una partición en XFS**

Linux

```bash
sudo mkfs.xfs /dev/sdb1
```

---

**Formatear un volumen en NTFS**

PowerShell

```powershell
Format-Volume `
-DriveLetter D `
-FileSystem NTFS
```

---

**Asignar una etiqueta durante el formateo**

Linux

```bash
sudo mkfs.ext4 `
-L Datos `
/dev/sdb1
```

PowerShell

```powershell
Format-Volume `
-DriveLetter D `
-FileSystem NTFS `
-NewFileSystemLabel "Datos"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| El sistema de archivos se especifica mediante el comando (`mkfs.ext4`, `mkfs.xfs`, etc.). | El sistema de archivos se indica mediante el parámetro `-FileSystem`. |
| Existen múltiples utilidades `mkfs` dependiendo del sistema de archivos. | Un único cmdlet permite formatear distintos sistemas de archivos. |
| El dispositivo debe identificarse mediante su partición (`/dev/sdb1`). | Se trabaja normalmente mediante la letra de unidad o el volumen. |

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

> **⚠️ Advertencia:** El formateo elimina todos los datos de la partición. Antes de ejecutar `mkfs` o `Format-Volume`, verifica cuidadosamente que has seleccionado el dispositivo o volumen correcto.

---

[⬆️ Volver al índice](#índice)

## Cambiar la etiqueta de un volumen

### Linux

```bash
sudo e2label <partición> <etiqueta>
```

También puede utilizarse:

```bash
sudo xfs_admin -L <etiqueta> <partición>
```

(según el sistema de archivos)

**Descripción**

Permite modificar la etiqueta (Label) de un sistema de archivos.

La etiqueta facilita la identificación de discos y particiones, especialmente cuando existen varios dispositivos conectados.

> **Importante:** La herramienta utilizada depende del sistema de archivos:
>
> - **ext2/ext3/ext4** → `e2label`
> - **XFS** → `xfs_admin`
> - **NTFS** → `ntfslabel`

---

### PowerShell

```powershell
Set-Volume
```

**Descripción**

Permite modificar la etiqueta de un volumen existente.

Cambiar la etiqueta no afecta a los datos almacenados en el volumen.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Cambiar la etiqueta de un volumen | `e2label` / `xfs_admin` | `Set-Volume` |

---

### Ejemplos

**Cambiar la etiqueta de una partición ext4**

Linux

```bash
sudo e2label /dev/sdb1 Datos
```

PowerShell

```powershell
Set-Volume `
-DriveLetter D `
-NewFileSystemLabel "Datos"
```

---

**Cambiar la etiqueta de un volumen XFS**

Linux

```bash
sudo xfs_admin `
-L Datos `
/dev/sdb1
```

PowerShell

```powershell
Set-Volume `
-DriveLetter D `
-NewFileSystemLabel "Datos"
```

---

**Comprobar la nueva etiqueta**

Linux

```bash
lsblk -f
```

PowerShell

```powershell
Get-Volume
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La utilidad depende del sistema de archivos utilizado. | `Set-Volume` funciona con los sistemas de archivos compatibles con Windows. |
| La partición se identifica mediante su dispositivo (`/dev/sdb1`). | El volumen suele identificarse mediante la letra de unidad. |
| El cambio es inmediato y no modifica el contenido del volumen. | El cambio también es inmediato y no afecta a los datos almacenados. |

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

> **💡 Consejo:** Utilizar etiquetas descriptivas como `Sistema`, `Datos`, `Backups` o `Multimedia` facilita enormemente la identificación de los volúmenes, especialmente en servidores con varios discos o particiones.

---

[⬆️ Volver al índice](#índice)

## Comprobar el uso del disco por directorios

### Linux

```bash
du -sh <directorio>
```

También puede utilizarse:

```bash
du -h --max-depth=1 <directorio>
```

**Descripción**

Permite conocer cuánto espacio ocupa un directorio y su contenido.

Es una herramienta muy útil para localizar rápidamente qué carpetas están consumiendo más espacio en disco.

La información puede incluir:

- Tamaño total del directorio.
- Tamaño de cada subdirectorio.
- Tamaño en formato legible (KB, MB, GB, TB).

---

### PowerShell

```powershell
Get-ChildItem
```

Combinado con:

```powershell
Measure-Object
```

**Descripción**

Permite calcular el tamaño de los archivos contenidos en un directorio.

Aunque PowerShell no dispone de un cmdlet equivalente directo a `du`, la combinación de `Get-ChildItem` y `Measure-Object` permite obtener información similar.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar el tamaño de un directorio | `du -sh` | `Get-ChildItem` + `Measure-Object` |

---

### Ejemplos

**Mostrar el tamaño total de un directorio**

Linux

```bash
du -sh /home
```

PowerShell

```powershell
(Get-ChildItem C:\Users `
-Recurse -File |
Measure-Object Length -Sum).Sum / 1GB
```

---

**Mostrar el tamaño de cada subdirectorio**

Linux

```bash
du -h --max-depth=1 /home
```

PowerShell

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

---

**Ordenar los directorios por tamaño**

Linux

```bash
du -h --max-depth=1 /home |
sort -hr
```

PowerShell

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
        TamañoGB   = $size / 1GB
    }

} |
Sort-Object TamañoGB -Descending
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `du` calcula directamente el tamaño de los directorios. | Es necesario combinar varios cmdlets para obtener un resultado similar. |
| Puede limitar fácilmente la profundidad mediante `--max-depth`. | Normalmente se utiliza `Get-ChildItem` junto con `Measure-Object`. |
| La salida es texto estructurado. | La salida son objetos que pueden ordenarse, filtrarse y exportarse fácilmente. |

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

> **💡 Consejo:** Cuando un disco aparece casi lleno con `df` o `Get-Volume`, el siguiente paso suele ser utilizar `du` (Linux) o un cálculo del tamaño de carpetas en PowerShell para localizar qué directorios están ocupando más espacio.

---

[⬆️ Volver al índice](#índice)

