# 🚀 Instalación de Google Chrome en Ubuntu

## 1. Actualizar el sistema
```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Instalar wget (si no lo tienes)
```bash
sudo apt install wget -y
```

## 3. Descargar el paquete oficial de Chrome
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

## 4. Instalar el paquete descargado
```bash
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

## 5. Resolver dependencias faltantes
```bash
sudo apt -f install -y
```

## 6. Abrir Google Chrome
Desde la terminal:
```bash
google-chrome
```

