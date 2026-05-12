<div align="center">

# 🚀 Despliegue de Aplicaciones Web  
### 📘 Tareas – 2º DAW

<img src="https://img.shields.io/badge/Despliegue-Aplicaciones%20Web-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/Curso-2025%2F2026-green?style=for-the-badge">
<img src="https://img.shields.io/badge/Alumno-José%20Ángel%20Aquino%20Tayllefert-orange?style=for-the-badge">

---

📚 **Repositorio dedicado a documentar todas las actividades, prácticas y configuraciones realizadas en la asignatura de _Despliegue de Aplicaciones Web_.**  
Incluye explicaciones, ejemplos, capturas y configuraciones reales de Apache, VirtualHosts, SSL, Rewrite, permisos, DNS, Docker, Docker Compose, etc.

---

</div>

## 📑 **Índice**

1. [📝 Descripción](#-descripción)
2. [📂 Estructura del repositorio](#-estructura-del-repositorio)
3. [🔥 Tema 1 – Servidores Web (Apache)](#-tema-1--servidores-web-apache)
4. [🐳 Tema 5 – Docker y Containerización](#-tema-5--docker-y-containerización)
5. [📌 Trabajo del 1º Trimestre](#-trabajo-del-1º-trimestre)
6. [📌 Trabajo del 2º Trimestre](#-trabajo-del-2º-trimestre)
7. [🔧 Tecnologías utilizadas](#-tecnologías-utilizadas)
8. [💬 Autor](#-autor)

---

## 📝 **Descripción**

Este repositorio contiene la documentación detallada de todas las tareas realizadas durante el módulo **Despliegue de Aplicaciones Web**.

Incluye:
- Instalación y configuración de servidores web (Apache)
- Gestión de VirtualHosts
- Configuración de seguridad (SSL, autenticación, permisos)
- Reglas Rewrite con expresiones regulares
- Servidor DNS local (BIND9)
- **Docker y containerización**
- **Docker Compose para aplicaciones multi-contenedor**
- **Creación de imágenes Docker optimizadas**
- Automatización con scripts bash
- Tareas explicadas paso a paso con capturas

El objetivo es tener una **documentación clara, profesional y reutilizable**.

---

## 📂 **Estructura del Repositorio**
```
tareas-despliegue-aplicaciones-web/
│
├── tema1-servidores-web/
│   ├── activity1-instalacion-apache/
│   ├── activity2-configuracion-basica/
│   ├── activity5-directiva-directory/
│   ├── activity6-expresiones-regulares/
│   ├── activity7-rewrite/
│   ├── activity8-virtualhost/
│   ├── activity9-authentication/
│   ├── activity10-ssl/
│   └── README.md
│
├── tema5-docker/
│   ├── README.md
│   ├── activity1-instalacion-docker/
│   │   ├── README.md
│   │   └── images/ (6 capturas)
│   ├── activity2-introduccion-contenedores/
│   │   ├── README.md
│   │   └── images/ (13 capturas)
│   ├── activity3-imagenes-contenedores/
│   │   ├── README.md
│   │   └── images/ (10 capturas)
│   ├── activity4-almacenamiento-redes/
│   │   ├── README.md
│   │   └── images/ (12 capturas)
│   ├── activity5-docker-compose/
│   │   ├── README.md
│   │   └── images/ (9 capturas)
│   └── activity6-creacion-imagenes/
│       ├── README.md
│       └── images/ (16 capturas)
│
├── trabajo-1er-trimestre/
│   ├── Paso1-Apache/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso2-PHP-MySQL/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso3-WordPress/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso4-Python-WSGI/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso5-Autenticacion/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso6-AWStats/
│   │   ├── README.md
│   │   └── capturas/
│   ├── Paso7-Segundo-Servidor/
│   │   ├── README.md
│   │   └── capturas/
│   └── README.md
│
└── trabajo-2er-trimestre/
    ├── servidor-alojamiento-web/
    │   ├── README.md (Documentación completa)
    │   ├── images/
    │   │   ├── paso1.png
    │   │   ├── paso2.png
    │   │   ├── paso3.png
    │   │   ├── paso4.png
    │   │   ├── paso5.png
    │   │   └── paso6.png
    └── README.md
```

> ✨ *Cada actividad tendrá su propio README con capturas, explicaciones y ejemplos de configuración.*

---

## 🔥 **Tema 1 — Servidores Web (Apache)**

| Actividad | Descripción | Enlace |
|----------|-------------|--------|
| **Activity #1** | Instalación de Apache | [`activity1`](./tema1-servidores-web/activity1-instalacion-apache/) |
| **Activity #2** | Configuración básica | [`activity2`](./tema1-servidores-web/activity2-configuracion-basica/) |
| **Activity #5** | Directiva `Directory` | [`activity5`](./tema1-servidores-web/activity5-directiva-directory/) |
| **Activity #6** | Expresiones regulares | [`activity6`](./tema1-servidores-web/activity6-expresiones-regulares/) |
| **Activity #7** | Reescritura de URL | [`activity7`](./tema1-servidores-web/activity7-rewrite/) |
| **Activity #8** | VirtualHosts | [`activity8`](./tema1-servidores-web/activity8-virtualhost/) |
| **Activity #9** | Autenticación básica | [`activity9`](./tema1-servidores-web/activity9-authentication/) |
| **Activity #10** | Certificados y SSL | [`activity10`](./tema1-servidores-web/activity10-ssl/) |

---

## 🐳 **Tema 5 — Docker y Containerización**

📁 **Acceder a:** [`tema5-docker`](./tema5-docker/)

### 📦 **Práctica — Docker: Instalación, Contenedores, Imágenes y Orquestación**

Tema completo dedicado a **Docker**, desde conceptos básicos hasta la creación de imágenes optimizadas y orquestación con Docker Compose.

| Actividad | Descripción | Duración | Nivel | Enlace |
|----------|-------------|----------|-------|--------|
| **Activity #1** | Instalación de Docker en Ubuntu 24.04 | 20 min | ⭐ | [`activity1-instalacion-docker`](./tema5-docker/activity1-instalacion-docker/) |
| **Activity #2** | Introducción a los contenedores | 45 min | ⭐ | [`activity2-introduccion-contenedores`](./tema5-docker/activity2-introduccion-contenedores/) |
| **Activity #3** | Imágenes y contenedores | 60 min | ⭐⭐ | [`activity3-imagenes-contenedores`](./tema5-docker/activity3-imagenes-contenedores/) |
| **Activity #4** | Almacenamiento y redes Docker | 90 min | ⭐⭐ | [`activity4-almacenamiento-redes`](./tema5-docker/activity4-almacenamiento-redes/) |
| **Activity #5** | Docker Compose | 120 min | ⭐⭐⭐ | [`activity5-docker-compose`](./tema5-docker/activity5-docker-compose/) |
| **Activity #6** | Creación de imágenes Docker | 120 min | ⭐⭐⭐ | [`activity6-creacion-imagenes`](./tema5-docker/activity6-creacion-imagenes/) |

**Características principales:**

✅ **Contenedores Docker**
- Instalación en Ubuntu 24.04
- Ciclo de vida del contenedor
- Ejecución en modo interactivo y detachado
- Mapeo de puertos y volúmenes
- Logs y debugging

✅ **Gestión de imágenes**
- Descargar imágenes desde Docker Hub
- Crear y nombrar contenedores
- Listar, inspeccionar y eliminar recursos
- Historial de capas
- Tamaño y optimización de imágenes

✅ **Almacenamiento y redes**
- Volúmenes Docker para persistencia
- Bind mounts para desarrollo
- Redes personalizadas
- Comunicación entre contenedores por nombre
- Ejemplos prácticos: MySQL, Nginx, phpMyAdmin

✅ **Docker Compose**
- Definición YAML de aplicaciones multi-contenedor
- 3 ejemplos: Nginx simple, Stack LEMP, Variables de entorno
- Gestión de servicios, volúmenes y redes
- Comandos: up, down, ps, logs, exec

✅ **Creación de imágenes**
- 5 Dockerfiles prácticos: Python, Node.js, Multi-stage, Best practices, Alpine
- Optimización de imágenes (reducir tamaño)
- Mejores prácticas: usuario no-root, .dockerignore, labels
- Multi-stage builds para producción
- Comparación de tamaños

✅ **6 actividades completas**
- 6 READMEs profesionales (550+ líneas totales)
- 61+ capturas de pantalla integradas
- 50+ ejemplos prácticos funcionales
- Documentación técnica detallada
- Troubleshooting y mejores prácticas

**Contenido incluido:**
- 📖 README principal del tema (con índice)
- 📖 6 READMEs específicos (1 por actividad)
- 📸 61+ capturas de pantalla en carpetas `images/`
- 🔧 Dockerfiles comentados y listos para usar
- 📊 Tablas de referencia y comandos
- 🎯 Checklist de evaluación por actividad
- 💡 Mejores prácticas y troubleshooting

**Duración total:** 8 horas (distribuidas en 6 actividades)

**Requisitos cumplidos:**
- ✅ Instalación y configuración de Docker
- ✅ Ciclo de vida completo de contenedores
- ✅ Gestión profesional de imágenes
- ✅ Almacenamiento persistente con volúmenes
- ✅ Redes Docker personalizadas
- ✅ Orquestación con Docker Compose
- ✅ Creación optimizada de imágenes
- ✅ Aplicaciones multi-contenedor funcionales

---

## 📌 **Trabajo del 1º Trimestre**

📁 **Acceder a:** [`trabajo-1er-trimestre`](./trabajo-1er-trimestre/)

### 🔥 **Práctica — Configuración de Servidores Web**

| Paso | Descripción | Enlace |
|-----|-------------|--------|
| **Paso 1** | Instalación y configuración de Apache + VirtualHosts | [`Paso1-Apache`](./trabajo-1er-trimestre/Paso1/) |
| **Paso 2** | Instalación de PHP y MySQL | [`Paso2-PHP-MySQL`](./trabajo-1er-trimestre/Paso2/) |
| **Paso 3** | Instalación y configuración de WordPress | [`Paso3-WordPress`](./trabajo-1er-trimestre/Paso3/) |
| **Paso 4** | Aplicación Python con WSGI en Apache | [`Paso4-Python-WSGI`](./trabajo-1er-trimestre/Paso4/) |
| **Paso 5** | Protección mediante autenticación básica | [`Paso5-Autenticacion`](./trabajo-1er-trimestre/Paso5) |
| **Paso 6** | Monitorización del servidor con AWStats | [`Paso6-AWStats`](./trabajo-1er-trimestre/Paso6/) |
| **Paso 7** | Segundo servidor web con Nginx, PHP y phpMyAdmin | [`Paso7-Segundo-Servidor`](./trabajo-1er-trimestre/Paso7/) |

**Incluye:**
- Informe completo  
- Configuración avanzada de Apache  
- Explicaciones de seguridad web  
- Archivos `.conf` comentados

---

## 📌 **Trabajo del 2º Trimestre**

📁 **Acceder a:** [`trabajo-2er-trimestre`](./trabajo-2er-trimestre/)

### 🌐 **Práctica — Servidor de Alojamiento Web Configurable**

**Descripción:**  
Implementación de un servidor web multicliente completamente automatizado con soporte para usuarios independientes, bases de datos, DNS, FTP, SSH y Python. Incluye script de automatización que gestiona la creación completa de clientes en un único comando.

| Paso | Descripción | Estado |
|-----|-------------|--------|
| **Paso 1** | Configuración inicial del sistema | ✅ Completado |
| **Paso 2** | Stack LAMP + phpMyAdmin | ✅ Completado |
| **Paso 3** | Script de automatización de clientes | ✅ Completado |
| **Paso 4** | FTP con TLS + SSH/SFTP + Python | ✅ Completado |
| **Paso 5** | Configuración DNS con BIND9 | ✅ Completado |
| **Paso 6** | Pruebas integrales y verificación | ✅ Completado |

**Características principales:**

✅ **Stack LAMP completo**
- Apache2 con múltiples VirtualHosts
- PHP 8.3 con módulos esenciales
- MariaDB para bases de datos
- phpMyAdmin para administración

✅ **Automatización mediante scripts**
- `crear_cliente.sh`: Crea usuario, directorio, vhost, DNS, BD en un paso
- Validación automática de configuración
- Incremento inteligente de serial DNS
- Recarga automática de servicios

✅ **DNS autoritario local (BIND9)**
- Zonas directa e inversa
- Resolución A (nombre → IP)
- Resolución PTR (IP → nombre)
- Inyección automática de registros al crear clientes

✅ **Seguridad**
- FTP con TLS 1.2+
- SSH/SFTP para acceso remoto
- Usuarios confinados a su directorio (chroot)
- Contraseñas aleatorias seguras

✅ **Aplicaciones Python**
- Soporte mod_wsgi en Apache2
- Integración con aplicaciones WSGI

✅ **6 pasos documentados**
- README profesional con 6+ secciones
- 6 capturas de pantalla integradas
- Guías de uso y troubleshooting
- Arquitectura técnica detallada

**Acceder al proyecto:**
```bash
cd trabajo-2er-trimestre/servidor-alojamiento-web
```

**Crear un nuevo cliente:**
```bash
sudo ~/servidor-web/scripts/crear_cliente.sh tienda 192.168.1.135
```

**Requisitos cumplidos según práctica:**
- ✅ Instalación y configuración de servidor web configurable
- ✅ Alojamiento de páginas estáticas y dinámicas (PHP)
- ✅ Directorios de usuario con páginas por defecto
- ✅ Bases de datos SQL con phpMyAdmin
- ✅ Acceso FTP con TLS
- ✅ Acceso SSH y SFTP
- ✅ Automatización mediante scripts
- ✅ Subdominios en DNS con resolución directa e inversa
- ✅ Bases de datos con usuarios con ALL PRIVILEGES
- ✅ Ejecución de aplicaciones Python

**Documentación:**
- 📖 README.md completo (350+ líneas)
- 📸 6 capturas de pantalla de terminal
- 🔧 Script bash comentado y funcional
- 📊 Tablas comparativas y diagramas
- 🔐 Sección de seguridad detallada

---

## 🔧 **Tecnologías utilizadas**

| Tecnología | Uso |
|-----------|-----|
| 🟦 Apache2 | Servidor web principal |
| 🟩 PHP 8.3 | Backend dinámico |
| 🟨 MariaDB | Base de datos |
| 🟪 BIND9 | Servidor DNS local |
| 🔴 vsftpd | Servidor FTP con TLS |
| 🔵 OpenSSH | Acceso remoto SSH/SFTP |
| 🐳 **Docker** | **Containerización** |
| 🐳 **Docker Compose** | **Orquestación de contenedores** |
| 🟧 Bash | Scripts de automatización |
| 🐧 Ubuntu 24.04 LTS | Sistema operativo |
| 🐍 Python | Aplicaciones WSGI |
| 📝 Markdown | Documentación |
| 🔐 OpenSSL | Cifrado y seguridad |

---

## 📊 **Estadísticas del repositorio**

- **Trimestres documentados:** 2
- **Tareas completadas:** 21+
- **Temas completados:** 2 (Tema 1 + Tema 5)
- **Prácticas finales:** 2
- **Líneas de código/configuración:** 8000+
- **Capturas incluidas:** 80+
- **README files:** 16+
- **Scripts bash:** 2+
- **Dockerfiles:** 5+

---

## 💬 **Autor**

👤 **José Ángel Aquino Tayllefert**  
📚 2º DAW – Desarrollo de Aplicaciones Web  
📌 Curso 2025/26  
🏫 IES La Marisma – Andalucía

---

## 📋 **Licencia**

Este repositorio es un trabajo académico para la asignatura **Despliegue de Aplicaciones Web** del ciclo formativo de grado superior.

---

<div align="center">

✨ _Este repositorio se actualiza periódicamente con nuevas tareas, mejoras y configuraciones._  

**[⬆ Volver arriba](#-despliegue-de-aplicaciones-web)**

¡Gracias por visitar! 🙌

</div>
