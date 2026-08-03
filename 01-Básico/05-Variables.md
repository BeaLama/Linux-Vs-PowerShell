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
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Crear una variable

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `nombre="usuario"` | `$nombre = "usuario"` |
| **Ejemplo** | `edad=25` | `$edad = 25` |

> 💡 **Diferencia clave** — 🐧 Las variables no llevan ningún prefijo al crearse. · 🪟 Todas las variables comienzan con `$`.

---

### Buenas prácticas

- Utiliza nombres descriptivos para facilitar la lectura del código.
- Evita caracteres especiales y espacios en el nombre de las variables.
- Sigue una convención de nombres consistente a lo largo de tus scripts.
- Utiliza nombres significativos que describan el contenido de la variable.

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

### Buenas prácticas

- Comprueba que la variable contiene un valor antes de utilizarla.
- Utiliza nombres descriptivos para facilitar la lectura del código.
- Si vas a mostrar varias variables, añade texto explicativo para mejorar la legibilidad de la salida.

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

### Buenas prácticas

- Utiliza nombres de variables descriptivos para facilitar la lectura del código.
- Modifica una variable únicamente cuando sea necesario para evitar confusiones.
- Comprueba el contenido de la variable después de modificarla si va a utilizarse en operaciones importantes.

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

### Buenas prácticas

- Elimina variables que ya no vayas a utilizar en scripts largos.
- Evita eliminar variables del sistema o de entorno si desconoces su función.
- Comprueba que la variable existe antes de eliminarla en procesos automatizados.

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

### Buenas prácticas

- No modifiques variables de entorno si desconoces su función.
- Consulta siempre el valor de una variable antes de utilizarla en un script.
- Evita sobrescribir variables importantes como `PATH`, ya que puede afectar al funcionamiento del sistema.

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

### Buenas prácticas

- Guarda en variables únicamente la información que vayas a reutilizar.
- Utiliza nombres descriptivos para identificar fácilmente el contenido de la variable.
- Comprueba el contenido de la variable antes de utilizarlo en operaciones importantes.

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

### Buenas prácticas

- Utiliza variables para evitar repetir información en un script.
- Emplea nombres descriptivos para facilitar el mantenimiento del código.
- Comprueba que la variable contiene un valor válido antes de utilizarla.
- Reutiliza las variables siempre que sea posible para hacer los scripts más claros y fáciles de modificar.

---

### Comandos relacionados

- [Guardar el resultado de un comando](#guardar-el-resultado-de-un-comando)
- [Mostrar el valor de una variable](#mostrar-el-valor-de-una-variable)
- [Variables de entorno](#variables-de-entorno)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Crear una variable | `variable="valor"` | `$variable = "valor"` |
| Mostrar el valor de una variable | `echo $variable` | `$variable` / `Write-Output $variable` |
| Modificar una variable | `variable="nuevo_valor"` | `$variable = "nuevo_valor"` |
| Eliminar una variable | `unset variable` | `Remove-Variable -Name variable` |
| Mostrar variables de entorno | `printenv` / `env` | `Get-ChildItem Env:` |
| Mostrar una variable de entorno | `echo $PATH` | `$env:PATH` |
| Guardar el resultado de un comando | `variable=$(comando)` | `$variable = comando` |
| Utilizar una variable en un comando | `<comando> $variable` | `<cmdlet> $variable` |

---

### Buenas prácticas generales

- Utiliza nombres descriptivos para facilitar la lectura y el mantenimiento de los scripts.
- Evita sobrescribir variables importantes si todavía van a utilizarse.
- Comprueba siempre el contenido de una variable antes de utilizarla en operaciones críticas.
- Reutiliza variables para evitar repetir información y simplificar el código.
- Utiliza variables de entorno cuando necesites acceder a información del sistema, como rutas o datos del usuario.
- Mantén una nomenclatura consistente a lo largo de todo el script.

---

[⬆️ Volver al índice](#índice)