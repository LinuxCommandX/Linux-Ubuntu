# Guía: Instalación de Visual Studio Code en Linux Ubuntu

Esta guía explica detalladamente cómo instalar el editor de código Visual Studio Code en tu sistema operativo Ubuntu.

### Enlaces de Acceso Rápido
* [Página oficial de VS Code](https://code.visualstudio.com/)
* [Documentación de VS Code para Linux](https://code.visualstudio.com/docs/setup/linux)

---

## Método 1: Instalación rápida a través de la Terminal (Recomendado - Paquete Snap)

Ubuntu viene con soporte nativo para paquetes Snap, lo que hace que la instalación y las actualizaciones automáticas de VS Code sean sumamente sencillas.

### Paso a Paso
1. Abre la terminal de Ubuntu (puedes usar el atajo de teclado `Ctrl` + `Alt` + `T`).
2. Ejecuta el siguiente comando para descargar e instalar VS Code de forma segura:

```bash
sudo snap install --classic code
```

## Método 2: Instalación clásica mediante Repositorio oficial (Paquete APT)
Si prefieres el gestor de paquetes tradicional de Debian/Ubuntu (apt), puedes añadir el repositorio oficial de Microsoft de la siguiente manera:

### Paso a Paso
1. Abre tu terminal (Ctrl + Alt + T).
2. Actualiza el índice de paquetes e instala las dependencias necesarias ejecutando:
```bash
sudo apt update
sudo apt install wget gpg apt-transport-https -y
```

3. Importa la clave GPG de Microsoft para asegurar la autenticidad del software:
```bash
wget -qO- [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc) | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
```

4. Añade el repositorio oficial de VS Code a tu sistema:
```bash
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] [https://packages.microsoft.com/repos/code](https://packages.microsoft.com/repos/code) stable main" > /etc/apt/sources.list.doc.d/vscode.list'
```

5. Limpia el archivo temporal de la clave:
```bash
rm -f packages.microsoft.gpg
```

6. Finalmente, actualiza la lista de paquetes e instala el programa:
```bash
sudo apt update
sudo apt install code -y
```

7. Verificación de la instalación
```bash
code --version
```