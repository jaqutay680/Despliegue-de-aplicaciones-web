# Paso 1 – Instalación y configuración del servidor Apache

---

## 1. Pasos a seguir (comandos listos para copiar y pegar)

### 1.1 Actualizar el sistema
```bash
sudo apt update
```
📸 Captura: `capturas/paso1/01-apt-update.png`

---

### 1.2 Instalar Apache
```bash
sudo apt install apache2
```
📸 Captura: `capturas/paso1/02-instalacion-apache.png`

---

### 1.3 Comprobar el estado del servicio
```bash
sudo systemctl status apache2
```
📸 Captura: `capturas/paso1/03-estado-apache.png`

---

### 1.4 Configurar dominios locales
Editar el archivo `/etc/hosts`:

```bash
sudo nano /etc/hosts
```

Añadir:
```
127.0.0.1 centro.intranet
127.0.0.1 departamentos.centro.intranet
```

📸 Captura: `capturas/paso1/04-hosts.png`

---

### 1.5 Crear directorios web
```bash
sudo mkdir -p /var/www/centro
sudo mkdir -p /var/www/departamentos
```

📸 Captura: `capturas/paso1/05-directorios.png`

---

### 1.6 Asignar permisos
```bash
sudo chown -R www-data:www-data /var/www/centro /var/www/departamentos
sudo chmod -R 755 /var/www/centro /var/www/departamentos
```

📸 Captura: `capturas/paso1/06-permisos.png`

---

### 1.7 Crear VirtualHost para centro.intranet
```bash
sudo nano /etc/apache2/sites-available/centro.intranet.conf
```

Contenido:
```apache
<VirtualHost *:80>
    ServerName centro.intranet
    DocumentRoot /var/www/centro

    <Directory /var/www/centro>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/centro_error.log
    CustomLog ${APACHE_LOG_DIR}/centro_access.log combined
</VirtualHost>
```

📸 Captura: `capturas/paso1/07-vhost-centro.png`

---

### 1.8 Crear VirtualHost para departamentos.centro.intranet
```bash
sudo nano /etc/apache2/sites-available/departamentos.centro.intranet.conf
```

Contenido:
```apache
<VirtualHost *:80>
    ServerName departamentos.centro.intranet
    DocumentRoot /var/www/departamentos

    <Directory /var/www/departamentos>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/departamentos_error.log
    CustomLog ${APACHE_LOG_DIR}/departamentos_access.log combined
</VirtualHost>
```

📸 Captura: `capturas/paso1/08-vhost-departamentos.png`

---

### 1.9 Activar los sitios y recargar Apache
```bash
sudo a2ensite centro.intranet.conf
sudo a2ensite departamentos.centro.intranet.conf
sudo a2dissite 000-default.conf
sudo systemctl reload apache2
```

📸 Captura: `capturas/paso1/09-activacion-sitios.png`

---

### 1.10 Comprobación en el navegador
- http://centro.intranet
- http://departamentos.centro.intranet

📸 Captura:  
- `capturas/paso1/10-centro-navegador.png`  
- `capturas/paso1/11-departamentos-navegador.png`

---

## 2. Resultado
Apache queda correctamente instalado y configurado para servir dos dominios internos mediante VirtualHost, quedando listo para los siguientes pasos de la práctica.
