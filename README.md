# 🌐 Configuración y Gestión de un Servidor Web Apache en Debian

Este documento resume la práctica académica sobre la instalación, configuración y gestión básica del servicio **Apache** en un entorno Linux Debian.

---

## 💡 Introducción y Objetivos

Esta práctica ha permitido explorar la instalación y configuración del servicio Apache en sistemas Debian. Los objetivos principales fueron:

* Instalación y configuración del servicio Apache en sistemas Debian.
* Análisis de los archivos de configuración principales, como `apache2.conf` y `ports.conf`.
* Personalización de páginas web básicas y gestión del archivo de inicio mediante la directiva `DirectoryIndex`.
* Adición y verificación del soporte para **PHP** a Apache.

---

## 1. Estructura y Componentes Principales

La configuración de Apache se organiza en directorios específicos en el sistema.

### Tabla de Directorios Clave

| Directorio | Descripción / Función principal |
| :--- | :--- |
| **`/etc/apache2/`** | Directorio de configuración principal. Contiene todos los archivos de configuración. |
| **`/etc/apache2/apache2.conf`** | Archivo de **configuración global**. Define configuraciones básicas y la ubicación de logs. |
| **`/etc/apache2/ports.conf`** | Define los **puertos** en los que Apache escucha las peticiones. |
| **`/etc/apache2/sites-available/`** | Contiene los archivos de configuración de todos los sitios web (`VirtualHosts`) creados. |
| **`/etc/apache2/sites-enabled/`** | Contiene los enlaces simbólicos a los sitios que están actualmente activos. |
| **`/var/www/html/`** | Ubicación por defecto del sitio web inicial (`DocumentRoot`). |
| **`/var/log/apache2/`** | Contiene los archivos de registro (logs), como `access.log` y `error.log`. |

---

## 2. Instalación y Verificación del Servicio

### 2.1 Instalación y Estado

1.  **Instalación:** Se utilizó el comando `sudo apt install apache2` para instalar el servidor Apache2.
2.  **Verificación:** El servicio se verificó como **`active (running)`** utilizando `sudo systemctl status apache2`.
3.  **Puertos:** Se confirmó que el servidor escucha por defecto en el **Puerto 80** revisando el archivo `/etc/apache2/ports.conf`.

### 2.2 Análisis de `apache2.conf`

* **Bloques `<Directory>`:** Definen permisos de acceso y opciones de configuración para directorios específicos.
* **Directivas `Include`:** Indican a Apache que incorpore configuraciones de otros archivos, como la carga de módulos y `ports.conf`.

---

## 3. Gestión del Sitio Web por Defecto

### 3.1 `DocumentRoot` y `DirectoryIndex`

1.  **`DocumentRoot`:** La directiva `DocumentRoot /var/www/html` indica a Apache la ubicación raíz de los archivos públicos del sitio web.
2.  **`DirectoryIndex`:** Para establecer un archivo personalizado (`hamza.html`) como página principal al acceder a `http://localhost/`, se utiliza la directiva **`DirectoryIndex`**.

---

## 4. Soporte PHP y Módulos

### 4.1 Instalación e Integración de PHP

1.  **Instalación:** Se instaló el intérprete de PHP y el módulo de Apache para procesar archivos `.php`.
2.  **Verificación:** Se verificó que el módulo **`php_module (shared)`** estaba cargado en Apache usando `sudo apache2ctl -M`.

### 4.2 Relación Apache y PHP

* **Delegación:** Apache necesita delegar la interpretación del código PHP a un módulo externo, ya que el código PHP no es lenguaje nativo de Apache.
* **Funcionamiento:** El módulo PHP actúa como intérprete; cuando Apache recibe un archivo `.php`, **delega la tarea de procesamiento** al módulo, el cual ejecuta el código y devuelve el resultado a Apache.

---

## 5. Comentarios

Se documentó un problema de **caché del navegador (Firefox)**, que estaba almacenando una respuesta antigua. Para resolverlo, se utilizó un navegador diferente (Chrome) para forzar una nueva conexión limpia al servidor Apache, lo cual permitió la correcta ejecución de PHP y la verificación de la página `phpinfo`.
