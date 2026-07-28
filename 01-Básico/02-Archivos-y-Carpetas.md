# Archivos y carpetas

## Índice

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
- [Resumen de equivalencias](#resumen-de-equivalencias)

## Crear un archivo

### Linux

```bash
touch <nombre_archivo>
```

**Descripción**

Crea un archivo vacío. Si el archivo ya existe, actualiza su fecha y hora de modificación.

---

### PowerShell

```powershell
New-Item -Path <nombre_archivo> -ItemType File
```

**Descripción**

Crea un nuevo archivo vacío en la ubicación especificada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear un archivo | `touch` | `New-Item -ItemType File` |

---

### Ejemplos

**Crear un archivo en el directorio actual**

Linux

```bash
touch notas.txt
```

PowerShell

```powershell
New-Item -Path notas.txt -ItemType File
```

---

**Crear un archivo utilizando una ruta absoluta**

Linux

```bash
touch /home/usuario/notas.txt
```

PowerShell

```powershell
New-Item -Path C:\Users\usuario\notas.txt -ItemType File
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `touch` también actualiza la fecha de modificación si el archivo ya existe. | `New-Item` devuelve un error si el archivo ya existe, salvo que se utilice el parámetro `-Force`. |

---

### Buenas prácticas

- Utiliza nombres descriptivos para los archivos.
- Comprueba que el archivo no exista antes de crearlo si no deseas sobrescribir información.
- En scripts, utiliza rutas absolutas para evitar errores de ubicación.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Mover archivos](#mover-archivos)
- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Copiar archivos

### Linux

```bash
cp <origen> <destino>
```

**Descripción**

Copia uno o varios archivos desde una ubicación a otra.

---

### PowerShell

```powershell
Copy-Item -Path <origen> -Destination <destino>
```

**Descripción**

Copia uno o varios archivos desde una ubicación a otra.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Copiar archivos | `cp` | `Copy-Item` |

---

### Ejemplos

**Copiar un archivo en el mismo directorio**

Linux

```bash
cp notas.txt copia_notas.txt
```

PowerShell

```powershell
Copy-Item -Path notas.txt -Destination copia_notas.txt
```

---

**Copiar un archivo a otro directorio**

Linux

```bash
cp notas.txt /home/usuario/Documentos
```

PowerShell

```powershell
Copy-Item -Path notas.txt -Destination C:\Users\usuario\Documents
```

---

**Sobrescribir un archivo existente**

Linux

```bash
cp -f notas.txt copia_notas.txt
```

PowerShell

```powershell
Copy-Item -Path notas.txt -Destination copia_notas.txt -Force
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Utiliza `cp` para copiar archivos y directorios. | Utiliza el cmdlet `Copy-Item`. |
| La sobrescritura puede forzarse con `-f`. | La sobrescritura puede realizarse con `-Force`. |

---

### Buenas prácticas

- Verifica el archivo de destino antes de sobrescribirlo.
- Utiliza rutas absolutas cuando trabajes en scripts.
- Comprueba que la copia se ha realizado correctamente.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Mover archivos](#mover-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Mover archivos

### Linux

```bash
mv <origen> <destino>
```

**Descripción**

Mueve un archivo de una ubicación a otra. También puede utilizarse para renombrar archivos.

---

### PowerShell

```powershell
Move-Item -Path <origen> -Destination <destino>
```

**Descripción**

Mueve uno o varios archivos entre directorios. También permite cambiar el nombre de un archivo.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mover archivos | `mv` | `Move-Item` |

---

### Ejemplos

**Mover un archivo a otro directorio**

Linux

```bash
mv notas.txt /home/usuario/Documentos
```

PowerShell

```powershell
Move-Item -Path notas.txt -Destination C:\Users\usuario\Documents
```

---

**Mover y renombrar un archivo**

Linux

```bash
mv notas.txt informe.txt
```

PowerShell

```powershell
Move-Item -Path notas.txt -Destination informe.txt
```

---

**Mover un archivo utilizando una ruta absoluta**

Linux

```bash
mv /home/usuario/notas.txt /home/usuario/Documentos
```

PowerShell

```powershell
Move-Item -Path C:\Users\usuario\notas.txt -Destination C:\Users\usuario\Documents
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `mv` mueve y renombra archivos con el mismo comando. | `Move-Item` también permite mover y renombrar archivos utilizando el parámetro `-Destination`. |
| Si el destino existe, el comportamiento depende del sistema y los permisos. | Puede utilizarse `-Force` para sobrescribir cuando sea necesario. |

---

### Buenas prácticas

- Comprueba que el archivo de destino no exista antes de sobrescribirlo.
- Utiliza rutas absolutas en scripts para evitar errores.
- Verifica que el archivo se ha movido correctamente antes de eliminar la copia original.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Renombrar archivos](#renombrar-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Renombrar archivos

### Linux

```bash
mv <nombre_actual> <nuevo_nombre>
```

**Descripción**

Cambia el nombre de un archivo sin modificar su contenido.

---

### PowerShell

```powershell
Rename-Item -Path <nombre_actual> -NewName <nuevo_nombre>
```

**Descripción**

Cambia el nombre de un archivo manteniéndolo en la misma ubicación.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Renombrar archivos | `mv` | `Rename-Item` |

---

### Ejemplos

**Renombrar un archivo**

Linux

```bash
mv notas.txt informe.txt
```

PowerShell

```powershell
Rename-Item -Path notas.txt -NewName informe.txt
```

---

**Renombrar un archivo utilizando una ruta absoluta**

Linux

```bash
mv /home/usuario/Documentos/notas.txt /home/usuario/Documentos/informe.txt
```

PowerShell

```powershell
Rename-Item -Path C:\Users\usuario\Documents\notas.txt -NewName informe.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Se utiliza `mv`, ya que renombrar es equivalente a mover el archivo con otro nombre dentro del mismo directorio. | Existe un cmdlet específico (`Rename-Item`) cuya única función es cambiar el nombre del archivo. |
| Puede utilizarse también para mover archivos entre directorios. | Solo cambia el nombre; no mueve el archivo de ubicación. |

---

### Buenas prácticas

- Utiliza nombres descriptivos y fáciles de identificar.
- Evita caracteres especiales que puedan causar problemas de compatibilidad entre sistemas.
- Comprueba que el nuevo nombre no exista para evitar conflictos.

---

### Comandos relacionados

- [Mover archivos](#mover-archivos)
- [Copiar archivos](#copiar-archivos)
- [Eliminar archivos](#eliminar-archivos)

---

[⬆️ Volver al índice](#índice)

## Eliminar archivos

### Linux

```bash
rm <archivo>
```

**Descripción**

Elimina uno o varios archivos del sistema de archivos.

---

### PowerShell

```powershell
Remove-Item -Path <archivo>
```

**Descripción**

Elimina uno o varios archivos de la ubicación especificada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar archivos | `rm` | `Remove-Item` |

---

### Ejemplos

**Eliminar un archivo**

Linux

```bash
rm notas.txt
```

PowerShell

```powershell
Remove-Item -Path notas.txt
```

---

**Eliminar varios archivos**

Linux

```bash
rm notas.txt informe.txt copia_notas.txt
```

PowerShell

```powershell
Remove-Item notas.txt, informe.txt, copia_notas.txt
```

---

**Eliminar un archivo utilizando una ruta absoluta**

Linux

```bash
rm /home/usuario/Documentos/notas.txt
```

PowerShell

```powershell
Remove-Item -Path C:\Users\usuario\Documents\notas.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `rm` elimina archivos de forma permanente. | `Remove-Item` elimina archivos y otros elementos del sistema de archivos. |
| Puede solicitar confirmación según la configuración o los parámetros utilizados. | Puede utilizarse `-Confirm` para solicitar confirmación antes de eliminar. |

---

### Buenas prácticas

- Comprueba siempre que estás eliminando el archivo correcto.
- Utiliza rutas absolutas cuando trabajes en scripts.
- Evita ejecutar comandos de eliminación con privilegios elevados si no es necesario.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Copiar archivos](#copiar-archivos)
- [Mover archivos](#mover-archivos)
- [Renombrar archivos](#renombrar-archivos)

---

[⬆️ Volver al índice](#índice)

## Eliminar directorios con contenido

### Linux

```bash
rm -r <directorio>
```

**Descripción**

Elimina un directorio y todo su contenido, incluidos los archivos y subdirectorios.

---

### PowerShell

```powershell
Remove-Item -Path <directorio> -Recurse
```

**Descripción**

Elimina un directorio junto con todos los archivos y subdirectorios que contiene.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar un directorio con contenido | `rm -r` | `Remove-Item -Recurse` |

---

### Ejemplos

**Eliminar un directorio con todo su contenido**

Linux

```bash
rm -r Proyecto
```

PowerShell

```powershell
Remove-Item -Path Proyecto -Recurse
```

---

**Forzar la eliminación sin confirmación**

Linux

```bash
rm -rf Proyecto
```

PowerShell

```powershell
Remove-Item -Path Proyecto -Recurse -Force
```

---

**Eliminar un directorio utilizando una ruta absoluta**

Linux

```bash
rm -r /home/usuario/Proyecto
```

PowerShell

```powershell
Remove-Item -Path C:\Users\usuario\Proyecto -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `-r` elimina el directorio y todo su contenido. | `-Recurse` elimina el directorio y todos sus elementos. |
| `-f` fuerza la eliminación sin solicitar confirmación. | `-Force` permite eliminar elementos ocultos o de solo lectura cuando sea posible. |

---

### Buenas prácticas

- Verifica siempre el contenido del directorio antes de eliminarlo.
- Evita utilizar `rm -rf` o `Remove-Item -Recurse -Force` si no estás completamente seguro del objetivo.
- Comprueba la ruta dos veces cuando utilices rutas absolutas.
- En scripts, registra las operaciones de eliminación si afectan a información importante.

---

### Comandos relacionados

- [Eliminar archivos](#eliminar-archivos)
- [Crear directorios](#crear-directorios)
- [Mover directorios](#mover-directorios)

---

[⬆️ Volver al índice](#índice)

## Ver el contenido de un archivo

### Linux

```bash
cat <archivo>
```

**Descripción**

Muestra el contenido completo de un archivo en la terminal.

---

### PowerShell

```powershell
Get-Content -Path <archivo>
```

**Descripción**

Muestra el contenido completo de un archivo en la consola.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver el contenido de un archivo | `cat` | `Get-Content` |

---

### Ejemplos

**Mostrar el contenido de un archivo**

Linux

```bash
cat notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt
```

---

**Mostrar el contenido de un archivo utilizando una ruta absoluta**

Linux

```bash
cat /home/usuario/Documentos/notas.txt
```

PowerShell

```powershell
Get-Content -Path C:\Users\usuario\Documents\notas.txt
```

---

**Mostrar el contenido de varios archivos**

Linux

```bash
cat notas.txt informe.txt
```

PowerShell

```powershell
Get-Content notas.txt, informe.txt
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `cat` muestra el contenido como texto plano. | `Get-Content` devuelve cada línea como un objeto de tipo `String`. |
| También puede utilizarse para concatenar archivos. | Está orientado principalmente a la lectura del contenido de archivos. |

---

### Buenas prácticas

- Utiliza este comando para visualizar archivos de texto pequeños o medianos.
- Para archivos muy grandes, es recomendable utilizar comandos específicos como `less`, `head` o `tail` en Linux, o `Get-Content` con parámetros adecuados en PowerShell.
- Comprueba que el archivo existe antes de intentar visualizar su contenido.

---

### Comandos relacionados

- [Ver el principio de un archivo](#ver-el-principio-de-un-archivo)
- [Ver el final de un archivo](#ver-el-final-de-un-archivo)
- [Crear un archivo](#crear-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Ver el principio de un archivo

### Linux

```bash
head <archivo>
```

**Descripción**

Muestra las primeras líneas de un archivo. Por defecto, muestra las primeras **10 líneas**.

---

### PowerShell

```powershell
Get-Content -Path <archivo> -TotalCount 10
```

**Descripción**

Muestra las primeras líneas de un archivo. El número de líneas puede modificarse mediante el parámetro `-TotalCount`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver el principio de un archivo | `head` | `Get-Content -TotalCount` |

---

### Ejemplos

**Mostrar las primeras 10 líneas**

Linux

```bash
head notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt -TotalCount 10
```

---

**Mostrar las primeras 5 líneas**

Linux

```bash
head -n 5 notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt -TotalCount 5
```

---

**Mostrar las primeras líneas utilizando una ruta absoluta**

Linux

```bash
head /home/usuario/Documentos/notas.txt
```

PowerShell

```powershell
Get-Content -Path C:\Users\usuario\Documents\notas.txt -TotalCount 10
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `head` muestra las primeras líneas de un archivo. | `Get-Content` utiliza el parámetro `-TotalCount` para limitar el número de líneas mostradas. |
| El número de líneas se modifica con `-n`. | El número de líneas se modifica con `-TotalCount`. |

---

### Buenas prácticas

- Utiliza este comando para revisar rápidamente archivos de configuración o registros.
- Reduce el número de líneas mostradas cuando solo necesites comprobar el encabezado del archivo.
- Es especialmente útil con archivos de gran tamaño.

---

### Comandos relacionados

- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)
- [Ver el final de un archivo](#ver-el-final-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Ver el final de un archivo

### Linux

```bash
tail <archivo>
```

**Descripción**

Muestra las últimas líneas de un archivo. Por defecto, muestra las últimas **10 líneas**.

---

### PowerShell

```powershell
Get-Content -Path <archivo> -Tail 10
```

**Descripción**

Muestra las últimas líneas de un archivo. El número de líneas puede modificarse mediante el parámetro `-Tail`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver el final de un archivo | `tail` | `Get-Content -Tail` |

---

### Ejemplos

**Mostrar las últimas 10 líneas**

Linux

```bash
tail notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt -Tail 10
```

---

**Mostrar las últimas 5 líneas**

Linux

```bash
tail -n 5 notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt -Tail 5
```

---

**Monitorizar un archivo en tiempo real**

Linux

```bash
tail -f notas.txt
```

PowerShell

```powershell
Get-Content -Path notas.txt -Tail 10 -Wait
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `tail` muestra las últimas líneas de un archivo. | `Get-Content` utiliza el parámetro `-Tail` para mostrar las últimas líneas. |
| `tail -f` permite seguir el crecimiento del archivo en tiempo real. | `Get-Content -Wait` actualiza la salida conforme el archivo recibe nuevas líneas. |

---

### Buenas prácticas

- Utiliza este comando para revisar registros (logs) sin necesidad de abrir el archivo completo.
- Combina `-Tail` con `-Wait` para monitorizar archivos que cambian continuamente.
- Es especialmente útil para analizar logs de aplicaciones, servicios o servidores.

---

### Comandos relacionados

- [Ver el contenido de un archivo](#ver-el-contenido-de-un-archivo)
- [Ver el principio de un archivo](#ver-el-principio-de-un-archivo)

---

[⬆️ Volver al índice](#índice)

## Crear varios archivos

### Linux

```bash
touch <archivo1> <archivo2> <archivo3>
```

**Descripción**

Crea varios archivos vacíos mediante un único comando.

---

### PowerShell

```powershell
New-Item archivo1.txt, archivo2.txt, archivo3.txt -ItemType File
```

**Descripción**

Crea varios archivos vacíos en una sola ejecución del comando.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Crear varios archivos | `touch archivo1 archivo2 archivo3` | `New-Item archivo1, archivo2, archivo3 -ItemType File` |

---

### Ejemplos

**Crear varios archivos en el directorio actual**

Linux

```bash
touch notas.txt informe.txt copia_notas.txt
```

PowerShell

```powershell
New-Item notas.txt, informe.txt, copia_notas.txt -ItemType File
```

---

**Crear varios archivos utilizando una ruta absoluta**

Linux

```bash
touch /home/usuario/Documentos/notas.txt \
      /home/usuario/Documentos/informe.txt \
      /home/usuario/Documentos/copia_notas.txt
```

PowerShell

```powershell
New-Item `
"C:\Users\usuario\Documents\notas.txt",
"C:\Users\usuario\Documents\informe.txt",
"C:\Users\usuario\Documents\copia_notas.txt" `
-ItemType File
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `touch` permite crear múltiples archivos separando sus nombres por espacios. | `New-Item` acepta varios archivos separados por comas. |
| Si el archivo ya existe, `touch` actualiza su fecha de modificación. | `New-Item` genera un error si el archivo ya existe, salvo que se utilice `-Force`. |

---

### Buenas prácticas

- Aprovecha esta técnica cuando necesites preparar rápidamente una estructura de trabajo.
- Utiliza nombres descriptivos para facilitar la organización de los archivos.
- Comprueba previamente que los archivos no existan si no deseas sobrescribirlos.

---

### Comandos relacionados

- [Crear un archivo](#crear-un-archivo)
- [Copiar archivos](#copiar-archivos)
- [Renombrar archivos](#renombrar-archivos)

---

[⬆️ Volver al índice](#índice)

## Copiar directorios

### Linux

```bash
cp -r <origen> <destino>
```

**Descripción**

Copia un directorio junto con todos los archivos y subdirectorios que contiene.

---

### PowerShell

```powershell
Copy-Item -Path <origen> -Destination <destino> -Recurse
```

**Descripción**

Copia un directorio completo junto con todo su contenido.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Copiar un directorio | `cp -r` | `Copy-Item -Recurse` |

---

### Ejemplos

**Copiar un directorio en la misma ubicación**

Linux

```bash
cp -r Proyecto Proyecto_Backup
```

PowerShell

```powershell
Copy-Item -Path Proyecto -Destination Proyecto_Backup -Recurse
```

---

**Copiar un directorio a otra ubicación**

Linux

```bash
cp -r Proyecto /home/usuario/Backups
```

PowerShell

```powershell
Copy-Item -Path Proyecto -Destination C:\Backups -Recurse
```

---

**Copiar un directorio utilizando una ruta absoluta**

Linux

```bash
cp -r /home/usuario/Proyecto /home/usuario/Backups
```

PowerShell

```powershell
Copy-Item -Path C:\Users\usuario\Proyecto -Destination C:\Backups -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Es necesario utilizar `-r` (o `-R`) para copiar directorios. | Es necesario utilizar el parámetro `-Recurse` para copiar todo el contenido del directorio. |
| Sin `-r`, `cp` solo copia archivos. | Sin `-Recurse`, `Copy-Item` no copiará correctamente el contenido del directorio. |

---

### Buenas prácticas

- Comprueba que el directorio de destino dispone de espacio suficiente.
- Verifica que la copia se ha completado correctamente antes de eliminar el directorio original.
- Utiliza rutas absolutas cuando automatices copias en scripts.

---

### Comandos relacionados

- [Copiar archivos](#copiar-archivos)
- [Mover directorios](#mover-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)

## Mover directorios

### Linux

```bash
mv <origen> <destino>
```

**Descripción**

Mueve un directorio completo, incluyendo todos los archivos y subdirectorios que contiene.

---

### PowerShell

```powershell
Move-Item -Path <origen> -Destination <destino>
```

**Descripción**

Mueve un directorio completo junto con todo su contenido a otra ubicación.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mover un directorio | `mv` | `Move-Item` |

---

### Ejemplos

**Mover un directorio a otra ubicación**

Linux

```bash
mv Proyecto /home/usuario/Backups
```

PowerShell

```powershell
Move-Item -Path Proyecto -Destination C:\Backups
```

---

**Mover un directorio utilizando una ruta absoluta**

Linux

```bash
mv /home/usuario/Proyecto /home/usuario/Backups
```

PowerShell

```powershell
Move-Item -Path C:\Users\usuario\Proyecto -Destination C:\Backups
```

---

**Mover un directorio y cambiar su nombre**

Linux

```bash
mv Proyecto Proyecto_Backup
```

PowerShell

```powershell
Move-Item -Path Proyecto -Destination Proyecto_Backup
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `mv` mueve y renombra directorios con el mismo comando. | `Move-Item` también permite mover y renombrar directorios utilizando `-Destination`. |
| No requiere parámetros adicionales para mover directorios. | El comportamiento es equivalente y tampoco requiere parámetros adicionales. |

---

### Buenas prácticas

- Comprueba que el directorio de destino existe antes de mover información importante.
- Verifica que ningún archivo esté siendo utilizado por otra aplicación.
- Utiliza rutas absolutas cuando automatices movimientos de directorios en scripts.

---

### Comandos relacionados

- [Copiar directorios](#copiar-directorios)
- [Renombrar directorios](#renombrar-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)

## Renombrar directorios

### Linux

```bash
mv <nombre_actual> <nuevo_nombre>
```

**Descripción**

Cambia el nombre de un directorio sin modificar su ubicación ni su contenido.

---

### PowerShell

```powershell
Rename-Item -Path <nombre_actual> -NewName <nuevo_nombre>
```

**Descripción**

Cambia el nombre de un directorio manteniéndolo en la misma ubicación.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Renombrar directorios | `mv` | `Rename-Item` |

---

### Ejemplos

**Renombrar un directorio**

Linux

```bash
mv Proyecto Proyecto_Backup
```

PowerShell

```powershell
Rename-Item -Path Proyecto -NewName Proyecto_Backup
```

---

**Renombrar un directorio utilizando una ruta absoluta**

Linux

```bash
mv /home/usuario/Proyecto /home/usuario/Proyecto_Backup
```

PowerShell

```powershell
Rename-Item -Path C:\Users\usuario\Proyecto -NewName Proyecto_Backup
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `mv` utiliza el mismo comando para mover y renombrar directorios. | `Rename-Item` está diseñado específicamente para cambiar el nombre de un elemento. |
| Puede mover el directorio a otra ubicación al mismo tiempo. | Solo cambia el nombre; para mover un directorio debe utilizarse `Move-Item`. |

---

### Buenas prácticas

- Utiliza nombres descriptivos y coherentes para facilitar la organización.
- Comprueba que el nuevo nombre no exista previamente.
- Evita utilizar caracteres especiales o nombres excesivamente largos.

---

### Comandos relacionados

- [Mover directorios](#mover-directorios)
- [Copiar directorios](#copiar-directorios)
- [Eliminar directorios con contenido](#eliminar-directorios-con-contenido)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Crear un archivo | `touch` | `New-Item -ItemType File` |
| Copiar archivos | `cp` | `Copy-Item` |
| Mover archivos | `mv` | `Move-Item` |
| Renombrar archivos | `mv` | `Rename-Item` |
| Eliminar archivos | `rm` | `Remove-Item` |
| Eliminar directorios con contenido | `rm -r` | `Remove-Item -Recurse` |
| Ver el contenido de un archivo | `cat` | `Get-Content` |
| Ver el principio de un archivo | `head` | `Get-Content -TotalCount` |
| Ver el final de un archivo | `tail` | `Get-Content -Tail` |
| Crear varios archivos | `touch archivo1 archivo2 ...` | `New-Item archivo1, archivo2 -ItemType File` |
| Copiar directorios | `cp -r` | `Copy-Item -Recurse` |
| Mover directorios | `mv` | `Move-Item` |
| Renombrar directorios | `mv` | `Rename-Item` |

---

### Buenas prácticas generales

- Utiliza siempre rutas absolutas en scripts siempre que sea posible.
- Comprueba la existencia de archivos y directorios antes de copiarlos, moverlos o eliminarlos.
- Evita utilizar comandos de eliminación (`rm`, `Remove-Item`) sin verificar previamente la ruta de destino.
- Aprovecha el autocompletado con la tecla **Tab** para reducir errores al escribir rutas y nombres de archivos.
- Utiliza nombres descriptivos para archivos y directorios.
- Cuando trabajes con información importante, realiza una copia de seguridad antes de modificar o eliminar datos.

---

[⬆️ Volver al índice](#índice)