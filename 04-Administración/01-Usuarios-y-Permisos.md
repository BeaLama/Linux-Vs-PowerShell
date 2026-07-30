# Usuarios y permisos

## Introducción


La gestión de usuarios y permisos es una de las tareas más importantes dentro de la administración de sistemas.

Los sistemas operativos necesitan mecanismos que permitan identificar a los usuarios, controlar sus accesos y limitar las acciones que pueden realizar sobre los recursos disponibles.

Cada usuario dentro de un sistema posee una identidad asociada, la cual determina cómo será reconocido por el sistema y qué permisos tendrá asignados. Estos permisos permiten controlar el acceso a archivos, carpetas, aplicaciones, servicios y otros recursos.

En entornos empresariales, la correcta administración de usuarios es fundamental para mantener la seguridad de la infraestructura. La creación de cuentas, asignación de permisos, pertenencia a grupos y gestión de privilegios deben realizarse siguiendo criterios de organización y seguridad.

Una mala configuración de usuarios o permisos puede provocar problemas como:

- Accesos no autorizados.
- Exposición de información sensible.
- Escaladas de privilegios.
- Pérdida de control sobre los recursos.
- Dificultad para realizar auditorías.

Por este motivo, los administradores de sistemas deben conocer cómo funcionan los usuarios, grupos y permisos tanto en sistemas Windows como Linux, además de aplicar principios como el mínimo privilegio y la correcta separación de funciones.

En este apartado se estudiará la gestión completa del ciclo de vida de los usuarios, desde su creación y configuración inicial hasta su modificación, auditoría y eliminación.

---

## Índice

- [Concepto de identidad digital](#concepto-de-identidad-digital)
- [Usuarios en sistemas operativos](#usuarios-en-sistemas-operativos)
- [Tipos de usuarios](#tipos-de-usuarios)
- [Grupos de usuarios](#grupos-de-usuarios)
- [Identificadores de usuario](#identificadores-de-usuario)
- [Autenticación y autorización](#autenticación-y-autorización)
- [Gestión de usuarios en Windows](#gestión-de-usuarios-en-windows)
- [Gestión de usuarios en Linux](#gestión-de-usuarios-en-linux)
- [Active Directory y usuarios empresariales](#active-directory-y-usuarios-empresariales)
- [Permisos de archivos y recursos](#permisos-de-archivos-y-recursos)
- [Listas de control de acceso (ACL)](#listas-de-control-de-acceso-acl)
- [Herencia de permisos](#herencia-de-permisos)
- [Roles y privilegios administrativos](#roles-y-privilegios-administrativos)
- [Cuentas de servicio](#cuentas-de-servicio)
- [Gestión del ciclo de vida de usuarios](#gestión-del-ciclo-de-vida-de-usuarios)
- [Auditoría de usuarios y permisos](#auditoría-de-usuarios-y-permisos)
- [Buenas prácticas de seguridad](#buenas-prácticas-de-seguridad)

--- 

