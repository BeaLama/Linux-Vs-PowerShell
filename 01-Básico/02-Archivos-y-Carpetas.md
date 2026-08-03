# Archivos y carpetas

## Índice

- [Crear un archivo](#crear-un-archivo)
- [Copiar archivos](#copiar-archivos)
- [Mover archivos](#mover-archivos)
- [Renombrar archivos](#renombrar-archivos)
- [Eliminar archivos](#eliminar-archivos)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)
- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)
- [Ver el principio de un archivo](#ver-el-principio-de-un-archivo)
- [Ver el final de un archivo](#ver-el-final-de-un-archivo)
- [Crear varios archivos](#crear-varios-archivos)
- [Copiar directorios](#copiar-directorios)
- [Mover directorios](#mover-directorios)
- [Renombrar directorios](#renombrar-directorios)

## Crear un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `touch <nombre_archivo>` | `New-Item -Path <nombre_archivo> -ItemType File` |
| **Ejemplo** | `touch /home/usuario/notas.txt` | `New-Item -Path C:\Users\usuario\notas.txt -ItemType File` |

> 💡 **Diferencia clave** — 🐧 `touch` también actualiza la fecha de modificación si el archivo ya existe. · 🪟 `New-Item` devuelve un error si el archivo ya existe, salvo que se utilice el parámetro `-Force`.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Mover archivos](#mover-archivos)
- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Copiar archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cp <origen> <destino>` | `Copy-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `cp notas.txt /home/usuario/Documentos` | `Copy-Item -Path notas.txt -Destination C:\Users\usuario\Documents` |

> 💡 **Diferencia clave** — 🐧 Utiliza `cp` para copiar archivos y directorios. · 🪟 Utiliza el cmdlet `Copy-Item`.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Mover archivos](#mover-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Mover archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <origen> <destino>` | `Move-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `mv notas.txt informe.txt` | `Move-Item -Path notas.txt -Destination informe.txt` |

> 💡 **Diferencia clave** — 🐧 `mv` mueve y renombra archivos con el mismo comando. · 🪟 `Move-Item` también permite mover y renombrar archivos utilizando el parámetro `-Destination`.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Renombrar archivos](#renombrar-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Renombrar archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <nombre_actual> <nuevo_nombre>` | `Rename-Item -Path <nombre_actual> -NewName <nuevo_nombre>` |

**Ejemplo**
```bash
mv /home/usuario/Documentos/notas.txt /home/usuario/Documentos/informe.txt
```
```powershell
Rename-Item -Path C:\Users\usuario\Documents\notas.txt -NewName informe.txt
```

> 💡 **Diferencia clave** — 🐧 Se utiliza `mv`, ya que renombrar es equivalente a mover el archivo con otro nombre dentro del mismo directorio. · 🪟 Existe un cmdlet específico (`Rename-Item`) cuya única función es cambiar el nombre del archivo.

---

### Comandos relacionados

- [Mover archivos](#mover-archivos)
- [Copiar archivos](#copiar-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Eliminar archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `rm <archivo>` | `Remove-Item -Path <archivo>` |
| **Ejemplo** | `rm notas.txt informe.txt copia_notas.txt` | `Remove-Item notas.txt, informe.txt, copia_notas.txt` |

> 💡 **Diferencia clave** — 🐧 `rm` elimina archivos de forma permanente. · 🪟 `Remove-Item` elimina archivos y otros elementos del sistema de archivos.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Copiar archivos](#copiar-archivos)
- [Mover archivos](#mover-archivos)
- [Renombrar archivos](#renombrar-archivos)

---

[⬆️ Volver al índice](#índice)

## Eliminar directorios con contenido

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `rm -r <directorio>` | `Remove-Item -Path <directorio> -Recurse` |
| **Ejemplo** | `rm -rf Proyecto` | `Remove-Item -Path Proyecto -Recurse -Force` |

> 💡 **Diferencia clave** — 🐧 `-r` elimina el directorio y todo su contenido. · 🪟 `-Recurse` elimina el directorio y todos sus elementos.

---

### Comandos relacionados

- [Eliminar archivos](#eliminar-archivos)
- [Crear directorios](#crear-directorios)
- [Mover directorios](#mover-directorios)

---

[⬆️ Volver al índice](#índice)

## Ver el contenido de un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cat <archivo>` | `Get-Content -Path <archivo>` |
| **Ejemplo** | `cat /home/usuario/Documentos/notas.txt` | `Get-Content -Path C:\Users\usuario\Documents\notas.txt` |

> 💡 **Diferencia clave** — 🐧 `cat` muestra el contenido como texto plano. · 🪟 `Get-Content` devuelve cada línea como un objeto de tipo `String`.

---

### Comandos relacionados

- [Ver el principio de un archivo](#ver-el-principio-de-un-archivo)
- [Ver el final de un archivo](#ver-el-final-de-un-archivo)
- [Crear un archivo](#crear-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Ver el principio de un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `head <archivo>` | `Get-Content -Path <archivo> -TotalCount 10` |
| **Ejemplo** | `head -n 5 notas.txt` | `Get-Content -Path notas.txt -TotalCount 5` |

> 💡 **Diferencia clave** — 🐧 `head` muestra las primeras líneas de un archivo. · 🪟 `Get-Content` utiliza el parámetro `-TotalCount` para limitar el número de líneas mostradas.

---

### Comandos relacionados

- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)
- [Ver el final de un archivo](#ver-el-final-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Ver el final de un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `tail <archivo>` | `Get-Content -Path <archivo> -Tail 10` |
| **Ejemplo** | `tail -n 5 notas.txt` | `Get-Content -Path notas.txt -Tail 5` |

> 💡 **Diferencia clave** — 🐧 `tail` muestra las últimas líneas de un archivo. · 🪟 `Get-Content` utiliza el parámetro `-Tail` para mostrar las últimas líneas.

---

### Comandos relacionados

- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)
- [Ver el principio de un archivo](#ver-el-principio-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Crear varios archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `touch <archivo1> <archivo2> <archivo3>` | `New-Item -Path archivo1.txt, archivo2.txt, archivo3.txt -ItemType File` |

**Ejemplo**
```bash
touch /home/usuario/Documentos/notas.txt \
      /home/usuario/Documentos/informe.txt \
      /home/usuario/Documentos/copia_notas.txt
```
```powershell
New-Item -Path `
"C:\Users\usuario\Documents\notas.txt",
"C:\Users\usuario\Documents\informe.txt",
"C:\Users\usuario\Documents\copia_notas.txt" `
-ItemType File
```

> 💡 **Diferencia clave** — 🐧 `touch` permite crear múltiples archivos separando sus nombres por espacios. · 🪟 `New-Item` acepta varios archivos separados por comas.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Copiar archivos](#copiar-archivos)
- [Renombrar archivos](#renombrar-archivos)

---

[⬆️ Volver al índice](#índice)

## Copiar directorios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cp -r <origen> <destino>` | `Copy-Item -Path <origen> -Destination <destino> -Recurse` |
| **Ejemplo** | `cp -r Proyecto /home/usuario/Backups` | `Copy-Item -Path Proyecto -Destination C:\Backups -Recurse` |

> 💡 **Diferencia clave** — 🐧 Es necesario utilizar `-r` (o `-R`) para copiar directorios. · 🪟 Es necesario utilizar el parámetro `-Recurse` para copiar todo el contenido del directorio.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Mover directorios](#mover-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)

## Mover directorios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <origen> <destino>` | `Move-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `mv /home/usuario/Proyecto /home/usuario/Backups` | `Move-Item -Path C:\Users\usuario\Proyecto -Destination C:\Backups` |

> 💡 **Diferencia clave** — 🐧 `mv` mueve y renombra directorios con el mismo comando. · 🪟 `Move-Item` también permite mover y renombrar directorios utilizando `-Destination`.

---

### Comandos relacionados

- [Copiar directorios](#copiar-directorios)
- [Renombrar directorios](#renombrar-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)

## Renombrar directorios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <nombre_actual> <nuevo_nombre>` | `Rename-Item -Path <nombre_actual> -NewName <nuevo_nombre>` |
| **Ejemplo** | `mv /home/usuario/Proyecto /home/usuario/Proyecto_Backup` | `Rename-Item -Path C:\Users\usuario\Proyecto -NewName Proyecto_Backup` |

> 💡 **Diferencia clave** — 🐧 `mv` utiliza el mismo comando para mover y renombrar directorios. · 🪟 `Rename-Item` está diseñado específicamente para cambiar el nombre de un elemento.

---

### Comandos relacionados

- [Mover directorios](#mover-directorios)
- [Copiar directorios](#copiar-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)