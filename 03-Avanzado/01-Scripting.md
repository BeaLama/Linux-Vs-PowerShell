# Scripting

## Introducción

Los scripts son archivos que contienen una serie de instrucciones que pueden ejecutarse automáticamente para realizar tareas de administración, mantenimiento o automatización.

En entornos profesionales, los scripts permiten:

- Automatizar tareas repetitivas.
- Reducir errores humanos.
- Estandarizar procedimientos.
- Recopilar información del sistema.
- Crear herramientas propias de administración.

Los principales lenguajes de scripting utilizados en administración de sistemas son:

- **Bash** → utilizado principalmente en sistemas Linux.
- **PowerShell** → utilizado principalmente en Windows, aunque también está disponible para Linux y macOS.

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
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Crear un script

### Linux (Bash)

Un script en Linux es un archivo de texto que contiene una serie de comandos que serán ejecutados por el intérprete de comandos.

Normalmente los scripts de Bash utilizan la extensión:

```text
.sh
```

Ejemplo:

```bash
backup.sh
```

---

### Crear un script

Crear un archivo:

```bash
nano script.sh
```

Añadir el contenido:

```bash
#!/bin/bash

echo "Hola, mundo"
```

La primera línea:

```bash
#!/bin/bash
```

se denomina **shebang** e indica qué intérprete debe utilizar el sistema para ejecutar el script.

En este caso:

```text
/bin/bash
```

indica que debe utilizar Bash.

---

### Dar permisos de ejecución

Por defecto, un archivo creado en Linux no tiene permisos de ejecución.

Para añadirlos:

```bash
chmod +x script.sh
```

Comprobar permisos:

```bash
ls -l script.sh
```

Ejemplo de salida:

```text
-rwxr-xr-x 1 usuario usuario 30 jul 29 10:00 script.sh
```

La letra:

```text
x
```

indica que el archivo tiene permiso de ejecución.

---

### Ejecutar un script

Existen varias formas:

Ejecutándolo directamente:

```bash
./script.sh
```

Mediante Bash:

```bash
bash script.sh
```

Mediante la ruta completa:

```bash
/home/usuario/scripts/script.sh
```

---

## PowerShell

Los scripts de PowerShell utilizan normalmente la extensión:

```text
.ps1
```

Ejemplo:

```text
inventario.ps1
```

Un script de PowerShell contiene comandos o instrucciones que serán ejecutados por el intérprete PowerShell.

---

### Crear un script

Crear un archivo:

```powershell
notepad script.ps1
```

Añadir contenido:

```powershell
Write-Host "Hola, mundo"
```

Ejecutar:

```powershell
.\script.ps1
```

---

### Política de ejecución

Windows puede bloquear la ejecución de scripts por motivos de seguridad.

Consultar la política actual:

```powershell
Get-ExecutionPolicy
```

Ejemplo:

```text
Restricted
```

significa que la ejecución de scripts está bloqueada.

---

### Cambiar la política de ejecución

Permitir scripts locales:

```powershell
Set-ExecutionPolicy RemoteSigned
```

Permitir todos los scripts:

```powershell
Set-ExecutionPolicy Unrestricted
```

> **⚠️ Nota:** No se recomienda utilizar políticas demasiado permisivas en equipos corporativos.

---

### Ejecutar un script ignorando la política

También puede ejecutarse un script concreto mediante:

```powershell
powershell.exe -ExecutionPolicy Bypass -File script.ps1
```

Esto permite ejecutar el script sin modificar la configuración permanente del sistema.

---

## Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un script | Crear archivo `.sh` | Crear archivo `.ps1` |
| Indicar intérprete | `#!/bin/bash` | No requiere shebang |
| Dar permisos de ejecución | `chmod +x` | No utiliza permisos de ejecución |
| Ejecutar script | `./script.sh` | `.\script.ps1` |
| Ejecutar mediante intérprete | `bash script.sh` | `powershell.exe -File script.ps1` |

---

## Diferencias

| Linux (Bash) | Windows (PowerShell) |
|--------------|----------------------|
| Los permisos de ejecución dependen del sistema de archivos. | La ejecución depende principalmente de la política de ejecución. |
| Utiliza archivos de texto simples con comandos Bash. | Utiliza objetos y cmdlets propios de PowerShell. |
| El shebang define el intérprete. | El propio archivo ya está asociado a PowerShell. |
| Es habitual ejecutar scripts mediante terminal. | Puede integrarse con el Programador de tareas y administración remota. |

---

## Buenas prácticas

- Utiliza nombres descriptivos para los scripts.
- Añade comentarios explicando la finalidad del código.
- Utiliza rutas absolutas cuando el script vaya a ejecutarse automáticamente.
- Prueba los scripts antes de utilizarlos en producción.
- Evita ejecutar scripts con privilegios elevados si no es necesario.
- Guarda los scripts en un sistema de control de versiones cuando sean importantes.

---

## Ejemplos reales de administración

Algunos usos habituales de scripts en administración:

### Inventario de equipos

Recopilar información como:

- Nombre del equipo.
- Usuario conectado.
- Sistema operativo.
- Memoria RAM.
- Procesador.
- Dirección IP.

---

### Comprobación del sistema

Automatizar revisiones como:

- Espacio disponible en disco.
- Uso de CPU.
- Memoria utilizada.
- Estado del firewall.
- Conectividad de red.

---

### Copias de seguridad

Automatizar:

- Copia de archivos.
- Compresión.
- Rotación de backups.
- Limpieza de copias antiguas.

---

