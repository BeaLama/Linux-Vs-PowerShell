# Scripting

## Introducción

Los scripts son archivos que contienen una serie de instrucciones que pueden ejecutarse automáticamente para realizar tareas de administración, mantenimiento o automatización.

En entornos profesionales, los scripts permiten:

- Automatizar tareas repetitivas.
- Reducir errores humanos.
- Estandarizar procedimientos.
- Recopilar información del sistema.
- Crear herramientas propias de administración.

---

## Índice

- [Crear un script](#crear-un-script)
- [Variables](#variables)
- [Entrada de datos](#entrada-de-datos)
- [Condicionales](#condicionales)
- [Bucles](#bucles)
- [Funciones](#funciones)
- [Parámetros](#parámetros)
- [Manejo de errores](#manejo-de-errores)

---

## Crear un script

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Extensión del script | `.sh` | `.ps1` |
| Crear script | `nano script.sh` | `notepad script.ps1` |
| Indicar intérprete | `#!/bin/bash` | No requiere |
| Dar permisos | `chmod +x script.sh` | Política de ejecución |
| Ejecutar script | `./script.sh` | `.\script.ps1` |
| Ejecutar con intérprete | `bash script.sh` | `powershell.exe -File script.ps1` |

> 💡 **Diferencia clave** — 🐧 Bash necesita permisos de ejecución (`chmod +x`). · 🪟 PowerShell usa una política de ejecución (`Set-ExecutionPolicy`) en vez de permisos de archivo.

---

[⬆️ Volver al índice](#índice)

## Variables

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Crear variable | `nombre="valor"` | `$nombre="valor"` |
| Mostrar variable | `echo $nombre` | `$nombre` |
| Variable de entorno | `export VARIABLE=valor` | `$env:VARIABLE="valor"` |
| Ver variables | `env` | `Get-ChildItem Env:` |
| Usuario actual | `$USER` | `$env:USERNAME` |
| Equipo actual | `hostname` | `$env:COMPUTERNAME` |

> 💡 **Diferencia clave** — 🐧 Las variables Bash no llevan prefijo al crearlas, solo al leerlas (`$`). · 🪟 PowerShell siempre antepone `$` al nombre de la variable.

---

## Ejemplo práctico

### Obtener información del equipo

Linux:

```bash
#!/bin/bash

equipo=$(hostname)
usuario=$USER

echo "Equipo: $equipo"
echo "Usuario: $usuario"
```

PowerShell:

```powershell
$equipo = $env:COMPUTERNAME
$usuario = $env:USERNAME

Write-Host "Equipo: $equipo"
Write-Host "Usuario: $usuario"
```

Salida:

```text
Equipo: PC-ADMIN01
Usuario: administrador
```

---

[⬆️ Volver al índice](#índice)

## Entrada de datos

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Solicitar información | `read` | `Read-Host` |
| Mostrar mensaje | `read -p` | `Read-Host "mensaje"` |
| Entrada oculta | `read -s` | `Read-Host -AsSecureString` |

> 💡 **Diferencia clave** — 🐧 `read -s` oculta la entrada pero la guarda como texto plano. · 🪟 `-AsSecureString` la almacena cifrada en memoria.

---

## Ejemplo práctico

### Solicitar información del equipo

Linux:

```bash
#!/bin/bash

read -p "Nombre del servidor: " servidor

echo "Configurando servidor $servidor"
```

PowerShell:

```powershell
$servidor = Read-Host "Nombre del servidor"

Write-Host "Configurando servidor $servidor"
```

Salida:

```text
Nombre del servidor: SRV01

Configurando servidor SRV01
```

---

[⬆️ Volver al índice](#índice)

## Condicionales

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Condición | `if [ ]` | `if ()` |
| Segunda condición | `elif` | `elseif` |
| Alternativa | `else` | `else` |
| Comparación igual | `-eq` | `-eq` |
| Mayor que | `-gt` | `-gt` |
| Menor que | `-lt` | `-lt` |
| Varias condiciones | `&&` / `\|\|` | `-and` / `-or` |
| Múltiples opciones | `case` | `switch` |

> 💡 **Diferencia clave** — 🐧 Bash usa operadores de texto (`-eq`, `-gt`) dentro de `[ ]`. · 🪟 PowerShell usa los mismos operadores pero como parte del lenguaje, sin corchetes.

---

## Ejemplo práctico

### Comprobar si un servicio está disponible

Linux:

```bash
#!/bin/bash

servicio="ssh"

if systemctl is-active --quiet $servicio
then
    echo "Servicio activo"
else
    echo "Servicio detenido"
fi
```

PowerShell:

```powershell
$servicio = "Spooler"

$estado = Get-Service $servicio

if ($estado.Status -eq "Running") {
    Write-Host "Servicio activo"
}
else {
    Write-Host "Servicio detenido"
}
```

---

[⬆️ Volver al índice](#índice)

## Bucles

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Bucle contador | `for` | `for` |
| Recorrer elementos | `for item in` | `foreach` |
| Mientras condición | `while` | `while` |
| Ejecutar una vez antes de comprobar | `until` | `do while` |

**Ejemplo**
```bash
for archivo in *.txt
do
    echo "$archivo"
done
```
```powershell
foreach ($archivo in Get-ChildItem *.txt) {
    Write-Host $archivo
}
```

> 💡 **Diferencia clave** — 🐧 Bash recorre texto o listas de palabras. · 🪟 PowerShell recorre objetos (por ejemplo, archivos como objetos `FileInfo`).

---

## Ejemplo práctico

### Comprobar el estado de varios servidores

Linux:

```bash
#!/bin/bash

for servidor in srv01 srv02 srv03
do

    ping -c 1 $servidor

done
```

PowerShell:

```powershell
$servidores = @(
    "srv01",
    "srv02",
    "srv03"
)

foreach ($servidor in $servidores) {

    Test-Connection $servidor -Count 1

}
```

---

[⬆️ Volver al índice](#índice)

## Funciones

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Crear función | `nombre_funcion()` | `function Nombre {}` |
| Pasar parámetros | `$1`, `$2` | `param()` |
| Ejecutar función | Nombre de función | Nombre de función |
| Devolver valores | `echo` / `return` | `return` |

**Ejemplo**
```bash
sumar() {
    echo $(($1 + $2))
}
```
```powershell
function Sumar {
    param([int]$Numero1, [int]$Numero2)
    return $Numero1 + $Numero2
}
```

> 💡 **Diferencia clave** — 🐧 Las funciones Bash suelen devolver texto (`echo`). · 🪟 Las funciones PowerShell pueden devolver objetos completos, no solo texto.|

---

# Ejemplo práctico

## Función para comprobar conectividad

### Linux

```bash
#!/bin/bash

comprobar_ping()
{

    servidor=$1

    if ping -c 1 $servidor > /dev/null
    then
        echo "$servidor responde"
    else
        echo "$servidor no responde"
    fi

}

comprobar_ping google.com
```

---

### PowerShell

```powershell
function Test-Servidor {

    param(
        $Servidor
    )

    if (Test-Connection $Servidor -Count 1 -Quiet) {

        Write-Host "$Servidor responde"

    }
    else {

        Write-Host "$Servidor no responde"

    }

}

Test-Servidor google.com
```

---

[⬆️ Volver al índice](#índice)

## Parámetros

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Primer parámetro | `$1` | Parámetro definido en `param()` |
| Segundo parámetro | `$2` | Parámetro definido en `param()` |
| Todos los parámetros | `$@` | `$args` |
| Número de parámetros | `$#` | `$args.Count` |
| Parámetro obligatorio | Validación manual | `[Parameter(Mandatory)]` |
| Validar valores | `if` | `ValidateSet` |

> 💡 **Diferencia clave** — 🐧 Bash accede a los parámetros por posición (`$1`, `$2`) sin nombre ni tipo. · 🪟 PowerShell define parámetros con nombre, tipo y validaciones integradas.

---

# Ejemplo práctico

## Obtener información de un equipo remoto

### Linux

```bash
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Uso: $0 <equipo>"
    exit 1
fi

equipo=$1

echo "Consultando equipo: $equipo"

ping -c 1 $equipo
```

Ejecución:

```bash
./inventario.sh servidor01
```

---

### PowerShell

```powershell
param(
    [Parameter(Mandatory)]
    [string]$Equipo
)

Write-Host "Consultando equipo: $Equipo"

Test-Connection $Equipo -Count 1
```

Ejecución:

```powershell
.\inventario.ps1 -Equipo servidor01
```

---

[⬆️ Volver al índice](#índice)

## Manejo de errores

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Estado del último comando | `$?` | `$?` |
| Código de salida | `$?` | `$LASTEXITCODE` |
| Detener ejecución | `set -e` | `-ErrorAction Stop` |
| Controlar errores | `if` | `try/catch` |
| Guardar errores | `2>` | `Out-File` |

> 💡 **Diferencia clave** — 🐧 Bash comprueba errores manualmente con `$?` tras cada comando. · 🪟 PowerShell dispone de manejo de excepciones estructurado (`try/catch/finally`).

---

# Ejemplo práctico

## Copia de seguridad con control de errores

### Linux

```bash
#!/bin/bash

origen="/datos"
destino="/backup"

cp -r $origen $destino

if [ $? -eq 0 ]
then
    echo "Backup realizado correctamente"
else
    echo "Error durante la copia"
fi
```

---

### PowerShell

```powershell
$origen = "C:\Datos"
$destino = "C:\Backup"

try {

    Copy-Item $origen $destino -Recurse -ErrorAction Stop

    Write-Host "Backup realizado correctamente"

}
catch {

    Write-Host "Error durante la copia"

}
```

---

[⬆️ Volver al índice](#índice)

# Resumen de equivalencias

A continuación se muestra una recopilación de las principales equivalencias entre **Bash (Linux)** y **PowerShell (Windows)** relacionadas con scripting.

Aunque ambos lenguajes permiten automatizar tareas, existen diferencias importantes:

- Bash está orientado principalmente al uso de comandos y procesamiento de texto.
- PowerShell está basado en objetos y permite una administración más avanzada del sistema.

---

## Crear y ejecutar scripts


| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Extensión del script | `.sh` | `.ps1` |
| Crear script | `nano script.sh` | `notepad script.ps1` |
| Indicar intérprete | `#!/bin/bash` | No requiere |
| Dar permisos | `chmod +x script.sh` | Política de ejecución |
| Ejecutar script | `./script.sh` | `.\script.ps1` |
| Ejecutar con intérprete | `bash script.sh` | `powershell.exe -File script.ps1` |

> 💡 **Diferencia clave** — 🐧 Bash necesita permisos de ejecución (`chmod +x`). · 🪟 PowerShell usa una política de ejecución (`Set-ExecutionPolicy`) en vez de permisos de archivo.

---

## Variables

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Crear variable | `nombre="valor"` | `$nombre="valor"` |
| Mostrar variable | `echo $nombre` | `$nombre` |
| Variable de entorno | `export VARIABLE=valor` | `$env:VARIABLE="valor"` |
| Ver variables | `env` | `Get-ChildItem Env:` |
| Usuario actual | `$USER` | `$env:USERNAME` |
| Equipo actual | `hostname` | `$env:COMPUTERNAME` |

> 💡 **Diferencia clave** — 🐧 Las variables Bash no llevan prefijo al crearlas, solo al leerlas (`$`). · 🪟 PowerShell siempre antepone `$` al nombre de la variable.

---

## Entrada de datos

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Solicitar información | `read` | `Read-Host` |
| Mostrar mensaje | `read -p` | `Read-Host "mensaje"` |
| Entrada oculta | `read -s` | `Read-Host -AsSecureString` |

> 💡 **Diferencia clave** — 🐧 `read -s` oculta la entrada pero la guarda como texto plano. · 🪟 `-AsSecureString` la almacena cifrada en memoria.

---

## Condicionales

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Condición | `if [ ]` | `if ()` |
| Segunda condición | `elif` | `elseif` |
| Alternativa | `else` | `else` |
| Comparación igual | `-eq` | `-eq` |
| Mayor que | `-gt` | `-gt` |
| Menor que | `-lt` | `-lt` |
| Varias condiciones | `&&` / `\|\|` | `-and` / `-or` |
| Múltiples opciones | `case` | `switch` |

> 💡 **Diferencia clave** — 🐧 Bash usa operadores de texto (`-eq`, `-gt`) dentro de `[ ]`. · 🪟 PowerShell usa los mismos operadores pero como parte del lenguaje, sin corchetes.

---

## Bucles

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Bucle contador | `for` | `for` |
| Recorrer elementos | `for item in` | `foreach` |
| Mientras condición | `while` | `while` |
| Ejecutar una vez antes de comprobar | `until` | `do while` |

**Ejemplo**
```bash
for archivo in *.txt
do
    echo "$archivo"
done
```
```powershell
foreach ($archivo in Get-ChildItem *.txt) {
    Write-Host $archivo
}
```

> 💡 **Diferencia clave** — 🐧 Bash recorre texto o listas de palabras. · 🪟 PowerShell recorre objetos (por ejemplo, archivos como objetos `FileInfo`).

---

## Funciones

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Crear función | `nombre_funcion()` | `function Nombre {}` |
| Pasar parámetros | `$1`, `$2` | `param()` |
| Ejecutar función | Nombre de función | Nombre de función |
| Devolver valores | `echo` / `return` | `return` |

**Ejemplo**
```bash
sumar() {
    echo $(($1 + $2))
}
```
```powershell
function Sumar {
    param([int]$Numero1, [int]$Numero2)
    return $Numero1 + $Numero2
}
```

> 💡 **Diferencia clave** — 🐧 Las funciones Bash suelen devolver texto (`echo`). · 🪟 Las funciones PowerShell pueden devolver objetos completos, no solo texto.

---

## Parámetros

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Primer parámetro | `$1` | Parámetro definido en `param()` |
| Segundo parámetro | `$2` | Parámetro definido en `param()` |
| Todos los parámetros | `$@` | `$args` |
| Número de parámetros | `$#` | `$args.Count` |
| Parámetro obligatorio | Validación manual | `[Parameter(Mandatory)]` |
| Validar valores | `if` | `ValidateSet` |

> 💡 **Diferencia clave** — 🐧 Bash accede a los parámetros por posición (`$1`, `$2`) sin nombre ni tipo. · 🪟 PowerShell define parámetros con nombre, tipo y validaciones integradas.

---

## Manejo de errores

| Acción | 🐧 Linux (Bash) | 🪟 PowerShell |
|---|---|---|
| Estado del último comando | `$?` | `$?` |
| Código de salida | `$?` | `$LASTEXITCODE` |
| Detener ejecución | `set -e` | `-ErrorAction Stop` |
| Controlar errores | `if` | `try/catch` |
| Guardar errores | `2>` | `Out-File` |

> 💡 **Diferencia clave** — 🐧 Bash comprueba errores manualmente con `$?` tras cada comando. · 🪟 PowerShell dispone de manejo de excepciones estructurado (`try/catch/finally`).

---

## Conceptos clave

| 🐧 Bash (Linux) | 🪟 PowerShell |
|---|---|
| Trabaja principalmente con texto. | Trabaja con objetos. |
| Usa comandos tradicionales del sistema. | Usa cmdlets. |
| Los scripts encadenan comandos mediante tuberías de texto. | El pipeline transmite objetos entre comandos. |
| La gestión de errores depende del programador. | Dispone de excepciones estructuradas. |
| Muy utilizado en servidores Linux. | Muy utilizado en entornos Windows empresariales. |

---

## Ejemplo final

**Script de comprobación de conectividad**

```bash
#!/bin/bash
servidor=$1
if ping -c 1 $servidor > /dev/null
then
    echo "$servidor responde"
else
    echo "$servidor no responde"
fi
```
```powershell
param($Servidor)
if (Test-Connection $Servidor -Count 1 -Quiet) {
    Write-Host "$Servidor responde"
} else {
    Write-Host "$Servidor no responde"
}
```

---

[⬆️ Volver al índice](#índice)