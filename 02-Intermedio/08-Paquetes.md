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

---

## Buscar un paquete

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `apt search <paquete>` | `winget search <paquete>` |
| **Ejemplo** | `apt search code` | `winget search vscode` |

> 💡 **Diferencia clave** — 🐧 Busca paquetes disponibles en los repositorios APT configurados. · 🪟 Busca aplicaciones disponibles en los orígenes configurados de Winget.

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

### Comandos relacionados

- [Actualizar los paquetes](#actualizar-los-paquetes)
- [Buscar un paquete](#buscar-un-paquete)
- [Mostrar los paquetes instalados](#mostrar-los-paquetes-instalados)

---

[⬆️ Volver al índice](#índice)