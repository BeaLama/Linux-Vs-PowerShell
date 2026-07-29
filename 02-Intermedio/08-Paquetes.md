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

### Linux

```bash
apt search <paquete>
```

También puede utilizarse:

```bash
apt-cache search <paquete>
```

**Descripción**

Permite buscar paquetes disponibles en los repositorios configurados del sistema.

La búsqueda puede realizarse utilizando el nombre completo o parte del nombre del paquete.

Los resultados suelen incluir:

- Nombre del paquete.
- Versión disponible.
- Breve descripción.
  
--- 

---

### PowerShell

```powershell
winget search <paquete>
```

**Descripción**

Permite buscar aplicaciones disponibles en los repositorios configurados por **Winget**.

La salida incluye información como:

- Nombre de la aplicación.
- Identificador (ID).
- Versión disponible.
- Origen del paquete.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar un paquete | `apt search` | `winget search` |

---

### Ejemplos

**Buscar Google Chrome**

Linux

```bash
apt search chrome
```

PowerShell

```powershell
winget search chrome
```

---

**Buscar Visual Studio Code**

Linux

```bash
apt search code
```

PowerShell

```powershell
winget search vscode
```

---

**Buscar Git**

Linux

```bash
apt search git
```

PowerShell

```powershell
winget search git
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Busca paquetes disponibles en los repositorios APT configurados. | Busca aplicaciones disponibles en los orígenes configurados de Winget. |
| Puede devolver bibliotecas, dependencias y herramientas del sistema. | Generalmente devuelve aplicaciones destinadas al usuario final. |
| La salida es texto estructurado. | La salida es una tabla con información de cada aplicación. |

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

> **💡 Consejo:** En **Winget**, muchas aplicaciones pueden encontrarse tanto por su nombre como por su **ID** (por ejemplo, `Microsoft.VisualStudioCode`). Utilizar el ID evita instalar por error una aplicación con un nombre similar.

---

[⬆️ Volver al índice](#índice)

## Instalar un paquete

### Linux

```bash
sudo apt install <paquete>
```
**Descripción**

Permite instalar un paquete disponible en los repositorios configurados del sistema.

Durante la instalación, APT resuelve automaticamente las dependencias necesarias y solicita confirmación antes de continuar.

### PowerShell

```powershell
winget install <paquete>
```

**Descripción**

Permite instalar una aplicación disponible en los repositorios configurados de Winget.

Winget descarga e instala automáticamente la aplicación seleccionada junto con los componentes necesarios, si procede.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Instalar un paquete | `apt install` | `winget install` |

---

### Ejemplos

**Instalar Git**

Linux

```bash
sudo apt install git
```

PowerShell

```powershell
winget install Git.Git
```

---

**Instalar Visual Studio Code**

Linux

```bash
sudo apt install code
```

PowerShell

```powershell
winget install Microsoft.VisualStudioCode
```

---

**Instalar VLC**

Linux

```bash
sudo apt install vlc
```

PowerShell

```powershell
winget install VideoLAN.VLC
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Instala paquetes desde los repositorios APT configurados. | Instala aplicaciones desde los orígenes configurados en Winget. |
| Resuelve automáticamente las dependencias necesarias. | También gestiona automáticamente la instalación cuando el paquete lo permite. |
| Requiere normalmente permisos de administrador (`sudo`). | Algunas aplicaciones requieren ejecutar PowerShell como administrador. |

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

> **💡 Consejo:** Siempre que sea posible, utiliza el **identificador completo** del paquete en Winget (por ejemplo, `Git.Git` o `Microsoft.VisualStudioCode`). Es más preciso que el nombre común y evita instalar aplicaciones incorrectas cuando existen varias con nombres similares.

---