[⬆️ Volver al índice](#índice)

## Variables

Las variables permiten almacenar información temporalmente para poder utilizarla posteriormente dentro de un script.

Son fundamentales para:

- Guardar valores obtenidos del sistema.
- Trabajar con datos introducidos por usuarios.
- Realizar cálculos.
- Controlar la ejecución de un script.
- Almacenar resultados de comandos.

Aunque Bash y PowerShell utilizan variables, su funcionamiento interno es diferente.

---

# Linux (Bash)

En Bash, las variables se crean asignando directamente un valor a un nombre.

La sintaxis es:

```bash
nombre_variable="valor"
```

Ejemplo:

```bash
nombre="Beatriz"
```

Para consultar el contenido de una variable se utiliza:

```bash
echo $nombre
```

Resultado:

```text
Beatriz
```

---

## Reglas para crear variables en Bash

Las variables deben cumplir ciertas normas:

- No pueden contener espacios.
- No pueden empezar por un número.
- Son sensibles a mayúsculas y minúsculas.

Ejemplo correcto:

```bash
usuario="admin"
```

Ejemplo incorrecto:

```bash
mi usuario="admin"
```

---

## Variables del sistema en Bash

Linux dispone de variables de entorno ya definidas por el sistema.

Consultar todas:

```bash
env
```

o:

```bash
printenv
```

Ejemplos:

| Variable | Descripción |
|----------|-------------|
| `$USER` | Usuario actual |
| `$HOME` | Directorio personal |
| `$PWD` | Directorio actual |
| `$SHELL` | Shell utilizado |
| `$PATH` | Rutas donde buscar comandos |

Ejemplo:

```bash
echo $USER
```

Salida:

```text
usuario
```

---

## Crear variables de entorno

Para crear una variable disponible para procesos hijos:

```bash
export VARIABLE="valor"
```

Ejemplo:

```bash
export SERVIDOR="SRV01"
```

Comprobar:

```bash
echo $SERVIDOR
```

---

# PowerShell

En PowerShell, todas las variables comienzan con el símbolo:

```powershell
$
```

La sintaxis es:

```powershell
$variable = valor
```

Ejemplo:

```powershell
$nombre = "Beatriz"
```

Mostrar el contenido:

```powershell
Write-Host $nombre
```

Resultado:

```text
Beatriz
```

También puede utilizarse:

```powershell
$nombre
```

---

## Tipos de variables

PowerShell utiliza un sistema basado en objetos, por lo que una variable puede contener distintos tipos de datos.

Ejemplo:

Texto:

```powershell
$nombre = "Servidor01"
```

Número:

```powershell
$ram = 32
```

Booleano:

```powershell
$activo = $true
```

Lista:

```powershell
$usuarios = @(
    "admin"
    "usuario1"
    "usuario2"
)
```

---

## Consultar el tipo de una variable

PowerShell permite conocer el tipo de dato almacenado:

```powershell
$variable.GetType()
```

Ejemplo:

```powershell
$ram = 32

$ram.GetType()
```

Resultado:

```text
Int32
```

---

## Variables automáticas de PowerShell

PowerShell incluye variables internas del sistema.

Ejemplos:

| Variable | Descripción |
|----------|-------------|
| `$HOME` | Carpeta personal del usuario |
| `$PWD` | Ubicación actual |
| `$env:USERNAME` | Usuario actual |
| `$env:COMPUTERNAME` | Nombre del equipo |
| `$env:PATH` | Rutas del sistema |
| `$PSVersionTable` | Información de versión |

Ejemplo:

```powershell
$env:COMPUTERNAME
```

Salida:

```text
PC-ADMIN01
```

---

## Variables de entorno en PowerShell

Se accede mediante:

```powershell
$env:NOMBRE_VARIABLE
```

Ejemplo:

```powershell
$env:TEMP
```

Crear una variable temporal:

```powershell
$env:SERVIDOR="SRV01"
```

---

## Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Crear variable | `variable="valor"` | `$variable = valor` |
| Mostrar variable | `echo $variable` | `$variable` |
| Variables de entorno | `export VARIABLE=valor` | `$env:VARIABLE=valor` |
| Ver variables | `env` / `printenv` | `Get-ChildItem Env:` |
| Usuario actual | `$USER` | `$env:USERNAME` |
| Equipo actual | `hostname` | `$env:COMPUTERNAME` |

---

## Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Las variables son principalmente texto. | Las variables almacenan objetos completos. |
| Los tipos se gestionan de forma más flexible. | Los tipos de datos son más importantes. |
| Utiliza `$` al consultar la variable. | Utiliza `$` tanto al crear como consultar. |
| Las variables de entorno utilizan `export`. | Las variables de entorno utilizan el proveedor `env:`. |

---

## Buenas prácticas

- Utiliza nombres descriptivos para las variables.
- Evita nombres demasiado cortos que dificulten entender el script.
- Inicializa las variables antes de utilizarlas.
- Comprueba que una variable contiene datos antes de procesarla.
- Evita sobrescribir variables importantes del sistema.
- Añade comentarios cuando una variable tenga una función específica.

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

La entrada de datos permite que un script reciba información proporcionada por un usuario durante la ejecución.

Esto permite crear scripts más dinámicos y reutilizables, ya que no es necesario modificar el código cada vez que cambia un valor.

Algunos ejemplos de uso:

- Solicitar un usuario.
- Pedir una ruta de archivo.
- Introducir una dirección IP.
- Seleccionar una opción de un menú.
- Introducir parámetros para una tarea.

---

# Linux (Bash)

En Bash se utiliza principalmente el comando:

```bash
read
```

para capturar información introducida por el usuario.

---

## Uso básico de `read`

Ejemplo:

```bash
#!/bin/bash

echo "Introduce tu nombre:"
read nombre

echo "Hola $nombre"
```

Ejecución:

```text
Introduce tu nombre:
Beatriz

Hola Beatriz
```

---

## Mostrar un mensaje directamente

También puede utilizarse:

```bash
read -p "Introduce tu nombre: " nombre
```

Ejemplo:

```bash
#!/bin/bash

read -p "Usuario: " usuario

echo "Usuario introducido: $usuario"
```

Salida:

```text
Usuario: admin

Usuario introducido: admin
```

---

## Introducir contraseñas

Para ocultar la información introducida:

```bash
read -s contraseña
```

Ejemplo:

```bash
#!/bin/bash

read -s -p "Contraseña: " password

echo
echo "Contraseña recibida"
```

El parámetro:

```text
-s
```

evita que los caracteres aparezcan por pantalla.

---

## Leer varios valores

Bash permite almacenar varios valores:

```bash
read nombre apellido
```

Ejemplo:

```bash
#!/bin/bash

read -p "Nombre y apellido: " nombre apellido

echo "Nombre: $nombre"
echo "Apellido: $apellido"
```

---

# PowerShell

En PowerShell se utiliza:

```powershell
Read-Host
```

para solicitar información al usuario.

---

## Uso básico de `Read-Host`

Ejemplo:

```powershell
$nombre = Read-Host "Introduce tu nombre"

Write-Host "Hola $nombre"
```

Salida:

```text
Introduce tu nombre: Beatriz

Hola Beatriz
```

---

## Solicitar información protegida

Para introducir contraseñas:

```powershell
$password = Read-Host "Contraseña" -AsSecureString
```

El parámetro:

```powershell
-AsSecureString
```

permite almacenar el valor como una cadena segura.

---

## Convertir una contraseña segura

Ejemplo:

```powershell
$password = Read-Host "Contraseña" -AsSecureString

$credencial = New-Object System.Management.Automation.PSCredential(
    "usuario",
    $password
)
```

Esto permite crear credenciales que pueden utilizarse en otras operaciones de administración.

---

## Validar datos introducidos

PowerShell permite comprobar valores antes de utilizarlos.

Ejemplo:

```powershell
$edad = Read-Host "Introduce tu edad"

if ($edad -match "^[0-9]+$") {
    Write-Host "Valor correcto"
}
else {
    Write-Host "Valor incorrecto"
}
```

---

## Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Solicitar datos al usuario | `read` | `Read-Host` |
| Mostrar mensaje al solicitar | `read -p` | `Read-Host "mensaje"` |
| Entrada oculta | `read -s` | `Read-Host -AsSecureString` |
| Guardar resultado | Variable Bash | Variable PowerShell |

---

## Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Utiliza el comando `read`. | Utiliza el cmdlet `Read-Host`. |
| La información suele almacenarse como texto. | Puede trabajar con objetos y tipos seguros. |
| Las contraseñas requieren ocultar manualmente la entrada. | Dispone de almacenamiento seguro mediante `SecureString`. |
| La validación suele realizarse mediante expresiones y comandos externos. | Dispone de métodos propios para trabajar con objetos y datos. |

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

## Buenas prácticas

- Valida siempre los datos introducidos por el usuario.
- Evita confiar directamente en valores introducidos manualmente.
- Utiliza entradas protegidas para contraseñas.
- Muestra mensajes claros indicando qué información se solicita.
- Controla qué valores son válidos antes de continuar la ejecución.
- Evita almacenar contraseñas en texto plano dentro de scripts.

---

[⬆️ Volver al índice](#índice)

## Condicionales

Los condicionales permiten que un script tome decisiones dependiendo de una condición determinada.

Gracias a ellos, un script puede ejecutar diferentes acciones según el resultado de una comprobación.

Algunos ejemplos:

- Comprobar si un archivo existe.
- Verificar si un servicio está activo.
- Validar datos introducidos por un usuario.
- Ejecutar acciones diferentes según una opción seleccionada.
- Controlar errores antes de continuar.

Las estructuras condicionales más utilizadas son:

- `if`
- `elif` / `elseif`
- `else`
- `switch`

---

# Linux (Bash)

En Bash se utilizan principalmente las estructuras:

```bash
if
elif
else
fi
```

La sintaxis básica es:

```bash
if [ condición ]
then
    comando
else
    comando
fi
```

---

## Condición simple

Ejemplo:

```bash
#!/bin/bash

usuario="admin"

if [ "$usuario" = "admin" ]
then
    echo "Usuario administrador"
else
    echo "Usuario estándar"
fi
```

Salida:

```text
Usuario administrador
```

---

## Comparar números

Bash utiliza operadores específicos para números:

| Operador | Significado |
|----------|-------------|
| `-eq` | Igual |
| `-ne` | Diferente |
| `-gt` | Mayor que |
| `-lt` | Menor que |
| `-ge` | Mayor o igual |
| `-le` | Menor o igual |

Ejemplo:

```bash
edad=20

if [ $edad -ge 18 ]
then
    echo "Mayor de edad"
else
    echo "Menor de edad"
fi
```

---

## Comprobar archivos

Bash permite comprobar diferentes propiedades de archivos:

| Operador | Descripción |
|----------|-------------|
| `-f` | Existe y es un archivo |
| `-d` | Existe y es un directorio |
| `-r` | Tiene permisos de lectura |
| `-w` | Tiene permisos de escritura |
| `-x` | Tiene permisos de ejecución |

Ejemplo:

```bash
archivo="/tmp/prueba.txt"

if [ -f "$archivo" ]
then
    echo "El archivo existe"
else
    echo "No existe"
fi
```

---

## Varias condiciones

Operadores habituales:

| Operador | Significado |
|----------|-------------|
| `&&` | AND |
| `||` | OR |

Ejemplo:

```bash
usuario="admin"
activo=true

if [ "$usuario" = "admin" ] && [ "$activo" = true ]
then
    echo "Acceso permitido"
fi
```

---

## Múltiples opciones con `elif`

Ejemplo:

```bash
nota=8

if [ $nota -ge 9 ]
then
    echo "Excelente"
elif [ $nota -ge 5 ]
then
    echo "Aprobado"
else
    echo "Suspenso"
fi
```

---

# PowerShell

En PowerShell se utilizan:

```powershell
if
elseif
else
```

La sintaxis es:

```powershell
if (condición) {

}
elseif (condición) {

}
else {

}
```

---

## Condición simple

Ejemplo:

```powershell
$usuario = "admin"

if ($usuario -eq "admin") {
    Write-Host "Usuario administrador"
}
else {
    Write-Host "Usuario estándar"
}
```

Salida:

```text
Usuario administrador
```

---

## Operadores de comparación

PowerShell utiliza operadores con guiones:

| Operador | Significado |
|----------|-------------|
| `-eq` | Igual |
| `-ne` | Diferente |
| `-gt` | Mayor que |
| `-lt` | Menor que |
| `-ge` | Mayor o igual |
| `-le` | Menor o igual |

Ejemplo:

```powershell
$ram = 16

if ($ram -ge 8) {
    Write-Host "Memoria suficiente"
}
else {
    Write-Host "Memoria insuficiente"
}
```

---

## Comprobar archivos

PowerShell utiliza cmdlets como:

```powershell
Test-Path
```

Ejemplo:

```powershell
$archivo = "C:\Logs\app.log"

if (Test-Path $archivo) {
    Write-Host "El archivo existe"
}
else {
    Write-Host "No existe"
}
```

---

## Varias condiciones

Operadores lógicos:

| Operador | Significado |
|----------|-------------|
| `-and` | AND |
| `-or` | OR |
| `-not` | NOT |

Ejemplo:

```powershell
$usuario = "admin"
$activo = $true

if (($usuario -eq "admin") -and ($activo -eq $true)) {
    Write-Host "Acceso permitido"
}
```

---

## Múltiples opciones con `elseif`

Ejemplo:

```powershell
$cpu = 85

if ($cpu -ge 90) {
    Write-Host "Uso crítico"
}
elseif ($cpu -ge 70) {
    Write-Host "Uso elevado"
}
else {
    Write-Host "Uso normal"
}
```

---

# Switch

Además de `if`, PowerShell incluye:

```powershell
switch
```

para evaluar múltiples opciones.

Ejemplo:

```powershell
$opcion = "backup"

switch ($opcion) {

    "backup" {
        Write-Host "Ejecutando copia"
    }

    "restore" {
        Write-Host "Restaurando datos"
    }

    default {
        Write-Host "Opción desconocida"
    }
}
```

---

## Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Condición | `if [ ]` | `if ()` |
| Segunda condición | `elif` | `elseif` |
| Alternativa | `else` | `else` |
| Comparar valores | `-eq`, `-gt`, etc. | `-eq`, `-gt`, etc. |
| Comprobar archivos | `[ -f archivo ]` | `Test-Path` |
| Varias condiciones | `&&`, `||` | `-and`, `-or` |
| Múltiples opciones | `case` | `switch` |

---

## Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Utiliza corchetes `[ ]` para evaluar condiciones. | Utiliza paréntesis `( )`. |
| Los operadores pueden cambiar según se comparen textos o números. | Utiliza operadores consistentes con prefijo `-`. |
| La comprobación de archivos se realiza mediante operadores integrados. | Utiliza cmdlets como `Test-Path`. |
| Para múltiples opciones suele utilizarse `case`. | Dispone de `switch` integrado. |

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

## Buenas prácticas

- Utiliza condiciones claras y fáciles de leer.
- Evita crear bloques `if` demasiado largos.
- Valida siempre los datos antes de utilizarlos.
- Utiliza `switch` cuando tengas muchas opciones posibles.
- Añade mensajes descriptivos para facilitar la resolución de errores.
- Prueba todos los caminos posibles del script.

---

[⬆️ Volver al índice](#índice)

## Bucles

Los bucles permiten ejecutar un conjunto de instrucciones varias veces sin necesidad de repetir el código manualmente.

Son especialmente útiles para tareas de administración como:

- Procesar múltiples archivos.
- Revisar varios equipos.
- Crear usuarios en lote.
- Comprobar servicios.
- Recorrer listas de elementos.
- Automatizar tareas repetitivas.

Los tipos de bucles más utilizados son:

- `for`
- `while`
- `foreach`

---

# Linux (Bash)

En Bash los bucles más utilizados son:

- `for`
- `while`
- `until`

---

## Bucle `for`

El bucle `for` permite recorrer una lista de valores y ejecutar instrucciones para cada elemento.

Sintaxis:

```bash
for variable in lista
do
    comandos
done
```

Ejemplo:

```bash
#!/bin/bash

for usuario in admin soporte usuario1
do
    echo "Usuario: $usuario"
done
```

Salida:

```text
Usuario: admin
Usuario: soporte
Usuario: usuario1
```

---

## Recorrer archivos

Ejemplo:

```bash
#!/bin/bash

for archivo in /var/log/*.log
do
    echo "Analizando: $archivo"
done
```

Este script recorrerá todos los archivos `.log` dentro de `/var/log`.

---

## Bucle con números

Ejemplo:

```bash
for numero in {1..5}
do
    echo "Número: $numero"
done
```

Salida:

```text
Número: 1
Número: 2
Número: 3
Número: 4
Número: 5
```

---

## Bucle `while`

El bucle `while` ejecuta instrucciones mientras una condición sea verdadera.

Sintaxis:

```bash
while [ condición ]
do
    comandos
done
```

Ejemplo:

```bash
contador=1

while [ $contador -le 5 ]
do
    echo "Valor: $contador"
    contador=$((contador+1))
done
```

Salida:

```text
Valor: 1
Valor: 2
Valor: 3
Valor: 4
Valor: 5
```

---

## Leer un archivo línea a línea

Ejemplo:

```bash
while read linea
do
    echo "$linea"
done < usuarios.txt
```

Este método es muy utilizado para procesar listas de usuarios, equipos o configuraciones.

---

# PowerShell

PowerShell utiliza principalmente:

- `for`
- `foreach`
- `while`
- `do while`

---

## Bucle `for`

Permite ejecutar código un número determinado de veces.

Sintaxis:

```powershell
for (inicio; condición; incremento) {

}
```

Ejemplo:

```powershell
for ($i = 1; $i -le 5; $i++) {

    Write-Host "Número: $i"

}
```

Salida:

```text
Número: 1
Número: 2
Número: 3
Número: 4
Número: 5
```

---

## Bucle `foreach`

Es uno de los más utilizados en administración.

Permite recorrer colecciones de objetos.

Ejemplo:

```powershell
$usuarios = @(
    "admin"
    "soporte"
    "usuario1"
)

foreach ($usuario in $usuarios) {

    Write-Host "Usuario: $usuario"

}
```

Salida:

```text
Usuario: admin
Usuario: soporte
Usuario: usuario1
```

---

## Recorrer procesos

Ejemplo:

```powershell
$procesos = Get-Process

foreach ($proceso in $procesos) {

    Write-Host $proceso.Name

}
```

Este ejemplo muestra todos los procesos activos del equipo.

---

## Bucle `while`

Ejecuta instrucciones mientras una condición sea verdadera.

Ejemplo:

```powershell
$contador = 1

while ($contador -le 5) {

    Write-Host "Valor: $contador"

    $contador++

}
```

---

## Bucle `do while`

Ejecuta el bloque al menos una vez antes de comprobar la condición.

Ejemplo:

```powershell
$numero = 1

do {

    Write-Host "Número: $numero"

    $numero++

}
while ($numero -le 5)
```

---

## Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Bucle con contador | `for` | `for` |
| Recorrer elementos | `for` | `foreach` |
| Repetir mientras condición | `while` | `while` |
| Ejecutar al menos una vez | `until` / `while` | `do while` |
| Recorrer archivos | `for archivo in` | `Get-ChildItem + foreach` |

---

## Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Los bucles trabajan principalmente con texto y valores simples. | Los bucles trabajan con objetos completos. |
| Es común recorrer la salida de comandos mediante tuberías. | Es habitual recorrer colecciones devueltas por cmdlets. |
| La gestión de listas suele hacerse mediante arrays simples. | Las colecciones pueden contener objetos complejos. |
| Requiere controlar manualmente muchos detalles del procesamiento. | Permite acceder directamente a propiedades y métodos de objetos. |

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

## Ejemplo práctico de administración

### Revisar espacio en disco de varios equipos

PowerShell:

```powershell
$equipos = @(
    "PC01",
    "PC02",
    "PC03"
)

foreach ($equipo in $equipos) {

    Get-CimInstance Win32_LogicalDisk `
    -ComputerName $equipo

}
```

Este tipo de automatización es habitual en tareas de inventario y mantenimiento.

---

## Buenas prácticas

- Evita bucles infinitos que puedan bloquear un sistema.
- Añade condiciones de salida cuando sea necesario.
- Prueba siempre los scripts con pocos elementos antes de ejecutarlos en producción.
- Controla los errores dentro del bucle para evitar detener toda la ejecución.
- Utiliza nombres descriptivos para las variables utilizadas.
- Evita realizar operaciones innecesarias dentro del bucle.

---

[⬆️ Volver al índice](#índice)

## Funciones

Las funciones permiten agrupar un conjunto de instrucciones dentro de un bloque reutilizable.

Su objetivo es evitar repetir código y facilitar la organización de scripts complejos.

Las funciones son especialmente útiles para:

- Dividir un script grande en partes más pequeñas.
- Reutilizar código varias veces.
- Facilitar el mantenimiento.
- Crear herramientas de administración más profesionales.
- Separar tareas concretas dentro de un proceso.

Ejemplos de funciones habituales en administración:

- Comprobar conectividad.
- Obtener información del sistema.
- Crear usuarios.
- Generar informes.
- Registrar errores.

---

# Linux (Bash)

En Bash las funciones se pueden crear utilizando:

```bash
nombre_funcion()
{
    comandos
}
```

También puede escribirse:

```bash
function nombre_funcion {
    comandos
}
```

---

## Crear una función básica

Ejemplo:

```bash
#!/bin/bash

saludar()
{
    echo "Hola administrador"
}

saludar
```

Salida:

```text
Hola administrador
```

La función se ejecuta llamando a su nombre:

```bash
saludar
```

---

## Funciones con parámetros

Las funciones pueden recibir valores mediante parámetros.

Ejemplo:

```bash
#!/bin/bash

saludar()
{
    echo "Hola $1"
}

saludar Beatriz
```

Salida:

```text
Hola Beatriz
```

Los parámetros funcionan igual que en un script:

| Parámetro | Descripción |
|-----------|-------------|
| `$1` | Primer argumento |
| `$2` | Segundo argumento |
| `$@` | Todos los argumentos |
| `$#` | Número de argumentos |

---

## Devolver valores

En Bash las funciones no devuelven valores directamente como otros lenguajes.

Normalmente se utiliza:

```bash
echo
```

para devolver información.

Ejemplo:

```bash
obtener_usuario()
{
    echo $USER
}

usuario=$(obtener_usuario)

echo "Usuario actual: $usuario"
```

Salida:

```text
Usuario actual: admin
```

---

## Código de retorno

También pueden devolver un código de salida:

```bash
return
```

Ejemplo:

```bash
comprobar()
{
    return 0
}
```

Códigos habituales:

| Código | Significado |
|--------|-------------|
| `0` | Correcto |
| Otro valor | Error |

---

# PowerShell

En PowerShell las funciones son más avanzadas debido a su modelo basado en objetos.

La sintaxis básica es:

```powershell
function Nombre-Funcion {

    comandos

}
```

---

## Crear una función básica

Ejemplo:

```powershell
function Saludar {

    Write-Host "Hola administrador"

}

Saludar
```

Salida:

```text
Hola administrador
```

---

## Funciones con parámetros

PowerShell permite definir parámetros dentro de una función:

```powershell
function Saludar {

    param(
        $Nombre
    )

    Write-Host "Hola $Nombre"

}

Saludar Beatriz
```

Salida:

```text
Hola Beatriz
```

---

## Parámetros tipados

Una ventaja de PowerShell es poder definir tipos de datos.

Ejemplo:

```powershell
function Sumar {

    param(
        [int]$Numero1,
        [int]$Numero2
    )

    return $Numero1 + $Numero2

}

Resultado = Sumar 5 10
```

Salida:

```text
15
```

---

## Devolver valores

En PowerShell cualquier salida de la función puede convertirse en un valor.

Ejemplo:

```powershell
function Obtener-Usuario {

    return $env:USERNAME

}

$usuario = Obtener-Usuario

Write-Host $usuario
```

---

## Funciones avanzadas

PowerShell permite crear funciones con características profesionales:

- Parámetros obligatorios.
- Ayuda integrada.
- Validación de datos.
- Gestión de errores.
- Salidas estructuradas.

Ejemplo:

```powershell
function Obtener-PC {

    param(
        [Parameter(Mandatory)]
        [string]$Equipo
    )

    Get-ComputerInfo -ComputerName $Equipo

}
```

---

# Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Crear función | `nombre()` | `function Nombre {}` |
| Pasar parámetros | `$1`, `$2` | `param()` |
| Ejecutar función | Escribir nombre | Escribir nombre |
| Devolver valor | `echo` / `return` | `return` |
| Código de salida | `return 0` | `$?` / excepciones |
| Ayuda integrada | Comentarios propios | `Get-Help` |

---

# Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Las funciones suelen devolver texto. | Las funciones pueden devolver objetos completos. |
| Los parámetros se gestionan mediante variables especiales (`$1`, `$2`). | Los parámetros se definen explícitamente con `param()`. |
| La validación de datos debe programarse manualmente. | Dispone de validaciones integradas. |
| Es habitual utilizar funciones pequeñas para comandos repetitivos. | Se pueden crear módulos completos de administración. |

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

# Buenas prácticas

- Utiliza nombres descriptivos para las funciones.
- Una función debería realizar una única tarea.
- Evita funciones demasiado largas.
- Documenta qué parámetros recibe y qué devuelve.
- Valida los datos recibidos.
- Controla posibles errores dentro de la función.
- Reutiliza funciones comunes en lugar de duplicar código.
- En PowerShell, aprovecha las funciones avanzadas y los objetos.

---

[⬆️ Volver al índice](#índice)

## Parámetros

Los parámetros permiten que un script reciba información externa cuando se ejecuta, evitando tener que modificar el código cada vez que se necesite cambiar un valor.

A diferencia de la entrada de datos interactiva, los parámetros se proporcionan directamente al ejecutar el script.

Esto permite crear herramientas más profesionales y automatizadas.

Ejemplos de uso:

- Ejecutar un script contra diferentes equipos.
- Pasar rutas de archivos.
- Indicar usuarios o grupos.
- Seleccionar opciones de ejecución.
- Automatizar tareas mediante otras herramientas.

---

# Linux (Bash)

En Bash, los parámetros recibidos por un script se almacenan en variables especiales.

---

## Parámetros básicos

Ejemplo:

```bash
#!/bin/bash

echo "Primer parámetro: $1"
echo "Segundo parámetro: $2"
```

Ejecución:

```bash
./script.sh servidor01 admin
```

Salida:

```text
Primer parámetro: servidor01
Segundo parámetro: admin
```

---

## Variables especiales de parámetros

Bash proporciona varias variables predefinidas:

| Variable | Descripción |
|----------|-------------|
| `$0` | Nombre del script ejecutado |
| `$1` | Primer parámetro |
| `$2` | Segundo parámetro |
| `$3` | Tercer parámetro |
| `$@` | Todos los parámetros separados |
| `$*` | Todos los parámetros como una cadena |
| `$#` | Número de parámetros recibidos |

Ejemplo:

```bash
#!/bin/bash

echo "Script: $0"
echo "Número de parámetros: $#"
echo "Parámetros: $@"
```

---

## Comprobar parámetros obligatorios

Es recomendable validar que el usuario ha introducido todos los valores necesarios.

Ejemplo:

```bash
#!/bin/bash

if [ $# -lt 1 ]
then
    echo "Uso: $0 <servidor>"
    exit 1
fi

echo "Servidor recibido: $1"
```

Ejecución incorrecta:

```bash
./script.sh
```

Salida:

```text
Uso: ./script.sh <servidor>
```

---

## Desplazar parámetros

Bash permite mover los parámetros utilizando:

```bash
shift
```

Ejemplo:

```bash
#!/bin/bash

echo "Primero: $1"

shift

echo "Ahora: $1"
```

Esto elimina el primer parámetro y desplaza los siguientes.

---

# PowerShell

PowerShell utiliza una estructura más avanzada mediante:

```powershell
param()
```

Esto permite definir claramente qué parámetros recibe un script.

---

## Parámetros básicos

Ejemplo:

```powershell
param(
    $Equipo
)

Write-Host "Equipo recibido: $Equipo"
```

Ejecución:

```powershell
.\script.ps1 -Equipo PC01
```

Salida:

```text
Equipo recibido: PC01
```

---

## Definir varios parámetros

Ejemplo:

```powershell
param(
    $Equipo,
    $Usuario
)

Write-Host "Equipo: $Equipo"
Write-Host "Usuario: $Usuario"
```

Ejecución:

```powershell
.\script.ps1 -Equipo PC01 -Usuario admin
```

---

## Parámetros obligatorios

PowerShell permite indicar que un parámetro es obligatorio.

Ejemplo:

```powershell
param(
    [Parameter(Mandatory)]
    $Equipo
)

Write-Host "Equipo: $Equipo"
```

Si no se proporciona:

```powershell
.\script.ps1
```

PowerShell solicitará el valor automáticamente.

---

## Definir tipos de datos

PowerShell permite especificar el tipo esperado.

Ejemplo:

```powershell
param(
    [string]$Usuario,
    [int]$Numero
)
```

Tipos habituales:

| Tipo | Descripción |
|------|-------------|
| `[string]` | Texto |
| `[int]` | Número entero |
| `[bool]` | Verdadero/Falso |
| `[array]` | Lista de valores |
| `[datetime]` | Fecha y hora |

---

## Validación de parámetros

PowerShell permite validar valores antes de ejecutar el script.

Ejemplo:

```powershell
param(
    [ValidateSet("Inicio","Parada")]
    $Accion
)

Write-Host "Acción seleccionada: $Accion"
```

Valores permitidos:

```text
Inicio
Parada
```

---

## Ayuda integrada

Los scripts de PowerShell pueden documentarse utilizando comentarios especiales.

Ejemplo:

```powershell
<#
.SYNOPSIS
Obtiene información de un equipo.

.DESCRIPTION
Consulta datos básicos del sistema.
#>
```

Después:

```powershell
Get-Help .\script.ps1
```

---

# Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Primer parámetro | `$1` | Variable definida en `param()` |
| Todos los parámetros | `$@` | `$args` |
| Número de parámetros | `$#` | `$args.Count` |
| Parámetro obligatorio | Comprobación manual | `[Parameter(Mandatory)]` |
| Validar valores | Condiciones (`if`) | `ValidateSet`, `ValidatePattern` |
| Mostrar ayuda | Comentarios propios | `Get-Help` |

---

# Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Los parámetros se reciben mediante posiciones (`$1`, `$2`). | Los parámetros tienen nombres propios. |
| La validación debe programarse manualmente. | Dispone de validadores integrados. |
| Los scripts suelen ejecutarse pasando valores por posición. | Es habitual utilizar parámetros con nombre. |
| La documentación depende del desarrollador. | Puede integrarse con el sistema de ayuda de PowerShell. |

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

# Buenas prácticas

- Define claramente qué parámetros necesita el script.
- Utiliza nombres descriptivos.
- Valida siempre los valores recibidos.
- Indica ejemplos de uso en comentarios.
- Utiliza parámetros obligatorios cuando sean necesarios.
- Evita depender de valores escritos directamente dentro del código.
- Documenta los parámetros para facilitar el mantenimiento.

---

[⬆️ Volver al índice](#índice)

## Manejo de errores

El manejo de errores permite controlar qué ocurre cuando un script encuentra un problema durante su ejecución.

Un script sin control de errores puede:

- Detenerse inesperadamente.
- Generar resultados incorrectos.
- Continuar ejecutando acciones peligrosas.
- Dificultar la identificación del problema.

En administración de sistemas es especialmente importante controlar errores en tareas como:

- Copias de seguridad.
- Modificación de usuarios.
- Cambios de configuración.
- Ejecución remota.
- Automatizaciones programadas.

Un buen script debe ser capaz de:

- Detectar errores.
- Informar al administrador.
- Registrar lo ocurrido.
- Continuar o detenerse según la situación.

---

# Linux (Bash)

En Bash el control de errores se basa principalmente en:

- Códigos de salida.
- Variables especiales.
- Condiciones.
- Redirección de errores.

---

## Códigos de salida

Cada comando ejecutado devuelve un código indicando si terminó correctamente.

El código se almacena en:

```bash
$?
```

Ejemplo:

```bash
ls /tmp

echo $?
```

Si el comando funciona:

```text
0
```

Si ocurre un error:

```text
1
```

---

## Interpretación de códigos

| Código | Significado |
|--------|-------------|
| `0` | Ejecución correcta |
| `1` | Error general |
| `2` | Error de uso del comando |
| Otros valores | Error específico del programa |

---

## Comprobar errores mediante `if`

Ejemplo:

```bash
#!/bin/bash

mkdir /backup

if [ $? -eq 0 ]
then
    echo "Directorio creado correctamente"
else
    echo "Error al crear directorio"
fi
```

---

## Detener un script ante errores

Bash permite utilizar:

```bash
set -e
```

Esto hace que el script finalice automáticamente cuando un comando devuelve un error.

Ejemplo:

```bash
#!/bin/bash

set -e

rm /archivo_inexistente

echo "Continuando script"
```

En este caso, el segundo comando no llegará a ejecutarse.

---

## Registrar errores

Los errores pueden enviarse a un archivo mediante:

```bash
2>
```

Ejemplo:

```bash
ls /ruta_inexistente 2> errores.log
```

El mensaje de error se guardará en:

```text
errores.log
```

---

## Separar salida normal y errores

Ejemplo:

```bash
comando > salida.log 2> error.log
```

Resultado:

```text
salida.log  → información correcta
error.log   → errores encontrados
```

---

# PowerShell

PowerShell dispone de mecanismos más avanzados para controlar errores:

- Variables automáticas.
- Bloques `try/catch`.
- Parámetros de error.
- Excepciones.

---

## Variable `$?`

Indica si el último comando se ejecutó correctamente.

Ejemplo:

```powershell
Get-Process explorer

$?
```

Resultado:

```text
True
```

Si falla:

```text
False
```

---

## Variable `$LASTEXITCODE`

Al ejecutar comandos externos, PowerShell almacena el código de salida:

```powershell
$LASTEXITCODE
```

Ejemplo:

```powershell
ping servidor_inexistente

$LASTEXITCODE
```

---

## Try / Catch

La estructura recomendada en PowerShell es:

```powershell
try {

    comando

}
catch {

    gestión del error

}
```

Ejemplo:

```powershell
try {

    Get-Content C:\archivo.txt

}
catch {

    Write-Host "No se pudo leer el archivo"

}
```

---

## Finally

También existe:

```powershell
finally
```

que se ejecuta siempre, haya error o no.

Ejemplo:

```powershell
try {

    Write-Host "Ejecutando tarea"

}
catch {

    Write-Host "Error encontrado"

}
finally {

    Write-Host "Proceso finalizado"

}
```

---

## Controlar errores no terminantes

PowerShell diferencia entre errores terminantes y no terminantes.

Ejemplo:

```powershell
Get-ChildItem C:\RutaInexistente
```

Puede mostrar un error pero continuar ejecutándose.

Para forzar una excepción:

```powershell
Get-ChildItem C:\RutaInexistente -ErrorAction Stop
```

---

## ErrorAction

El parámetro:

```powershell
-ErrorAction
```

permite controlar cómo actuar ante errores.

Valores habituales:

| Valor | Acción |
|-------|--------|
| `Continue` | Muestra error y continúa |
| `Stop` | Detiene y genera excepción |
| `SilentlyContinue` | Oculta error |
| `Ignore` | Ignora completamente |

Ejemplo:

```powershell
Remove-Item C:\archivo.txt -ErrorAction Stop
```

---

## Registrar errores

PowerShell permite guardar errores:

```powershell
try {

    Get-Service ServicioIncorrecto

}
catch {

    $_ | Out-File errores.log

}
```

La variable:

```powershell
$_
```

contiene el error actual.

---

# Equivalencia

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Código de salida | `$?` | `$?` / `$LASTEXITCODE` |
| Detener ante error | `set -e` | `-ErrorAction Stop` |
| Capturar errores | `if` comprobando `$?` | `try/catch` |
| Guardar errores | `2> archivo.log` | `Out-File` |
| Mostrar último error | `$?` | `$Error[0]` |

---

# Diferencias

| Linux (Bash) | PowerShell |
|--------------|------------|
| Se basa principalmente en códigos numéricos de salida. | Utiliza excepciones y objetos de error. |
| El programador debe controlar manualmente muchos errores. | Dispone de herramientas integradas de gestión. |
| Los errores suelen enviarse a texto plano. | Los errores contienen propiedades detalladas. |
| Es común utilizar `$?` después de cada comando. | Se recomienda utilizar `try/catch`. |

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

# Buenas prácticas

- Controla siempre los posibles fallos.
- No ignores errores importantes.
- Utiliza mensajes claros para facilitar la resolución.
- Guarda registros de errores en tareas críticas.
- Utiliza códigos de salida adecuados.
- En PowerShell, utiliza `try/catch` para operaciones importantes.
- Prueba los scripts simulando situaciones de fallo.
- Evita mostrar información sensible en mensajes de error.

---

[⬆️ Volver al índice](#índice)

# Resumen de equivalencias

A continuación se muestra una recopilación de las principales equivalencias entre **Bash (Linux)** y **PowerShell (Windows)** relacionadas con scripting.

Aunque ambos lenguajes permiten automatizar tareas, existen diferencias importantes:

- Bash está orientado principalmente al uso de comandos y procesamiento de texto.
- PowerShell está basado en objetos y permite una administración más avanzada del sistema.

---

## Crear y ejecutar scripts

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Extensión del script | `.sh` | `.ps1` |
| Crear script | `nano script.sh` | `notepad script.ps1` |
| Indicar intérprete | `#!/bin/bash` | No requiere |
| Dar permisos | `chmod +x script.sh` | Política de ejecución |
| Ejecutar script | `./script.sh` | `.\script.ps1` |
| Ejecutar con intérprete | `bash script.sh` | `powershell.exe -File script.ps1` |

---

# Variables

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Crear variable | `nombre="valor"` | `$nombre="valor"` |
| Mostrar variable | `echo $nombre` | `$nombre` |
| Variable de entorno | `export VARIABLE=valor` | `$env:VARIABLE="valor"` |
| Ver variables | `env` | `Get-ChildItem Env:` |
| Usuario actual | `$USER` | `$env:USERNAME` |
| Equipo actual | `hostname` | `$env:COMPUTERNAME` |

---

# Entrada de datos

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Solicitar información | `read` | `Read-Host` |
| Mostrar mensaje | `read -p` | `Read-Host "mensaje"` |
| Entrada oculta | `read -s` | `Read-Host -AsSecureString` |

---

# Condicionales

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Condición | `if [ ]` | `if ()` |
| Segunda condición | `elif` | `elseif` |
| Alternativa | `else` | `else` |
| Comparación igual | `-eq` | `-eq` |
| Mayor que | `-gt` | `-gt` |
| Menor que | `-lt` | `-lt` |
| Varias condiciones | `&&` / `||` | `-and` / `-or` |
| Múltiples opciones | `case` | `switch` |

---

# Bucles

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Bucle contador | `for` | `for` |
| Recorrer elementos | `for item in` | `foreach` |
| Mientras condición | `while` | `while` |
| Ejecutar una vez antes de comprobar | `until` | `do while` |

---

# Funciones

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Crear función | `nombre_funcion()` | `function Nombre {}` |
| Pasar parámetros | `$1`, `$2` | `param()` |
| Ejecutar función | Nombre de función | Nombre de función |
| Devolver valores | `echo` / `return` | `return` |

---

# Parámetros

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Primer parámetro | `$1` | Parámetro definido |
| Segundo parámetro | `$2` | Parámetro definido |
| Todos los parámetros | `$@` | `$args` |
| Número de parámetros | `$#` | `$args.Count` |
| Parámetro obligatorio | Validación manual | `[Parameter(Mandatory)]` |
| Validar valores | `if` | `ValidateSet` |

---

# Manejo de errores

| Acción | Linux (Bash) | PowerShell |
|---------|-------------|------------|
| Estado del último comando | `$?` | `$?` |
| Código de salida | `$?` | `$LASTEXITCODE` |
| Detener ejecución | `set -e` | `-ErrorAction Stop` |
| Controlar errores | `if` | `try/catch` |
| Guardar errores | `2>` | `Out-File` |

---

# Conceptos clave

| Bash (Linux) | PowerShell |
|--------------|------------|
| Trabaja principalmente con texto. | Trabaja con objetos. |
| Usa comandos tradicionales del sistema. | Usa cmdlets. |
| Los scripts suelen encadenar comandos mediante tuberías. | El pipeline transmite objetos entre comandos. |
| La gestión de errores suele depender del programador. | Dispone de excepciones estructuradas. |
| Muy utilizado en servidores Linux. | Muy utilizado en entornos Windows empresariales. |

---

# Buenas prácticas comunes

Independientemente del lenguaje utilizado:

- Utiliza nombres claros para scripts, variables y funciones.
- Añade comentarios cuando el código no sea evidente.
- Valida siempre los datos recibidos.
- Controla los errores.
- Evita valores escritos directamente dentro del código.
- Guarda copias de scripts importantes.
- Prueba los cambios antes de utilizarlos en producción.
- Registra las acciones realizadas por scripts críticos.

---

# Ejemplo final

## Script de comprobación de conectividad

### Bash

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

Ejecución:

```bash
./ping.sh servidor01
```

---

### PowerShell

```powershell
param(
    $Servidor
)

if (Test-Connection $Servidor -Count 1 -Quiet) {

    Write-Host "$Servidor responde"

}
else {

    Write-Host "$Servidor no responde"

}
```

Ejecución:

```powershell
.\ping.ps1 -Servidor servidor01
```

---

[⬆️ Volver al índice](#índice)