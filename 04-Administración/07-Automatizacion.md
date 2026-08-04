# Automatización 

## Introducción

La automatización consiste en utilizar scripts, herramientas y procesos programados para ejecutar tareas de forma automática, reduciendo la intervención manual del administrador.

## Índice

- [Concepto de automatización](#concepto-de-automatizacion)
- [Ventajas e inconvenientes](#ventajas-e-inconvenientes)
- [Scripts de automatización](#scripts-de-automatizacion)
- [PowerShell como herramienta de automatización](#powershell-como-herramienta-de-automatizacion)
- [Scripts Bash en Linux](#scripts-bash-en-linux)
- [Automatización mediante tareas programadas](#automatizacion-mediante-tareas-programadas)
- [Automatización en entornos empresariales](#automatizacion-en-entornos-empresariales)
- [Herramientas de automatización](#herramientas-de-automatizacion)
- [Seguridad en la automatización](#seguridad-en-la-automatizacion)
- [Resolución de problemas habituales](#resolucion-de-problemas-habituales)

---

## Concepto de automatización

*La automatización consiste en utilizar programas, scripts o herramientas capaces de ejecutar tareas de forma automática, sin que sea necesaria la intervención constante del administrador.*

**Conceptos clave:**

- **¿Qué es la automatización?:** La automatización consiste en sustituir procesos manuales por tareas ejecutadas automáticamente mediante software.
- **Objetivo de la automatización:** El objetivo principal es reducir el trabajo repetitivo del administrador.
- **Funcionamiento:** El proceso de automatización puede representarse así.
- **Tareas que pueden automatizarse:** En administración de sistemas es habitual automatizar procesos como: Creación de usuarios.
- **Automatización mediante scripts:** Una de las formas más habituales de automatizar tareas consiste en utilizar scripts.
- **Automatización programada:** Muchas tareas se ejecutan automáticamente en determinados momentos.
- **Automatización basada en eventos:** También es posible ejecutar tareas únicamente cuando ocurre una determinada condición.
- **Ámbitos de utilización:** La automatización se utiliza en numerosos escenarios.
- **Ventajas generales:** La automatización aporta importantes beneficios.

---

## Ventajas e inconvenientes

*La automatización aporta importantes beneficios a la administración de sistemas, ya que permite ejecutar tareas de forma rápida, uniforme y sin intervención constante del administrador.*

**Conceptos clave:**

- **Ventajas de la automatización:** La automatización mejora notablemente la gestión de los sistemas informáticos.
- **Ahorro de tiempo:** Muchas tareas administrativas deben realizarse de forma periódica.
- **Reducción de errores:** Las tareas manuales pueden dar lugar a errores como: Introducir datos incorrectos.
- **Mayor productividad:** Un único script puede realizar el trabajo que anteriormente requería intervenir manualmente en decenas o cientos de equipos.
- **Estandarización:** Los procesos automatizados siguen siempre la misma secuencia de pasos.
- **Disponibilidad:** Las tareas automatizadas pueden ejecutarse: De madrugada.
- **Inconvenientes:** Aunque la automatización ofrece numerosas ventajas, también presenta algunas limitaciones.
- **Errores en los scripts:** Si un script contiene un error, este puede repetirse automáticamente en todos los equipos afectados.
- **Mantenimiento:** Los procesos automatizados también requieren mantenimiento.

### Comparativa

| Ventajas | Inconvenientes |
|----------|----------------|
| Ahorro de tiempo. | Tiempo inicial de desarrollo. |
| Menor número de errores. | Necesidad de realizar pruebas. |
| Mayor productividad. | Posibles errores en los scripts. |
| Procesos estandarizados. | Requiere mantenimiento periódico. |
| Ejecución automática. | Un fallo puede afectar a muchos equipos. |

---

## Scripts de automatización

*Los scripts de automatización son pequeños programas que contienen una secuencia de instrucciones destinadas a ejecutar tareas de forma automática.*

**Conceptos clave:**

- **¿Qué es un script?:** Un script es un archivo de texto que contiene una serie de comandos ejecutados de forma secuencial por un intérprete.
- **Funcionamiento:** El funcionamiento de un script puede representarse así.
- **Tareas habituales:** Los scripts permiten automatizar numerosas operaciones administrativas.
- **Ventajas de utilizar scripts:** El uso de scripts ofrece numerosos beneficios.
- **Estructura básica:** Aunque la sintaxis depende del lenguaje utilizado, la mayoría de scripts siguen una estructura similar.
- **Variables:** Las variables permiten almacenar información durante la ejecución del script.
- **Condiciones:** Los scripts pueden tomar decisiones mediante estructuras condicionales.
- **Bucles:** Los bucles permiten repetir una misma acción varias veces sin escribir el mismo código repetidamente.
- **Registro de resultados:** Es recomendable que los scripts registren la información sobre su ejecución.

---

## PowerShell como herramienta de automatización

*PowerShell es la consola de administración y lenguaje de scripting desarrollado por Microsoft para automatizar tareas en sistemas Windows.*

**Conceptos clave:**

- **¿Qué es PowerShell?:** PowerShell es una consola de comandos basada en .NET que permite administrar sistemas mediante comandos y scripts.

### Cmdlets

*Los comandos de PowerShell reciben el nombre de cmdlets.*

```powershell
Get-Service
```
```powershell
Restart-Service
```

---

**Conceptos clave:**

- **Automatización mediante scripts:** Los scripts de PowerShell utilizan la extensión.

### Variables

*Las variables se identifican mediante el símbolo.*

```powershell
$
```
```powershell
$Servidor = "SRV-01"
```

---

### Condiciones

*PowerShell permite ejecutar instrucciones únicamente cuando se cumple una determinada condición.*

```powershell
if ($true) {

}
```

---

### Bucles

*Los bucles permiten repetir una tarea varias veces.*

```powershell
foreach ($Equipo in $Equipos) {

}
```

---

### Ejecución remota

*PowerShell permite ejecutar comandos en equipos remotos mediante PowerShell Remoting.*

```powershell
Invoke-Command -ComputerName SERVIDOR01 -ScriptBlock {
Get-Service
}
```

---

**Conceptos clave:**

- **Programación de scripts:** Los scripts pueden ejecutarse automáticamente mediante el Programador de tareas de Windows.
- **Ventajas:** PowerShell ofrece numerosas ventajas para la automatización.

---

## Scripts Bash en Linux

*Bash (Bourne Again SHell) es el intérprete de comandos más utilizado en sistemas Linux y uno de los principales lenguajes de scripting para la automatización de tareas.*

**Conceptos clave:**

- **¿Qué es Bash?:** Bash es un intérprete de comandos que permite interactuar con el sistema operativo mediante una consola de texto.
- **¿Qué es un script Bash?:** Un script Bash es un archivo de texto que contiene comandos del sistema Linux escritos para ejecutarse automáticamente.

### Estructura básica

*Todo script Bash suele comenzar indicando el intérprete que debe utilizarse.*

```bash
#!/bin/bash
```

---

### Variables

*Las variables permiten almacenar información durante la ejecución del script.*

```bash
usuario="admin"
```
```bash
echo $usuario
```

---

### Condiciones

*Bash permite ejecutar acciones únicamente cuando se cumple una determinada condición.*

```bash
if [ -f archivo.txt ]
then
    echo "El archivo existe"
fi
```

---

### Bucles

*Los bucles permiten repetir automáticamente una serie de instrucciones.*

```bash
for archivo in *.log
do
    echo $archivo
done
```

---

### Permisos de ejecución

*Antes de ejecutar un script es necesario concederle permisos.*

```bash
chmod +x script.sh
```
```bash
./script.sh
```

---

**Conceptos clave:**

- **Tareas habituales:** Los scripts Bash permiten automatizar numerosas operaciones.
- **Ventajas:** Bash ofrece importantes ventajas.

---

## Automatización mediante tareas programadas

*No todas las tareas automatizadas deben ejecutarse manualmente.*

**Conceptos clave:**

- **¿Qué son las tareas programadas?:** Las tareas programadas permiten ejecutar automáticamente una acción cuando se cumple una condición previamente definida.
- **Funcionamiento:** El proceso puede representarse así.
- **Programador de tareas en Windows:** Windows incorpora el Programador de tareas (*Task Scheduler*), una herramienta que permite automatizar la ejecución de programas, scripts y comandos.
- **Elementos de una tarea programada:** Una tarea suele estar formada por varios componentes.
- **Desencadenadores:** El desencadenador indica el momento en el que debe iniciarse la tarea.
- **Acciones:** La acción define qué realizará la tarea.
- **Cron en Linux:** En sistemas Linux la herramienta más utilizada para programar tareas es cron.

### Ejemplo de programación en cron

*Un ejemplo sencillo sería.*

```bash
0 2 * * * /home/admin/backup.sh
```

---

**Conceptos clave:**

- **Ventajas:** La programación de tareas ofrece numerosas ventajas.

---

## Automatización en entornos empresariales

*En las organizaciones actuales, la automatización constituye uno de los pilares fundamentales de la administración de sistemas.*

**Conceptos clave:**

- **Administración de grandes infraestructuras:** En una empresa pueden existir: Cientos de equipos.
- **Automatización del despliegue de software:** Una de las tareas más habituales consiste en instalar aplicaciones automáticamente.
- **Automatización de actualizaciones:** Las empresas suelen automatizar la instalación de actualizaciones del sistema operativo y de las aplicaciones.
- **Gestión automática de usuarios:** Muchas organizaciones automatizan tareas relacionadas con las cuentas de usuario.
- **Automatización de copias de seguridad:** Las copias de seguridad son uno de los procesos que con mayor frecuencia se automatizan.
- **Monitorización automática:** Los sistemas de monitorización pueden ejecutar acciones automáticamente cuando detectan determinados eventos.
- **Automatización en la nube:** Las plataformas cloud incorporan numerosas funciones de automatización.
- **Beneficios para la empresa:** La automatización proporciona numerosas ventajas.
- **Retos de la automatización:** La automatización también presenta algunos desafíos.

---

## Herramientas de automatización

*La automatización puede llevarse a cabo mediante una amplia variedad de herramientas, desde lenguajes de scripting hasta plataformas especializadas para la gestión de infraestructuras completas.*

**Conceptos clave:**

- **Tipos de herramientas:** Las herramientas de automatización pueden clasificarse en varios grupos.
- **PowerShell:** PowerShell es la herramienta de automatización integrada en Windows.
- **Bash:** Bash es el intérprete de comandos más empleado en sistemas Linux.
- **Python:** Python es uno de los lenguajes de programación más utilizados para automatizar tareas de administración.
- **Ansible:** Ansible es una plataforma de automatización y gestión de configuración ampliamente utilizada en entornos empresariales.
- **Puppet:** Puppet es una herramienta de gestión de configuración orientada a grandes infraestructuras.
- **Chef:** Chef automatiza la configuración y administración de infraestructuras mediante código.
- **Terraform:** Terraform permite automatizar el despliegue de infraestructuras mediante el enfoque Infrastructure as Code (IaC).

### Comparativa

| Herramienta | Uso principal | Sistemas habituales |
|-------------|---------------|---------------------|
| PowerShell | Automatización de Windows | Windows |
| Bash | Automatización de Linux | Linux |
| Python | Automatización general | Multiplataforma |
| Ansible | Gestión de configuración | Multiplataforma |
| Puppet | Gestión de configuración | Multiplataforma |
| Chef | Automatización de infraestructuras | Multiplataforma |
| Terraform | Infraestructura como código | Multiplataforma |

---

**Conceptos clave:**

- **Criterios de elección:** Antes de seleccionar una herramienta conviene valorar: Sistema operativo.

---

## Seguridad en la automatización

*La automatización permite ejecutar tareas de forma rápida y eficiente, pero también puede convertirse en un riesgo si los procesos no se diseñan adecuadamente.*

**Conceptos clave:**

- **Importancia de la seguridad:** Los procesos automatizados suelen ejecutarse con permisos elevados y pueden afectar a numerosos equipos simultáneamente.
- **Principio de mínimo privilegio:** Los scripts y herramientas deben ejecutarse únicamente con los permisos estrictamente necesarios.
- **Protección de credenciales:** Uno de los errores más habituales consiste en almacenar usuarios y contraseñas directamente en los scripts.
- **Validación de datos:** Antes de ejecutar cualquier acción automática conviene comprobar que los datos recibidos son correctos.
- **Control de errores:** Todo proceso automatizado debería contemplar posibles fallos.
- **Registro de actividades:** Las tareas automatizadas deberían generar registros que permitan conocer qué acciones se han realizado.
- **Pruebas antes de producción:** Antes de ejecutar un script sobre sistemas reales se recomienda probarlo en un entorno controlado.
- **Control de versiones:** Los scripts deben mantenerse bajo un sistema de control de versiones.
- **Supervisión de procesos automáticos:** No basta con automatizar una tarea; también es necesario comprobar que continúa funcionando correctamente.

---

## Resolución de problemas habituales

*Los procesos automatizados pueden fallar por múltiples motivos, como errores en los scripts, configuraciones incorrectas, problemas de permisos o fallos en los servicios del sistema.*

**Conceptos clave:**

- **Comprobar el script:** El primer paso consiste en verificar que el script no contiene errores de sintaxis o lógica.
- **Ejecutar manualmente:** Antes de revisar otros elementos, conviene ejecutar el script manualmente.
- **Revisar los permisos:** Un problema frecuente consiste en que el script no dispone de permisos suficientes.
- **Comprobar las rutas:** Muchos errores aparecen porque el script intenta acceder a archivos o directorios inexistentes.
- **Revisar las tareas programadas:** Cuando el script se ejecuta automáticamente, es importante comprobar que la programación es correcta.

### Analizar los registros

*Los registros permiten conocer qué ocurrió durante la ejecución.*

```bash
journalctl
```
```bash
cat /var/log/syslog
```

---

**Conceptos clave:**

- **Comprobar dependencias:** Algunos scripts dependen de programas o servicios adicionales.
- **Verificar la conectividad:** Cuando la automatización trabaja con equipos remotos, también debe comprobarse la comunicación de red.
- **Procedimiento de diagnóstico:** Un procedimiento ordenado puede representarse así.

---

[⬆️ Volver al índice](#índice)
