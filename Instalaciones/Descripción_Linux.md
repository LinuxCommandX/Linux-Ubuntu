# Linux — Un sistema operativo libre, seguro y versátil

![Linux](https://img.shields.io/badge/OS-Linux-blue?logo=linux)
![Licencia](https://img.shields.io/badge/Licencia-GPL--compatible-brightgreen)

Bienvenido: este repositorio contiene notas y recursos sobre Linux. Este README ofrece una guía rápida, comandos útiles y recursos para comenzar.

**Contenido**

- [¿Qué es Linux?](#que-es-linux)
- [Por qué usar Linux](#por-qué-usar-linux)
- [Componentes clave](#componentes-clave)
- [Distribuciones populares](#distribuciones-populares)
- [Comandos básicos](#comandos-básicos)
- [Primeros pasos / Prueba rápida](#primeros-pasos--prueba-rápida)
- [Diagrama conceptual](#diagrama-conceptual)
- [Recursos y guía de instalación](#recursos-y-guía-de-instalación)

## ¿Qué es Linux?

Linux es un conjunto de software libre centrado en el kernel Linux —el núcleo que gestiona el hardware— y combinado con utilidades y programas que forman un sistema operativo completo. Es la base de miles de distribuciones usadas en servidores, escritorios, dispositivos embebidos y supercomputadoras.

## Por qué usar Linux

- **Libre y auditable**: código abierto y verificable por cualquiera.
- **Estabilidad y rendimiento**: ideal para servidores y sistemas críticos.
- **Seguridad**: diseño modular y una gran comunidad que publica parches.
- **Flexibilidad**: desde sistemas minimalistas hasta escritorios completos.

## Componentes clave

- **Kernel**: controla procesos, memoria y dispositivos.
- **Userland**: herramientas GNU, gestores de paquetes y aplicaciones.
- **Distribuciones (distros)**: combinaciones empaquetadas del kernel + userland + instaladores + repositorios.

## Distribuciones populares

- **Ubuntu / Debian** — amigables, gran ecosistema.
- **Fedora** — vanguardista y con tecnologías recientes.
- **Arch Linux** — minimalismo y control absoluto.
- **CentOS / Rocky / AlmaLinux** — orientadas a servidores.

## Comandos básicos

Abre una terminal y prueba:

```bash
# Mostrar información del kernel
uname -sr

# Información detallada de la distro (si está disponible)
lsb_release -a

# Actualizar paquetes (ejemplo en Debian/Ubuntu)
sudo apt update && sudo apt upgrade

# Listar archivos en formato largo
ls -la

# Buscar procesos
ps aux | grep nombre_proceso
```

## Primeros pasos / Prueba rápida

1. Abre una terminal.
2. Ejecuta `uname -a` para ver el kernel.
3. Prueba un comando simple como `ls` y `pwd`.

<details>
<summary>¿Qué aprendo aquí? (clic para desplegar)</summary>

- Conceptos básicos del kernel y distribuciones.
- Comandos para moverte y gestionar paquetes.
- Dónde encontrar guías de instalación y documentación.

</details>

## Diagrama conceptual

```mermaid
graph LR
  K[Kernel] --> U[Userland (GNU, utilidades)]
  U --> D1[Ubuntu / Debian]
  U --> D2[Fedora / RHEL]
  U --> D3[Arch Linux]
  User[Usuario] --> D1
  User --> D2
  User --> D3
```

## Recursos y guía de instalación

- Guía de instalación incluida en este repositorio: [01-Intalación/Linux.md](01-Intalación/Linux.md)
- Documentación oficial del kernel: https://www.kernel.org/
- Comunidad y foros: Stack Overflow, foros de cada distribución.

---

¿Quieres que convierta este README en una página más visual (por ejemplo, agregando capturas, GIFs o una sección de comparación entre distros)? Dime qué prefieres y lo preparo.
# Linux-Ubuntu