[⬆️ Volver al índice](#índice)

## Actualizar los paquetes

### Linux

```bash
sudo apt update
```

Para instalar las actualizaciones disponiles:

```bash
sudo apt upgrade
```

También puede realizarse todo en un único comando:

```bash
sudo apt update && sudo apt upgrade
```

**Descripción**

Actualizar el sistema en APT consta de dos pasos:

- `apt update` actualiza la lista de paquetes disponibles en los repositorios.
- `apt upgrade` instala las nuevas versiones de los paquetes ya instalados.

> **Importante:** `apt update` **no actualiza el software**, únicamente actualiza la información de los repositorios.

---

### PowerShell

```powershell
winget upgrade
```

Para actualizar todas las aplicaciones:

```powershell
winget upgrade --all
```

**Descripción**

Permite comprobar qué aplicaciones tiene una versión más reciente disponible.

La opción `--all` instala automáticamente todas las actualizaciones disponibles.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Actualizar la información de los repositorios | `apt update` | `winget source update` *(opcional)* |
| Actualizar los paquetes instalados | `apt upgrade` | `winget upgrade --all` |

---

### Ejemplos

**Actualizar la lista de paquetes**

Linux

```bash
sudo apt update
```

PowerShell

```powershell
winget source update
```

---

**Actualizar todo el software instalado**

Linux

```bash
sudo apt update && sudo apt upgrade
```

PowerShell

```powershell
winget upgrade --all
```

---

**Comprobar qué paquetes pueden actualizarse**

Linux

```bash
apt list --upgradable
```

PowerShell

```powershell
winget upgrade
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Es necesario ejecutar `apt update` antes de instalar las actualizaciones. | Winget consulta automáticamente las versiones disponibles al ejecutar `winget upgrade`. |
| `apt update` y `apt upgrade` realizan tareas distintas. | `winget upgrade` muestra directamente las aplicaciones que pueden actualizarse. |
| La salida es texto estructurado. | La salida es una tabla con las aplicaciones disponibles para actualizar. |

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

> **💡 Consejo:** Mucha gente piensa que `apt update` actualiza el sistema, pero no es así. **`apt update` solo actualiza la información de los repositorios**. Para instalar las nuevas versiones de los paquetes es necesario ejecutar posteriormente **`apt upgrade`**.

---

[⬆️ Volver al índice](#índice)

## Actualizar un paquete concreto

### Linux

```bash
sudo apt install --only-upgrade <paquete>
```

**Descripción**

Permite actualizar únicamente un paquete concreto sin modificar el resto del software instalado.

Si el paquete no está instalado, APT no realizará la actualización.

### Powershell

```powershell
winget upgrade <paquete>
```

También puede utilizarse el identificador del paquete:

```powershell
winget upgrade --id <ID>
```

**Descripción**

Permite actualizar una única aplicación instalada a su versión más reciente.

Es recomendable utilizar el identificador (`--id`) para evitar ambigüedades cuando existe varias aplicaciones con nombres similares.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Actualizar un paquete concreto | `apt install --only-upgrade` | `winget upgrade` |

---

### Ejemplos

**Actualizar Git**

Linux

```bash
sudo apt install --only-upgrade git
```

PowerShell

```powershell
winget upgrade Git.Git
```

---

**Actualizar Visual Studio Code**

Linux

```bash
sudo apt install --only-upgrade code
```

PowerShell

```powershell
winget upgrade Microsoft.VisualStudioCode
```

---

**Actualizar utilizando el ID del paquete**

Linux

```bash
sudo apt install --only-upgrade git
```

PowerShell

```powershell
winget upgrade `
--id Git.Git
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Solo actualiza el paquete indicado si ya está instalado. | Actualiza únicamente la aplicación seleccionada. |
| Utiliza el nombre del paquete presente en los repositorios APT. | Puede utilizarse el nombre o el identificador (`--id`). |
| Requiere normalmente permisos de administrador (`sudo`). | Algunas aplicaciones requieren ejecutar PowerShell como administrador. |

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

> **💡 Consejo:** Actualizar un único paquete es una buena opción cuando solo necesitas corregir un problema concreto o probar una nueva versión de una aplicación sin modificar el resto del sistema.

---

[⬆️ Volver al índice](#índice)

## Eliminar un paquete

### Linux

```bash
sudo apt remove <paquete>
```

También puede utilizarse:

```bash
sudo apt purge <paquete>
```

Para eliminar dependencias que ya no se utilizan:

```bash
sudo apt autoremove
```

**Descripción**

Permite desinstalar paquetes del sistema.

Existen distintas opciones según el nivel de limpieza deseado:

- `apt-remove` -> Elimina el paquete, pero conserva los archivos de configuración.
- `apt purge` -> Elimina el paquete y también sus archivos de configuración.
- `apt autoremove` -> Elimina dependencias instaladas automáticamente que ya no son necesarias.

---

## PowerShell

```powershell
winget uninstall <paquete>
```

También puede utilizarse:

```powershell
winget uninstall --id <ID>
```

**Descripción**

Permite desinstalar una aplicación instalada mediante Winget.

Es recomendable utilizar el identificador (`--id`) cuando existan varias aplicaciones con nombres similares.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar un paquete | `apt remove` | `winget uninstall` |
| Eliminar paquete y configuración | `apt purge` | No existe un equivalente directo |
| Eliminar dependencias innecesarias | `apt autoremove` | No existe un equivalente directo |

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

**Eliminar Visual Studio Code**

Linux

```bash
sudo apt purge code
```

PowerShell

```powershell
winget uninstall Microsoft.VisualStudioCode
```

---

**Eliminar dependencias innecesarias**

Linux

```bash
sudo apt autoremove
```

PowerShell

```powershell
# Winget no dispone de un comando equivalente.
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `apt remove` conserva los archivos de configuración. | `winget uninstall` elimina la aplicación siguiendo el desinstalador del fabricante. |
| `apt purge` elimina también la configuración del paquete. | No existe un cmdlet equivalente para eliminar automáticamente la configuración de todas las aplicaciones. |
| `apt autoremove` elimina dependencias que ya no se utilizan. | Winget no gestiona dependencias de esta forma. |

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

> **💡 Consejo:** Si tienes pensado reinstalar una aplicación más adelante, normalmente es suficiente con utilizar **`apt remove`**. Si deseas eliminar cualquier rastro de configuración y comenzar desde cero, utiliza **`apt purge`**.

---

[⬆️ Volver al índice](#índice)

## Mostrar los paquetes instalados

### Linux

```bash
apt list --installed
```

También puede utilizarse:

```bash
dpkg -l
```

**Descripción**

Permite mostrar todos los papeles instalados en el sistema.

La información puede incluir:

- Nombre del paquete.
- Versión instalada.
- Arquitectura.
- Estado del paquete.

Mientas que `apt list --installed` ofrece una salida más sencilla, `dpkg -l` proporciona información más detallada sobre cada paquete.

---

### Powershell

```powershell
winget list
```

**Descipción**

Permite mostrar todas las aplicaciones detectadas por Winget.

La información puede incluir:

- Nombre de la aplicación.
- Identidicador (ID).
- Versión instalada.
- Origen del paquete.

> **Importante:** `winget list` puede mostrar aplicaciones que no fueron instaladas mediante Winget, siempre que pueda detectarlas correctamente.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Mostrar los paquetes instalados | `apt list --installed` | `winget list` |
| Mostrar información detallada | `dpkg -l` | `winget list` |

---

### Ejemplos

**Mostrar todos los paquetes instalados**

Linux

```bash
apt list --installed
```

PowerShell

```powershell
winget list
```

---

**Buscar un paquete instalado**

Linux

```bash
apt list --installed | grep git
```

PowerShell

```powershell
winget list git
```

---

**Mostrar información detallada de los paquetes**

Linux

```bash
dpkg -l
```

PowerShell

```powershell
winget list
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| `apt list --installed` muestra únicamente los paquetes instalados mediante APT. | `winget list` muestra las aplicaciones detectadas por Winget. |
| `dpkg -l` proporciona información más detallada sobre el estado de los paquetes. | La salida incluye nombre, versión, ID y origen de la aplicación. |
| La salida es texto estructurado. | La salida es una tabla organizada. |

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

> **💡 Consejo:** En servidores Linux es habitual combinar `apt list --installed` o `dpkg -l` con herramientas como `grep` para localizar rápidamente un paquete concreto entre los cientos o miles que pueden estar instalados.

---

[⬆️ Volver al índice](#índice)

## Obtener información de un paquete

### Linux

```bash
apt show <paquete>
```

También puede utilizarse:

```bash
apt-cache show <paquete>
```

**Descripción**

Permite consultar información detallada sobre un paquete disponible en los repositorios o ya instalado.

La información puede incluir:

- Nombre.
- Versión.
- Descripción.
- Tamaño.
- Mantenedor.
- Dependencias.
- Repositorio de origen.

---

### PowerShell

```powershell
winget show <paquete>
```

También puede utilizarse:

```powershell
winget show --id <ID>
```

**Descripción**

Permite mostrar información detallada sobre una aplicación disponible en los orígenes configurados de Winget.

La información puede incluir:

- Nombre.
- Identificador (ID).
- Versión.
- Autor o proveedor.
- Descripción.
- Página oficial.
- Licencia.
- Origen del paquete.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Obtener información de un paquete | `apt show` | `winget show` |

---

### Ejemplos

**Mostrar información de Git**

Linux

```bash
apt show git
```

PowerShell

```powershell
winget show Git.Git
```

---

**Mostrar información de Visual Studio Code**

Linux

```bash
apt show code
```

PowerShell

```powershell
winget show Microsoft.VisualStudioCode
```

---

**Mostrar información utilizando el ID**

Linux

```bash
apt show git
```

PowerShell

```powershell
winget show `
--id Git.Git
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| Muestra información procedente de los repositorios APT. | Muestra información del repositorio configurado en Winget. |
| Incluye dependencias y datos técnicos del paquete. | Incluye información del desarrollador, licencia y página oficial. |
| La salida es texto estructurado. | La salida también es texto estructurado, organizada por secciones. |

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

> **💡 Consejo:** Antes de instalar un programa que no conoces, consulta su información con `apt show` o `winget show`. Revisar la descripción, el proveedor y las dependencias puede ayudarte a confirmar que se trata del software correcto.

---

[⬆️ Volver al índice](#índice)

## Limpiar la caché de paquetes

### Linux

```bash
sudo apt clean
```

También puede utilizarse:

```bash
sudo apt autoclean
```

**Descripción**

APT almacena en caché los paquetes descargados para evitar volver a descargarlos en futuras instalaciones o actualizaciones.

Con el tiempo, esta caché puede ocupar una cantidad considerable de espacio en disco.

Existen dos opciones principales:

- `apt clean` → Elimina **toda** la caché de paquetes descargados.
- `apt autoclean` → Elimina únicamente los paquetes descargados que ya no pueden obtenerse desde los repositorios.

---

### PowerShell

```powershell
winget source reset --force
```

También puede utilizarse:

```powershell
winget source update
```

**Descripción**

Winget no dispone de un comando equivalente para limpiar una caché de paquetes como APT.

Los comandos disponibles permiten restaurar o actualizar la información de los orígenes configurados, pero **no eliminan archivos descargados del mismo modo que `apt clean`**.

---

### Equivalencia

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Eliminar toda la caché | `apt clean` | No existe un equivalente directo |
| Eliminar únicamente paquetes obsoletos | `apt autoclean` | No existe un equivalente directo |
| Restablecer la información de los repositorios | — | `winget source reset --force` |

---

### Ejemplos

**Eliminar toda la caché de APT**

Linux

```bash
sudo apt clean
```

---

**Eliminar únicamente paquetes obsoletos**

Linux

```bash
sudo apt autoclean
```

---

**Restablecer los orígenes de Winget**

PowerShell

```powershell
winget source reset --force
```

---

**Actualizar la información de los orígenes**

PowerShell

```powershell
winget source update
```

---

### Diferencias

| Linux | PowerShell |
|--------|------------|
| APT almacena los paquetes descargados en una caché local. | Winget no utiliza una caché gestionable mediante un comando equivalente. |
| `apt clean` puede liberar una cantidad importante de espacio en disco. | Los comandos de Winget únicamente administran los orígenes del repositorio. |
| `apt autoclean` conserva los paquetes que todavía pueden reutilizarse. | No existe una funcionalidad equivalente. |

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

> **💡 Consejo:** A diferencia de APT, **Winget no mantiene una caché de paquetes descargados que pueda limpiarse mediante un comando**. Por ello, este apartado tiene equivalente en Linux, pero no existe una operación idéntica en PowerShell.

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

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Buscar software | `apt search` | `winget search` |
| Instalar software | `apt install` | `winget install` |
| Actualizar repositorios | `apt update` | `winget source update` |
| Actualizar software | `apt upgrade` | `winget upgrade --all` |
| Desinstalar software | `apt remove` | `winget uninstall` |
| Ver software instalado | `apt list --installed` | `winget list` |
| Ver información de un paquete | `apt show` | `winget show` |

---

### Flujo de trabajo recomendado

Cuando necesites instalar una aplicación nueva, el proceso habitual suele ser:

1. Buscar el paquete disponible.
2. Consultar su información.
3. Instalarlo.
4. Verificar que se ha instalado correctamente.
5. Mantenerlo actualizado.
6. Desinstalarlo cuando deje de ser necesario.

---

[⬆️ Volver al índice](#índice)