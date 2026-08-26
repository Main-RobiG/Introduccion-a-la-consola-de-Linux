# MANUAL TÉCNICO Y PRÁCTICO: UBUNTU LINUX & DESPLIEGUE WEB APACHE2

**Universidad de San Carlos de Guatemala**  
**Facultad de Ingeniería**  
**Escuela de Ciencias y Sistemas**  
**Curso:** Prácticas Iniciales  
**Semestre:** Segundo Semestre 2026  
**Estudiante:** Sergio Gudiel  
**Carné:** 201404365  
**Fecha:** 27 de Agosto de 2026  

---

## 1. RESUMEN DE ENTORNO Y MODALIDAD DE INSTALACIÓN

### 1.1. Contexto de Infraestructura
El presente manual técnico abarca la gestión del sistema operativo **Ubuntu Linux 26.04 LTS**, enfocado en la administración por línea de comandos (CLI) y la puesta en marcha de servicios web en la nube o servidores locales.

### 1.2. Especificaciones del Entorno
* **Modalidad elegida:** Virtualización mediante Hipervisor de Tipo 2.
* **Hipervisor utilizado:** Oracle VM VirtualBox (v7.0).
* **Sistema Operativo Guest:** Ubuntu Linux 26.04 LTS.
* **Configuración del sistema:** 2 vCPUs, 4096 MB de RAM, 30 GB de disco dinámico VDI y controlador de red NAT.
* **Herramientas de integración:** Guest Additions activadas para soporte de portapapeles compartido y ajuste dinámico de pantalla.

