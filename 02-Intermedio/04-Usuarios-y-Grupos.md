# Usuarios y grupos

## Introducción

Los usuarios y grupos permiten organizar y controlar el acceso a los recursos del sistema.

Cada usuario dispone de una identidad propia, mientras que los grupos facilitan la asignación de permisos a varios usuarios de forma simultánea.

Administrar correctamente usuarios y grupos es una tarea esencial para mantener la seguridad, el orden y el correcto funcionamiento de equipos y servidores.

---

## Índice

- [Listar usuarios](#listar-usuarios)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un usuario](#crear-un-usuario)
- [Eliminar un usuario](#eliminar-un-usuario)
- [Listar grupos](#listar-grupos)
- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

## Listar usuarios

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cat /etc/passwd` | `Get-LocalUser` |

**Ejemplo**
```bash
cat /etc/passwd | grep usuario
```
```powershell
Get-LocalUser usuario
```

> 💡 **Diferencia clave** — 🐧 Los usuarios se almacenan en `/etc/passwd`. · 🪟 Los usuarios se almacenan en la base de datos de cuentas locales de Windows.

---

### Comandos relacionados

- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un usuario](#crear-un-usuario)
- [Eliminar un usuario](#eliminar-un-usuario)

---

[⬆️ Volver al índice](#índice)

## Consultar información de un usuario

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `id <usuario>` | `Get-LocalUser <usuario>` |
| **Ejemplo** | `id` | `Get-LocalUser $env:USERNAME` |

> 💡 **Diferencia clave** — 🐧 `id` muestra el UID, GID y todos los grupos del usuario. · 🪟 `Get-LocalUser` muestra únicamente la información de la cuenta.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Crear un usuario](#crear-un-usuario)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Crear un usuario

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo useradd <usuario>` | `New-LocalUser -Name <usuario>` |
| **Ejemplo** | `sudo useradd -m usuario` | `New-LocalUser -Name "usuario"` |

> 💡 **Diferencia clave** — 🐧 `useradd` crea la cuenta de forma básica. · 🪟 `New-LocalUser` crea un usuario local de Windows.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Eliminar un usuario](#eliminar-un-usuario)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Eliminar un usuario

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo userdel <usuario>` | `Remove-LocalUser -Name <usuario>` |
| **Ejemplo** | `sudo userdel -r usuario` | `Remove-LocalUser -Name "usuario"` |

> 💡 **Diferencia clave** — 🐧 `userdel` elimina la cuenta del usuario. · 🪟 `Remove-LocalUser` elimina la cuenta local del usuario.

---

### Comandos relacionados

- [Listar usuarios](#listar-usuarios)
- [Crear un usuario](#crear-un-usuario)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)

---

[⬆️ Volver al índice](#índice)

## Listar grupos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `cat /etc/group` | `Get-LocalGroup` |

**Ejemplo**
```bash
cat /etc/group | grep desarrolladores
```
```powershell
Get-LocalGroup desarrolladores
```

> 💡 **Diferencia clave** — 🐧 Los grupos se almacenan en `/etc/group`. · 🪟 Los grupos se almacenan en la base de datos de grupos locales de Windows.

---

### Comandos relacionados

- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Crear un grupo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo groupadd <grupo>` | `New-LocalGroup -Name <grupo>` |

**Ejemplo**
```bash
sudo groupadd administradores
```
```powershell
New-LocalGroup `
-Name "administradores" `
-Description "Grupo de administradores del sistema"
```

> 💡 **Diferencia clave** — 🐧 `groupadd` crea un nuevo grupo local. · 🪟 `New-LocalGroup` crea un grupo local de Windows.

---

### Comandos relacionados

- [Listar grupos](#listar-grupos)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Agregar un usuario a un grupo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo usermod -aG <grupo> <usuario>` | `Add-LocalGroupMember -Group <grupo> -Member <usuario>` |

**Ejemplo**
```bash
sudo usermod -aG desarrolladores,docker usuario
```
```powershell
Add-LocalGroupMember -Group "desarrolladores" -Member "usuario"

Add-LocalGroupMember -Group "docker" -Member "usuario"
```

> 💡 **Diferencia clave** — 🐧 `usermod -aG` permite agregar uno o varios grupos en un único comando. · 🪟 `Add-LocalGroupMember` agrega el usuario a un grupo cada vez.

---

### Comandos relacionados

- [Consultar información de un usuario](#consultar-información-de-un-usuario)
- [Crear un grupo](#crear-un-grupo)
- [Eliminar un usuario de un grupo](#eliminar-un-usuario-de-un-grupo)

---

[⬆️ Volver al índice](#índice)

## Eliminar un usuario de un grupo

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `sudo gpasswd -d <usuario> <grupo>` | `Remove-LocalGroupMember -Group <grupo> -Member <usuario>` |

**Ejemplo**
```bash
sudo gpasswd -d usuario desarrolladores

sudo gpasswd -d usuario docker
```
```powershell
Remove-LocalGroupMember -Group "desarrolladores" -Member "usuario"

Remove-LocalGroupMember -Group "docker" -Member "usuario"
```

> 💡 **Diferencia clave** — 🐧 `gpasswd -d` elimina la pertenencia a un grupo. · 🪟 `Remove-LocalGroupMember` elimina al usuario del grupo indicado.

---

### Comandos relacionados

- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)

---

[⬆️ Volver al índice](#índice)