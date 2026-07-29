# Paquetes

## Introducción

Los gestores de paquetes permiten instalar, actualizar, eliminar y administrar el software del sistema de forma sencilla y segura.

Cada distribución Linux utiliza su propio gestor de paquetes (APT, DNF, YUM, Pacman, Zypper, etc.), mientras que Windows dispone de herramientas como **Winget** y **PowerShell PackageManagement** para realizar tareas similares.

En este capítulo aprenderás las operaciones más habituales relacionadas con la gestión de paquetes tanto en Linux como en PowerShell.

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

```

**Descripción**

### Powershell

```powershell

```

**Descripción**

