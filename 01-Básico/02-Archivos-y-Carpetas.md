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
- [Resumen de equivalencias](#resumen-de-equivalencias)

## Crear un archivo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `touch <nombre_archivo>` | `New-Item -Path <nombre_archivo> -ItemType File` |
| **Ejemplo** | `touch /home/usuario/notas.txt` | `New-Item -Path C:\Users\usuario\notas.txt -ItemType File` |

> 💡 **Diferencia clave** — 🐧 `touch` también actualiza la fecha de modificación si el archivo ya existe. · 🪟 `New-Item` devuelve un error si el archivo ya existe, salvo que se utilice el parámetro `-Force`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cp <origen> <destino>` | `Copy-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `cp notas.txt /home/usuario/Documentos` | `Copy-Item -Path notas.txt -Destination C:\Users\usuario\Documents` |

> 💡 **Diferencia clave** — 🐧 Utiliza `cp` para copiar archivos y directorios. · 🪟 Utiliza el cmdlet `Copy-Item`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <origen> <destino>` | `Move-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `mv notas.txt informe.txt` | `Move-Item -Path notas.txt -Destination informe.txt` |

> 💡 **Diferencia clave** — 🐧 `mv` mueve y renombra archivos con el mismo comando. · 🪟 `Move-Item` también permite mover y renombrar archivos utilizando el parámetro `-Destination`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `rm <archivo>` | `Remove-Item -Path <archivo>` |
| **Ejemplo** | `rm notas.txt informe.txt copia_notas.txt` | `Remove-Item notas.txt, informe.txt, copia_notas.txt` |

> 💡 **Diferencia clave** — 🐧 `rm` elimina archivos de forma permanente. · 🪟 `Remove-Item` elimina archivos y otros elementos del sistema de archivos.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `rm -r <directorio>` | `Remove-Item -Path <directorio> -Recurse` |
| **Ejemplo** | `rm -rf Proyecto` | `Remove-Item -Path Proyecto -Recurse -Force` |

> 💡 **Diferencia clave** — 🐧 `-r` elimina el directorio y todo su contenido. · 🪟 `-Recurse` elimina el directorio y todos sus elementos.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cat <archivo>` | `Get-Content -Path <archivo>` |
| **Ejemplo** | `cat /home/usuario/Documentos/notas.txt` | `Get-Content -Path C:\Users\usuario\Documents\notas.txt` |

> 💡 **Diferencia clave** — 🐧 `cat` muestra el contenido como texto plano. · 🪟 `Get-Content` devuelve cada línea como un objeto de tipo `String`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `head <archivo>` | `Get-Content -Path <archivo> -TotalCount 10` |
| **Ejemplo** | `head -n 5 notas.txt` | `Get-Content -Path notas.txt -TotalCount 5` |

> 💡 **Diferencia clave** — 🐧 `head` muestra las primeras líneas de un archivo. · 🪟 `Get-Content` utiliza el parámetro `-TotalCount` para limitar el número de líneas mostradas.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `tail <archivo>` | `Get-Content -Path <archivo> -Tail 10` |
| **Ejemplo** | `tail -n 5 notas.txt` | `Get-Content -Path notas.txt -Tail 5` |

> 💡 **Diferencia clave** — 🐧 `tail` muestra las últimas líneas de un archivo. · 🪟 `Get-Content` utiliza el parámetro `-Tail` para mostrar las últimas líneas.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cp -r <origen> <destino>` | `Copy-Item -Path <origen> -Destination <destino> -Recurse` |
| **Ejemplo** | `cp -r Proyecto /home/usuario/Backups` | `Copy-Item -Path Proyecto -Destination C:\Backups -Recurse` |

> 💡 **Diferencia clave** — 🐧 Es necesario utilizar `-r` (o `-R`) para copiar directorios. · 🪟 Es necesario utilizar el parámetro `-Recurse` para copiar todo el contenido del directorio.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <origen> <destino>` | `Move-Item -Path <origen> -Destination <destino>` |
| **Ejemplo** | `mv /home/usuario/Proyecto /home/usuario/Backups` | `Move-Item -Path C:\Users\usuario\Proyecto -Destination C:\Backups` |

> 💡 **Diferencia clave** — 🐧 `mv` mueve y renombra directorios con el mismo comando. · 🪟 `Move-Item` también permite mover y renombrar directorios utilizando `-Destination`.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `mv <nombre_actual> <nuevo_nombre>` | `Rename-Item -Path <nombre_actual> -NewName <nuevo_nombre>` |
| **Ejemplo** | `mv /home/usuario/Proyecto /home/usuario/Proyecto_Backup` | `Rename-Item -Path C:\Users\usuario\Proyecto -NewName Proyecto_Backup` |

> 💡 **Diferencia clave** — 🐧 `mv` utiliza el mismo comando para mover y renombrar directorios. · 🪟 `Rename-Item` está diseñado específicamente para cambiar el nombre de un elemento.

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