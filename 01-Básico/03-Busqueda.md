# Búsqueda

## Introducción

Localizar archivos, directorios o información específica es una de las tareas más habituales tanto en Linux como en Windows.

Mientras que Linux utiliza principalmente herramientas como `find` y `grep`, PowerShell dispone de cmdlets como `Get-ChildItem` y `Select-String`, capaces de realizar búsquedas muy precisas gracias al uso de objetos.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name "<nombre_archivo>"` | `Get-ChildItem -Path <ruta> -Filter "<nombre_archivo>" -File -Recurse` |

**Ejemplo**
```bash
find /home/usuario/Documentos -name "informe.txt"
```
```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "informe.txt" -File -Recurse
```

> 💡 **Diferencia clave** — 🐧 `find` busca tanto archivos como directorios; el comportamiento depende de los parámetros utilizados. · 🪟 `-File` limita la búsqueda únicamente a archivos.

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

**Sintaxis**
```bash
find <ruta> -type d -name "<nombre_directorio>"
```
```powershell
Get-ChildItem -Path <ruta> -Directory -Filter "<nombre_directorio>" -Recurse
```

> 💡 **Diferencia clave** — 🐧 `-type d` limita la búsqueda únicamente a directorios. · 🪟 `-Directory` devuelve exclusivamente directorios.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name "*.extensión"` | `Get-ChildItem -Path <ruta> -Filter "*.extensión" -File -Recurse` |

**Ejemplo**
```bash
find /home/usuario/Documentos -name "*.pdf"
```
```powershell
Get-ChildItem -Path C:\Users\usuario\Documents -Filter "*.pdf" -File -Recurse
```

> 💡 **Diferencia clave** — 🐧 La búsqueda se realiza mediante `find` utilizando el parámetro `-name`. · 🪟 Se utiliza `Get-ChildItem` junto con `-Filter`, lo que mejora el rendimiento.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `grep "<texto>" <archivo>` | `Select-String -Path <archivo> -Pattern "<texto>"` |
| **Ejemplo** | `grep "ERROR" *.log` | `Select-String -Path *.log -Pattern "ERROR"` |

> 💡 **Diferencia clave** — 🐧 `grep` busca texto plano dentro de archivos. · 🪟 `Select-String` utiliza expresiones regulares por defecto y devuelve objetos con información de la coincidencia.ormación como el archivo, el número de línea y el texto encontrado. |

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> <criterios>` | `Get-ChildItem -Path <ruta> -Recurse` |

**Ejemplo**
```bash
grep -r "ERROR" .
```
```powershell
Get-ChildItem -Path . -Filter *.txt -Recurse |
Select-String -Pattern "ERROR"
```

> 💡 **Diferencia clave** — 🐧 `find` realiza búsquedas recursivas por defecto. · 🪟 La búsqueda recursiva requiere el parámetro `-Recurse`.

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

**Sintaxis**
```bash
find <ruta> -mtime <días>
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(<días>)}
```

> 💡 **Diferencia clave** — 🐧 `-mtime` trabaja con días completos desde la última modificación. · 🪟 Se compara la propiedad `LastWriteTime` con una fecha calculada mediante `Get-Date`.

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

**Sintaxis**
```bash
find <ruta> -size <tamaño>
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length <operador> <tamaño>}
```

> 💡 **Diferencia clave** — 🐧 `find` utiliza el parámetro `-size` junto con unidades como `k`, `M` o `G`. · 🪟 PowerShell compara el tamaño mediante la propiedad `Length`.

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

**Sintaxis**
```bash
find <ruta> -type f -empty
```
```powershell
Get-ChildItem -Path <ruta> -File -Recurse |
Where-Object {$_.Length -eq 0}
```

> 💡 **Diferencia clave** — 🐧 `-empty` permite localizar archivos y directorios vacíos. · 🪟 Se utiliza la propiedad `Length` para comprobar el tamaño del archivo.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `find <ruta> -name ".*"` | `Get-ChildItem -Path <ruta> -File -Force -Recurse` |

**Ejemplo**
```bash
find /home/usuario -type f -name ".*"
```
```powershell
Get-ChildItem -Path C:\Users\usuario -File -Force -Recurse |
Where-Object {$_.Attributes -match "Hidden"}
```

> 💡 **Diferencia clave** — 🐧 Los archivos ocultos se identifican porque su nombre comienza por un punto (`.`). · 🪟 Los archivos ocultos se identifican mediante el atributo `Hidden`.

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