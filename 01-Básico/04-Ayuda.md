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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `man <comando>` | `Get-Help <cmdlet>` |
| **Ejemplo** | `man cp` | `Get-Help Copy-Item` |

> 💡 **Diferencia clave** — 🐧 `man` abre el manual completo del comando. · 🪟 `Get-Help` muestra la ayuda integrada del cmdlet.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `compgen -c` | `Get-Command` |

**Ejemplo**
```bash
compgen -c | grep "^get"
```
```powershell
Get-Command Get*
```

> 💡 **Diferencia clave** — 🐧 `compgen -c` lista todos los comandos disponibles en el shell. · 🪟 `Get-Command` muestra cmdlets, funciones, alias y aplicaciones.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `apropos "<acción>"` | `Get-Command -Verb <verbo>` |
| **Ejemplo** | `apropos process` | `Get-Command *Process*` |

> 💡 **Diferencia clave** — 🐧 `apropos` busca palabras dentro de la descripción de las páginas del manual. · 🪟 `Get-Command -Verb` busca cmdlets utilizando los verbos estándar de PowerShell.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `man <comando>` | `Get-Help <cmdlet> -Examples` |
| **Ejemplo** | `man ls` | `Get-Help Get-ChildItem -Examples` |

> 💡 **Diferencia clave** — 🐧 Los ejemplos aparecen integrados en la página del manual si el desarrollador los ha incluido. · 🪟 `-Examples` muestra únicamente la sección de ejemplos del cmdlet.
> 
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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `man <comando>` | `Get-Help <cmdlet> -Full` |
| **Ejemplo** | `man mv` | `Get-Help Move-Item -Full` |

> 💡 **Diferencia clave** — 🐧 `man` muestra toda la documentación disponible del comando. · 🪟 `Get-Help -Full` muestra la documentación completa del cmdlet.

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

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo mandb` | `Update-Help` |
| **Ejemplo** | `sudo mandb` | `Update-Help -Module Microsoft.PowerShell.Management` |

> 💡 **Diferencia clave** — 🐧 `mandb` reconstruye la base de datos de las páginas del manual instaladas en el sistema. · 🪟 `Update-Help` descarga la documentación más reciente desde Internet.

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
