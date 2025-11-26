# 🌐 Servidor Web Apache en Linux: Configuración y Gestión

---

## 💡 Introducción y Objetivos

Esta práctica ha permitido explorar en profundidad la **instalación, configuración y gestión de un servidor web Apache** en un entorno Debian.

Los objetivos cubiertos incluyen:
* Instalación y configuración del servicio Apache en sistemas Debian.
* Análisis y edición de archivos de configuración principales (`apache2.conf`, `ports.conf`, `sites-available/`).
* Personalización de páginas web básicas y gestión del archivo de inicio (`DirectoryIndex`).
* Añadir y verificar el soporte de PHP a Apache.
* Análisis de los módulos habilitados y su función.

---

## 1. Instalación y Verificación del Servicio

### 1.1 Instalación de Apache

Para instalar el servidor web, primero se actualizó el sistema y luego se instaló el paquete `apache2`.

| Comando | Función |
| :--- | :--- |
| `sudo apt update` | Actualiza la lista de paquetes del sistema. |
| `sudo apt install apache2` | Instala el servidor Apache2 y sus dependencias (`apache2-data`, `apache2-utils`). |

### 1.2 Verificación del Servicio y Puertos

Se verificó el estado del servicio y el puerto de escucha por defecto.

1.  **Estado del Servicio:** Se utilizó el comando `sudo systemctl status apache2` para confirmar que el servicio está **`active (running)`**.
2.  **Puerto de Escucha:** Se confirmó que el puerto de escucha por defecto es el **Puerto 80**, revisando el archivo de configuración **`/etc/apache2/ports.conf`**. El tráfico HTTPS se escucha en el puerto `443` si el módulo SSL está activo.

### 1.3 Análisis del Archivo de Configuración Principal (`apache2.conf`)

El archivo **`/etc/apache2/apache2.conf`** contiene la **configuración global y las directivas** que se aplican a todo el servidor Apache.Es crucial porque define configuraciones de seguridad, la ubicación de módulos, sitios web y registros de errores.

* **Bloques `<Directory>`:** Definen permisos de acceso y opciones para directorios específicos (ej., `/var/www/`) para controlar cómo el servidor gestiona el contenido.
* **Directivas `Include`:** Indican a Apache que incorpore configuraciones de otros archivos y directorios, como la configuración de módulos (`mods-enabled`) y la lista de puertos (`ports.conf`).
* **Definición de Usuario/Grupo:** Establece el usuario y grupo con los que se ejecutarán los procesos de Apache (definidos en `/etc/apache2/envvars`), lo cual es crucial para la gestión de permisos y seguridad.
* **Registro de Errores (`ErrorLog`):** Define la ubicación del archivo de registro de errores, que por defecto es `${APACHE_LOG_DIR}/error.log`.

---

## 2. Gestión del Sitio Web por Defecto

### 2.1 Modificación del Sitio Web por Defecto

Sí, es posible modificar el sitio por defecto editando el archivo de configuración **`000-default.conf`** ubicado en `/etc/apache2/sites-available/`.

La directiva **`DocumentRoot /var/www/html`** le indica a Apache la ubicación en el sistema de archivos (`/var/www/html/`) donde se encuentran los archivos públicos del sitio web que debe servir[cite: 163, 164, 171].

### 2.2 Personalización de la Página Principal

1.  Se creó un nuevo fichero HTML (`hamza.html`) dentro del directorio `/var/www/html/`.
2.  Para establecer `hamza.html` como la página principal al acceder a la web, se modificó el archivo **`000-default.conf`**.
3.  Se añadió la directiva **`DirectoryIndex`** dentro del bloque `<Directory /var/www/html>`.

**Configuración Añadida:**
```conf
<Directory /var/www/html>
    DirectoryIndex hamza.html index.html index.php
</Directory>
