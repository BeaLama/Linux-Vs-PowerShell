# Permisos avanzados

## Introducción

Los permisos son uno de los elementos fundamentales en la administración de sistemas, ya que permiten controlar quién puede acceder a los recursos y qué acciones puede realizar sobre ellos.

---

## Índice

- [ACL en Linux](#acl-en-linux)
- [Permisos especiales Linux](#permisos-especiales-linux)
- [ACL en Windows](#acl-en-windows)
- [Herencia de permisos](#herencia-de-permisos)
- [Permisos efectivos](#permisos-efectivos)
- [Delegación de permisos](#delegación-de-permisos)
- [Auditoría de permisos](#auditoría-de-permisos)

---

## ACL en Linux

Las **ACL (Access Control Lists)** permiten asignar permisos específicos a usuarios y grupos individuales sin modificar los permisos tradicionales de propietario, grupo y otros.*

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `mount \| grep acl` | *(no aplica)* |

---

### Ver las ACL de un archivo

Para consultar las ACL de un archivo se utiliza:

```bash
getfacl archivo.txt
```
Ejemplo:

```bash
getfacl informe.txt
```

---

### Asignar ACL a un usuario

Para conceder permisos a un usuario específico:

```bash
setfacl -m u:usuario:permisos archivo
```

Ejemplo:

```bash
setfacl -m u:juan:rw informe.txt
```

Ahora **juan** podrá leer y modificar el archivo aunque no sea el propietario.

Comprobar:

```bash
getfacl informe.txt
```

---

### Asignar ACL a un grupo

También pueden asignarse permisos a un grupo.

Sintaxis:

```bash
setfacl -m g:grupo:permisos archivo
```

Ejemplo:

```bash
setfacl -m g:informatica:rwx proyecto
```

---

### Eliminar una ACL

Eliminar permisos de un usuario:

```bash
setfacl -x u:juan informe.txt
```

Eliminar permisos de un grupo:

```bash
setfacl -x g:informatica informe.txt
```

---

### Eliminar todas las ACL

Para volver únicamente a los permisos tradicionales:

```bash
setfacl -b informe.txt
```

Esto elimina todas las ACL del archivo.

---

[⬆️ Volver al índice](#índice)

## Permisos especiales Linux

Además de los permisos tradicionales (**lectura, escritura y ejecución**), Linux dispone de tres permisos especiales que proporcionan un comportamiento diferente al habitual:

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `ls -l /usr/bin/passwd` | *(no aplica)* |

---

## Ejemplo práctico

*Supongamos un directorio compartido:*

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `chmod g+s proyectos` | *(no aplica)* |

---

[⬆️ Volver al índice](#índice)

## ACL en Windows

En Windows, los permisos avanzados se gestionan mediante las **ACL (Access Control Lists)** o **Listas de Control de Acceso**.

| Acción | Linux | Windows |
|---------|--------|----------|
| Consultar permisos | `getfacl` | `Get-Acl` |
| Modificar permisos | `setfacl` | `Set-Acl` |
| Propietario | `chown` | Owner |
| Permisos especiales | ACL | ACL NTFS |
| Gestión gráfica | No habitual | Explorador de archivos |

| Linux (ACL) | Windows (ACL NTFS) |
|--------------|--------------------|
| Basadas en usuarios y grupos. | Basadas en usuarios, grupos y cuentas del sistema. |
| Se gestionan principalmente mediante comandos. | Disponen de una interfaz gráfica muy completa. |
| Menor número de permisos predefinidos. | Gran variedad de permisos específicos. |
| La herencia suele utilizarse principalmente en directorios. | La herencia es un elemento fundamental del sistema NTFS. |

---

[⬆️ Volver al índice](#índice)

## Herencia de permisos

La **herencia de permisos** es un mecanismo que permite que archivos y carpetas reciban automáticamente los permisos definidos en su carpeta padre.*

| Característica | Linux | Windows |
|----------------|--------|----------|
| Herencia en permisos tradicionales | No | Sí |
| Herencia mediante ACL | Sí | Sí |
| Herencia del grupo | SGID | Integrada |
| Herencia de permisos NTFS | No aplica | Integrada |

| Característica | Linux | Windows |
|----------------|--------|----------|
| Propietario | Sí | Sí |
| Grupos | Sí | Sí |
| ACL | Opcional | Integrada en NTFS |
| Herencia | Solo mediante ACL | Integrada |
| Permisos de denegación | No existen como tal | Sí (`Deny`) |
| Cálculo automático | Manual | Herramienta de "Acceso efectivo" |

---

[⬆️ Volver al índice](#índice)

## Delegación de permisos

La **delegación de permisos** consiste en conceder a un usuario o grupo la capacidad de realizar determinadas tareas administrativas sin otorgarle privilegios completos sobre el sistema.*

| Método | Linux | Windows |
|---------|--------|----------|
| Grupos | Sí | Sí |
| ACL | Sí | Sí |
| Permisos elevados | `sudo` | Grupos administrativos / UAC |
| Delegación parcial | `sudoers`, ACL, Capabilities | ACL, GPO, Active Directory |
| Administración centralizada | Limitada | Active Directory |

---

[⬆️ Volver al índice](#índice)

## Auditoría de permisos

La **auditoría de permisos** consiste en revisar y supervisar quién tiene acceso a un recurso, qué acciones puede realizar y quién ha accedido realmente a dicho recurso.*

| Acción | Linux | Windows |
|---------|--------|----------|
| Revisar permisos | `ls -l` | Propiedades → Seguridad |
| Revisar ACL | `getfacl` | `Get-Acl` |
| Auditoría integrada | `auditd` | Auditoría NTFS |
| Consultar eventos | `/var/log` | Visor de eventos |
| Buscar permisos especiales | `find` | PowerShell |

---

[⬆️ Volver al índice](#índice)

## Buenas prácticas

Una correcta gestión de permisos es esencial para proteger la información, reducir riesgos de seguridad y facilitar la administración de sistemas.*

| 🐧 Linux | 🪟 PowerShell |
|---|---|
| `find /datos -perm -777` | `Get-Acl C:\Compartido` |

---

[⬆️ Volver al índice](#índice)