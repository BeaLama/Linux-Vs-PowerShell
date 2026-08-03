# Paquetes

## Introducción

Los gestores de paquetes permiten instalar, actualizar, eliminar y administrar el software del sistema de forma sencilla y segura.

Cada distribución Linux utiliza su propio gestor de paquetes (APT, DNF, YUM, Pacman, Zypper, etc.), mientras que Windows dispone de herramientas como **Winget** y **PowerShell PackageManagement** para realizar tareas similares.

---

## Índice

- [Buscar un paquete](#buscar-un-paquete)
- [Instalar un paquete](#instalar-un-paquete)
- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Actualizar un paquete concreto](#actualizar-un-paquete-concreto)
- [Eliminar un paquete](#eliminar-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)
- [Obtener información de un paquete](#obtener-información-de-un-paquete)
- [Limpiar la caché de paquetes](#limpiar-la-caché-de-paquetes)
- [Resumen de equivalencias](#resumen-de-equivalencias)

---

## Buscar un paquete

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `apt search <paquete>` | `winget search <paquete>` |
| **Ejemplo** | `apt search code` | `winget search vscode` |

> 💡 **Diferencia clave** — 🐧 Busca paquetes disponibles en los repositorios APT configurados. · 🪟 Busca aplicaciones disponibles en los orígenes configurados de Winget.

---

### Buenas prácticas

- Utiliza palabras clave cortas si no recuerdas el nombre exacto del paquete.
- Comprueba siempre el nombre oficial antes de instalar un paquete.
- Revisa la descripción para asegurarte de que corresponde al software que necesitas.
- Si existen varios resultados similares, verifica el identificador o el origen antes de instalar.

---

### Comandos relacionados

- [Instalar un paquete](#instalar-un-paquete)
- [Obtener información de un paquete](#obtener-información-de-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)

## Instalar un paquete

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo apt install <paquete>` | `winget install <paquete>` |
| **Ejemplo** | `sudo apt install code` | `winget install Microsoft.VisualStudioCode` |

> 💡 **Diferencia clave** — 🐧 Instala paquetes desde los repositorios APT configurados. · 🪟 Instala aplicaciones desde los orígenes configurados en Winget.

---

### Buenas prácticas

- Actualiza la información de los repositorios antes de instalar software nuevo.
- Instala únicamente paquetes procedentes de repositorios o fuentes de confianza.
- Comprueba el nombre o el identificador del paquete antes de iniciar la instalación.
- Verifica que la instalación se haya completado correctamente antes de utilizar la aplicación.

---

### Comandos relacionados

- [Buscar un paquete](#buscar-un-paquete)
- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Eliminar un paquete](#eliminar-un-paquete)

---

[⬆️ Volver al índice](#índice)

## Actualizar los paquetes

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo apt update` | `winget upgrade` |
| **Ejemplo** | `sudo apt update && sudo apt upgrade` | `winget upgrade --all` |

> 💡 **Diferencia clave** — 🐧 Es necesario ejecutar `apt update` antes de instalar las actualizaciones. · 🪟 Winget consulta automáticamente las versiones disponibles al ejecutar `winget upgrade`.

---

### Buenas prácticas

- Ejecuta `apt update` antes de instalar o actualizar paquetes.
- Mantén el sistema actualizado para corregir errores y vulnerabilidades de seguridad.
- Revisa los paquetes que van a actualizarse antes de confirmar la operación.
- Reinicia el sistema cuando una actualización afecte al núcleo o a componentes críticos.

---

### Comandos relacionados

- [Actualizar un paquete concreto](#actualizar-un-paquete-concreto)
- [Instalar un paquete](#instalar-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)

## Actualizar un paquete concreto

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo apt install --only-upgrade <paquete>` | *(no aplica)* |
| **Ejemplo** | `sudo apt install --only-upgrade code` | `winget upgrade Microsoft.VisualStudioCode` |

> 💡 **Diferencia clave** — 🐧 Solo actualiza el paquete indicado si ya está instalado. · 🪟 Actualiza únicamente la aplicación seleccionada.

---

### Buenas prácticas

- Actualiza únicamente el paquete que necesites cuando no quieras modificar el resto del sistema.
- Comprueba previamente si existe una versión más reciente disponible.
- Utiliza el identificador (`--id`) en Winget para evitar instalar o actualizar una aplicación incorrecta.
- Verifica el funcionamiento de la aplicación después de la actualización.

---

### Comandos relacionados

- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Instalar un paquete](#instalar-un-paquete)
- [Obtener información de un paquete](#obtener-información-de-un-paquete)

---

[⬆️ Volver al índice](#índice)

## Eliminar un paquete

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo apt remove <paquete>` | `winget uninstall <paquete>`|

---

### Ejemplos

**Eliminar Git**

Linux

```bash
sudo apt remove git
```

PowerShell

```powershell
winget uninstall Git.Git
```

---

### Buenas prácticas

- Comprueba que el paquete no sea una dependencia crítica antes de eliminarlo.
- Utiliza `apt purge` cuando quieras eliminar completamente un paquete y su configuración.
- Ejecuta `apt autoremove` periódicamente para liberar espacio eliminando dependencias innecesarias.
- Verifica que la aplicación se ha desinstalado correctamente antes de instalar una versión diferente.

---

### Comandos relacionados

- [Instalar un paquete](#instalar-un-paquete)
- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)

## Mostrar los paquetes instalados

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `apt list --installed` | *(no aplica)* |

**Ejemplo**
```bash
apt list --installed | grep git
```
```powershell
winget list git
```

> 💡 **Diferencia clave** — 🐧 `apt list --installed` muestra únicamente los paquetes instalados mediante APT. · 🪟 `winget list` muestra las aplicaciones detectadas por Winget.

---

### Buenas prácticas

- Revisa periódicamente el software instalado para detectar aplicaciones innecesarias.
- Comprueba la versión instalada antes de actualizar o desinstalar un paquete.
- Utiliza filtros o búsquedas cuando trabajes con sistemas que tengan un gran número de paquetes instalados.
- Mantén únicamente el software necesario para reducir la superficie de ataque del sistema.

---

### Comandos relacionados

- [Buscar un paquete](#buscar-un-paquete)
- [Obtener información de un paquete](#obtener-información-de-un-paquete)
- [Eliminar un paquete](#eliminar-un-paquete)

---

[⬆️ Volver al índice](#índice)

## Obtener información de un paquete

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `apt show <paquete>` | `winget show <paquete>` |
| **Ejemplo** | `apt show code` | `winget show Microsoft.VisualStudioCode` |

> 💡 **Diferencia clave** — 🐧 Muestra información procedente de los repositorios APT. · 🪟 Muestra información del repositorio configurado en Winget.

---

### Buenas prácticas

- Consulta siempre la información del paquete antes de instalarlo.
- Revisa las dependencias cuando el paquete vaya a instalarse en servidores o sistemas de producción.
- Comprueba el origen del paquete para asegurarte de que procede de una fuente confiable.
- Utiliza el identificador (`--id`) en Winget cuando existan varias aplicaciones con nombres similares.

---

### Comandos relacionados

- [Buscar un paquete](#buscar-un-paquete)
- [Instalar un paquete](#instalar-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)

## Limpiar la caché de paquetes

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo apt clean` | `winget source reset --force` |
| **Ejemplo** | `sudo apt autoclean` | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 APT almacena los paquetes descargados en una caché local. · 🪟 Winget no utiliza una caché gestionable mediante un comando equivalente.

---

### Buenas prácticas

- Ejecuta `apt clean` cuando necesites liberar espacio en disco.
- Utiliza `apt autoclean` como opción habitual, ya que elimina únicamente los paquetes innecesarios.
- No elimines la caché con frecuencia si realizas instalaciones repetidas, ya que APT tendrá que volver a descargar los paquetes.
- Si Winget presenta problemas al buscar o instalar aplicaciones, prueba a restablecer sus orígenes mediante `winget source reset --force`.

---

### Comandos relacionados

- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Buscar un paquete](#buscar-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un paquete | `apt search` | `winget search` |
| Instalar un paquete | `apt install` | `winget install` |
| Actualizar los repositorios | `apt update` | `winget source update` |
| Actualizar todos los paquetes | `apt upgrade` | `winget upgrade --all` |
| Actualizar un paquete concreto | `apt install --only-upgrade` | `winget upgrade` |
| Eliminar un paquete | `apt remove` | `winget uninstall` |
| Eliminar paquete y configuración | `apt purge` | No existe un equivalente directo |
| Eliminar dependencias innecesarias | `apt autoremove` | No existe un equivalente directo |
| Mostrar paquetes instalados | `apt list --installed` | `winget list` |
| Obtener información de un paquete | `apt show` | `winget show` |
| Limpiar la caché de paquetes | `apt clean` | No existe un equivalente directo |

---

### Buenas prácticas generales

- Mantén siempre actualizados los repositorios antes de instalar software nuevo.
- Instala únicamente paquetes procedentes de repositorios o fuentes de confianza.
- Revisa el nombre o identificador del paquete antes de instalarlo o actualizarlo.
- Elimina aplicaciones que ya no utilices para reducir la superficie de ataque del sistema.
- Mantén el sistema actualizado para corregir errores y vulnerabilidades de seguridad.
- Ejecuta `apt autoremove` periódicamente para eliminar dependencias innecesarias.
- Consulta la información del paquete antes de instalar software desconocido.

---

[⬆️ Volver al índice](#índice)