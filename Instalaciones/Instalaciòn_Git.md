# Guía: Instalación y Configuración Inicial de Git en Linux Ubuntu

Esta guía te llevará paso a paso para instalar Git desde los repositorios oficiales de Ubuntu y dejarlo correctamente configurado para tus proyectos de desarrollo.

### Enlaces de Acceso Rápido
* [Página Oficial de Git](https://git-scm.com/)
* [Documentación oficial de Git (En Español)](https://git-scm.com/doc)

---

## Paso 1: Instalación de Git

El método más rápido y recomendado en Ubuntu es utilizar el gestor de paquetes avanzado (`apt`).

1. Abre la terminal de Ubuntu usando el atajo `Ctrl` + `Alt` + `T`.
2. Actualiza la lista de paquetes locales para asegurarte de descargar la versión más reciente:

```bash
sudo apt update
```

3. Instala Git ejecutando el siguiente comando:

```bash
sudo apt install git -y
```

4. Escribe tu contraseña de administrador cuando el sistema lo solicite y presiona Enter.

## Paso 2: Verificación de la instalación
Para confirmar que Git se instaló correctamente y comprobar qué versión tienes, ejecuta:
```bash
git --version
```

Resultado esperado: Deberías ver en la terminal algo como git version 2.x.x.

## Paso 3: Configuración Inicial Obligatoria
Antes de realizar tu primer commit, Git necesita saber quién eres para asociar los cambios a tu identidad. Debes configurar tu nombre y tu correo electrónico (se recomienda usar el mismo correo de tu cuenta de GitHub/GitLab).
1. Configurar tu nombre global:
```bash
git config --global user.name "Tu Nombre Completo"
```

2. Configurar tu correo electrónico global:
```bash
git config --global user.email "tu-correo@ejemplo.com"
```

3. Configurar la rama por defecto (Opcional pero muy recomendado):
Para que tus nuevos repositorios locales utilicen main como rama principal en lugar de la antigua master:
```bash
git config --global init.defaultBranch main
```

## Paso 4: Validar la configuración
Para asegurarte de que los datos se guardaron correctamente, puedes listar la configuración global con el siguiente comando:/GitLab).

```bash
git config --list
```

Tip Extra: Si alguna vez quieres verificar únicamente el nombre o el correo guardado, puedes ejecutar git config user.name o git config user.email. ¡Tu Git ya está completamente operativo y configurado!
