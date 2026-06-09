# Navegación: Rutas Relativas y Absolutas en Linux

## Conceptos fundamentales

### Ruta Absoluta
Es la ruta **completa** que comienza desde la raíz `/` y especifica la ubicación exacta de un fichero o directorio, sin importar dónde te encuentres.

**Características:**
- Siempre empieza con `/`
- No depende de tu posición actual
- Es única y no ambigua

**Ejemplos de rutas absolutas:**
```bash
/home/usuario/Documentos/informe.txt
/etc/nginx/nginx.conf
/var/log/syslog
/usr/bin/python3
```

### Ruta Relativa
Es la ruta referenciada desde el directorio actual donde te encuentras.
Características:
- No empieza con `/`
- Depende de tu posición actual
- Usa símbolos especiales para navegar

Símbolos especiales para rutas relativas:
| Símbolo | Significado |
|------------|-----------|
| `.` | Directorio actual |
| `..` | Directorio padre (un nivel arriba) |
| `~` | Directorio home del usuario |
| `~usuario` | Home de un usuario específico |
| `-` | Directorio anterior (donde estabas antes) |

Ejemplos de rutas relativas:
```bash
Documentos/informe.txt     # dentro del directorio actual
../imagenes/foto.jpg       # un nivel arriba y luego a imagenes
~/Descargas/archivo.pdf    # dentro de la carpeta Descargas del home
```

### Comandos básicos de navegación
| Comando | Descripción | Ejemplo |
|------------|-----------|-----------|
| `pwd` | Muestra la ruta absoluta del directorio actual | `pwd → /home/usuario` |
| `ls` | Lista el contenido de un directorio | `ls -la` |
| `cd` | Cambia de directorio | `cd /etc` |
| `cd ~` | Va al home del usuario actual | `cd ~` |
| `cd ..` | Sube un nivel (directorio padre) | `cd ../..` |
| `cd -` | Va al directorio anterior | `cd -` |

## Ejemplos prácticos de navegación
### Escenario 1: Desde el home, ir a Documentos y luego subir
```bash
usuario@ubuntu:~$ pwd
/home/usuario

usuario@ubuntu:~$ cd Documentos
usuario@ubuntu:~/Documentos$ pwd
/home/usuario/Documentos

usuario@ubuntu:~/Documentos$ cd ..
usuario@ubuntu:~$ pwd
/home/usuario
```

### Escenario 2: Usar ruta absoluta desde cualquier lugar
```bash
D# Estés donde estés, este comando te lleva directamente a /etc/nginx
usuario@ubuntu:~$ cd /etc/nginx
usuario@ubuntu:/etc/nginx$ pwd
/etc/nginx
```

### Escenario 3: Navegación relativa avanzada
```bash
# Estructura de directorios:
# /home/usuario/
#   ├── Documentos/
#   │   └── proyectos/
#   │       └── web/
#   └── Descargas/

usuario@ubuntu:~$ cd Documentos/proyectos/web
usuario@ubuntu:~/Documentos/proyectos/web$

# Subir dos niveles (a Documentos)
usuario@ubuntu:~/Documentos/proyectos/web$ cd ../..
usuario@ubuntu:~/Documentos$

# Ir a Descargas usando ruta relativa desde Documentos
usuario@ubuntu:~/Documentos$ cd ../Descargas
usuario@ubuntu:~/Descargas$
```

### Escenario 4: Uso de ~ y -
```bash
# Desde cualquier lugar, ir al home
usuario@ubuntu:/var/log$ cd ~
usuario@ubuntu:~$

# Ir al directorio anterior (volver a /var/log)
usuario@ubuntu:~$ cd -
/var/log
usuario@ubuntu:/var/log$
```

### Comparativa: Absoluta vs Relativa
| Situación | Mejor opción | Por qué |
|------------|-----------|-----------|
| En scripts o configuraciones | **Absoluta** | No depende de dónde se ejecute el script |
| En la terminal, navegando cerca | **Relativa** | Menos escritura, más rápida |
| Para referenciar archivos del sistema | **Absoluta** | Claridad y precisión |
| `Para moverte dentro de tu proyecto | **Relativa** | Flexible y portable |

### Consejos y buenas prácticas
1. Usa pwd frecuentemente si no estás seguro de dónde estás
2. cd sin argumentos te lleva directamente a tu home
3. cd .. se puede encadenar: cd ../../../ sube 3 niveles
4. Autocompletado con Tab funciona para rutas absolutas y relativas
5. Las rutas relativas son útiles en comandos como cp, mv, rm

### Ejercicios para practicar
```bash
# 1. Desde tu home, crea esta estructura:
#    ~/practica/nivel1/nivel2/

mkdir -p practica/nivel1/nivel2

# 2. Navega a nivel2 usando ruta relativa
cd practica/nivel1/nivel2

# 3. Vuelve a practica usando ruta relativa
cd ../..

# 4. Ve a /tmp desde donde estés (ruta absoluta)
cd /tmp

# 5. Regresa al directorio anterior (donde estabas)
cd -
```