# Ayuda

## Introducción

Conocer un comando es importante, pero saber dónde consultar su documentación es una habilidad imprescindible para cualquier administrador de sistemas.

Tanto Linux como PowerShell incorporan herramientas que permiten acceder a información detallada sobre comandos, parámetros, ejemplos y funcionamiento sin necesidad de utilizar un navegador web.

---

## Índice

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Buscar comandos disponibles](#buscar-comandos-disponibles)
- [Buscar comandos relacionados con una acción](#buscar-comandos-relacionados-con-una-acción)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)
- [Consultar los parámetros de un comando](#consultar-los-parámetros-de-un-comando)
- [Actualizar la ayuda (PowerShell)](#actualizar-la-ayuda-powershell)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Mostrar la ayuda de un comando

### Linux

```bash
man <comando>
```

También puede utilizarse:

```bash
<comando> --help
```

**Descripción**

Muestra la documentación de un comando, incluyendo su descripción, sintaxis, parámetros y opciones disponibles.

---

### PowerShell

```powershell
Get-Help <cmdlet>
```

**Descripción**

Muestra la ayuda integrada de un cmdlet, incluyendo su descripción, sintaxis, parámetros y ejemplos disponibles.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar la ayuda de un comando | `man` / `--help` | `Get-Help` |

---

### Ejemplos

**Consultar la ayuda del comando `ls`**

Linux

```bash
man ls
```

PowerShell

```powershell
Get-Help Get-ChildItem
```

---

**Consultar la ayuda del comando `cp`**

Linux

```bash
man cp
```

PowerShell

```powershell
Get-Help Copy-Item
```

---

**Mostrar una ayuda rápida**

Linux

```bash
ls --help
```

PowerShell

```powershell
Get-Help Get-ChildItem
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `man` abre el manual completo del comando. | `Get-Help` muestra la ayuda integrada del cmdlet. |
| Muchos comandos también disponen del parámetro `--help` para mostrar una versión resumida. | La ayuda puede ampliarse mediante parámetros como `-Examples`, `-Detailed` o `-Full`. |
| Los manuales suelen instalarse junto con el sistema operativo. | La ayuda puede actualizarse independientemente del sistema mediante `Update-Help`. |

---

### Buenas prácticas

- Consulta siempre la ayuda antes de utilizar un comando desconocido.
- Utiliza `--help` cuando necesites una referencia rápida.
- Recurre al manual completo (`man`) o a `Get-Help` cuando necesites conocer todos los parámetros disponibles.

---

### Comandos relacionados

- [Buscar comandos disponibles](#buscar-comandos-disponibles)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)
- [Consultar los parámetros de un comando](#consultar-los-parámetros-de-un-comando)

---

[⬆️ Volver al índice](#índice)

## Buscar comandos disponibles

### Linux

```bash
compgen -c
```

También puede utilizarse:

```bash
apropos .
```

**Descripción**

Muestra todos los comandos disponibles en el sistema o aquellos que disponen de una página del manual.

---

### PowerShell

```powershell
Get-Command
```

**Descripción**

Muestra todos los cmdlets, funciones, alias y aplicaciones disponibles en la sesión actual de PowerShell.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar los comandos disponibles | `compgen -c` / `apropos .` | `Get-Command` |

---

### Ejemplos

**Mostrar todos los comandos disponibles**

Linux

```bash
compgen -c
```

PowerShell

```powershell
Get-Command
```

---

**Buscar comandos cuyo nombre empiece por "Get"**

Linux

```bash
compgen -c | grep "^get"
```

PowerShell

```powershell
Get-Command Get*
```

---

**Buscar comandos relacionados con "copy"**

Linux

```bash
apropos copy
```

PowerShell

```powershell
Get-Command *Copy*
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `compgen -c` lista todos los comandos disponibles en el shell. | `Get-Command` muestra cmdlets, funciones, alias y aplicaciones. |
| `apropos` busca comandos basándose en la descripción de sus páginas del manual. | `Get-Command` permite buscar utilizando comodines en el nombre del comando. |
| Es habitual combinar `compgen` con `grep` para filtrar resultados. | El filtrado puede realizarse directamente mediante comodines (`*`). |

---

### Buenas prácticas

- Utiliza `Get-Command` como primer paso cuando desconozcas el nombre exacto de un cmdlet.
- Aprovecha los comodines para localizar comandos similares.
- En Linux, utiliza `apropos` cuando conozcas la función que deseas realizar, pero no recuerdes el nombre del comando.

---

### Comandos relacionados

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Buscar comandos relacionados con una acción](#buscar-comandos-relacionados-con-una-acción)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)

---

[⬆️ Volver al índice](#índice)

## Buscar comandos relacionados con una acción

### Linux

```bash
apropos "<acción>"
```

**Descripción**

Busca comandos cuya descripción esté relacionada con la acción indicada utilizando la base de datos de las páginas del manual.

---

### PowerShell

```powershell
Get-Command -Verb <verbo>
```

También puede utilizarse:

```powershell
Get-Command *<acción>*
```

**Descripción**

Busca cmdlets relacionados con una acción concreta mediante el verbo o utilizando comodines.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar comandos relacionados con una acción | `apropos` | `Get-Command -Verb` / `Get-Command *texto*` |

---

### Ejemplos

**Buscar comandos relacionados con la copia de archivos**

Linux

```bash
apropos copy
```

PowerShell

```powershell
Get-Command -Verb Copy
```

---

**Buscar comandos relacionados con procesos**

Linux

```bash
apropos process
```

PowerShell

```powershell
Get-Command *Process*
```

---

**Buscar comandos relacionados con servicios**

Linux

```bash
apropos service
```

PowerShell

```powershell
Get-Command *Service*
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `apropos` busca palabras dentro de la descripción de las páginas del manual. | `Get-Command -Verb` busca cmdlets utilizando los verbos estándar de PowerShell. |
| Los resultados dependen de la documentación instalada en el sistema. | Los resultados incluyen cmdlets, funciones, alias y aplicaciones. |
| Puede buscar cualquier palabra clave. | Puede buscar por verbo (`Get`, `Set`, `Start`, `Stop`, `New`, etc.) o mediante comodines. |

---

### Buenas prácticas

- Utiliza palabras clave sencillas para obtener mejores resultados.
- En PowerShell, intenta buscar primero por verbo (`Get`, `Set`, `New`, `Remove`, etc.).
- Si no encuentras el comando adecuado, utiliza comodines para ampliar la búsqueda.

---

### Comandos relacionados

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Buscar comandos disponibles](#buscar-comandos-disponibles)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)

---

[⬆️ Volver al índice](#índice)

## Mostrar ejemplos de uso

### Linux

```bash
man <comando>
```

También puede utilizarse:

```bash
<comando> --help
```

**Descripción**

Permite consultar ejemplos de uso y la sintaxis de un comando. Algunos comandos incluyen ejemplos directamente en la ayuda, mientras que otros únicamente muestran la descripción de sus parámetros.

---

### PowerShell

```powershell
Get-Help <cmdlet> -Examples
```

**Descripción**

Muestra únicamente los ejemplos de uso disponibles para un cmdlet.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar ejemplos de uso | `man` / `--help` | `Get-Help -Examples` |

---

### Ejemplos

**Mostrar ejemplos del comando de copia**

Linux

```bash
man cp
```

PowerShell

```powershell
Get-Help Copy-Item -Examples
```

---

**Mostrar ejemplos del comando para listar archivos**

Linux

```bash
man ls
```

PowerShell

```powershell
Get-Help Get-ChildItem -Examples
```

---

**Mostrar ejemplos del comando para eliminar archivos**

Linux

```bash
man rm
```

PowerShell

```powershell
Get-Help Remove-Item -Examples
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Los ejemplos aparecen integrados en la página del manual si el desarrollador los ha incluido. | `-Examples` muestra únicamente la sección de ejemplos del cmdlet. |
| Algunos comandos solo ofrecen información sobre los parámetros. | La mayoría de cmdlets incluyen ejemplos prácticos y comentados. |
| `--help` suele mostrar una ayuda resumida. | `Get-Help -Examples` está orientado exclusivamente al aprendizaje mediante ejemplos. |

---

### Buenas prácticas

- Consulta siempre los ejemplos antes de utilizar un comando desconocido.
- Modifica los ejemplos según tus necesidades en lugar de ejecutarlos directamente.
- Si un comando no dispone de ejemplos, consulta la documentación completa mediante `man` o `Get-Help`.

---

### Comandos relacionados

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Consultar los parámetros de un comando](#consultar-los-parámetros-de-un-comando)
- [Buscar comandos disponibles](#buscar-comandos-disponibles)

---

[⬆️ Volver al índice](#índice)

## Consultar los parámetros de un comando

### Linux

```bash
man <comando>
```

También puede utilizarse:

```bash
<comando> --help
```

**Descripción**

Permite consultar todos los parámetros y opciones disponibles de un comando, junto con una explicación de su funcionamiento.

---

### PowerShell

```powershell
Get-Help <cmdlet> -Full
```

**Descripción**

Muestra la documentación completa de un cmdlet, incluyendo su descripción, sintaxis, parámetros, ejemplos y notas adicionales.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Consultar los parámetros de un comando | `man` / `--help` | `Get-Help -Full` |

---

### Ejemplos

**Consultar los parámetros del comando para copiar archivos**

Linux

```bash
man cp
```

PowerShell

```powershell
Get-Help Copy-Item -Full
```

---

**Consultar los parámetros del comando para mover archivos**

Linux

```bash
man mv
```

PowerShell

```powershell
Get-Help Move-Item -Full
```

---

**Consultar los parámetros del comando para eliminar archivos**

Linux

```bash
man rm
```

PowerShell

```powershell
Get-Help Remove-Item -Full
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `man` muestra toda la documentación disponible del comando. | `Get-Help -Full` muestra la documentación completa del cmdlet. |
| `--help` suele ofrecer una versión resumida con los parámetros más utilizados. | Incluye sintaxis, parámetros, ejemplos y notas adicionales en una única salida. |
| La documentación depende del comando instalado en el sistema. | La documentación puede actualizarse mediante `Update-Help`. |

---

### Buenas prácticas

- Consulta la documentación completa cuando necesites conocer todos los parámetros disponibles.
- Utiliza `--help` para una consulta rápida y `man` para una explicación detallada.
- En PowerShell, utiliza `Get-Help -Full` antes de ejecutar cmdlets desconocidos.

---

### Comandos relacionados

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)
- [Actualizar la ayuda (PowerShell)](#actualizar-la-ayuda-powershell)

---

[⬆️ Volver al índice](#índice)

## Actualizar la ayuda (PowerShell)

### Linux

```bash
sudo mandb
```

**Descripción**

Actualiza la base de datos utilizada por `man` y `apropos`. Este comando es útil cuando se instalan nuevas páginas del manual o se actualiza la documentación del sistema.

---

### PowerShell

```powershell
Update-Help
```

**Descripción**

Descarga e instala la versión más reciente de la ayuda de los módulos de PowerShell desde Internet.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Actualizar la documentación del sistema | `mandb` | `Update-Help` |

---

### Ejemplos

**Actualizar la base de datos del manual**

Linux

```bash
sudo mandb
```

PowerShell

```powershell
Update-Help
```

---

**Actualizar la ayuda de un módulo específico**

Linux

```bash
sudo mandb
```

PowerShell

```powershell
Update-Help -Module Microsoft.PowerShell.Management
```

---

**Actualizar la ayuda utilizando credenciales de administrador**

Linux

```bash
sudo mandb
```

PowerShell

```powershell
Update-Help -Force
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `mandb` reconstruye la base de datos de las páginas del manual instaladas en el sistema. | `Update-Help` descarga la documentación más reciente desde Internet. |
| No descarga documentación nueva; únicamente indexa la existente. | Requiere conexión a Internet para descargar la ayuda más reciente. |
| Suele ejecutarse automáticamente al instalar nuevos paquetes. | Es recomendable ejecutarlo tras instalar nuevos módulos o versiones de PowerShell. |

---

### Buenas prácticas

- Ejecuta `Update-Help` periódicamente para disponer de la documentación más reciente.
- En Linux, utiliza `mandb` cuando instales nuevas páginas del manual o si `apropos` no encuentra resultados esperados.
- Ejecuta ambos comandos con privilegios de administrador cuando sea necesario.

---

### Comandos relacionados

- [Mostrar la ayuda de un comando](#mostrar-la-ayuda-de-un-comando)
- [Consultar los parámetros de un comando](#consultar-los-parámetros-de-un-comando)
- [Mostrar ejemplos de uso](#mostrar-ejemplos-de-uso)

---

[⬆️ Volver al índice](#índice)
