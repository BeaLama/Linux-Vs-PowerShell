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

### Linux

```bash
pwd
```

**Descripción**

Muestra la ruta del directorio de trabajo actual.

---

### PowerShell

```powershell
Get-Location
```

**Descripción**

Muestra la ubicación actual desde la que se está trabajando.

También puede utilizarse el alias:

```powershell
pwd
```

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar el directorio actual | `pwd` | `Get-Location` (`pwd`) |

---

### Ejemplo

**Linux**

```bash
pwd
```

Salida:

```text
/home/usuario/Documentos
```

**PowerShell**

```powershell
Get-Location
```

Salida:

```text
Path
----
C:\Users\usuario\Documents
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Devuelve una ruta en formato texto. | Devuelve un objeto cuya propiedad principal es `Path`. |

---

### Buenas prácticas

- Comprueba siempre tu ubicación antes de ejecutar comandos que modifiquen o eliminen archivos.
- En scripts, utiliza rutas absolutas cuando sea posible para evitar errores de ejecución.

---

[⬆️ Volver al índice](#índice)

## Cambiar de directorio

### Linux

```bash
cd <ruta>
```

**Descripción**

Cambia el directorio de trabajo actual al indicado.

---

### PowerShell

```powershell
Set-Location <ruta>
```

**Descripción**

Cambia la ubicación actual al directorio especificado.

También puede utilizarse el alias:

```powershell
cd <ruta>
```

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Cambiar de directorio | `cd` | `Set-Location` (`cd`) |

---

### Ejemplos

**Cambiar a un directorio específico**

Linux

```bash
cd /etc
```

PowerShell

```powershell
Set-Location C:\Windows
```

---

**Ir al directorio anterior**

Linux

```bash
cd ..
```

PowerShell

```powershell
cd ..
```

---

**Retroceder dos niveles**

Linux

```bash
cd ../..
```

PowerShell

```powershell
cd ../..
```

---

**Ir al directorio raíz**

Linux

```bash
cd /
```

PowerShell

```powershell
cd C:\
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| El comando principal es `cd`. | El cmdlet oficial es `Set-Location`, aunque `cd` es un alias. |
| La raíz del sistema es `/`. | Cada unidad tiene su propia raíz (`C:\`, `D:\`, etc.). |

---

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

### Linux

```bash
cd ..
```

**Descripción**

Cambia al directorio inmediatamente superior al actual.

---

### PowerShell

```powershell
Set-Location ..
```

**Descripción**

Cambia al directorio anterior de la ubicación actual.

También puede utilizarse el alias:

```powershell
cd ..
```

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Volver al directorio anterior (padre) | `cd ..` | `Set-Location ..` (`cd ..`) |

---

### Ejemplos

**Subir un nivel**

Linux

```bash
cd ..
```

PowerShell

```powershell
cd ..
```

---

**Subir dos niveles**

Linux

```bash
cd ../..
```

PowerShell

```powershell
cd ../..
```

---

**Subir tres niveles**

Linux

```bash
cd ../../..
```

PowerShell

```powershell
cd ../../..
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza `..` para representar el directorio padre. | Utiliza la misma sintaxis (`..`). |

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

### Linux

```bash
cd ~
```

o simplemente:

```bash
cd
```

**Descripción**

Cambia al directorio personal del usuario actual.

---

### PowerShell

```powershell
Set-Location ~
```

También puede utilizarse:

```powershell
cd ~
```

o

```powershell
cd $HOME
```

**Descripción**

Cambia al directorio personal del usuario actual.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ir al directorio personal | `cd ~` | `Set-Location ~` (`cd ~`) |

---

### Ejemplos

**Ir al directorio personal**

Linux

```bash
cd ~
```

PowerShell

```powershell
cd ~
```

---

**Utilizando la variable HOME**

Linux

```bash
cd $HOME
```

PowerShell

```powershell
cd $HOME
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `~` y `$HOME` apuntan al directorio personal del usuario. | También admite `~` y la variable `$HOME`, que resuelve la ruta del perfil del usuario. |

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

### Linux

```bash
ls
```

**Descripción**

Muestra el contenido del directorio actual.

---

### PowerShell

```powershell
Get-ChildItem
```

También puede utilizarse el alias:

```powershell
ls
```

**Descripción**

Muestra los archivos y directorios del directorio actual.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar el contenido de un directorio | `ls` | `Get-ChildItem` (`ls`) |

---

### Ejemplos

**Listar el contenido del directorio actual**

Linux

```bash
ls
```

PowerShell

```powershell
Get-ChildItem
```

---

**Listar el contenido de un directorio específico**

Linux

```bash
ls /etc
```

PowerShell

```powershell
Get-ChildItem C:\Windows
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Devuelve una lista en formato texto. | Devuelve objetos que representan archivos y carpetas. |
| La información mostrada depende de las opciones utilizadas. | Permite acceder directamente a propiedades como `Name`, `Length` o `LastWriteTime`. |

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

### Linux

```bash
ls -l
```

**Descripción**

Muestra el contenido del directorio junto con información adicional de cada archivo y carpeta.

---

### PowerShell

```powershell
Get-ChildItem | Format-Table Mode, LastWriteTime, Length, Name
```

**Descripción**

Muestra los elementos del directorio actual con información detallada como permisos, fecha de modificación, tamaño y nombre.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Listar información detallada | `ls -l` | `Get-ChildItem \| Format-Table Mode, LastWriteTime, Length, Name` |

---

### Ejemplos

**Listar información detallada del directorio actual**

Linux

```bash
ls -l
```

PowerShell

```powershell
Get-ChildItem | Format-Table Mode, LastWriteTime, Length, Name
```

---

**Listar información detallada de otro directorio**

Linux

```bash
ls -l /etc
```

PowerShell

```powershell
Get-ChildItem C:\Windows |
Format-Table Mode, LastWriteTime, Length, Name
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `ls -l` muestra una lista detallada en formato texto. | `Get-ChildItem` devuelve objetos y `Format-Table` controla únicamente la forma en la que se presentan. |
| La información está limitada a las columnas que muestra `ls`. | Los objetos contienen muchas más propiedades accesibles mediante `Select-Object` o `Get-Member`. |

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

### Linux

```bash
ls -la
```

**Descripción**

Muestra todos los archivos y directorios, incluidos los ocultos.

En Linux, los archivos ocultos son aquellos cuyo nombre comienza por un punto (`.`).

---

### PowerShell

```powershell
Get-ChildItem -Force
```

**Descripción**

Muestra todos los archivos y directorios, incluidos los elementos ocultos y del sistema.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar archivos ocultos | `ls -la` | `Get-ChildItem -Force` |

---

### Ejemplos

**Mostrar archivos ocultos del directorio actual**

Linux

```bash
ls -la
```

PowerShell

```powershell
Get-ChildItem -Force
```

---

**Mostrar archivos ocultos de otro directorio**

Linux

```bash
ls -la /etc
```

PowerShell

```powershell
Get-ChildItem C:\Windows -Force
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los archivos ocultos comienzan por un punto (`.`). | Los archivos ocultos utilizan atributos del sistema (`Hidden`, `System`, etc.). |
| `-a` muestra todos los archivos y `-l` añade información detallada. | `-Force` muestra los elementos ocultos y del sistema sin necesidad de opciones adicionales. |

---

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

### Linux

```bash
mkdir <nombre_directorio>
```

**Descripción**

Crea un nuevo directorio en la ubicación actual o en la ruta especificada.

---

### PowerShell

```powershell
New-Item -Path <nombre_directorio> -ItemType Directory
```

También puede utilizarse el alias:

```powershell
mkdir <nombre_directorio>
```

**Descripción**

Crea un nuevo directorio en la ubicación indicada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un directorio | `mkdir` | `New-Item -ItemType Directory` (`mkdir`) |

---

### Ejemplos

**Crear un directorio en la ubicación actual**

Linux

```bash
mkdir Proyecto
```

PowerShell

```powershell
New-Item -Path Proyecto -ItemType Directory
```

---

**Crear varios directorios**

Linux

```bash
mkdir Docs Scripts Backups
```

PowerShell

```powershell
New-Item Docs -ItemType Directory
New-Item Scripts -ItemType Directory
New-Item Backups -ItemType Directory
```

---

**Crear un directorio en una ruta específica**

Linux

```bash
mkdir /home/usuario/Proyecto
```

PowerShell

```powershell
New-Item -Path C:\Users\usuario\Proyecto -ItemType Directory
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `mkdir` es el comando principal para crear directorios. | El cmdlet oficial es `New-Item`, aunque `mkdir` es un alias. |
| Permite crear varios directorios en un único comando. | Habitualmente se crea un directorio por comando, aunque puede automatizarse fácilmente. |

---

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

### Linux

```bash
cd /ruta/completa
```

**Descripción**

Permite acceder a un directorio indicando la ruta completa desde la raíz del sistema de archivos.

---

### PowerShell

```powershell
Set-Location C:\ruta\completa
```

También puede utilizarse el alias:

```powershell
cd C:\ruta\completa
```

**Descripción**

Permite cambiar directamente a un directorio indicando su ruta completa.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Navegar utilizando una ruta absoluta | `cd /ruta/completa` | `Set-Location C:\ruta\completa` |

---

### Ejemplos

**Acceder al directorio de configuración**

Linux

```bash
cd /etc
```

PowerShell

```powershell
Set-Location C:\Windows
```

---

**Acceder al directorio de un usuario**

Linux

```bash
cd /home/usuario/Documentos
```

PowerShell

```powershell
Set-Location C:\Users\usuario\Documents
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La ruta comienza siempre por `/`. | La ruta comienza por la unidad correspondiente (`C:\`, `D:\`, etc.). |
| Existe una única raíz del sistema de archivos. | Cada unidad dispone de su propia raíz. |

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

### Linux

```bash
cd <ruta_relativa>
```

**Descripción**

Permite desplazarse entre directorios utilizando la ubicación actual como punto de referencia, sin necesidad de indicar la ruta completa.

---

### PowerShell

```powershell
Set-Location <ruta_relativa>
```

También puede utilizarse el alias:

```powershell
cd <ruta_relativa>
```

**Descripción**

Permite cambiar de directorio utilizando una ruta relativa respecto a la ubicación actual.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Navegar utilizando una ruta relativa | `cd <ruta_relativa>` | `Set-Location <ruta_relativa>` |

---

### Ejemplos

**Acceder a un subdirectorio**

Linux

```bash
cd Documentos
```

PowerShell

```powershell
Set-Location Documentos
```

---

**Retroceder un nivel**

Linux

```bash
cd ..
```

PowerShell

```powershell
Set-Location ..
```

---

**Retroceder dos niveles**

Linux

```bash
cd ../..
```

PowerShell

```powershell
Set-Location ../..
```

---

**Acceder a un directorio hermano**

Linux

```bash
cd ../Descargas
```

PowerShell

```powershell
Set-Location ..\Descargas
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza `/` como separador de directorios. | Utiliza `\` como separador de directorios (aunque PowerShell también acepta `/` en la mayoría de los casos). |
| Las rutas relativas parten del directorio actual. | Funcionan del mismo modo, tomando como referencia la ubicación actual. |

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

## Historial de comandos

### Linux

```bash
history
```

**Descripción**

Muestra el historial de comandos ejecutados por el usuario en la terminal.

---

### PowerShell

```powershell
Get-History
```

**Descripción**

Muestra el historial de comandos ejecutados durante la sesión actual de PowerShell.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar el historial de comandos | `history` | `Get-History` |

---

### Ejemplos

**Mostrar el historial completo**

Linux

```bash
history
```

PowerShell

```powershell
Get-History
```

---

**Mostrar los últimos 10 comandos**

Linux

```bash
history | tail -10
```

PowerShell

```powershell
Get-History -Count 10
```

---

**Buscar un comando en el historial**

Linux

```bash
history | grep ssh
```

PowerShell

```powershell
Get-History | Where-Object CommandLine -Match "ssh"
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| El historial se almacena en un archivo (normalmente `~/.bash_history`). | `Get-History` muestra únicamente el historial de la sesión actual. |
| Puede consultarse incluso después de cerrar la terminal. | El historial persistente depende de la configuración de PSReadLine. |

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