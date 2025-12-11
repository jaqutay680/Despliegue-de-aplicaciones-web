# 📘 Activity #2 - Configuración básica de Apache

## 🔧 2.1 Configuración básica de Apache
### 1️⃣ Apache utilizará el puerto 81 además del 80

Editar el archivo:

sudo nano /etc/apache2/ports.conf


Añadir:

Listen 81


Reiniciar Apache:

sudo systemctl restart apache2


Comprobar:

sudo ss -tulnp | grep apache

### 2️⃣ Añadir dominio "marisma.intranet" en /etc/hosts

Editar:

sudo nano /etc/hosts


Añadir:

127.0.0.1   marisma.intranet

### 3️⃣ Cambiar directiva ServerTokens

Editar:

sudo nano /etc/apache2/conf-available/security.conf


Buscar:

ServerTokens


Cambiar por:

ServerTokens ProductOnly


Reiniciar:

sudo systemctl restart apache2

### 4️⃣ Comprobar y modificar ServerSignature

En el mismo archivo:

ServerSignature On


Cambiar a:

ServerSignature Off


Recargar:

sudo systemctl reload apache2


Probar en páginas de error:

http://localhost/noexiste

### 5️⃣ Crear directorios "prueba" y "prueba2" con páginas
sudo mkdir /var/www/prueba
sudo mkdir /var/www/prueba2


Crear archivos:

echo "<h1>Prueba 1</h1>" | sudo tee /var/www/prueba/index.html
echo "<h1>Prueba 2</h1>" | sudo tee /var/www/prueba2/index.html

### 6️⃣ Redirigir carpeta "/prueba" hacia "/prueba2"

Editar el VirtualHost por defecto:

sudo nano /etc/apache2/sites-available/000-default.conf


Añadir dentro de <VirtualHost *:80>:

Redirect /prueba /prueba2


Reiniciar:

sudo systemctl restart apache2

### 7️⃣ Redirigir solo una página

Ejemplo:

Redirect /prueba/pagina.html /prueba2/pagina2.html

### 8️⃣ Activar y usar la directiva UserDir

Activar módulo:

sudo a2enmod userdir
sudo systemctl restart apache2


Crear carpeta pública para usuario:

mkdir ~/public_html
echo "<h1>Página UserDir</h1>" > ~/public_html/index.html


Acceder:

http://localhost/~usuario

### 9️⃣ Usar directiva Alias

Ejemplo:

En /etc/apache2/sites-available/000-default.conf:

Alias /docs /home/usuario/public_html


Reiniciar:

sudo systemctl restart apache2

### 🔟 ¿Para qué sirve Options y cómo desactivar la indexación?

La directiva controla permisos dentro de directorios:

Ejemplos:

Indexes → permite listar contenido

FollowSymLinks

ExecCGI

Includes

Comprobar si Apache indexa directorios:

curl -I http://localhost/prueba


Desactivar indexación:

En 000-default.conf:

<Directory /var/www/>
    Options -Indexes
</Directory>


Reiniciar:

sudo systemctl restart apache2

# 🐚 Activity #2.2 — Scripts Bash

A continuación, los 3 scripts listos para entregar, con sintaxis perfecta.

Inclúyelos en una carpeta /scripts en tu repositorio GitHub.

## 📌 Script 1 — Añadir un puerto de escucha

add_port.sh

#!/bin/bash

if [ "$#" -ne 1 ]; then
    echo "Error: debe especificar el puerto."
    echo "Uso: $0 <puerto>"
    exit 1
fi

PUERTO=$1
ARCHIVO="/etc/apache2/ports.conf"

# Comprobar si el puerto ya existe
grep -q "Listen $PUERTO" $ARCHIVO

if [ $? -eq 0 ]; then
    echo "El puerto $PUERTO ya existe en $ARCHIVO"
else
    echo "Añadiendo puerto $PUERTO..."
    sudo cp $ARCHIVO $ARCHIVO.bak
    echo "Listen $PUERTO" | sudo tee -a $ARCHIVO
    sudo systemctl restart apache2
    echo "Puerto añadido y Apache reiniciado."
fi

## 📌 Script 2 — Añadir dominio a /etc/hosts

add_domain.sh

#!/bin/bash

if [ "$#" -ne 2 ]; then
    echo "Error: parámetros insuficientes."
    echo "Uso: $0 <ip> <dominio>"
    exit 1
fi

IP=$1
DOM=$2

ARCHIVO="/etc/hosts"

# Comprobar si el dominio ya existe
grep -q "$DOM" $ARCHIVO

if [ $? -eq 0 ]; then
    echo "El dominio '$DOM' ya está en $ARCHIVO"
else
    echo "Añadiendo dominio..."
    echo "$IP $DOM" | sudo tee -a $ARCHIVO
    echo "Dominio añadido correctamente."
fi

## 📌 Script 3 — Crear una página web sencilla

create_page.sh

#!/bin/bash

if [ "$#" -ne 3 ]; then
    echo "Error: parámetros incorrectos."
    echo "Uso: $0 <archivo> <titulo> <mensaje>"
    exit 1
fi

ARCHIVO=$1
TITULO=$2
MENSAJE=$3

echo "Creando página en $ARCHIVO..."

cat <<EOF | sudo tee $ARCHIVO
<html>
<head>
<title>$TITULO</title>
</head>
<body>
<h1>$TITULO</h1>
<p>$MENSAJE</p>
</body>
</html>
EOF

echo "Página creada con éxito."
