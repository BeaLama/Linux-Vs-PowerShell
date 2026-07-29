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

### Linux

```bash
nombre="usuario"
```

**Descripción**

Crea una variable y le asigna un valor. En Linux no debe haber espacios antes ni después del signo `=`.

---

### PowerShell

```powershell
$nombre = "usuario"
```

**Descripción**

Crea una variable y le asigna un valor. En PowerShell todas las variables comienzan con el símbolo `$`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear una variable | `nombre="valor"` | `$nombre = "valor"` |

---

### Ejemplos

**Crear una variable de texto**

Linux

```bash
usuario="usuario"
```

PowerShell

```powershell
$usuario = "usuario"
```

---

**Crear una variable numérica**

Linux

```bash
edad=25
```

PowerShell

```powershell
$edad = 25
```

---

**Crear una variable con una ruta**

Linux

```bash
ruta="/home/usuario/Documentos"
```

PowerShell

```powershell
$ruta = "C:\Users\usuario\Documents"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Las variables no llevan ningún prefijo al crearse. | Todas las variables comienzan con `$`. |
| No puede haber espacios alrededor del signo `=`. | Los espacios alrededor de `=` son opcionales, aunque se recomienda utilizarlos para mejorar la legibilidad. |
| Bash trata inicialmente el contenido como texto. | PowerShell asigna automáticamente el tipo de dato más adecuado (texto, número, fecha, objeto, etc.). |

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

### Linux

```bash
echo $nombre
```

**Descripción**

Muestra el contenido almacenado en una variable.

---

### PowerShell

```powershell
$nombre
```

También puede utilizarse:

```powershell
Write-Output $nombre
```

**Descripción**

Muestra el valor almacenado en una variable.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar el valor de una variable | `echo $variable` | `$variable` / `Write-Output $variable` |

---

### Ejemplos

**Mostrar el nombre de un usuario**

Linux

```bash
usuario="Administrador"

echo $usuario
```

PowerShell

```powershell
$usuario = "Administrador"

$usuario
```

---

**Mostrar una dirección IP**

Linux

```bash
ip="192.168.1.10"

echo $ip
```

PowerShell

```powershell
$ip = "192.168.1.10"

$ip
```

---

**Mostrar una ruta**

Linux

```bash
ruta="/home/usuario/Backups"

echo $ruta
```

PowerShell

```powershell
$ruta = "C:\Backups"

$ruta
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Es necesario utilizar `echo` para mostrar el contenido de una variable. | Basta con escribir el nombre de la variable para mostrar su contenido. |
| Las variables se referencian con `$` al utilizarlas. | También se referencian con `$`, pero la variable ya se creó con ese prefijo. |
| `echo` siempre genera una salida de texto. | La salida mantiene el tipo de dato original de la variable. |

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

### Linux

```bash
nombre="Nuevo valor"
```

**Descripción**

Modifica el valor de una variable asignándole un nuevo contenido.

---

### PowerShell

```powershell
$nombre = "Nuevo valor"
```

**Descripción**

Modifica el valor de una variable sustituyendo el contenido anterior por uno nuevo.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Modificar una variable | `variable="nuevo_valor"` | `$variable = "nuevo_valor"` |

---

### Ejemplos

**Modificar el nombre de un servidor**

Linux

```bash
servidor="SRV-01"

servidor="SRV-02"
```

PowerShell

```powershell
$servidor = "SRV-01"

$servidor = "SRV-02"
```

---

**Modificar una dirección IP**

Linux

```bash
ip="192.168.1.10"

ip="192.168.1.20"
```

PowerShell

```powershell
$ip = "192.168.1.10"

$ip = "192.168.1.20"
```

---

**Modificar una ruta**

Linux

```bash
ruta="/home/usuario/Backups"

ruta="/home/usuario/Documentos"
```

PowerShell

```powershell
$ruta = "C:\Backups"

$ruta = "C:\Users\usuario\Documents"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La variable se modifica realizando una nueva asignación. | La variable también se modifica realizando una nueva asignación. |
| El contenido anterior se reemplaza completamente. | El contenido anterior también se sustituye por el nuevo valor. |
| No es necesario declarar previamente el tipo de dato. | PowerShell adapta automáticamente el tipo de dato si el nuevo valor es diferente. |

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

### Linux

```bash
unset <variable>
```

**Descripción**

Elimina una variable de la sesión actual, liberando el nombre para que pueda volver a utilizarse.

---

### PowerShell

```powershell
Remove-Variable -Name <variable>
```

También puede utilizarse:

```powershell
Clear-Variable -Name <variable>
```

**Descripción**

Elimina una variable de la sesión actual. Si únicamente se desea borrar su contenido conservando la variable, puede utilizarse `Clear-Variable`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar una variable | `unset` | `Remove-Variable` |

---

### Ejemplos

**Eliminar una variable**

Linux

```bash
usuario="Administrador"

unset usuario
```

PowerShell

```powershell
$usuario = "Administrador"

