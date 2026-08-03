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
- [Resumen de equivalencias](#resumen-de-equivalencias)

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

### Buenas prácticas

- Comprueba periódicamente qué usuarios existen en el sistema.
- Elimina o deshabilita las cuentas que ya no sean necesarias.
- Evita utilizar cuentas compartidas entre varios usuarios.
- Revisa que únicamente existan cuentas con privilegios administrativos cuando sea realmente necesario.

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

### Buenas prácticas

- Comprueba siempre a qué grupos pertenece un usuario antes de modificar sus permisos.
- Verifica el UID y el grupo principal cuando administres usuarios en Linux.
- Revisa periódicamente las cuentas con privilegios administrativos.
- Mantén actualizada la información descriptiva de las cuentas cuando sea posible.

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

### Buenas prácticas

- Utiliza nombres de usuario claros y fáciles de identificar.
- Asigna una descripción cuando el usuario vaya a administrarse durante largo tiempo.
- Evita utilizar cuentas compartidas entre varias personas.
- Comprueba que el usuario se ha creado correctamente antes de asignarle permisos o grupos.

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

### Buenas prácticas

- Verifica que el usuario ya no necesita acceder al sistema antes de eliminarlo.
- Realiza una copia de seguridad de la información importante del usuario si es necesario.
- Comprueba que el usuario no está ejecutando procesos antes de eliminar la cuenta.
- Elimina únicamente las cuentas que ya no vayan a utilizarse.

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

### Buenas prácticas

- Utiliza grupos para administrar permisos en lugar de asignarlos directamente a cada usuario.
- Mantén una estructura de grupos clara y coherente.
- Elimina los grupos que ya no sean necesarios.
- Revisa periódicamente qué grupos existen en el sistema.

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

### Buenas prácticas

- Utiliza nombres descriptivos y coherentes para los grupos.
- Agrupa usuarios con funciones similares en lugar de crear grupos para cada usuario.
- Añade una descripción cuando el grupo vaya a utilizarse durante largo tiempo.
- Revisa periódicamente los grupos existentes para eliminar aquellos que ya no sean necesarios.

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

### Buenas prácticas

- Utiliza siempre `-aG` con `usermod` para evitar eliminar otros grupos del usuario.
- Asigna los permisos mediante grupos en lugar de hacerlo usuario por usuario.
- Comprueba la pertenencia al grupo después de realizar el cambio.
- Agrega únicamente a los usuarios que realmente necesiten los permisos del grupo.

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

### Buenas prácticas

- Comprueba que el usuario realmente ya no necesita los permisos del grupo.
- Verifica la pertenencia del usuario después de realizar el cambio.
- Evita eliminar usuarios de grupos críticos sin conocer el impacto.
- Mantén actualizada la pertenencia a grupos para aplicar correctamente el principio de mínimo privilegio.

---

### Comandos relacionados

- [Crear un grupo](#crear-un-grupo)
- [Agregar un usuario a un grupo](#agregar-un-usuario-a-un-grupo)
- [Consultar información de un usuario](#consultar-información-de-un-usuario)

---

[⬆️ Volver al índice](#índice)

## Resumen de equivalencias

| Acción | Linux | PowerShell |
|--------|--------|------------|
| Listar usuarios | `getent passwd` / `cat /etc/passwd` | `Get-LocalUser` |
| Consultar información de un usuario | `id` | `Get-LocalUser` |
| Crear un usuario | `adduser` / `useradd` | `New-LocalUser` |
| Eliminar un usuario | `userdel` | `Remove-LocalUser` |
| Listar grupos | `getent group` / `cat /etc/group` | `Get-LocalGroup` |
| Crear un grupo | `groupadd` | `New-LocalGroup` |
| Agregar un usuario a un grupo | `usermod -aG` / `gpasswd -a` | `Add-LocalGroupMember` |
| Eliminar un usuario de un grupo | `gpasswd -d` | `Remove-LocalGroupMember` |

---

### Buenas prácticas generales

- Utiliza grupos para asignar permisos en lugar de hacerlo directamente a los usuarios.
- Evita utilizar cuentas compartidas entre varias personas.
- Aplica siempre el principio de **mínimo privilegio**: cada usuario debe disponer únicamente de los permisos necesarios para realizar su trabajo.
- Revisa periódicamente los usuarios y grupos existentes para eliminar cuentas o grupos que ya no sean necesarios.
- Comprueba siempre los cambios realizados antes de asignar permisos sobre archivos, carpetas o servicios.
- Documenta las cuentas administrativas y los grupos con privilegios elevados.

---

### Comandos más utilizados

| Acción | Linux | PowerShell |
|---------|--------|------------|
| Ver usuarios | `getent passwd` | `Get-LocalUser` |
| Ver grupos | `getent group` | `Get-LocalGroup` |
| Consultar un usuario | `id usuario` | `Get-LocalUser usuario` |
| Crear un usuario | `adduser usuario` | `New-LocalUser -Name "usuario"` |
| Eliminar un usuario | `userdel usuario` | `Remove-LocalUser -Name "usuario"` |
| Crear un grupo | `groupadd desarrolladores` | `New-LocalGroup -Name "desarrolladores"` |
| Agregar usuario a un grupo | `usermod -aG desarrolladores usuario` | `Add-LocalGroupMember -Group "desarrolladores" -Member "usuario"` |
| Eliminar usuario de un grupo | `gpasswd -d usuario desarrolladores` | `Remove-LocalGroupMember -Group "desarrolladores" -Member "usuario"` |

---

[⬆️ Volver al índice](#índice)