### 1.3. Diferencias Clave: Windows vs. Linux Ubuntu
| Característica | Windows | Linux Ubuntu |
| :--- | :--- | :--- |
| **Estructura de Directorios** | Unidades lógicas independientes (`C:\`, `D:\`). | Árbol jerárquico único a partir del directorio raíz (`/`). |
| **Sensibilidad a Mayúsculas** | Insensible a mayúsculas/minúsculas (*Case-insensitive*). | Estrictamente sensible a mayúsculas/minúsculas (*Case-sensitive*). |
| **Separador de Rutas** | Barra invertida (`\`). | Barra diagonal (`/`). |
| **Arquitectura Base** | Basado en Kernel Windows NT. | Basado en el estándar POSIX / Arquitectura UNIX. |

---

## 2. INVESTIGACIÓN Y DOCUMENTACIÓN DE COMANDOS CLI

### 2.1. Gestión de Navegación

#### `pwd` (Print Working Directory)
Imprime en pantalla la ruta absoluta del directorio de trabajo actual.

* **Sintaxis:** `pwd [opciones]`
* **Opciones principales:**
  * `pwd`: Muestra la ruta actual resolviendo enlaces simbólicos por defecto.
  * `pwd -P`: Muestra la ruta física real excluyendo enlaces simbólicos (*symlinks*).
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop$ pwd -P
  /home/vboxuser/Desktop
  ```

#### `cd` (Change Directory)
Permite desplazarse a través de la estructura de directorios del sistema de archivos.

* **Sintaxis:** `cd [ruta_destino]`
* **Variantes comunes:**
  * `cd /ruta/destino`: Navega a una ruta absoluta o relativa específica.
  * `cd ..`: Sube un nivel en la jerarquía (directorio padre).
  * `cd ../..`: Sube dos niveles en la jerarquía.
  * `cd /`: Desplaza al directorio raíz del sistema.
  * `cd` o `cd ~`: Regresa directamente al directorio personal del usuario (`/home/usuario`).
  * `cd -`: Regresa al directorio de trabajo anterior.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~$ cd /home/vboxuser/Desktop/Usac/Segundo\ semestre/Practicas\ iniciales/
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre/Practicas iniciales$ cd ../..
  vboxuser@Ubuntu:~/Desktop/Usac$ cd -
  /home/vboxuser/Desktop/Usac/Segundo semestre/Practicas iniciales
  ```

---

### 2.2. Lectura e Inspección de Contenido

#### `ls` (List)
Lista carpetas y archivos dentro del directorio actual o especificado.

* **Sintaxis:** `ls [opciones] [directorio]`
* **Opciones principales:**
  * `ls`: Muestra únicamente los archivos y carpetas visibles.
  * `ls -l`: Muestra el formato detallado (permisos, propietario, grupo, tamaño y fecha).
  * `ls -a`: Lista todos los elementos, incluyendo archivos y carpetas ocultas (aquellos que inician con `.`).
  * `ls -la` / `ls -al`: Combina la visualización detallada con la inclusión de archivos ocultos.
  * `ls -lh`: Muestra tamaños en un formato legible para humanos (KB, MB, GB).
  * `ls -lt`: Ordena los elementos por fecha de última modificación (más reciente primero).
  * `ls -R`: Muestra el contenido de forma recursiva (incluyendo subdirectorios).
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre/Practicas iniciales$ ls -al
  total 168
  drwxrwxr-x 2 vboxuser vboxuser  4096 Aug 14 05:19 .
  drwxrwxr-x 6 vboxuser vboxuser  4096 Aug 14 04:58 ..
  -rw-rw-r-- 1 vboxuser vboxuser    17 Aug 14 04:48 .PoemaAlaAuxi<3
  -rw-rw-r-- 1 vboxuser vboxuser 66039 Aug 14 03:23 Fijo 100
  -rw-rw-r-- 1 vboxuser vboxuser    17 Aug 14 04:46 Reporte_1
  ```

---

### 2.3. Creación de Directorios

#### `mkdir` (Make Directory)
Crea una o más carpetas en el sistema de archivos.

* **Sintaxis:** `mkdir [opciones] nombre_directorio`
* **Opciones principales:**
  * `mkdir carpeta`: Crea una única carpeta en la ruta actual.
  * `mkdir -p ruta/a/carpeta/anidada`: Crea la ruta completa de subcarpetas si no existen previamente.
  * `mkdir dir1 dir2 dir3`: Crea múltiples directorios simultáneamente.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ mkdir -p Lenguajes_Formales/LabLenguajes/Practicas
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre/Lenguajes_Formales$ mkdir Proyecto1 Proyecto2 Cortos
  ```

---

### 2.4. Manipulación de Archivos y Carpetas

#### `cp` (Copy)
Copia archivos o directorios de una ubicación de origen a una de destino.

* **Sintaxis:** `cp [opciones] origen destino`
* **Opciones principales:**
  * `cp archivo.txt destino/`: Copia un archivo simple.
  * `cp -r` / `cp -R`: Copia recursiva (necesario para copiar carpetas completas y su contenido).
  * `cp -i`: Activa el modo interactivo (pide confirmación previo a sobrescribir).
  * `cp -v`: Modo explicativo (*verbose*), muestra el proceso de copiado en tiempo real.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ cp Recurrencias Intermedia\ 2/
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ cp -r Lenguajes_Formales/ IPC\ 2/
  ```

#### `mv` (Move)
Desplaza archivos/directorios de ubicación o les cambia de nombre si el destino es la misma ruta.

* **Sintaxis:** `mv [opciones] origen destino`
* **Opciones principales:**
  * `mv nombre_viejo nombre_nuevo`: Renombra un elemento en la misma ubicación.
  * `mv archivo.txt /nueva/ruta/`: Mueve el archivo a otro directorio.
  * `mv -i`: Pide confirmación si la operación sobrescribirá un archivo destino existente.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ mv Recurrencias newDoc
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ mv ABB IPC\ 2/
  ```

#### `rm` (Remove)
Elimina archivos y directorios de forma permanente.

* **Sintaxis:** `rm [opciones] archivo_o_directorio`
* **Opciones principales:**
  * `rm archivo.txt`: Elimina un archivo regular.
  * `rm -r` / `rm -R`: Eliminación recursiva para borrar directorios con su contenido.
  * `rm -f`: Fuerza la eliminación ignorando advertencias y archivos inexistentes.
  * `rm -rf carpeta/`: Eliminación forzada y recursiva de una estructura completa sin pedir confirmación.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ rm newDoc
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ rm -r Intermedia\ 2/
  ```

#### `rmdir` (Remove Directory)
Elimina exclusivamente directorios que estén vacíos.

* **Sintaxis:** `rmdir [opciones] nombre_directorio`
* **Opciones principales:**
  * `rmdir carpeta`: Elimina el directorio únicamente si no contiene archivos o subdirectorios.
  * `rmdir -p ruta/anidada`: Elimina el directorio y sus padres si también quedan vacíos.
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ rmdir Quimica/
  vboxuser@Ubuntu:~/Desktop/Usac/Segundo semestre$ rmdir IPC\ 2/
  rmdir: failed to remove 'IPC 2/': Directory not empty
  ```

---

### 2.5. Elevación de Privilegios y Administración de Permisos

#### Elevación de Privilegios (`sudo` y `su`)
* **`sudo` (Superuser Do):** Permite a un usuario autorizado ejecutar un comando individual con privilegios root.
  * *Ejemplo:* `sudo apt update`
* **`su` (Switch User):** Permite cambiar a la cuenta de otro usuario o a superusuario root de forma interactiva.
  * *Ejemplo:* `su -` (inicia sesión interactiva como root).

#### Gestión de Permisos (`chmod` y `chown`)
* **`chmod` (Change Mode):** Modifica los permisos de acceso (lectura `r`, escritura `w`, ejecución `x`) para el propietario, grupo y otros usuarios.
  * *Sintaxis en octal:* `chmod 755 archivo.sh` (Propietario: `rwx`, Grupo: `r-x`, Otros: `r-x`).
  * *Sintaxis simbólica:* `chmod +x archivo.sh` (Agrega permiso de ejecución).
* **`chown` (Change Owner):** Cambia el propietario y/o el grupo al que pertenece un archivo o carpeta.
  * *Sintaxis:* `chown usuario:grupo archivo.txt`
  * *Ejemplo:* `sudo chown www-data:www-data /var/www/html/index.html`

---

### 2.6. Edición de Texto en Consola y Gestión de Paquetes (`apt`)

#### Editores de Texto CLI (`nano` / `vim`)
* **`nano`:** Editor CLI de fácil uso orientado a la edición rápida. Las combinaciones principales son `Ctrl + O` para guardar y `Ctrl + X` para salir.
* **`vim`:** Editor avanzado modal. Requiere presionar `i` para entrar a modo inserción, `Esc` para volver a modo comando y `:wq` para guardar y salir.

#### Gestor de Paquetes (`apt`)
* **`sudo apt update`:** Actualiza el índice local de paquetes leyendo las listas de repositorios oficiales.
* **`sudo apt upgrade`:** Actualiza todas las aplicaciones y paquetes del sistema a su versión más reciente disponible.
* **`sudo apt install <paquete>`:** Descarga e instala el software especificado en la máquina.
* **`sudo apt remove <paquete>`:** Elimina el ejecutable del paquete manteniendo archivos de configuración.
* **`sudo apt purge <paquete>`:** Elimina completamente el paquete incluyendo todas sus configuraciones del sistema.

---

## 3. ACTIVIDAD PRÁCTICA: DESPLIEGUE DEL SERVIDOR HTTP APACHE2

A continuación se detalla la secuencia de comandos ejecutada en la terminal de Ubuntu para el despliegue del servidor web Apache2.

### Paso 1: Actualización del Índice de Paquetes
Se sincronizan las listas de software de los repositorios para garantizar la descarga de la última versión estable del servidor web.

```bash
sudo apt update
```
> **Resultado esperable:** La terminal procesa las listas `Hit` y `Get` finalizando con la lectura de paquetes completada sin errores.

### Paso 2: Instalación del Servidor Apache2
Se procede con la instalación del servidor HTTP Apache2 mediante el gestor `apt`.

```bash
sudo apt install apache2 -y
```
> **Resultado esperable:** `apt` resuelve las dependencias del paquete `apache2`, descarga los binarios y configura el servicio para su arranque en el sistema.

### Paso 3: Verificación Inicial del Servicio y Acceso Web
Se verifica el estado operativo del servicio y se comprueba el funcionamiento ingresando al navegador web.

```bash
systemctl status apache2
```
* **Acceso desde Navegador Web:** Abrir el navegador e ingresar a la URL `http://localhost`.
> **Resultado esperable:** Aparece la página por defecto de Apache2 (**Ubuntu Default Page**), confirmando que el puerto 80 responde adecuadamente.

### Paso 4: Navegación al Directorio Raíz de Contenido Web
Se cambia el directorio de trabajo hacia la ruta predeterminada donde reside la página web de bienvenida.

```bash
cd /var/www/html/
pwd
```
> **Resultado esperable:** La salida de `pwd` confirma la ubicación actual en `/var/www/html/`.

### Paso 5: Edición del Archivo Web `index.html`
Se modifica el contenido del archivo web para personalizar la entrega según los requerimientos solicitados (Carné y Nombre Completo).

```bash
sudo nano index.html
```

**Contenido ingresado en el archivo `index.html`:**
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Despliegue Servidor Apache2</title>
</head>
<body>
    <h1>Carné: 201404365</h1>
    <h2>Nombre Completo: Sergio Gudiel</h2>
</body>
</html>
```
*(Se guardan los cambios en `nano` presionando `Ctrl + O`, `Enter` y luego `Ctrl + X`).*

### Paso 6: Validación y Confirmación de Cambios
Se efectúa la recarga (*refresh*) de la página en el navegador web accediendo nuevamente a `http://localhost`.

> **Resultado esperable:** La página predeterminada de Apache2 es reemplazada y visualiza correctamente el encabezado con el carné (**201404365**) y nombre completo (**Sergio Gudiel**), confirmando la correcta modificación del archivo y publicación por el servidor HTTP.

---

## 4. CONCLUSIONES

1. **Eficiencia de la Interfaz CLI:** El control total del sistema operativo y los servicios de red a través de la interfaz de línea de comandos (CLI) prescinde de entornos gráficos, reduciendo significativamente el consumo de recursos de hardware y facilitando el despliegue remoto en servidores en la nube.
2. **Gestión Estructurada de Archivos y Permisos:** Comprender la jerarquía del sistema de archivos POSIX/UNIX, junto con el uso de herramientas como `chmod`, `chown` y la elevación mediante `sudo`, garantiza un control de acceso estricto sobre los servicios desplegados como Apache2.
3. **Despliegue de Servicios Base:** La instalación y configuración de Apache2 mediante el gestor `apt` evidencia la facilidad de habilitar servidores de producción sobre distribuciones estables de Linux como Ubuntu.