Remove-Variable -Name usuario
```

---

**Eliminar una variable de dirección IP**

Linux

```bash
ip="192.168.1.10"

unset ip
```

PowerShell

```powershell
$ip = "192.168.1.10"

Remove-Variable -Name ip
```

---

**Comprobar que la variable ha sido eliminada**

Linux

```bash
echo $usuario
```

PowerShell

```powershell
$usuario
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `unset` elimina completamente la variable. | `Remove-Variable` elimina completamente la variable. |
| Si se intenta mostrar posteriormente, no devolverá ningún valor. | Si se intenta acceder posteriormente, la variable ya no existirá. |
| No dispone de un comando para vaciar únicamente el contenido. | `Clear-Variable` elimina el contenido manteniendo la variable. |

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

### Linux

```bash
printenv
```

También puede utilizarse:

```bash
env
```

**Descripción**

Muestra todas las variables de entorno disponibles en la sesión actual. Estas variables almacenan información utilizada por el sistema operativo y por las aplicaciones.

---

### PowerShell

```powershell
Get-ChildItem Env:
```

**Descripción**

Muestra todas las variables de entorno disponibles en la sesión actual de PowerShell.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar las variables de entorno | `printenv` / `env` | `Get-ChildItem Env:` |

---

### Ejemplos

**Mostrar todas las variables de entorno**

Linux

```bash
printenv
```

PowerShell

```powershell
Get-ChildItem Env:
```

---

**Mostrar el directorio personal del usuario**

Linux

```bash
echo $HOME
```

PowerShell

```powershell
$env:USERPROFILE
```

---

**Mostrar la variable PATH**

Linux

```bash
echo $PATH
```

PowerShell

```powershell
$env:PATH
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Las variables de entorno se acceden mediante `$NOMBRE_VARIABLE`. | Se accede a ellas mediante `$env:NOMBRE_VARIABLE`. |
| `HOME`, `PATH` y `USER` son algunas de las variables más habituales. | `PATH`, `USERNAME` y `USERPROFILE` son algunas de las más utilizadas. |
| `printenv` y `env` muestran todas las variables disponibles. | `Get-ChildItem Env:` muestra todas las variables del proveedor `Env:`. |

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

### Linux

```bash
variable=$(comando)
```

**Descripción**

Guarda el resultado de un comando dentro de una variable para poder reutilizarlo posteriormente.

---

### PowerShell

```powershell
$variable = comando
```

**Descripción**

Guarda la salida de un cmdlet o comando en una variable. En PowerShell, la variable puede almacenar texto, números, fechas u objetos completos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Guardar el resultado de un comando | `variable=$(comando)` | `$variable = comando` |

---

### Ejemplos

**Guardar el usuario actual**

Linux

```bash
usuario=$(whoami)
```

PowerShell

```powershell
$usuario = whoami
```

---

**Guardar la fecha actual**

Linux

```bash
fecha=$(date)
```

PowerShell

```powershell
$fecha = Get-Date
```

---

**Guardar el nombre del equipo**

Linux

```bash
equipo=$(hostname)
```

PowerShell

```powershell
$equipo = hostname
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza la sustitución de comandos mediante `$( )`. | Basta con asignar directamente el resultado del comando a la variable. |
| Normalmente almacena texto como resultado del comando. | Puede almacenar objetos completos además de texto. |
| Es muy utilizado en scripts Bash para reutilizar información. | Es una práctica habitual en scripts de PowerShell para trabajar posteriormente con los datos obtenidos. |

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

### Linux

```bash
<comando> $variable
```

### PowerShell

```powershell
<comando> $variable
```

**Descripción**

Permite reutilizar el valor almacenado en una variable como argumento de otro comando o cmdlet, evitando escribir el mismo dato varias veces.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Utilizar una variable en un comando | `<comando> $variable` | `<cmdlet> $variable` |

---

### Ejemplos

**Mostrar el contenido de un directorio almacenado en una variable**

Linux

```bash
ruta="/home/usuario/Documentos"

ls $ruta
```

PowerShell

```powershell
$ruta = "C:\Users\usuario\Documents"

Get-ChildItem $ruta
```

---

**Copiar un archivo utilizando una variable**

Linux

```bash
archivo="informe.pdf"

cp $archivo /home/usuario/Backups
```

PowerShell

```powershell
$archivo = "informe.pdf"

Copy-Item $archivo C:\Backups
```

---

**Eliminar un archivo utilizando una variable**

Linux

```bash
archivo="temporal.txt"

rm $archivo
```

PowerShell

```powershell
$archivo = "temporal.txt"

Remove-Item $archivo
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La variable se expande automáticamente antes de ejecutar el comando. | La variable también se expande automáticamente antes de ejecutar el cmdlet. |
| Generalmente contiene texto que será interpretado por el comando. | Puede contener texto, números, rutas u objetos completos. |
| Es habitual utilizar variables para rutas, nombres de archivos y resultados de comandos. | Además de rutas y nombres, es frecuente almacenar objetos completos para procesarlos posteriormente. |

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