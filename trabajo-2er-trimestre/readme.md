# 🌐 Práctica 2º Trimestre - Servidor de Alojamiento Web (DAW 2025/26)

**Autor:** José Ángel Aquino Tayllefert    
**Entorno:** Ubuntu Desktop 24.04 en VirtualBox (Red: Adaptador Puente)  
**IP del Servidor:** 192.168.1.135  
**Dominio Local:** marisma.local  
**Repositorio:** `~/servidor-web/` (estructura: `images/`, `scripts/`, `backups/`)

---

## 📋 Índice de Pasos
1. [Paso 1: Configuración inicial del sistema](#-paso-1-configuración-inicial-del-sistema)
2. [Paso 2: Instalación de Apache2, PHP y MariaDB + phpMyAdmin](#-paso-2-instalación-de-apache2-php-y-mariadb--phpmyadmin)
3. [Paso 3: Script de automatización de clientes](#-paso-3-script-de-automatización-de-clientes)
4. [Paso 4: FTP con TLS + SSH/SFTP + Python con Apache](#-paso-4-ftp-con-tls--sshsftp--python-con-apache)
5. [Paso 5: Configuración de DNS con BIND9](#-paso-5-configuración-de-dns-con-bind9)
6. [Paso 6: Pruebas integrales y verificación final](#-paso-6-pruebas-integrales-y-verificación-final)
7. [Cómo usar el servidor](#-cómo-usar-el-servidor)
8. [Arquitectura y componentes](#-arquitectura-y-componentes)

---

## 🛠️ Paso 1: Configuración inicial del sistema

**📝 Descripción:**  
Actualización del sistema, instalación de herramientas base de red y gestión, configuración de IP estática/dinámica y creación de la estructura de directorios del proyecto.

**💻 Comandos ejecutados:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y net-tools vim curl wget git
ip addr show
ping -c 4 google.com
mkdir -p ~/servidor-web/{images,scripts,backups}
cd ~/servidor-web
```

**✅ Resultado:**  
- Sistema completamente actualizado y sin errores de dependencias.  
- Conectividad externa verificada.  
- Estructura de proyecto creada en `~/servidor-web/`.  

🖼️ `images/paso1.png`

---

## 🛠️ Paso 2: Instalación de Apache2, PHP y MariaDB + phpMyAdmin

**📝 Descripción:**  
Despliegue del stack LAMP y la herramienta de administración web de bases de datos. Se habilitaron los módulos de Apache necesarios y se verificó el correcto funcionamiento de cada servicio.

**💻 Comandos ejecutados:**
```bash
sudo apt update
sudo apt install -y apache2 php php-cli php-mysql php-curl php-gd php-mbstring php-xml php-zip libapache2-mod-php mariadb-server mariadb-client phpmyadmin
sudo systemctl enable apache2 mariadb
sudo systemctl start apache2 mariadb
sudo a2enmod rewrite ssl
sudo systemctl restart apache2
sudo ln -sf /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin
sudo systemctl reload apache2
```

**✅ Resultado:**  
- Apache2 sirviendo en puerto 80.  
- PHP 8.3 operativo con módulos esenciales.  
- MariaDB activo y accesible.  
- phpMyAdmin disponible en `/phpmyadmin`.  

🖼️ `images/paso2.png`

---

## 🛠️ Paso 3: Script de automatización de clientes

**📝 Descripción:**  
Creación del script `crear_cliente.sh` que automatiza en un único comando: usuario del sistema, directorio web, VirtualHost Apache, entrada DNS BIND9 y base de datos MySQL con privilegios completos.

**💻 Comando de instalación:**
```bash
nano ~/servidor-web/scripts/crear_cliente.sh
chmod +x ~/servidor-web/scripts/crear_cliente.sh

# Ejecución de prueba
sudo ~/servidor-web/scripts/crear_cliente.sh cliente1 192.168.1.135

# Verificación
id cliente1
ls -la /var/www/html/cliente1/
ls /etc/apache2/sites-enabled/ | grep cliente1
sudo mysql -e "SHOW DATABASES LIKE 'cliente1_db';"
sudo mysql -e "SELECT User FROM mysql.user WHERE User='cliente1_user';"
```

**✅ Resultado:**  
- Script funcional que crea en un paso: usuario, web, vhost, DNS y BD.  
- Cliente `cliente1` con directorio `/var/www/html/cliente1/` y `index.html`.  
- Base de datos `cliente1_db` con usuario `cliente1_user` y contraseña segura generada.  
- VirtualHost habilitado (resolución DNS completa en paso siguiente).  

🖼️ `images/paso3.png`

---

## 🛠️ Paso 4: FTP con TLS + SSH/SFTP + Python con Apache

**📝 Descripción:**  
Configuración de vsftpd con cifrado TLS para transferencia segura, habilitación de acceso SSH/SFTP nativo, y ejecución de aplicaciones Python mediante `mod_wsgi` en Apache.

**💻 Comandos ejecutados:**
```bash
sudo apt install -y vsftpd libapache2-mod-wsgi-py3 openssh-server
# /etc/vsftpd.conf: ssl_enable=YES, chroot_local_user=YES, pasv_address=192.168.1.135
sudo systemctl enable vsftpd ssh && sudo systemctl restart vsftpd ssh
sudo ufw allow 21/tcp && sudo ufw allow 40000:40100/tcp
sudo a2enmod wsgi
# Creación de app.py y configuración WSGIScriptAlias en VirtualHost de cliente1
sudo systemctl reload apache2
```

**✅ Resultado:**  
- vsftpd activo con TLS 1.2+, usuarios confinados a su home (`chroot_local_user=YES`).  
- SSH/SFTP operativo para administración remota segura.  
- Python 3 ejecutándose en Apache vía `mod_wsgi` en ruta `/app`.  

🖼️ `images/paso4.png`

---

## 🛠️ Paso 5: Configuración de DNS con BIND9

**📝 Descripción:**  
Instalación y configuración de BIND9 como servidor DNS autoritario local. Se crean zonas directa (`marisma.local`) e inversa (`1.168.192.in-addr.arpa`) con resolución A y PTR. El script `crear_cliente.sh` se actualiza para inyectar automáticamente registros DNS al crear nuevos clientes.

**💻 Comandos ejecutados:**

```bash
# Instalación de BIND9
sudo apt update
sudo apt install -y bind9 bind9-utils bind9-doc dnsutils
sudo systemctl enable named
sudo systemctl start named
```

**Configuración de zonas en `/etc/bind/named.conf.local`:**
- Zona directa: `marisma.local` → Resuelve nombres a IPs (registros A)
- Zona inversa: `1.168.192.in-addr.arpa` → Resuelve IPs a nombres (registros PTR)

**Archivos de zona:**
- `/etc/bind/db.marisma.local` → Contiene registros SOA, NS, A para servidor y cliente1
- `/etc/bind/db.192` → Contiene registros SOA, NS, PTR para resolución inversa

**Validación de configuración:**

```bash
sudo named-checkconf
sudo named-checkzone marisma.local /etc/bind/db.marisma.local
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/db.192
```

**Verificación con `dig`:**

```bash
# Resolución directa - servidor
dig @192.168.1.135 marisma.local

# Resolución directa - cliente1
dig @192.168.1.135 cliente1.marisma.local

# Resolución inversa
dig @192.168.1.135 -x 192.168.1.135
```

**Integración en script `crear_cliente.sh`:**  
El script ahora inyecta automáticamente registros A y PTR en las zonas BIND9 al crear un nuevo cliente, incrementando el serial de zona e recargando el servicio.

**✅ Resultado:**  
- BIND9 operativo como servidor DNS autoritario local.  
- Resolución directa (`cliente1.marisma.local` → `192.168.1.135`) verificada.  
- Resolución inversa (`192.168.1.135` → `cliente1.marisma.local`) verificada.  
- Inyección automática de registros DNS en nuevos clientes.  

🖼️ `images/paso5.png`

---

## 🛠️ Paso 6: Pruebas integrales y verificación final

**📝 Descripción:**  
Ejecución de suite completa de pruebas para verificar el funcionamiento integrado de todos los servicios: Apache2, PHP, MariaDB, BIND9, vsftpd, SSH y mod_wsgi. Se valida la creación de clientes, resolución DNS, acceso web y bases de datos.

**💻 Suite de pruebas:**

### **A. Verificación de servicios:**

```bash
# Todos los servicios deben estar active (running)
sudo systemctl status apache2 mariadb named vsftpd ssh
```

### **B. Verificación de usuarios y directorios:**

```bash
# Listar usuarios del sistema
cut -d: -f1 /etc/passwd | grep -E "^cliente|^usuario"

# Listar directorios web
ls -la /var/www/html/

# Verificar contenido de cliente1
cat /var/www/html/cliente1/index.html
```

### **C. Verificación de bases de datos:**

```bash
# Listar bases de datos
sudo mysql -e "SHOW DATABASES;"

# Verificar usuarios MySQL
sudo mysql -e "SELECT User, Host FROM mysql.user WHERE User LIKE 'cliente%';"

# Verificar permisos
sudo mysql -e "SHOW GRANTS FOR 'cliente1_user'@'localhost';"
```

### **D. Verificación DNS:**

```bash
# Validar configuración BIND9
sudo named-checkconf
sudo named-checkzone marisma.local /etc/bind/db.marisma.local
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/db.192

# Pruebas de resolución
dig @192.168.1.135 cliente1.marisma.local +short
dig @192.168.1.135 -x 192.168.1.135 +short
```

### **E. Verificación Apache y VirtualHosts:**

```bash
# Listar VirtualHosts habilitados
ls /etc/apache2/sites-enabled/

# Acceso a servidor principal
curl -s http://192.168.1.135 -I | head -5

# phpMyAdmin
curl -s -o /dev/null -w "Status: %{http_code}\n" http://192.168.1.135/phpmyadmin
```

### **F. Verificación FTP/SFTP/SSH:**

```bash
# Verificar puertos abiertos
sudo netstat -tlnp | grep -E "21|22"

# Verificar configuración FTP
sudo grep -E "ssl_enable|chroot_local_user" /etc/vsftpd.conf
```

### **G. Verificación Python/WSGI:**

```bash
# Verificar módulo mod_wsgi
sudo apache2ctl -M | grep wsgi

# Verificar archivo app.py
ls -la /var/www/html/cliente1/
```

### **H. Prueba integral - Crear nuevo cliente:**

```bash
# Crear cliente2 completo
sudo ~/servidor-web/scripts/crear_cliente.sh cliente2 192.168.1.135

# Verificar usuario
id cliente2

# Verificar directorio
ls -la /var/www/html/cliente2/

# Verificar base de datos
sudo mysql -e "SHOW DATABASES LIKE 'cliente2_db';"

# Verificar DNS
dig @192.168.1.135 cliente2.marisma.local +short

# Acceso HTTP
curl -s http://cliente2.marisma.local -H "Host: cliente2.marisma.local" | head -5
```

**✅ Resultado:**  
- ✓ Todos los 5 servicios operativos: Apache2, MariaDB, BIND9, vsftpd, SSH  
- ✓ Usuarios creados: `cliente1`, `cliente2` (ejemplo)  
- ✓ Directorios web con contenido por defecto en `/var/www/html/cliente{1,2}/`  
- ✓ Bases de datos independientes para cada cliente con usuarios con ALL PRIVILEGES  
- ✓ Resolución DNS directa e inversa funcional para todos los subdominios  
- ✓ VirtualHosts habilitados y accesibles vía HTTP  
- ✓ phpMyAdmin operativo en `/phpmyadmin`  
- ✓ FTP/SFTP con TLS y SSH accesibles en puertos 21 y 22  
- ✓ Python ejecutándose en Apache2 vía mod_wsgi  
- ✓ Script `crear_cliente.sh` completamente automatizado y funcional  

🖼️ `images/paso6.png`

---

## 📖 Cómo usar el servidor

### Crear un nuevo cliente

```bash
sudo ~/servidor-web/scripts/crear_cliente.sh nombre_cliente 192.168.1.135
```

**El script automáticamente:**
- ✅ Crea usuario del sistema
- ✅ Crea directorio web `/var/www/html/nombre_cliente/`
- ✅ Crea página de bienvenida con `index.html`
- ✅ Crea VirtualHost Apache con `ServerName nombre_cliente.marisma.local`
- ✅ Inyecta registros DNS (A y PTR) en BIND9 con validación automática
- ✅ Incrementa serial de zona DNS
- ✅ Crea base de datos MySQL `nombre_cliente_db`
- ✅ Crea usuario MySQL `nombre_cliente_user` con ALL PRIVILEGES
- ✅ Genera contraseña segura (openssl rand -base64 12)
- ✅ Recarga Apache2 y BIND9 automáticamente

**Ejemplo de uso:**
```bash
sudo ~/servidor-web/scripts/crear_cliente.sh tienda 192.168.1.135
sudo ~/servidor-web/scripts/crear_cliente.sh blog 192.168.1.135
sudo ~/servidor-web/scripts/crear_cliente.sh api 192.168.1.135
```

---

## 🌐 Acceder a los clientes

### Acceso Web
```bash
# Cliente principal
http://192.168.1.135

# Cliente específico
http://cliente_prueba.marisma.local
http://www.cliente_prueba.marisma.local
```

### phpMyAdmin (administración de bases de datos)
```
URL: http://192.168.1.135/phpmyadmin
Usuario: nombre_cliente_user
Contraseña: (generada por el script al crear cliente)
```

### FTP Seguro (TLS)
```bash
# Conexión FTP
ftp://nombre_cliente@192.168.1.135
Puerto: 21
TLS: Habilitado (FTPS)

# Ejemplo con cliente:
ftp nombre_cliente@192.168.1.135
```

### SSH / SFTP
```bash
# SSH
ssh nombre_cliente@192.168.1.135

# SFTP
sftp nombre_cliente@192.168.1.135

# Transferencia de archivos
sftp> put archivo.txt /var/www/html/
sftp> get archivo.txt
```

---

## 📡 Verificar DNS

### Resolución directa
```bash
dig @192.168.1.135 cliente_prueba.marisma.local
dig @192.168.1.135 www.cliente_prueba.marisma.local
```

**Resultado esperado:** `192.168.1.135`

### Resolución inversa
```bash
dig @192.168.1.135 -x 192.168.1.135
```

**Resultado esperado:** `cliente_prueba.marisma.local`

### Ver todos los registros de una zona
```bash
dig @192.168.1.135 marisma.local AXFR
```

---

## 🏗️ Arquitectura y componentes

### Stack teknológico

| Componente | Versión | Puerto | Estado |
|-----------|---------|--------|--------|
| Apache2 | 2.4.x | 80, 443 | ✅ Activo |
| PHP | 8.3 | N/A | ✅ Activo |
| MariaDB | 10.11.x | 3306 | ✅ Activo |
| BIND9 DNS | 9.18.x | 53 | ✅ Activo |
| vsftpd FTP | 3.0.x | 21 | ✅ Activo (TLS) |
| OpenSSH | 8.9.x | 22 | ✅ Activo |
| mod_wsgi | 4.9.x | N/A | ✅ Activo |

### Componentes del servidor

- **Web Server:** Apache2 con módulos rewrite, ssl, wsgi
- **Backend:** PHP 8.3 con extensiones mysql, curl, gd, mbstring, xml, zip
- **Database:** MariaDB (compatible MySQL)
- **Admin Web:** phpMyAdmin
- **DNS:** BIND9 (servidor autoritario local)
- **Transferencia FTP:** vsftpd con cifrado TLS
- **Shell remoto:** OpenSSH (SSH/SFTP)
- **Python:** Soporte mediante mod_wsgi en Apache2

---

## 📁 Estructura del proyecto

```
~/servidor-web/
├── README.md                    # Este archivo - Documentación completa
├── images/
│   ├── paso1.png               # Captura configuración inicial
│   ├── paso2.png               # Captura Stack LAMP + phpMyAdmin
│   ├── paso3.png               # Captura script crear_cliente
│   ├── paso4.png               # Captura FTP/SSH/Python
│   ├── paso5.png               # Captura DNS BIND9
│   └── paso6.png               # Captura pruebas integrales
```

---

## 🔐 Seguridad implementada

- ✅ **FTP con TLS 1.2+**: Cifrado de credenciales y datos en tránsito
- ✅ **SSH con OpenSSH**: Acceso remoto seguro sin contraseña (keys)
- ✅ **Usuarios independientes**: Cada cliente con usuario del sistema separado
- ✅ **Chroot FTP**: Usuarios confinados a su directorio home (`chroot_local_user=YES`)
- ✅ **Permisos restrictivos**: Directorios web con permisos 755 (dir) / 644 (archivos)
- ✅ **BD independientes**: Cada cliente con BD y usuario MySQL separados
- ✅ **Contraseñas aleatorias**: Generadas con openssl (12 caracteres, base64)
- ✅ **Validación DNS**: `named-checkzone` valida antes de recargar BIND9
- ✅ **Módulos SSL habilitados**: Soporte para HTTPS en Apache2

---

## 🧪 Pruebas de funcionalidad completas

### Verificar todos los servicios
```bash
sudo systemctl status apache2 mariadb named vsftpd ssh
```

### Crear cliente de prueba
```bash
sudo ~/servidor-web/scripts/crear_cliente.sh test 192.168.1.135
```

### Verificar acceso web
```bash
curl http://test.marisma.local -H "Host: test.marisma.local"
```

### Verificar base de datos
```bash
sudo mysql -u test_user -p -e "SHOW DATABASES;"
```

### Verificar DNS (ambas direcciones)
```bash
dig @192.168.1.135 test.marisma.local +short
dig @192.168.1.135 -x 192.168.1.135 +short
```

### Verificar FTP
```bash
ftp -d test@192.168.1.135
# Login y exit
```

### Verificar SSH
```bash
ssh test@192.168.1.135 "echo 'SSH funciona'"
```

---

## 📝 Requisitos cumplidos de la práctica

✅ **Instalación y configuración de servidor web configurable**
- Apache2 con múltiples VirtualHosts
- Cada cliente con directorio independiente
- Fácil escalabilidad con script automatizado

✅ **Alojamiento de páginas estáticas y dinámicas**
- HTML/CSS en directorio público
- PHP 8.3 ejecutándose en Apache2
- Python ejecutándose vía mod_wsgi

✅ **Directorio de usuario con página por defecto**
- Script crea `/var/www/html/{cliente}/index.html` automáticamente
- Muestra información del cliente y versión de PHP
- Diseño HTML responsivo

✅ **Base de datos SQL con phpMyAdmin**
- MariaDB con BD independiente por cliente
- Usuario MySQL con ALL PRIVILEGES
- phpMyAdmin en `/phpmyadmin` accesible desde navegador

✅ **Acceso FTP configurado con TLS**
- vsftpd con `ssl_enable=YES`
- Cifrado de credenciales y datos (FTPS)
- PASV mode con `pasv_address=192.168.1.135`
- Rango de puertos 40000-40100

✅ **Acceso SSH y SFTP**
- OpenSSH operativo en puerto 22
- SFTP para transferencia segura de archivos
- Usuarios del sistema con acceso remoto

✅ **Automatización mediante scripts**
- `crear_cliente.sh` crea usuario, directorio, vhost, DNS, BD en un paso
- Validación automática de configuración
- Incremento inteligente de serial DNS
- Recarga automática de servicios (Apache2 y BIND9)
- Generación segura de contraseñas

✅ **Crear subdominio en DNS**
- BIND9 con zonas directa e inversa
- Resolución A (nombre → IP)
- Resolución PTR (IP → nombre inversa)
- Inyección automática de registros al crear cliente
- Validación con `named-checkzone`

✅ **Base de datos con usuario con ALL PRIVILEGES**
- Script crea usuario MySQL con `GRANT ALL PRIVILEGES`
- Contraseña aleatoria segura generada automáticamente
- Flush privileges para aplicar cambios

✅ **Ejecución de aplicaciones Python**
- mod_wsgi habilitado en Apache2
- Soporte para aplicaciones WSGI
- Ejemplos de integración disponibles
- Funciona en paralelo con PHP

---

## 🎓 Información técnica del entorno

- **Sistema operativo:** Ubuntu 24.04 LTS Desktop
- **Arquitectura:** x86_64
- **Hipervisor:** VirtualBox con Adaptador Puente (Bridged)
- **IP servidor:** 192.168.1.135
- **Dominio local:** marisma.local
- **Zona inversa:** 1.168.192.in-addr.arpa

### Archivos de configuración principales

```bash
# Apache2
/etc/apache2/sites-available/          # VirtualHosts por cliente
/etc/apache2/mods-enabled/             # Módulos habilitados

# DNS BIND9
/etc/bind/named.conf.local             # Definición de zonas
/etc/bind/db.marisma.local             # Zona directa
/etc/bind/db.192                       # Zona inversa

# FTP
/etc/vsftpd.conf                       # Configuración vsftpd con TLS

# SSH
/etc/ssh/sshd_config                   # Configuración OpenSSH

# MariaDB
/etc/mysql/mariadb.conf.d/             # Configuración MariaDB

# PHP
/etc/php/8.3/apache2/php.ini           # Configuración PHP
```

---

## 📊 Estadísticas del servidor

- **Servicios activos:** 5 (Apache2, MariaDB, BIND9, vsftpd, SSH)
- **Clientes creados:** 2+ (cliente1, cliente2, cliente_prueba)
- **Bases de datos:** 1+ por cliente
- **Usuarios del sistema:** 1+ por cliente
- **VirtualHosts:** 1+ por cliente
- **Módulos Apache:** rewrite, ssl, wsgi, php
- **Extensiones PHP:** mysql, curl, gd, mbstring, xml, zip

---

## 🚀 Cómo empezar

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/servidor-web.git
cd servidor-web
```

### 2. Ejecutar el sistema (en Ubuntu)
```bash
# Todos los servicios ya están instalados y configurados
sudo systemctl status apache2 mariadb named vsftpd ssh
```

### 3. Crear tu primer cliente
```bash
sudo ~/servidor-web/scripts/crear_cliente.sh micliente 192.168.1.135
```

### 4. Acceder
```bash
# Web
http://micliente.marisma.local

# Administración BD
http://192.168.1.135/phpmyadmin
```

---

## 📞 Soporte y documentación

Para información adicional sobre cada componente:

- **Apache2:** `man apache2ctl` | https://httpd.apache.org/
- **PHP:** `php -v` | https://www.php.net/
- **MariaDB:** `mysql -V` | https://mariadb.org/
- **BIND9:** `named -v` | https://www.isc.org/bind/
- **vsftpd:** `man vsftpd` | https://security.appspot.com/vsftpd.html
- **OpenSSH:** `man ssh` | https://www.openssh.com/

---

## 📜 Licencia

Este proyecto es un trabajo académico para la asignatura **Despliegue de Aplicaciones Web (DAW)** del ciclo formativo de grado superior de Despliegue de Aplicaciones Web (DAW).

---

## ✍️ Autores y contribuciones

**Desarrollo y configuración:** José Ángel Aquino Tayllefert  
**Centro educativo:** IES La Marisma  
**Comunidad autónoma:** Andalucía (Consejería de Educación y Deporte)

---

**Última actualización:** Mayo 2026  
**Versión:** 1.0 - Release

---
