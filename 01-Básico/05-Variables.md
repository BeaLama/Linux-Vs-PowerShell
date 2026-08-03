# Variables

## Introducción

Las variables permiten almacenar información temporal para reutilizarla posteriormente dentro de la terminal o de un script.

Pueden contener texto, números, rutas, resultados de comandos e incluso objetos completos, dependiendo del sistema utilizado.

Aunque Linux y PowerShell utilizan una sintaxis diferente, ambos comparten el mismo objetivo: guardar información para facilitar la automatización y evitar repetir datos.

---

## Índice

- [Crear una variable](#crear-una-variable)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Modificar una variable](#modificar-una-variable)
- [Eliminar una variable](#eliminar-una-variable)
- [Variables de entorno](#variables-de-entorno)
- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)
- [Utilizar variables en comandos](#utilizar-variables-en-comandos)

---

## Crear una variable

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `nombre="usuario"` | `$nombre = "usuario"` |
| **Ejemplo** | `edad=25` | `$edad = 25` |

> 💡 **Diferencia clave** — 🐧 Las variables no llevan ningún prefijo al crearse. · 🪟 Todas las variables comienzan con `$`.

---

### Comandos relacionados

- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Modificar una variable](#modificar-una-variable)
- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)

---

[⬆️ Volver al índice](#índice)

## Mostrar el valor de una variable

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `echo $nombre` | `$nombre` |

**Ejemplo**
```bash
ip="192.168.1.10"

echo $ip
```
```powershell
$ip = "192.168.1.10"

$ip
```

> 💡 **Diferencia clave** — 🐧 Es necesario utilizar `echo` para mostrar el contenido de una variable. · 🪟 Basta con escribir el nombre de la variable para mostrar su contenido.

---

### Comandos relacionados

- [Crear una variable](#crear-una-variable)
- [Modificar una variable](#modificar-una-variable)
- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)

---

[⬆️ Volver al índice](#índice)

## Modificar una variable

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `nombre="Nuevo valor"` | `$nombre = "Nuevo valor"` |

**Ejemplo**
```bash
ip="192.168.1.10"

ip="192.168.1.20"
```
```powershell
$ip = "192.168.1.10"

$ip = "192.168.1.20"
```

> 💡 **Diferencia clave** — 🐧 La variable se modifica realizando una nueva asignación. · 🪟 La variable también se modifica realizando una nueva asignación.

---

### Comandos relacionados

- [Crear una variable](#crear-una-variable)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Eliminar una variable](#eliminar-una-variable)

---

[⬆️ Volver al índice](#índice)

## Eliminar una variable

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `unset <variable>` | `Remove-Variable -Name <variable>` |

**Ejemplo**
```bash
ip="192.168.1.10"

unset ip
```
```powershell
$ip = "192.168.1.10"

Remove-Variable -Name ip
```

> 💡 **Diferencia clave** — 🐧 `unset` elimina completamente la variable. · 🪟 `Remove-Variable` elimina completamente la variable.

---

### Comandos relacionados

- [Crear una variable](#crear-una-variable)
- [Modificar una variable](#modificar-una-variable)
- [Variables de entorno](#variables-de-entorno)

---

[⬆️ Volver al índice](#índice)

## Variables de entorno

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `printenv` | `Get-ChildItem Env:` |
| **Ejemplo** | `echo $HOME` | `$env:USERPROFILE` |

> 💡 **Diferencia clave** — 🐧 Las variables de entorno se acceden mediante `$NOMBRE_VARIABLE`. · 🪟 Se accede a ellas mediante `$env:NOMBRE_VARIABLE`.

---

### Comandos relacionados

- [Crear una variable](#crear-una-variable)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)

---

[⬆️ Volver al índice](#índice)

## Guardar el resultado de un comando

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `variable=$(comando)` | `$variable = comando` |
| **Ejemplo** | `fecha=$(date)` | `$fecha = Get-Date` |

> 💡 **Diferencia clave** — 🐧 Utiliza la sustitución de comandos mediante `$( )`. · 🪟 Basta con asignar directamente el resultado del comando a la variable.

---

### Comandos relacionados

- [Crear una variable](#crear-una-variable)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Utilizar variables en comandos](#utilizar-variables-en-comandos)

---

[⬆️ Volver al índice](#índice)

## Utilizar variables en comandos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `<comando> $variable` | `<comando> $variable` |

**Ejemplo**
```bash
archivo="informe.pdf"

cp $archivo /home/usuario/Backups
```
```powershell
$archivo = "informe.pdf"

Copy-Item $archivo C:\Backups
```

> 💡 **Diferencia clave** — 🐧 La variable se expande automáticamente antes de ejecutar el comando. · 🪟 La variable también se expande automáticamente antes de ejecutar el cmdlet.

---

### Comandos relacionados

- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Variables de entorno](#variables-de-entorno)

---

[⬆️ Volver al índice](#índice)