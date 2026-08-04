# Gestión de servicios

## Introducción

Los servicios son programas especializados que se ejecutan en segundo plano para proporcionar funciones esenciales al sistema operativo y a las aplicaciones.

## Índice

- [Concepto de servicio](#concepto-de-servicio)
- [Diferencia entre proceso y servicio](#diferencia-entre-proceso-y-servicio)
- [Tipos de servicios](#tipos-de-servicios)
- [Estados de un servicio](#estados-de-un-servicio)
- [Dependencias entre servicios](#dependencias-entre-servicios)
- [Gestión de servicios en Windows](#gestión-de-servicios-en-windows)
- [Gestión de servicios en Linux](#gestión-de-servicios-en-linux)
- [Inicio automático y tipos de inicio](#inicio-automático-y-tipos-de-inicio)
- [Administración mediante PowerShell](#administración-mediante-powershell)
- [Administración mediante CMD](#administración-mediante-cmd)
- [Administración mediante systemctl](#administración-mediante-systemctl)
- [Monitorización y resolución de problemas](#monitorización-y-resolución-de-problemas)

---

## Concepto de servicio

*Los servicios son uno de los componentes fundamentales de cualquier sistema operativo moderno.*

**Conceptos clave:**

- **¿Qué es un servicio?:** Un servicio es un programa o proceso especializado que se ejecuta en segundo plano para proporcionar una función específica al sistema operativo o a otras aplicaciones.
- **Características de los servicios:** Los servicios presentan una serie de características comunes: Se ejecutan en segundo plano.
- **¿Para qué sirven los servicios?:** Los servicios permiten automatizar tareas esenciales que deben estar disponibles continuamente.
- **Funcionamiento de un servicio:** Cuando el sistema operativo inicia, comprueba qué servicios deben ejecutarse automáticamente.
- **Ejemplos de servicios:** Algunos de los servicios más habituales son: Windows Update.
- **Importancia de los servicios:** Los servicios son imprescindibles para garantizar el funcionamiento correcto del sistema.

## Diferencia entre proceso y servicio

*Aunque los términos proceso y servicio suelen utilizarse conjuntamente, no hacen referencia al mismo concepto.*

**Conceptos clave:**

- **¿Qué es un proceso?:** Un proceso es una instancia de un programa que se encuentra en ejecución.
- **¿Qué es un servicio?:** Un servicio es un proceso especializado que trabaja en segundo plano proporcionando funciones al sistema operativo o a otras aplicaciones.

### Principales diferencias

| Proceso | Servicio |
|---------|----------|
| Ejecuta un programa. | Proporciona una función al sistema o a otras aplicaciones. |
| Puede tener interfaz gráfica. | Normalmente no dispone de interfaz gráfica. |
| Suele iniciarse por acción del usuario. | Puede iniciarse automáticamente durante el arranque. |
| Puede finalizar al cerrar la aplicación. | Habitualmente permanece activo mientras el sistema está funcionando. |
| Puede existir de forma independiente. | Frecuentemente trabaja de manera continua en segundo plano. |

---

**Conceptos clave:**

- **Relación entre procesos y servicios:** Todos los servicios son procesos, pero no todos los procesos son servicios.
- **Ejemplos de procesos:** Algunos procesos habituales son: Microsoft Word.
- **Ejemplos de servicios:** Algunos servicios habituales son: Windows Update.
- **¿Cuándo se inicia cada uno?:** Los procesos suelen iniciarse cuando: El usuario abre una aplicación.
- **Administración:** Los procesos suelen administrarse mediante herramientas como: Administrador de tareas.

## Tipos de servicios

*Los servicios pueden clasificarse de diferentes formas según su función, su modo de ejecución o el momento en que se inician.*

**Conceptos clave:**

- **Servicios del sistema:** Son aquellos que forman parte del propio sistema operativo y permiten su funcionamiento.
- **Servicios de red:** Permiten la comunicación entre equipos y el acceso a recursos compartidos.
- **Servicios de aplicaciones:** Son instalados junto con determinadas aplicaciones para proporcionar funciones adicionales.
- **Servicios de seguridad:** Se encargan de proteger el sistema frente a amenazas y accesos no autorizados.
- **Servicios de mantenimiento:** Realizan tareas periódicas destinadas a mantener el sistema operativo en buen estado.
- **Servicios locales y remotos:** Según el ámbito en el que actúan, pueden distinguirse dos tipos.
- **Servicios esenciales y opcionales:** Otra forma habitual de clasificarlos es según su importancia para el funcionamiento del sistema.
- **Servicios según su tipo de inicio:** Los servicios también pueden clasificarse según el momento en que se ejecutan.
- **Ejemplos de servicios habituales:** - Windows Update.
- **Importancia de identificar el tipo de servicio:** Conocer el tipo de servicio permite: Comprender su función.

## Estados de un servicio

*Un servicio no permanece siempre en la misma situación durante su ejecución.*

**Conceptos clave:**

- **¿Qué es el estado de un servicio?:** El estado de un servicio indica su situación actual dentro del sistema operativo.
- **Servicio en ejecución (Running):** Es el estado más habitual.
- **Servicio detenido (Stopped):** El servicio no está ejecutándose y, por tanto, no realiza ninguna función.
- **Servicio iniciándose (Start Pending):** Este estado indica que el sistema está cargando el servicio.
- **Servicio deteniéndose (Stop Pending):** Indica que el sistema está finalizando la ejecución del servicio.
- **Servicio pausado (Paused):** Algunos servicios permiten suspender temporalmente su funcionamiento sin detenerlos completamente.
- **Servicio reanudándose (Continue Pending):** Cuando un servicio pausado vuelve a funcionar, pasa brevemente por este estado antes de regresar a En ejecución.
- **Cambios de estado:** Un servicio puede cambiar de estado varias veces durante su ciclo de vida.

### Consultar el estado en Windows

*Desde services.msc es posible comprobar el estado de todos los servicios.*

```powershell
Get-Service
```
```powershell
Get-Service spooler
```

---

### Consultar el estado en Linux

*En sistemas Linux con systemd, el estado puede consultarse mediante.*

```bash
systemctl status apache2
```
```bash
systemctl list-units --type=service
```

---

**Conceptos clave:**

- **Importancia de conocer el estado:** Comprobar el estado de un servicio permite: Detectar servicios detenidos.

## Dependencias entre servicios

*Los servicios de un sistema operativo no siempre funcionan de manera independiente.*

**Conceptos clave:**

- **¿Qué es una dependencia?:** Una dependencia es la relación existente entre dos o más servicios, donde uno de ellos necesita que otro esté disponible para poder funcionar correctamente.
- **¿Por qué existen las dependencias?:** Las dependencias permiten organizar el funcionamiento del sistema operativo y evitar que un servicio intente ejecutarse cuando aún no dispone de los recursos necesarios.
- **Tipos de dependencias:** Existen dos situaciones principales.
- **Ejemplos de dependencias en Windows:** Algunos ejemplos habituales son: Print Spooler depende de Remote Procedure Call (RPC).

### Consultar dependencias en Windows

*Las dependencias pueden consultarse desde.*

```powershell
Get-Service spooler | Select-Object Name, ServicesDependedOn
```
```powershell
Get-Service spooler | Select-Object Name, DependentServices
```

---

**Conceptos clave:**

- **Ejemplos de dependencias en Linux:** En sistemas Linux administrados mediante systemd, los servicios también pueden depender unos de otros.

### Consultar dependencias en Linux

*Consultar información de un servicio.*

```bash
systemctl status apache2
```
```bash
systemctl list-dependencies apache2
```

---

**Conceptos clave:**

- **Problemas relacionados con las dependencias:** Las dependencias mal configuradas pueden provocar: Servicios que no arrancan.

---

## Gestión de servicios en Windows

*Windows incorpora diversas herramientas que permiten administrar los servicios del sistema de forma gráfica y mediante línea de comandos.*

**Conceptos clave:**

- **Consola de servicios (services.msc):** La herramienta principal para administrar servicios en Windows es la consola Servicios.
- **Información mostrada:** La consola muestra información relevante de cada servicio.
- **Iniciar un servicio:** Para iniciar un servicio desde la consola.
- **Detener un servicio:** Para detener un servicio.
- **Reiniciar un servicio:** Cuando un servicio presenta problemas, una de las primeras acciones suele ser reiniciarlo.
- **Configurar el tipo de inicio:** Desde las propiedades del servicio puede modificarse su comportamiento durante el arranque del sistema.
- **Consultar dependencias:** Las propiedades del servicio incluyen una pestaña denominada Dependencias.
- **Configuración del usuario de inicio:** Cada servicio se ejecuta utilizando una cuenta determinada.

### Administración mediante PowerShell

*PowerShell permite gestionar servicios de forma rápida y automatizada.*

```powershell
Get-Service
```
```powershell
Get-Service spooler
```

---

**Conceptos clave:**

- **Administración mediante CMD:** El símbolo del sistema también permite administrar servicios.
- **Solución de problemas:** Si un servicio no funciona correctamente, conviene seguir un procedimiento ordenado.

---

## Gestión de servicios en Linux

*En los sistemas Linux, los servicios desempeñan un papel fundamental en el funcionamiento del sistema operativo y de las aplicaciones.*

**Conceptos clave:**

- **¿Qué es systemd?:** systemd es el sistema de inicialización utilizado por la mayoría de las distribuciones Linux actuales.
- **Servicios en Linux:** En Linux, un servicio suele ejecutarse como un daemon.
- **Archivos de configuración:** Cada servicio dispone de un archivo de configuración que define cómo debe iniciarse y comportarse.

### Consultar servicios

*Para visualizar los servicios cargados en el sistema puede utilizarse.*

```bash
systemctl list-units --type=service
```
```bash
systemctl list-unit-files --type=service
```

---

### Iniciar un servicio

*Para iniciar un servicio manualmente.*

```bash
sudo systemctl start nombre_servicio
```
```bash
sudo systemctl start apache2
```

---

### Detener un servicio

*Para detener un servicio.*

```bash
sudo systemctl stop nombre_servicio
```
```bash
sudo systemctl stop apache2
```

---

### Reiniciar un servicio

*Cuando un servicio presenta problemas, una de las primeras acciones consiste en reiniciarlo.*

```bash
sudo systemctl restart nombre_servicio
```
```bash
sudo systemctl restart apache2
```

---

### Consultar el estado

*Para comprobar el estado de un servicio.*

```bash
systemctl status nombre_servicio
```
```bash
systemctl status ssh
```

---

### Habilitar y deshabilitar servicios

*Para configurar que un servicio se inicie automáticamente durante el arranque.*

```bash
sudo systemctl enable nombre_servicio
```
```bash
sudo systemctl enable apache2
```

---

### Consultar dependencias

*Las dependencias de un servicio pueden visualizarse mediante.*

```bash
systemctl list-dependencies nombre_servicio
```

---

### Registros del servicio

*Los eventos registrados por los servicios pueden consultarse mediante.*

```bash
journalctl -u nombre_servicio
```
```bash
journalctl -u apache2
```

---

## Inicio automático y tipos de inicio

*No todos los servicios se inician de la misma forma cuando arranca un sistema operativo.*

**Conceptos clave:**

- **¿Qué es el tipo de inicio?:** El tipo de inicio determina cómo y cuándo se pondrá en marcha un servicio.
- **Inicio automático:** Los servicios configurados con inicio automático se ejecutan durante el arranque del sistema operativo.
- **Inicio automático (inicio retrasado):** En Windows existe una modalidad denominada Inicio automático (inicio retrasado).
- **Inicio manual:** Un servicio configurado con inicio manual no se ejecuta durante el arranque del sistema.
- **Servicio deshabilitado:** Un servicio deshabilitado no puede iniciarse automáticamente ni manualmente mientras permanezca en ese estado.

### Comparativa de los tipos de inicio

| Tipo de inicio | Se inicia al arrancar | Puede iniciarse manualmente | Uso habitual |
|----------------|----------------------|-----------------------------|--------------|
| Automático | Sí | Sí | Servicios esenciales |
| Automático (inicio retrasado) | Sí, con retraso | Sí | Servicios no críticos durante el arranque |
| Manual | No | Sí | Servicios ocasionales |
| Deshabilitado | No | No | Servicios que no deben ejecutarse |

---

**Conceptos clave:**

- **Configuración en Windows:** El tipo de inicio puede modificarse desde.

### Configuración en Linux

*En sistemas Linux administrados mediante systemd, el comportamiento durante el arranque se controla habilitando o deshabilitando el servicio.*

```bash
sudo systemctl enable nombre_servicio
```
```bash
sudo systemctl disable nombre_servicio
```

---

**Conceptos clave:**

- **¿Qué tipo de inicio elegir?:** La elección dependerá de la función del servicio.

---

## Administración mediante PowerShell

*PowerShell es la herramienta de automatización y administración de Windows basada en línea de comandos y scripting.*

### Consultar todos los servicios

*Para mostrar todos los servicios del sistema.*

```powershell
Get-Service
```

---

### Consultar un servicio concreto

*Para obtener información de un servicio específico.*

```powershell
Get-Service -Name spooler
```
```powershell
Get-Service spooler
```

---

### Filtrar servicios por estado

*Es posible mostrar únicamente los servicios que están en ejecución.*

```powershell
Get-Service | Where-Object Status -eq "Running"
```
```powershell
Get-Service | Where-Object Status -eq "Stopped"
```

---

### Iniciar un servicio

*Para iniciar un servicio.*

```powershell
Start-Service -Name spooler
```

---

### Detener un servicio

*Para detener un servicio.*

```powershell
Stop-Service -Name spooler
```

---

### Reiniciar un servicio

*Una de las operaciones más habituales consiste en reiniciar un servicio.*

```powershell
Restart-Service -Name spooler
```

---

### Cambiar el tipo de inicio

*PowerShell permite modificar el modo en que un servicio se inicia.*

```powershell
Set-Service -Name spooler -StartupType Automatic
```
```powershell
Set-Service -Name spooler -StartupType Manual
```

---

### Consultar dependencias

*Para conocer los servicios de los que depende un servicio.*

```powershell
Get-Service spooler | Select-Object ServicesDependedOn
```
```powershell
Get-Service spooler | Select-Object DependentServices
```

---

### Obtener información detallada

*Para mostrar todas las propiedades disponibles de un servicio.*

```powershell
Get-Service spooler | Format-List *
```

---

### Automatización mediante scripts

*PowerShell permite integrar la administración de servicios dentro de scripts.*

```powershell
$Servicio = Get-Service spooler

if ($Servicio.Status -eq "Stopped") {
    Start-Service spooler
}
```

---

## Administración mediante CMD

**Conceptos clave:**

- **El comando `sc`:** El comando Service Control (sc) es la herramienta principal de CMD para administrar servicios.
- **Consultar un servicio:** Para mostrar información sobre un servicio concreto.
- **Consultar todos los servicios:** Para listar todos los servicios del sistema.
- **Iniciar un servicio:** Para iniciar un servicio.
- **Detener un servicio:** Para detener un servicio.
- **Configurar el tipo de inicio:** El comando `sc` también permite modificar la forma en que se inicia un servicio.
- **Consultar la configuración:** Para visualizar la configuración completa de un servicio.
- **El comando `net`:** El comando net es una herramienta clásica de Windows que permite administrar distintos recursos del sistema, incluidos los servicios.

### Diferencias entre `sc` y `net`

| `sc` | `net` |
|------|-------|
| Más completo y flexible. | Más sencillo de utilizar. |
| Permite configurar servicios. | Solo permite iniciar y detener servicios. |
| Muestra información detallada. | Proporciona información básica. |
| Muy utilizado en administración avanzada. | Muy utilizado para tareas rápidas. |

---

## Administración mediante systemctl

### ¿Qué es systemctl?

*`systemctl` es la utilidad de línea de comandos utilizada para interactuar con systemd.*

```bash
systemctl [comando] [servicio]
```

---

### Consultar el estado de un servicio

*Para comprobar el estado de un servicio.*

```bash
systemctl status apache2
```

---

### Listar servicios

*Mostrar los servicios activos.*

```bash
systemctl list-units --type=service
```
```bash
systemctl list-unit-files --type=service
```

---

### Iniciar un servicio

*Para iniciar un servicio.*

```bash
sudo systemctl start apache2
```

---

### Detener un servicio

*Para detener un servicio.*

```bash
sudo systemctl stop apache2
```

---

### Reiniciar un servicio

*Cuando un servicio presenta problemas, puede reiniciarse mediante.*

```bash
sudo systemctl restart apache2
```

---

### Recargar la configuración

*Algunos servicios permiten recargar su configuración sin necesidad de reiniciarlos.*

```bash
sudo systemctl reload apache2
```

---

### Habilitar un servicio

*Para configurar un servicio de forma que se inicie automáticamente al arrancar el sistema.*

```bash
sudo systemctl enable apache2
```

---

### Deshabilitar un servicio

*Para impedir que un servicio se inicie automáticamente.*

```bash
sudo systemctl disable apache2
```

---

### Comprobar si un servicio está habilitado

*Puede verificarse mediante.*

```bash
systemctl is-enabled apache2
```

---

### Consultar dependencias

*Para mostrar las dependencias de un servicio.*

```bash
systemctl list-dependencies apache2
```

---

### Consultar los registros

*Los eventos generados por un servicio pueden visualizarse mediante.*

```bash
journalctl -u apache2
```
```bash
journalctl -u apache2 -n 20
```

---

## Monitorización y resolución de problemas

*La monitorización de los servicios permite comprobar su estado, detectar incidencias y garantizar que continúan funcionando correctamente.*

**Conceptos clave:**

- **¿Por qué monitorizar los servicios?:** La supervisión continua de los servicios permite: Detectar fallos de funcionamiento.
- **Indicadores de un servicio con problemas:** Algunos síntomas habituales son: El servicio no inicia.
- **Comprobaciones iniciales:** Ante un problema relacionado con un servicio, conviene seguir un procedimiento ordenado.

### Monitorización en Windows

*Las herramientas más utilizadas son: Servicios (`services.*

```powershell
Get-Service spooler
```
```powershell
Restart-Service spooler
```

---

### Monitorización en Linux

*Linux dispone de diferentes herramientas para supervisar servicios.*

```bash
systemctl status apache2
```
```bash
journalctl -u apache2
```

---

### Revisión de registros

*Los registros suelen contener información muy útil para identificar la causa de una incidencia.*

```bash
journalctl -u nombre_servicio
```

---

**Conceptos clave:**

- **Problemas habituales:** Entre las incidencias más frecuentes destacan: Servicio detenido accidentalmente.
- **Resolución de problemas:** Una vez localizada la causa, las acciones más habituales son: Reiniciar el servicio.
- **Herramientas de monitorización:** En entornos profesionales es habitual utilizar herramientas específicas para supervisar servicios y servidores.

---

[⬆️ Volver al índice](#índice)
