# Navegación

## Introducción

La navegación por el sistema de archivos es una de las tareas más habituales en cualquier sistema operativo.

Aunque Linux y PowerShell utilizan comandos diferentes, ambos permiten realizar prácticamente las mismas operaciones.

---

## Índice

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Volver al directorio anterior](#volver-al-directorio-anterior)
- [Ir al directorio personal](#ir-al-directorio-personal)
- [Listar archivos](#listar-archivos)
- [Listar información detallada](#listar-información-detallada)
- [Mostrar archivos ocultos](#mostrar-archivos-ocultos)
- [Crear directorios](#crear-directorios)
- [Eliminar directorios vacíos](#eliminar-directorios-vacíos)
- [Utilizar rutas absolutas](#utilizar-rutas-absolutas)
- [Utilizar rutas relativas](#utilizar-rutas-relativas)
- [Historial de comandos](#historial-de-comandos)

---

## Mostrar el directorio actual

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `pwd` | `Get-Location` |

> 💡 **Diferencia clave** — 🐧 Devuelve una ruta en formato texto. · 🪟 Devuelve un objeto cuya propiedad principal es `Path`.

---

[⬆️ Volver al índice](#índice)

## Cambiar de directorio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd ..` | `Set-Location ..` |
| **Ejemplo** | `cd ../..` | `cd ../..` |

> 💡 **Diferencia clave** — 🐧 Utiliza `..` para representar el directorio padre. · 🪟 Utiliza la misma sintaxis (`..`).

---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Ir al directorio personal](#ir-al-directorio-personal)
- [Listar el contenido de un directorio](#listar-archivos)

---

[⬆️ Volver al índice](#índice)

## Volver al directorio anterior

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd ..` | `Set-Location ..` |
| **Ejemplo** | `cd ../..` | `cd ../..` |

> 💡 **Diferencia clave** — 🐧 Utiliza `..` para representar el directorio padre. · 🪟 Utiliza la misma sintaxis (`..`).

---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Ir al directorio personal](#ir-al-directorio-personal)

---

[⬆️ Volver al índice](#índice)

## Ir al directorio personal

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd ~` | `Set-Location ~` |
| **Ejemplo** | `cd $HOME` | `cd $HOME` |

> 💡 **Diferencia clave** — 🐧 `~` y `$HOME` apuntan al directorio personal del usuario. · 🪟 También admite `~` y la variable `$HOME`, que resuelve la ruta del perfil del usuario.

---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Volver al directorio anterior](#volver-al-directorio-anterior)
---

[⬆️ Volver al índice](#índice)

## Listar archivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ls` | `Get-ChildItem` |
| **Ejemplo** | `ls /etc` | `Get-ChildItem C:\Windows` |

> 💡 **Diferencia clave** — 🐧 Devuelve una lista en formato texto. · 🪟 Devuelve objetos que representan archivos y carpetas.
---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Listar información detallada](#listar-información-detallada)
- [Mostrar archivos ocultos](#mostrar-archivos-ocultos)

---

[⬆️ Volver al índice](#índice)

## Listar información detallada

**Sintaxis**
```bash
ls -l
```
```powershell
Get-ChildItem | Format-Table Mode, LastWriteTime, Length, Name
```

> 💡 **Diferencia clave** — 🐧 `ls -l` muestra una lista detallada en formato texto. · 🪟 `Get-ChildItem` devuelve objetos y `Format-Table` controla únicamente la forma en la que se presentan.


### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar información detallada | `ls -l` | `Get-ChildItem \| Format-Table Mode, LastWriteTime, Length, Name` |

---

### Comandos relacionados

- [Listar el contenido de un directorio](#listar-archivos)
- [Mostrar archivos ocultos](#mostrar-archivos-ocultos)
- [Crear un directorio](#crear-un-directorio)

---

[⬆️ Volver al índice](#índice)

## Mostrar archivos ocultos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ls -la` | `Get-ChildItem -Force` |
| **Ejemplo** | `ls -la /etc` | `Get-ChildItem C:\Windows -Force` |

> 💡 **Diferencia clave** — 🐧 Los archivos ocultos comienzan por un punto (`.`). · 🪟 Los archivos ocultos utilizan atributos del sistema (`Hidden`, `System`, etc.).

---

### Comandos relacionados

- [Listar el contenido de un directorio](#listar-archivos)
- [Listar información detallada](#listar-información-detallada)
- [Crear un directorio](#crear-un-directorio)

---

[⬆️ Volver al índice](#índice)

## Crear un directorio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mkdir <nombre_directorio>` | `New-Item -Path <nombre_directorio> -ItemType Directory` |

**Ejemplo**
```bash
mkdir Docs Scripts Backups
```
```powershell
New-Item Docs -ItemType Directory
New-Item Scripts -ItemType Directory
New-Item Backups -ItemType Directory
```

> 💡 **Diferencia clave** — 🐧 `mkdir` es el comando principal para crear directorios. · 🪟 El cmdlet oficial es `New-Item`, aunque `mkdir` es un alias.

---

### Comandos relacionados

- [Cambiar de directorio](#cambiar-de-directorio)
- [Listar el contenido de un directorio](#listar-archivos)
- [Eliminar un directorio vacío](#eliminar-un-directorio-vacío)

---

[⬆️ Volver al índice](#índice)

## Utilizar rutas absolutas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd /ruta/completa` | `Set-Location C:\ruta\completa` |
| **Ejemplo** | `cd /home/usuario/Documentos` | `Set-Location C:\Users\usuario\Documents` |

> 💡 **Diferencia clave** — 🐧 La ruta comienza siempre por `/`. · 🪟 La ruta comienza por la unidad correspondiente (`C:\`, `D:\`, etc.).

---

### Comandos relacionados

- [Cambiar de directorio](#cambiar-de-directorio)
- [Navegar utilizando rutas relativas](#utilizar-rutas-relativas)
- [Mostrar el directorio actual](#mostrar-el-directorio-actual)

---

[⬆️ Volver al índice](#índice)

## Utilizar rutas relativas

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd <ruta_relativa>` | `Set-Location <ruta_relativa>` |
| **Ejemplo** | `cd ..` | `Set-Location ..` |

> 💡 **Diferencia clave** — 🐧 Utiliza `/` como separador de directorios. · 🪟 Utiliza `\` como separador de directorios (aunque PowerShell también acepta `/` en la mayoría de los casos).

---

### Comandos relacionados

- [Cambiar de directorio](#cambiar-de-directorio)
- [Volver al directorio anterior](#volver-al-directorio-anterior)
- [Navegar utilizando rutas absolutas](#utilizar-rutas-absolutas)

---

[⬆️ Volver al índice](#índice)

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `history` | `Get-History` |

**Ejemplo**
```bash
history | tail -10
```
```powershell
Get-History -Count 10
```

> 💡 **Diferencia clave** — 🐧 El historial se almacena en un archivo (normalmente `~/.bash_history`). · 🪟 `Get-History` muestra únicamente el historial de la sesión actual.

---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Utilizar rutas relativas](#navegar-utilizando-rutas-relativas)

---

[⬆️ Volver al índice](#índice)