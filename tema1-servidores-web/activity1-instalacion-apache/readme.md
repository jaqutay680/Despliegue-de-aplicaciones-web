# 📘 Instalación y Configuración Básica de Apache en Ubuntu

Este documento explica paso a paso cómo instalar, verificar y gestionar el servidor web Apache2 en Ubuntu. Incluye comandos, explicaciones y secciones donde puedes colocar tus capturas de pantalla.

## 🔧 1. Actualizar repositorios

Antes de instalar cualquier paquete, es recomendable actualizar la lista de repositorios y los paquetes del sistema.

sudo apt update
sudo apt upgrade -y


📸 Captura 1 (opcional): Salida del comando apt update.

## 🌐 2. Instalar Apache2
sudo apt install apache2 -y


📸 Captura 2: Instalación completa de Apache en la terminal.

## 🚀 3. Comprobar el estado del servicio Apache
sudo systemctl status apache2


El estado debe aparecer como:

active (running)


📸 Captura 3: Salida del servicio mostrando que Apache está activo.

## 🌍 4. Probar funcionamiento en el navegador

Para verificar que Apache está sirviendo contenido, abre:

http://localhost


O consulta tu IP local:

hostname -I


📸 Captura 4: Página por defecto de Apache en el navegador.

## 🧭 5. Directorio raíz del servidor web

El contenido que Apache sirve por defecto se encuentra en:

/var/www/html/


Archivo principal:

index.html


📸 Captura 5: Vista del directorio /var/www/html/.

## ⚙️ 6. Archivos de configuración principales

Configuración global de Apache:

/etc/apache2/apache2.conf


Sitios disponibles:

/etc/apache2/sites-available/


Archivo del sitio por defecto:

000-default.conf


📸 Captura 6: Contenido del directorio sites-available.

## 🔥 7. Comandos de gestión de Apache
▶️ Iniciar Apache
sudo systemctl start apache2

⏸️ Detener Apache
sudo systemctl stop apache2

🔄 Reiniciar Apache
sudo systemctl restart apache2


📸 Captura 7 (opcional): Ejemplo usando uno de los comandos.

## 🔒 8. Configurar Firewall (UFW) (solo si lo tienes activo)

Permitir tráfico HTTP:

sudo ufw allow 'Apache'


Comprobar estado:

sudo ufw status


📸 Captura 8: Firewall mostrando Apache permitido.

## 📡 9. Verificar puertos activos de Apache
sudo ss -tulnp | grep apache


📸 Captura 9: Puertos abiertos (normalmente el 80).

## 🧹 10. Desinstalar Apache (opcional)
sudo apt remove apache2 -y
sudo apt purge apache2 -y
sudo apt autoremove -y
