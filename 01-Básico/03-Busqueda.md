# Búsqueda

## Introducción

Localizar archivos, directorios o información específica es una de las tareas más habituales tanto en Linux como en Windows.

Mientras que Linux utiliza principalmente herramientas como `find` y `grep`, PowerShell dispone de cmdlets como `Get-ChildItem` y `Select-String`, capaces de realizar búsquedas muy precisas gracias al uso de objetos.

En este capítulo aprenderás a localizar archivos, carpetas y contenido utilizando los comandos más utilizados por administradores de sistemas.

---

## Índice

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)
- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)
- [Buscar archivos ocultos](#buscar-archivos-ocultos)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Buscar archivos por nombre

### Linux

```bash
find <ruta> -name "<nombre_archivo>"
```

**Descripción**

Busca archivos cuyo nombre coincida exactamente con el indicado dentro de la ruta especificada.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -Filter "<nombre_archivo>" -File -Recurse
```

**Descripción**

Busca archivos por nombre dentro de la ruta especificada y todos sus subdirectorios.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un archivo por nombre | `find -name` | `Get-ChildItem -Filter -File -Recurse` |

---

### Ejemplos

**Buscar un archivo en el directorio actual y sus subdirectorios**

Linux

```bash
find . -name "notas.txt"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter "notas.txt" -File -Recurse
```

---

**Buscar un archivo en una ruta específica**

Linux

```bash
find /home/usuario/Documentos -name "informe.txt"
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "informe.txt" -File -Recurse
```

---

**Buscar utilizando comodines**

Linux

```bash
find . -name "*.txt"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter "*.txt" -File -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `find` busca tanto archivos como directorios; el comportamiento depende de los parámetros utilizados. | `-File` limita la búsqueda únicamente a archivos. |
| El parámetro `-name` distingue entre mayúsculas y minúsculas según el sistema de archivos. | La búsqueda no suele distinguir entre mayúsculas y minúsculas en Windows. |
| Los comodines (`*`, `?`) son compatibles. | También admite comodines mediante `-Filter`. |

---

### Buenas prácticas

- Utiliza `-Filter` en PowerShell siempre que sea posible, ya que es más eficiente que filtrar posteriormente con `Where-Object`.
- Limita la búsqueda a la carpeta necesaria para reducir el tiempo de ejecución.
- Aprovecha los comodines para localizar grupos de archivos similares.

---

### Comandos relacionados

- [Buscar directorios](#buscar-directorios)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

## Buscar directorios

### Linux

```bash
find <ruta> -type d -name "<nombre_directorio>"
```

**Descripción**

Busca directorios cuyo nombre coincida con el indicado dentro de la ruta especificada.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -Directory -Filter "<nombre_directorio>" -Recurse
```

**Descripción**

Busca directorios por nombre dentro de la ruta especificada y todos sus subdirectorios.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un directorio por nombre | `find -type d -name` | `Get-ChildItem -Directory -Filter -Recurse` |

---

### Ejemplos

**Buscar un directorio en la ubicación actual**

Linux

```bash
find . -type d -name "Proyecto"
```

PowerShell

```powershell
Get-ChildItem -Path . -Directory -Filter "Proyecto" -Recurse
```

---

**Buscar un directorio en una ruta específica**

Linux

```bash
find /home/usuario -type d -name "Backups"
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario -Directory -Filter "Backups" -Recurse
```

---

**Buscar directorios utilizando comodines**

Linux

```bash
find . -type d -name "Pro*"
```

PowerShell

```powershell
Get-ChildItem -Path . -Directory -Filter "Pro*" -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `-type d` limita la búsqueda únicamente a directorios. | `-Directory` devuelve exclusivamente directorios. |
| Los comodines (`*`, `?`) son compatibles mediante `-name`. | Los comodines también son compatibles mediante `-Filter`. |
| La búsqueda distingue entre archivos y directorios mediante `-type`. | La distinción se realiza mediante el parámetro `-Directory`. |

---

### Buenas prácticas

- Limita la búsqueda a la carpeta necesaria para mejorar el rendimiento.
- Utiliza nombres descriptivos para los directorios, facilitando su localización.
- Emplea comodines cuando no recuerdes el nombre completo del directorio.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

## Buscar por extensión

### Linux

```bash
find <ruta> -name "*.extensión"
```

**Descripción**

Busca archivos que tengan una determinada extensión dentro de la ruta especificada.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -Filter "*.extensión" -File -Recurse
```

**Descripción**

Busca archivos con una extensión determinada dentro de la ruta especificada y todos sus subdirectorios.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar archivos por extensión | `find -name "*.extensión"` | `Get-ChildItem -Filter "*.extensión" -File -Recurse` |

---

### Ejemplos

**Buscar todos los archivos de texto**

Linux

```bash
find . -name "*.txt"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter "*.txt" -File -Recurse
```

---

**Buscar todos los archivos PDF**

Linux

```bash
find /home/usuario/Documentos -name "*.pdf"
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "*.pdf" -File -Recurse
```

---

**Buscar todos los archivos de registro**

Linux

```bash
find . -name "*.log"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter "*.log" -File -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| La búsqueda se realiza mediante `find` utilizando el parámetro `-name`. | Se utiliza `Get-ChildItem` junto con `-Filter`, lo que mejora el rendimiento. |
| Admite comodines (`*`, `?`) en el nombre del archivo. | También admite comodines mediante `-Filter`. |
| Es posible combinar la búsqueda con otros parámetros de `find`. | Puede combinarse con `Where-Object` para realizar filtros adicionales. |

---

### Buenas prácticas

- Utiliza `-Filter` en PowerShell siempre que sea posible para obtener un mejor rendimiento.
- Limita la búsqueda a la carpeta necesaria para reducir el tiempo de ejecución.
- Utiliza extensiones específicas cuando conozcas el tipo de archivo que deseas localizar.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)

---

[⬆️ Volver al índice](#índice)

## Buscar texto dentro de archivos

### Linux

```bash
grep "<texto>" <archivo>
```

**Descripción**

Busca una cadena de texto dentro del contenido de uno o varios archivos.

---

### PowerShell

```powershell
Select-String -Path <archivo> -Pattern "<texto>"
```

**Descripción**

Busca una cadena de texto dentro del contenido de uno o varios archivos.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar texto dentro de archivos | `grep` | `Select-String` |

---

### Ejemplos

**Buscar una palabra dentro de un archivo**

Linux

```bash
grep "ERROR" servidor.log
```

PowerShell

```powershell
Select-String -Path servidor.log -Pattern "ERROR"
```

---

**Buscar una palabra en varios archivos**

Linux

```bash
grep "ERROR" *.log
```

PowerShell

```powershell
Select-String -Path *.log -Pattern "ERROR"
```

---

**Ignorar mayúsculas y minúsculas**

Linux

```bash
grep -i "error" servidor.log
```

PowerShell

```powershell
Select-String -Path servidor.log -Pattern "error" -CaseSensitive:$false
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `grep` busca texto plano dentro de archivos. | `Select-String` utiliza expresiones regulares por defecto y devuelve objetos con información de la coincidencia. |
| La búsqueda distingue entre mayúsculas y minúsculas salvo que se utilice `-i`. | Por defecto no distingue entre mayúsculas y minúsculas. |
| La salida es texto plano. | La salida contiene información como el archivo, el número de línea y el texto encontrado. |

---

### Buenas prácticas

- Utiliza palabras o patrones específicos para reducir el número de resultados.
- Aprovecha los comodines (`*.log`, `*.txt`) para buscar en varios archivos simultáneamente.
- Si buscas en archivos grandes, limita la ruta de búsqueda para mejorar el rendimiento.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar de forma recursiva](#buscar-de-forma-recursiva)

---

[⬆️ Volver al índice](#índice)

## Buscar de forma recursiva

### Linux

```bash
find <ruta> <criterios>
```

También puede utilizarse:

```bash
grep -r "<texto>" <ruta>
```

**Descripción**

Permite realizar búsquedas dentro de todos los subdirectorios de una ruta determinada.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -Recurse
```

También puede combinarse con:

```powershell
Select-String
```

**Descripción**

Permite buscar archivos o texto recorriendo todos los subdirectorios de la ruta especificada.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar de forma recursiva | `find` / `grep -r` | `Get-ChildItem -Recurse` / `Select-String` |

---

### Ejemplos

**Buscar todos los archivos PDF de forma recursiva**

Linux

```bash
find . -name "*.pdf"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter "*.pdf" -File -Recurse
```

---

**Buscar la palabra "ERROR" en todos los archivos de texto**

Linux

```bash
grep -r "ERROR" .
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter *.txt -Recurse |
Select-String -Pattern "ERROR"
```

---

**Buscar archivos de registro de forma recursiva**

Linux

```bash
find . -name "*.log"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter *.log -File -Recurse
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `find` realiza búsquedas recursivas por defecto. | La búsqueda recursiva requiere el parámetro `-Recurse`. |
| `grep -r` busca texto dentro de todos los archivos de una ruta. | Habitualmente se combina `Get-ChildItem` con `Select-String` mediante una tubería (`|`). |
| Es habitual combinar varias herramientas (`find`, `grep`, `xargs`, etc.). | PowerShell utiliza el pipeline de objetos para combinar cmdlets. |

---

### Buenas prácticas

- Limita siempre la ruta de búsqueda cuando sea posible.
- Utiliza filtros (`-Filter`, `-name`) para mejorar el rendimiento.
- Evita realizar búsquedas recursivas sobre unidades completas salvo que sea realmente necesario.
- Combina la búsqueda recursiva con otros filtros para obtener resultados más precisos.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar texto dentro de archivos](#buscar-texto-dentro-de-archivos)
- [Buscar por extensión](#buscar-por-extensión)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos modificados recientemente

### Linux

```bash
find <ruta> -mtime <días>
```

**Descripción**

Busca archivos modificados dentro de un determinado intervalo de tiempo.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(<días>)}
```

**Descripción**

Busca archivos cuya fecha de modificación sea posterior al intervalo indicado.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar archivos modificados recientemente | `find -mtime` | `Get-ChildItem` + `Where-Object` |

---

### Ejemplos

**Buscar archivos modificados durante el último día**

Linux

```bash
find . -mtime -1
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-1)}
```

---

**Buscar archivos modificados durante los últimos 7 días**

Linux

```bash
find /home/usuario/Documentos -mtime -7
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -File -Recurse |
Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
```

---

**Buscar archivos modificados hace más de 30 días**

Linux

```bash
find . -mtime +30
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.LastWriteTime -lt (Get-Date).AddDays(-30)}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `-mtime` trabaja con días completos desde la última modificación. | Se compara la propiedad `LastWriteTime` con una fecha calculada mediante `Get-Date`. |
| Un valor negativo (`-7`) busca archivos modificados en los últimos días. | Se utiliza `AddDays(-7)` para calcular el intervalo de tiempo. |
| Un valor positivo (`+30`) busca archivos modificados hace más de ese número de días. | Se utiliza el operador `-lt` para buscar fechas anteriores. |

---

### Buenas prácticas

- Limita la búsqueda al directorio necesario para mejorar el rendimiento.
- Combina este criterio con otros filtros, como la extensión del archivo.
- Resulta especialmente útil para localizar documentos recientes o analizar cambios en un sistema.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos por tamaño

### Linux

```bash
find <ruta> -size <tamaño>
```

**Descripción**

Busca archivos cuyo tamaño coincida con el criterio especificado.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length <operador> <tamaño>}
```

**Descripción**

Busca archivos cuyo tamaño cumpla la condición indicada utilizando la propiedad `Length`.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar archivos por tamaño | `find -size` | `Get-ChildItem` + `Where-Object` |

---

### Ejemplos

**Buscar archivos mayores de 100 MB**

Linux

```bash
find . -size +100M
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.Length -gt 100MB}
```

---

**Buscar archivos menores de 1 MB**

Linux

```bash
find . -size -1M
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.Length -lt 1MB}
```

---

**Buscar archivos de exactamente 10 MB**

Linux

```bash
find . -size 10M
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.Length -eq 10MB}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `find` utiliza el parámetro `-size` junto con unidades como `k`, `M` o `G`. | PowerShell compara el tamaño mediante la propiedad `Length`. |
| Los operadores `+` y `-` permiten buscar archivos mayores o menores que un tamaño determinado. | Se utilizan operadores como `-gt`, `-lt` o `-eq`. |
| Es posible combinar este criterio con otros parámetros de `find`. | Puede combinarse fácilmente con otros filtros utilizando `Where-Object`. |

---

### Buenas prácticas

- Limita la búsqueda a la carpeta necesaria para reducir el tiempo de ejecución.
- Utiliza este criterio para localizar archivos que ocupen mucho espacio en disco.
- Combina la búsqueda por tamaño con la búsqueda por extensión para obtener resultados más precisos.

---

### Comandos relacionados

- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos vacíos

### Linux

```bash
find <ruta> -type f -empty
```

**Descripción**

Busca archivos vacíos (0 bytes) dentro de la ruta especificada.

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length -eq 0}
```

**Descripción**

Busca archivos cuyo tamaño sea igual a **0 bytes**.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar archivos vacíos | `find -type f -empty` | `Get-ChildItem` + `Where-Object {$_.Length -eq 0}` |

---

### Ejemplos

**Buscar archivos vacíos en el directorio actual**

Linux

```bash
find . -type f -empty
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Recurse |
Where-Object {$_.Length -eq 0}
```

---

**Buscar archivos vacíos en una ruta específica**

Linux

```bash
find /home/usuario/Documentos -type f -empty
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -File -Recurse |
Where-Object {$_.Length -eq 0}
```

---

**Buscar archivos vacíos con extensión `.txt`**

Linux

```bash
find . -type f -name "*.txt" -empty
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter *.txt -File -Recurse |
Where-Object {$_.Length -eq 0}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `-empty` permite localizar archivos y directorios vacíos. | Se utiliza la propiedad `Length` para comprobar el tamaño del archivo. |
| `-type f` limita la búsqueda únicamente a archivos. | `-File` limita la búsqueda únicamente a archivos. |
| Puede combinarse fácilmente con otros filtros de `find`. | Puede combinarse con `-Filter` y `Where-Object` para realizar búsquedas más específicas. |

---

### Buenas prácticas

- Revisa el contenido antes de eliminar archivos vacíos, ya que algunos pueden utilizarse como marcadores o plantillas.
- Combina este criterio con la extensión del archivo para obtener resultados más precisos.
- Utiliza rutas específicas para reducir el tiempo de búsqueda.

---

### Comandos relacionados

- [Buscar archivos por tamaño](#buscar-archivos-por-tamaño)
- [Buscar por extensión](#buscar-por-extensión)
- [Buscar archivos modificados recientemente](#buscar-archivos-modificados-recientemente)

---

[⬆️ Volver al índice](#índice)

## Buscar archivos ocultos

### Linux

```bash
find <ruta> -name ".*"
```

**Descripción**

Busca archivos ocultos dentro de la ruta especificada. En Linux, los archivos ocultos son aquellos cuyo nombre comienza por un punto (`.`).

---

### PowerShell

```powershell
Get-ChildItem -Path <ruta> -File -Force -Recurse
```

**Descripción**

Muestra los archivos ocultos del directorio especificado y de todos sus subdirectorios.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar archivos ocultos | `find -name ".*"` | `Get-ChildItem -Force -File -Recurse` |

---

### Ejemplos

**Buscar archivos ocultos en el directorio actual**

Linux

```bash
find . -type f -name ".*"
```

PowerShell

```powershell
Get-ChildItem -Path . -File -Force -Recurse |
Where-Object {$_.Attributes -match "Hidden"}
```

---

**Buscar archivos ocultos en una ruta específica**

Linux

```bash
find /home/usuario -type f -name ".*"
```

PowerShell

```powershell
Get-ChildItem -Path C:\Users\usuario -File -Force -Recurse |
Where-Object {$_.Attributes -match "Hidden"}
```

---

**Buscar archivos ocultos con extensión `.txt`**

Linux

```bash
find . -type f -name ".*.txt"
```

PowerShell

```powershell
Get-ChildItem -Path . -Filter *.txt -File -Force -Recurse |
Where-Object {$_.Attributes -match "Hidden"}
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los archivos ocultos se identifican porque su nombre comienza por un punto (`.`). | Los archivos ocultos se identifican mediante el atributo `Hidden`. |
| `find` los localiza utilizando el patrón `.*`. | `-Force` permite mostrarlos y `Where-Object` filtra únicamente los que tienen el atributo `Hidden`. |
| No existe un atributo específico para ocultarlos. | Un archivo puede tener varios atributos (`Hidden`, `ReadOnly`, `System`, etc.). |

---

### Buenas prácticas

- Evita modificar archivos ocultos si desconoces su función.
- Revisa cuidadosamente los resultados antes de eliminar archivos ocultos del sistema.
- Limita la búsqueda a la carpeta necesaria para mejorar el rendimiento.

---

### Comandos relacionados

- [Buscar archivos por nombre](#buscar-archivos-por-nombre)
- [Buscar directorios](#buscar-directorios)
- [Buscar archivos vacíos](#buscar-archivos-vacíos)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Buscar archivos por nombre | `find -name` | `Get-ChildItem -Filter -File -Recurse` |
| Buscar directorios | `find -type d -name` | `Get-ChildItem -Directory -Filter -Recurse` |
| Buscar por extensión | `find -name "*.ext"` | `Get-ChildItem -Filter "*.ext" -File -Recurse` |
| Buscar texto dentro de archivos | `grep` | `Select-String` |
| Buscar de forma recursiva | `find` / `grep -r` | `Get-ChildItem -Recurse` / `Select-String` |
| Buscar archivos modificados recientemente | `find -mtime` | `Get-ChildItem` + `Where-Object` |
| Buscar archivos por tamaño | `find -size` | `Get-ChildItem` + `Where-Object` |
| Buscar archivos vacíos | `find -empty` | `Get-ChildItem` + `Where-Object {$_.Length -eq 0}` |
| Buscar archivos ocultos | `find -name ".*"` | `Get-ChildItem -Force` + `Where-Object` |

---

### Buenas prácticas generales

- Limita siempre la búsqueda a la ruta necesaria para mejorar el rendimiento.
- Utiliza filtros (`-Filter`, `-name`) siempre que sea posible para reducir el número de resultados.
- Aprovecha los comodines (`*`, `?`) cuando no conozcas el nombre exacto del archivo o directorio.
- Combina distintos criterios de búsqueda (nombre, extensión, tamaño o fecha) para obtener resultados más precisos.
- Verifica siempre los resultados antes de modificar o eliminar archivos encontrados.
- En PowerShell, prioriza `-Filter` frente a `Where-Object` cuando sea posible, ya que ofrece un mejor rendimiento.

---

[⬆️ Volver al índice](#índice)