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

### Buenas prácticas

- Comprueba siempre tu ubicación antes de ejecutar comandos que modifiquen o eliminen archivos.
- En scripts, utiliza rutas absolutas cuando sea posible para evitar errores de ejecución.

---

[⬆️ Volver al índice](#índice)

## Cambiar de directorio

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cd ..` | `Set-Location ..` |
| **Ejemplo** | `cd ../..` | `cd ../..` |

> 💡 **Diferencia clave** — 🐧 Utiliza `..` para representar el directorio padre. · 🪟 Utiliza la misma sintaxis (`..`).

### Buenas prácticas

- Utiliza rutas absolutas cuando escribas scripts para evitar errores.
- Comprueba que el directorio existe antes de cambiar a él.
- Aprovecha el autocompletado con la tecla **Tab** para escribir rutas más rápidamente.

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

### Buenas prácticas

- Comprueba tu ubicación con `pwd` o `Get-Location` si no estás seguro del directorio actual.
- Cuando necesites retroceder varios niveles, puedes encadenar `../..` en lugar de ejecutar varios comandos `cd ..`.

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

### Buenas prácticas

- Utiliza `~` cuando quieras escribir comandos independientes del nombre del usuario.
- En scripts, emplea `$HOME` cuando necesites construir rutas dentro del perfil del usuario.

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

### Buenas prácticas

- Utiliza rutas explícitas cuando necesites consultar un directorio diferente al actual.
- Si necesitas información adicional (permisos, tamaño o fechas), utiliza los comandos específicos del siguiente apartado.

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

### Buenas prácticas

- Utiliza este comando cuando necesites consultar rápidamente el tamaño o la fecha de modificación de archivos.
- Si necesitas trabajar con los datos posteriormente en PowerShell, evita usar `Format-Table` hasta el final de la tubería.

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

### Buenas prácticas

- Revisa siempre el contenido oculto antes de eliminar archivos o directorios.
- Ten especial cuidado al modificar archivos ocultos o del sistema, ya que muchos son necesarios para el correcto funcionamiento del sistema operativo.

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

### Buenas prácticas

- Utiliza nombres descriptivos para los directorios.
- Comprueba que el directorio no exista previamente para evitar errores.
- En scripts, utiliza rutas absolutas cuando sea posible.

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

### Buenas prácticas

- Utiliza rutas absolutas en scripts para evitar errores debidos al directorio de trabajo actual.
- Comprueba que la ruta exista antes de acceder a ella.
- Emplea el autocompletado con la tecla **Tab** para reducir errores al escribir rutas.

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

### Buenas prácticas

- Utiliza rutas relativas cuando trabajes dentro de una misma estructura de directorios.
- En scripts, prioriza las rutas absolutas si el directorio de ejecución puede variar.
- Comprueba el directorio actual antes de utilizar rutas relativas complejas.

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

### Buenas prácticas

- Revisa el historial para repetir comandos complejos sin necesidad de escribirlos de nuevo.
- Evita introducir contraseñas o información sensible directamente en la línea de comandos.
- Borra el historial cuando trabajes con información confidencial.

---

### Comandos relacionados

- [Mostrar el directorio actual](#mostrar-el-directorio-actual)
- [Cambiar de directorio](#cambiar-de-directorio)
- [Utilizar rutas relativas](#navegar-utilizando-rutas-relativas)

---

[⬆️ Volver al índice](#índice)