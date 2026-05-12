# 🐳 Activity #3 - Imágenes y contenedores Docker

## 📝 Descripción

Esta actividad cubre la **gestión de imágenes Docker** y la **creación, manipulación y eliminación de contenedores** con nombres personalizados.

**Objetivo:** Dominar los comandos para descargar imágenes, ejecutar contenedores con nombres específicos, y limpiar recursos de forma ordenada.

---

## 📚 Recursos

- [Pull docker images & run docker containers](http://www.servermom.org/pull-docker-images-run-docker-containers/3225/)
- [Remove Docker images, containers and volumes](https://www.tecmint.com/remove-docker-images-containers-and-volumes/)
- [Name Docker containers](https://www.tecmint.com/name-docker-containers/)
- [Play with Docker - Interactive](https://training.play-with-docker.com/ops-s1-hello/)

---

## 🎯 Conceptos clave

### Imagen Docker
Una **plantilla inmutable** que contiene todo lo necesario para ejecutar una aplicación (código, dependencias, variables de entorno, etc.).

### Contenedor Docker
Una **instancia en ejecución** de una imagen Docker. Es un proceso aislado y ligero que se crea a partir de una imagen.

### Registro Docker
Un repositorio centralizado (ej: Docker Hub) donde se almacenan y distribuyen imágenes públicas y privadas.

### Nombre de contenedor
Un identificador legible que se asigna a un contenedor para distinguirlo de otros. Más fácil que usar el ID hexadecimal.

---

## 🛠️ Las 13 tareas prácticas

### TAREA 1️⃣: Descargar la imagen de Ubuntu

```bash
docker pull ubuntu
```

**Explicación:** Descarga la imagen más reciente de Ubuntu desde Docker Hub.

**Resultado esperado:**
```
Using default tag: latest
latest: Pulling from library/ubuntu
Pulling fs layer...
...
Status: Downloaded newer image for ubuntu:latest
```

![Descarga de imagen Ubuntu](images/pull-ubuntu.png)

---

### TAREA 2️⃣: Descargar la imagen de hello-world

```bash
docker pull hello-world
```

**Explicación:** Descarga la imagen hello-world (pequeña y útil para pruebas).

**Resultado esperado:**
```
Using default tag: latest
latest: Pulling from library/hello-world
...
Status: Downloaded newer image for hello-world:latest
```

---

### TAREA 3️⃣: Descargar la imagen de Nginx

```bash
docker pull nginx
```

**Explicación:** Descarga la imagen nginx (servidor web).

**Resultado esperado:**
```
Using default tag: latest
latest: Pulling from library/library/nginx
...
Status: Downloaded newer image for nginx:latest
```

---

## 📸 **CAPTURA 1: `pull-ubuntu.png`**

Ejecuta:
```bash
docker pull ubuntu
```

Captura desde el comando hasta el "Status: Downloaded".

---

## 📸 **CAPTURA 2: `pull-images.png`**

Ejecuta:
```bash
docker pull hello-world && docker pull nginx
```

Captura ambas descargas.

---

### TAREA 4️⃣: Mostrar un listado de todas las imágenes

```bash
docker images
```

**Explicación:** Muestra todas las imágenes descargadas localmente con sus tamaños e IDs.

**Resultado esperado:**
```
REPOSITORY    TAG       IMAGE ID      CREATED       SIZE
ubuntu        latest    e43e20a0b...  2 weeks ago   77.8MB
hello-world   latest    d2c94e258...  13 months ago 13.3kB
nginx         latest    a1be4ac8e...  2 weeks ago   187MB
```

---

## 📸 **CAPTURA 3: `docker-images-list.png`**

Ejecuta:
```bash
docker images
```

Captura la tabla completa con todas las imágenes (ubuntu, hello-world, nginx).

---

### TAREA 5️⃣: Ejecutar un contenedor hello-world y darle nombre "myhello1"

```bash
docker run --name myhello1 hello-world
```

**Explicación:** 
- `docker run`: Crea y ejecuta un contenedor
- `--name myhello1`: Asigna nombre al contenedor
- `hello-world`: Imagen a utilizar

**Resultado esperado:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

---

### TAREA 6️⃣: Ejecutar un contenedor hello-world y darle nombre "myhello2"

```bash
docker run --name myhello2 hello-world
```

**Explicación:** Crea un segundo contenedor hello-world con nombre diferente.

**Resultado esperado:** Mismo mensaje de bienvenida.

---

### TAREA 7️⃣: Ejecutar un contenedor hello-world y darle nombre "myhello3"

```bash
docker run --name myhello3 hello-world
```

**Explicación:** Crea un tercer contenedor hello-world con nombre diferente.

**Resultado esperado:** Mismo mensaje de bienvenida.

---

## 📸 **CAPTURA 4: `hello-three-containers.png`**

Ejecuta:
```bash
docker run --name myhello1 hello-world && docker run --name myhello2 hello-world && docker run --name myhello3 hello-world
```

Captura los tres mensajes de bienvenida ejecutándose en secuencia.

---

### TAREA 8️⃣: Mostrar los contenedores que se están ejecutando

```bash
docker ps
```

**Explicación:** Muestra los contenedores que están ACTUALMENTE corriendo.

**Resultado esperado:**
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS   NAMES
```

(Tabla vacía porque los contenedores hello-world terminan inmediatamente)

---

## 📸 **CAPTURA 5: `docker-ps-empty.png`**

Ejecuta:
```bash
docker ps
```

Captura la tabla vacía (confirmando que no hay contenedores activos).

---

### TAREA 9️⃣: Parar el contenedor "myhello1"

```bash
docker stop myhello1
```

**Explicación:** Detiene la ejecución del contenedor (nota: ya estaba parado, pero docker lo reconoce por nombre).

**Resultado esperado:**
```
myhello1
```

---

### TAREA 🔟: Parar el contenedor "myhello2"

```bash
docker stop myhello2
```

**Explicación:** Detiene el contenedor myhello2.

**Resultado esperado:**
```
myhello2
```

---

## 📸 **CAPTURA 6: `docker-stop-containers.png`**

Ejecuta:
```bash
docker stop myhello1 && docker stop myhello2
```

Captura los nombres (myhello1 y myhello2) confirmando que se detuvieron.

---

### TAREA 1️⃣1️⃣: Borrar el contenedor "myhello1"

```bash
docker rm myhello1
```

**Explicación:** Elimina completamente el contenedor myhello1 (no puede recuperarse).

**Resultado esperado:**
```
myhello1
```

---

## 📸 **CAPTURA 7: `docker-rm-container.png`**

Ejecuta:
```bash
docker rm myhello1
```

Captura el nombre "myhello1" confirmando que se eliminó.

---

### TAREA 1️⃣2️⃣: Mostrar los contenedores que se están ejecutando (después de eliminar)

```bash
docker ps -a
```

**Explicación:** Muestra TODOS los contenedores (activos y detenidos). Note que myhello1 ya no aparece.

**Resultado esperado:**
```
CONTAINER ID   IMAGE         COMMAND    CREATED      STATUS
def456...      hello-world   "/hello"   2 mins ago   Exited (0)   myhello2
ghi789...      hello-world   "/hello"   2 mins ago   Exited (0)   myhello3
```

(myhello1 no aparece porque fue eliminado)

---

## 📸 **CAPTURA 8: `docker-ps-after-rm.png`**

Ejecuta:
```bash
docker ps -a
```

Captura la tabla mostrando myhello2 y myhello3, pero SIN myhello1.

---

### TAREA 1️⃣3️⃣: Borrar todos los contenedores

```bash
docker rm myhello2 myhello3
```

**Explicación:** Elimina múltiples contenedores en un comando.

**Resultado esperado:**
```
myhello2
myhello3
```

Alternativamente, podrías usar:
```bash
docker container prune -f
```

(Elimina todos los contenedores detenidos sin preguntar)

---

## 📸 **CAPTURA 9: `docker-rm-all.png`**

Ejecuta:
```bash
docker rm myhello2 myhello3
```

Captura los dos nombres (myhello2 y myhello3) confirmando eliminación.

---

### VERIFICACIÓN FINAL: Ver estado final

```bash
docker ps -a
```

**Explicación:** Verifica que todos los contenedores han sido eliminados.

**Resultado esperado:**
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS   NAMES
```

(Tabla completamente vacía)

---

## 📸 **CAPTURA 10: `docker-ps-final-empty.png`**

Ejecuta:
```bash
docker ps -a
```

Captura la tabla completamente vacía (confirmando que todo se eliminó).

---

## 📊 Ciclo completo de una imagen

```
┌─────────────────────────────────────┐
│     Docker Hub (Repositorio)        │
└──────────────┬──────────────────────┘
               │
               │ docker pull
               ▼
┌─────────────────────────────────────┐
│   Imagen local (almacenada)         │
└──────────────┬──────────────────────┘
               │
               │ docker run
               ▼
┌─────────────────────────────────────┐
│   Contenedor en ejecución           │
└──────────────┬──────────────────────┘
               │
               │ docker stop
               ▼
┌─────────────────────────────────────┐
│   Contenedor detenido               │
└──────────────┬──────────────────────┘
               │
               │ docker rm
               ▼
┌─────────────────────────────────────┐
│   Contenedor eliminado              │
└─────────────────────────────────────┘
```

---

## 📋 Tabla de referencia de comandos

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `docker pull` | Descargar imagen | `docker pull ubuntu` |
| `docker images` | Listar imágenes locales | `docker images` |
| `docker search` | Buscar imágenes en Hub | `docker search nginx` |
| `docker run` | Crear y ejecutar contenedor | `docker run ubuntu` |
| `docker run --name` | Asignar nombre al contenedor | `docker run --name web nginx` |
| `docker ps` | Listar contenedores activos | `docker ps` |
| `docker ps -a` | Listar todos los contenedores | `docker ps -a` |
| `docker stop` | Detener contenedor | `docker stop web` |
| `docker start` | Iniciar contenedor detenido | `docker start web` |
| `docker rm` | Eliminar contenedor | `docker rm web` |
| `docker rmi` | Eliminar imagen | `docker rmi ubuntu` |
| `docker inspect` | Ver detalles | `docker inspect web` |
| `docker logs` | Ver logs del contenedor | `docker logs web` |

---

## 💡 Buenas prácticas

### 1. Usar nombres descriptivos para contenedores
```bash
# ❌ Malo - nombre genérico
docker run --name app1 nginx

# ✅ Bien - nombre descriptivo
docker run --name webserver nginx
```

### 2. Especificar versión de imagen
```bash
# ❌ Malo - usa latest (impredecible)
docker pull ubuntu

# ✅ Bien - versión específica
docker pull ubuntu:22.04
```

### 3. Limpiar recursos regularmente
```bash
# Eliminar contenedores no utilizados
docker container prune -f

# Eliminar imágenes no utilizadas
docker image prune -f

# Eliminar todo (contenedores + imágenes no utilizadas)
docker system prune -a
```

### 4. Usar -a con docker ps para ver todo
```bash
# ❌ Malo - solo ve activos
docker ps

# ✅ Bien - ve todos
docker ps -a
```

### 5. Documentar contenedores con nombres
```bash
# ❌ Difícil de rastrear
docker run -d abc123def456

# ✅ Fácil de identificar
docker run -d --name my-database mysql
```

---

## 🔍 Troubleshooting

### Error: "Error response from daemon: Conflict. The container name already in use"

**Problema:** El nombre ya existe.

```bash
# Ver si existe
docker ps -a | grep nombre

# Eliminar el contenedor anterior
docker rm nombre

# Crear el nuevo
docker run --name nombre imagen
```

---

### Error: "Error response from daemon: No such image"

**Problema:** La imagen no existe localmente.

```bash
# Descargar la imagen primero
docker pull ubuntu

# Luego ejecutar
docker run --name test ubuntu
```

---

### Error: "Cannot remove a running container"

**Problema:** Intentas eliminar un contenedor que está corriendo.

```bash
# Detenerlo primero
docker stop nombre

# Luego eliminarlo
docker rm nombre

# O forzar eliminación (no recomendado)
docker rm -f nombre
```

---

## 🎯 Tareas completadas

- ✅ Descargar imágenes desde Docker Hub (ubuntu, hello-world, nginx)
- ✅ Listar imágenes locales
- ✅ Crear múltiples contenedores con nombres personalizados
- ✅ Entender que hello-world termina inmediatamente
- ✅ Usar docker ps para ver contenedores activos
- ✅ Usar docker ps -a para ver todos los contenedores
- ✅ Detener contenedores por nombre
- ✅ Eliminar contenedores individuales
- ✅ Eliminar múltiples contenedores en un comando
- ✅ Limpiar completamente los recursos

---

## 📊 Resumen de lo aprendido

| Concepto | Comando | Función |
|----------|---------|---------|
| **Descarga** | `docker pull` | Obtener imagen de Hub |
| **Listar** | `docker images` | Ver imágenes locales |
| **Crear** | `docker run` | Crear contenedor |
| **Nombrar** | `--name` | Asignar identificador |
| **Listar activos** | `docker ps` | Ver contenedores en ejecución |
| **Listar todos** | `docker ps -a` | Ver todos (activos y parados) |
| **Parar** | `docker stop` | Detener contenedor |
| **Eliminar** | `docker rm` | Borrar contenedor |

---

## 📸 Capturas de pantalla incluidas

1. ✅ `pull-ubuntu.png` - Descarga de imagen Ubuntu
2. ✅ `pull-images.png` - Descarga de hello-world y Nginx
3. ✅ `docker-images-list.png` - Listado de todas las imágenes
4. ✅ `hello-three-containers.png` - Ejecución de 3 hello-world
5. ✅ `docker-ps-empty.png` - docker ps mostrando tabla vacía
6. ✅ `docker-stop-containers.png` - Parada de contenedores
7. ✅ `docker-rm-container.png` - Eliminación de myhello1
8. ✅ `docker-ps-after-rm.png` - docker ps -a sin myhello1
9. ✅ `docker-rm-all.png` - Eliminación de myhello2 y myhello3
10. ✅ `docker-ps-final-empty.png` - docker ps -a completamente vacío

---

## 📝 Resumen de comandos ejecutados

```bash
# TAREAS 1-3: Descargar imágenes
docker pull ubuntu
docker pull hello-world
docker pull nginx

# TAREA 4: Ver imágenes descargadas
docker images

# TAREAS 5-7: Crear 3 contenedores hello-world
docker run --name myhello1 hello-world
docker run --name myhello2 hello-world
docker run --name myhello3 hello-world

# TAREA 8: Ver contenedores activos
docker ps

# TAREAS 9-10: Parar contenedores
docker stop myhello1
docker stop myhello2

# TAREA 11: Eliminar un contenedor
docker rm myhello1

# TAREA 12: Ver contenedores después de eliminar
docker ps -a

# TAREA 13: Eliminar todos los contenedores restantes
docker rm myhello2 myhello3

# VERIFICACIÓN FINAL
docker ps -a
docker images
```

---

## 🔗 Referencias

- [Docker Images Documentation](https://docs.docker.com/engine/reference/commandline/image/)
- [Docker Run Reference](https://docs.docker.com/engine/reference/commandline/run/)
- [Docker RM Documentation](https://docs.docker.com/engine/reference/commandline/rm/)
- [Docker RMI Documentation](https://docs.docker.com/engine/reference/commandline/rmi/)
- [Docker PS Documentation](https://docs.docker.com/engine/reference/commandline/ps/)

---

## 📚 Próximos pasos

Una vez completada esta actividad:

1. ✅ Activity #1: Instalación (Completada)
2. ✅ Activity #2: Introducción a contenedores (Completada)
3. ✅ Activity #3: Imágenes y contenedores (AQUÍ ESTAMOS)
4. 🔜 **Activity #4:** Almacenamiento y redes
5. 🔜 **Activity #5:** Docker Compose
6. 🔜 **Activity #6:** Creación de imágenes

→ Continúa con **[Activity #4 - Almacenamiento y redes](../activity4-almacenamiento-redes/README.md)**

---

## 🎓 Evaluación

**Criterios de éxito para Activity #3:**

- ✅ Las 3 imágenes descargadas (ubuntu, hello-world, nginx)
- ✅ `docker images` muestra al menos 3 imágenes
- ✅ 3 contenedores hello-world creados con nombres
- ✅ Contenedores detenidos correctamente
- ✅ Contenedores eliminados correctamente
- ✅ docker ps -a final está vacío
- ✅ 10 capturas de pantalla tomadas

---

**Autor:** José Ángel Aquino Tayllefert  
**Fecha:** Curso 2025/26  
**Estado:** ✅ Completado

---

<div align="center">

**¡Felicidades! Has dominado la gestión de imágenes y contenedores Docker 🎉**

**[⬆ Volver arriba](#-activity-3---imágenes-y-contenedores-docker)**

</div>
