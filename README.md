# MANUAL TÉCNICO Y PRÁCTICO: UBUNTU LINUX & DESPLIEGUE WEB APACHE2

**Universidad de San Carlos de Guatemala**  
**Facultad de Ingeniería**  
**Escuela de Ciencias y Sistemas**  
**Curso:** Prácticas Iniciales  
**Semestre:** Segundo Semestre 2026  
**Estudiante:** Sergio Roberto Gudiel Sian  
**Carné:** 201404365  
**Fecha de Calificación:** 27 de Agosto de 2026  

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
| **Intérprete por Defecto** | PowerShell / CMD. | Bash Shell. |
| **Arquitectura Base** | Basado en Kernel Windows NT. | Basado en el estándar POSIX / Arquitectura UNIX. |

---

## 2. INVESTIGACIÓN Y DOCUMENTACIÓN DE COMANDOS CLI

### 2.1. Gestión de Navegación

#### `pwd` (Print Working Directory)
Muestra la ruta absoluta del directorio de trabajo actual en el que se encuentra posicionado el usuario.

* **Sintaxis:** `pwd [opciones]`
* **Opciones principales:**
  * `pwd`: Imprime la ruta actual resolviendo enlaces simbólicos por defecto.
  * `pwd -P`: Muestra la ruta física real excluyendo enlaces simbólicos (*symlinks*).
* **Ejemplo de ejecución:**
  ```bash
  vboxuser@Ubuntu:~$ pwd
  /home/vboxuser
  vboxuser@Ubuntu:~$ pwd -P
  /home/vboxuser
