# Permisos

## Introducción

Los permisos determinan qué usuarios pueden leer, modificar o ejecutar archivos y directorios.

Comprender el funcionamiento de los permisos es fundamental para proteger la información del sistema, evitar accesos no autorizados y administrar correctamente equipos y servidores.

Linux y Windows utilizan modelos de permisos diferentes, pero ambos persiguen el mismo objetivo: controlar el acceso a los recursos del sistema.

---

## Índice
- [Consultar permisos](#consultar-permisos)
- [Interpretar los permisos](#interpretar-los-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Permisos recursivos](#permisos-recursivos)
- [Permisos especiales](#permisos-especiales)

---

## Consultar permisos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `ls -l` | `Get-Acl <ruta>` |
| **Ejemplo** | `ls -l informe.txt` | `Get-Acl .\informe.txt` |

> 💡 **Diferencia clave** — 🐧 `ls -l` muestra los permisos mediante la notación `rwx`. · 🪟 `Get-Acl` utiliza listas de control de acceso (ACL).

---

### Comandos relacionados

- [Interpretar los permisos](#interpretar-los-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)

---

[⬆️ Volver al índice](#índice)

## Interpretar los permisos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | *(no aplica)* | `Get-Acl .\archivo.txt` |
| **Ejemplo** | *(no aplica)* | *(no aplica)* |

> 💡 **Diferencia clave** — 🐧 Utiliza permisos POSIX representados mediante `rwx`. · 🪟 Utiliza listas de control de acceso (ACL).

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)

---

[⬆️ Volver al índice](#índice)

## Cambiar permisos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chmod <permisos> <archivo>` | `icacls <ruta> /grant <usuario>:<permisos>` |
| **Ejemplo** | `chmod 600 informe.txt` | `icacls .\informe.txt /grant Usuario:M` |

> 💡 **Diferencia clave** — 🐧 `chmod` modifica permisos POSIX (`rwx`). · 🪟 `icacls` modifica permisos NTFS mediante ACL.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Cambiar propietario

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chown <propietario> <archivo>` | `takeown /F <ruta>` |
| **Ejemplo** | `sudo chown usuario Documentos` | `takeown /F .\Documentos` |

> 💡 **Diferencia clave** — 🐧 `chown` cambia el propietario de archivos y directorios. · 🪟 `takeown` asigna la propiedad del recurso al usuario actual o al administrador.

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Permisos recursivos

| | 🐧 Linux | 🪟 PowerShell |
|---|---|---|
| **Sintaxis** | `chmod -R <permisos> <directorio>` | `icacls <ruta> /grant <usuario>:<permisos> /T` |
| **Ejemplo** | `sudo chown -R usuario Proyecto` | `takeown /F .\Proyecto /R` |

> 💡 **Diferencia clave** — 🐧 La opción `-R` aplica los cambios a todos los archivos y subdirectorios. · 🪟 La opción `/T` aplica los cambios de permisos de forma recursiva.

---

### Comandos relacionados

- [Cambiar permisos](#cambiar-permisos)
- [Cambiar propietario](#cambiar-propietario)
- [Cambiar grupo](#cambiar-grupo)

---

[⬆️ Volver al índice](#índice)

## Permisos especiales

| Permiso Linux | Octal | Función | Equivalente PowerShell |
|---|---|---|---|
| SUID | `4` | Ejecuta con permisos del propietario | *(no existe; usa ACL/NTFS)* |
| SGID | `2` | Ejecuta con permisos del grupo / hereda grupo | Herencia de permisos vía ACL |
| Sticky Bit | `1` | Solo el propietario puede borrar en un directorio | *(no existe)* |

**Ejemplo** — `chmod g+s Proyecto` / `chmod 2775 Proyecto`

> 💡 **Diferencia clave** — 🐧 Linux tiene 3 bits especiales (SUID/SGID/Sticky) además de `rwx`. · 🪟 Windows resuelve estos casos con ACL/NTFS (herencia, permisos explícitos, propietario).

---

### Comandos relacionados

- [Consultar permisos](#consultar-permisos)
- [Cambiar permisos](#cambiar-permisos)
- [Permisos recursivos](#permisos-recursivos)

---

[⬆️ Volver al índice](#índice)
