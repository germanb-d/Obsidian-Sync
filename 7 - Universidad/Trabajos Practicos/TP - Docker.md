- **Introducción a los Sistemas Operativos**
- **Germán Beratz Dingebauer**

# Desarrollo Teórico

## 1. Virtualización Vs Contenedores

### Virtualización Tradicional (hipervisores)

* La virtualización tradicional utiliza hipervisores para crear máquinas virtuales (VMs) que emulan completamente una computadora física.
* Existen dos tipos:
  * **Tipo 1 (Bare Metal):** se instala directamente sobre el hardware
  * **Tipo 2 (Hosted):** se instala sobre un sistema operativo existente
* Cada VM necesita su propio sistema operativo completo, lo que implica un mayor consumo de recursos (CPU, RAM, almacenamiento).

### Virtualización a Nivel De Sistema Operativo (Contenedores)

* Los contenedores, como los de Docker, no emulan un hardware completo, sino que comparten el kernel del sistema operativo anfitrión, pero están aislados entre sí.
* Son mucho más ligeros y rápidos que las máquinas virtuales.
* Ideal para despliegues rápidos, pruebas y aplicaciones distribuidas.

![[TP - Docker-1750281482743.webp]]

En la imagen se ve como los VMs son más pesados, más lentos a la hora de iniciar además sé no ser portables. Pero en contraparte, estos persisten mucho más tiempo y están más aisladas.

---

### Ventajas De Los Contenedores

**Mayor eficiencia:** Los contenedores comparten el kernel del sistema operativo host, lo que elimina la necesidad de un sistema operativo invitado completo para cada aplicación. Esto reduce la sobrecarga y permite una mayor densidad de aplicaciones en el mismo hardware.  

**Inicio más rápido:** Debido a que no es necesario iniciar un sistema operativo completo, los contenedores se inician mucho más rápido que las máquinas virtuales.  

**Menor tamaño de imagen:** Las imágenes de contenedores suelen ser mucho más pequeñas que las imágenes de máquinas virtuales, lo que facilita su distribución y almacenamiento.  

**Portabilidad:** Los contenedores están diseñados para ser portátiles, lo que significa que se pueden ejecutar en diferentes entornos (por ejemplo, desde un entorno de desarrollo a un entorno de producción) sin necesidad de modificaciones significativas.  

**Aislamiento:** Aunque comparten el kernel, los contenedores proporcionan un nivel de aislamiento entre las aplicaciones, lo que impide que una aplicación interfiera con otra.

---

## 2. ¿Qué Es Docker? ¿Cuáles Son Sus Componentes Principales?

* **Docker** es una plataforma de contenerización que permite **empaquetar aplicaciones y sus dependencias** en contenedores autocontenidos y portables.
* Es **ligero**, **rápido** y **multiplataforma**, ideal para desarrollo, testing y producción.

### Componentes Principales De Docker:

* **Docker Daemon (dockerd):** Es el proceso que se ejecuta en segundo plano en el host y gestiona los contenedores Docker. Recibe comandos de la Docker CLI (o a través de la API de Docker) y se encarga de construir, ejecutar y administrar los contenedores. Piensa en él como el "motor" de Docker.  
* **Docker Client (Docker CLI):** Es la interfaz de línea de comandos que usas para interactuar con el Docker Daemon. Permite enviar comandos para construir imágenes, ejecutar contenedores, gestionar redes, etc. Es la herramienta con la que el usuario final interactúa.  
* **Docker Images:** Son plantillas de solo lectura que contienen las instrucciones para crear un contenedor. Piensa en ellas como "snapshots" de un sistema de archivos que incluyen el código, las bibliotecas, las dependencias y las herramientas necesarias para ejecutar una aplicación. Las imágenes se construyen a partir de un Dockerfile.  
* **Docker Containers:** Son instancias ejecutables de una Docker Image. Un contenedor contiene todo lo necesario para ejecutar una aplicación: el código, el runtime, las bibliotecas, las variables de entorno y los archivos de configuración. Los contenedores están aislados unos de otros y del sistema host.  
* **Docker Registry:** Es un repositorio para almacenar y compartir Docker Images. El Docker Hub es el registry público más conocido, pero también puedes crear registries privados para almacenar tus propias imágenes.

---

## 3. Respecto a Docker, Defina Y Explique:

### Dockerfile

* Es un archivo de texto con instrucciones para construir una imagen Docker.
* Define el sistema base, qué dependencias instalar, archivos a copiar, comandos a ejecutar, etc.

### Volúmenes

En Docker, los volúmenes son mecanismos para **persistir datos** generados por un contenedor. Por defecto, cuando un contenedor se elimina, todos los datos almacenados dentro de su sistema de archivos también se pierden. Los volúmenes permiten que los datos sobrevivan a la vida útil del contenedor, y también permiten que los datos sean compartidos entre contenedores.

### Redes

* Docker permite la creación de redes virtuales para que los contenedores se comuniquen entre sí o con el exterior.
* Facilita la segmentación, aislamiento y configuración de puertos.

### Docker Compose

* Herramienta que permite definir y administrar múltiples contenedores en un solo archivo.
* Es útil para aplicaciones complejas con múltiples servicios (bases de datos, servidores web, etc.).

# Desarrollo Práctico

## Creación De la Instancia

Se inicia el laboratorio:

![[TP - Docker-1750203547773.webp]]

Y se crea la instancia:

![[TP - Docker-1750203643559.webp|383x245]]

Se configura la nueva instancia en mi caso lo haré con Ubuntu. (el trabajo dice Ubuntu/Debian).

![[TP - Docker-1750203742497.webp]]

---

Los únicos cambios que realice dentro de la configuración de la instancia fue la selección del par de claves vockey, el permitir el tráfico HTTP porque voy a tener que acceder para mostrar el msj posteriormente y la configuración de almacenamiento de 8 a 20.

![[TP - Docker-1750204179475.webp]]

![[TP - Docker-1750204291191.webp]]

![[TP - Docker-1750204356852.webp]]

---

Se creó correctamente y ahora aparece en la sección de instancias:

![[TP - Docker-1750204437881.webp]]

![[TP - Docker-1750204520032.webp]]

## Instalación De Docker

Nos conectamos a la instancia:

![[TP - Docker-1750204652561.webp]]

![[TP - Docker-1750204779362.webp]]

---

Primero se ejecuta `sudo apt update` para actualizar los paquetes

![[TP - Docker-1750204857184.webp]]

---

Se ejecuta `sudo apt install apt-transport-https ca-certificates curl software-properties-common` para instalar las dependencias

![[TP - Docker-1750205028970.webp]]

---

Seguimos ejecutando:

*Agregar clave GPG oficial de Docker*
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`

*Agregar repositorio*
`echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

*Instalar Docker Engine*
`sudo apt update`
`sudo apt install docker-ce docker-ce-cli containerd.io`

![[TP - Docker-1750205654790.webp]]

---

Se ejecuta `sudo docker run hello-world` y se muestra el `Hello from Docker!` por lo cual  se instaló correctamente:

![[TP - Docker-1750206049392.webp]]

## Crear Una Aplicación Web Simple

Crear un directorio para el proyecto:

![[TP - Docker-1750206211948.webp]]

---

> Crear un archivo index.html con el siguiente contenido

(pequeña pausa para buscar como se hacía esto)

Se escribe este comando `nano index.html`para crear el html. A lo cual se muestra la siguiente pantalla:

![[TP - Docker-1750206422557.webp]]

---

En esta pantalla se pega el código, después se guarda y se sale de la pantalla con Ctrl + X

![[TP - Docker-1750206665303.webp]]

![[TP - Docker-1750206697007.webp]]

---

> Crear un archivo Dockerfile (sin extensión) con el siguiente contenido

Mismo proceso que el anterior, se crea con `nano Dockerfile`, se pega el código y se guarda.

![[TP - Docker-1750206887823.webp]]

---

Después al ejecutar `docker build -t my-webapp-iso `.  mostraba el siguiente error

![[TP - Docker-1750207044681.webp]]

Este error sale porque el usuario no tiene permisos para ejecutar comandos de Docker. Al usar `sudo` al principio ya funciono.

![[TP - Docker-1750207172379.webp]]

---

Tanto con `docker run -d -p 8080:80 --name webapp-iso my-webapp-iso` como con `docker ps` tuve los mismos errores, pero se solucionaron usando `sudo`

![[TP - Docker-1750207549592.webp]]

---

> Acceder a la aplicación desde un navegador web en http://<IP pública o nombre de servidor>:8080

(búsqueda para saber como sacaba mi IP pública, se sacaba con `curl ifconfig.me` )

Ejecutar `curl ifconfig.me` y sale:

![[TP - Docker-1750207881917.webp]]

Por lo cual mi IP es 54.172.191.194, entonces entro a http://54.172.191.194:8080.

---

No funciono.

Después de buscar, además de haberlo hablado con el profe en clase, faltaba crear el intervalo de puertos 8080 a la hora de crear la instancia.

Hay que volver a las Instancias y en la instancia actual elegir el apartado de Seguridad

![[TP - Docker-1750208242352.webp]]

En reglas de entrada entramos al grupo por el link

![[TP - Docker-1750208317912.webp]]

![[TP - Docker-1750208340318.webp]]

Hay que editarlo y agregar para ejecutar el puerto 8080

![[TP - Docker-1750208418599.webp]]

---

Ahora si retomando lo anterior:

Por lo cual mi IP es 54.172.191.194, entonces entro a http://54.172.191.194:8080.

![[TP - Docker-1750208469657.webp]]

Funciono.

# Preguntas Finales

## Preguntas

1. ¿Qué ventajas ofrece Docker sobre la virtualización tradicional?
2. Explicar qué hace cada línea del Dockerfile creado
3. ¿Qué ocurre si cambiamos el puerto en el comando docker run (ej: -p 9090:80)?
4. Describir posibles usos profesionales de Docker en el desarrollo de software

## Desarrollo

### 1. ¿Qué Ventajas Ofrece Docker Sobre la Virtualización Tradicional?

**Menor sobrecarga:** Los contenedores Docker comparten el kernel del sistema operativo host, lo que reduce significativamente la sobrecarga en comparación con las máquinas virtuales tradicionales que requieren un sistema operativo completo para cada instancia. Esto significa que Docker utiliza menos recursos (CPU, memoria, almacenamiento) y permite ejecutar más aplicaciones en el mismo hardware.  
  
**Mayor portabilidad:** Las imágenes Docker son portátiles y se pueden ejecutar en cualquier plataforma que admita Docker, lo que facilita la implementación y el despliegue de aplicaciones en diferentes entornos.  
  
**Mayor velocidad:** Los contenedores Docker se inician mucho más rápido que las máquinas virtuales, lo que agiliza el desarrollo, las pruebas y la implementación de aplicaciones.  
  
**Mejor escalabilidad:** La naturaleza ligera de los contenedores Docker permite una escalabilidad más fácil y rápida de las aplicaciones.  

En resumen, Docker ofrece una alternativa más ligera, rápida y portátil a la virtualización tradicional, lo que la convierte en una opción atractiva para el desarrollo y la implementación de aplicaciones modernas.

### 2. Explicación Del Dockerfile Línea Por Línea

```dockerfile
# Usar una imagen base de Nginx
FROM nginx:alpine
```

**FROM**: Define la imagen base. `nginx:alpine` es una versión ligera de Nginx basada en Alpine Linux. Nginx es un software que actúa como intermediario entre los usuarios que visitan un sitio web y los servidores que alojan ese contenido.

```dockerfile
# Copiar nuestro archivo HTML al directorio de Nginx
COPY index.html /usr/share/nginx/html/index.html
```

**COPY**: Copia el [[Archivo]] `index.html` desde tu directorio local al directorio donde Nginx sirve archivos web dentro del contenedor.

```dockerfile
# Exponer el puerto 80
EXPOSE 80
```

**EXPOSE**: Documenta que el contenedor escucha en el puerto 80. Es informativo, no abre el puerto automáticamente. Osea dice: "Este contenedor tiene un servicio corriendo en el puerto 80".

```dockerfile
# Comando para iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]
```

**CMD**: Define el comando que se ejecuta cuando inicia el contenedor. Inicia Nginx en modo foreground (no como daemon).
- **nginx**: Es el comando que inicia el servidor web Nginx.
- **-g**: Es una opción que permite pasar directivas de configuración directamente desde la línea de comandos.
- **"daemon off;"**: Hace que nginx se ejecute en primer plano, mantiene el proceso principal activo y no se desconecta de la terminal Docker necesita que haya un proceso principal corriendo para mantener el contenedor vivo.

### 3. ¿Qué Ocurre Si Cambiamos El Puerto En Docker Run (-p 9090:80)?

Cambiar el puerto en el comando `docker run -p 9090:80` afecta la forma en que accedes al servicio dentro del contenedor desde tu máquina host.

* **`-p 9090:80`**: Esta opción crea un mapeo de puertos. Significa "mapear el puerto 80 dentro del contenedor al puerto 9090 en mi máquina host".  
* **Puerto 80 (dentro del contenedor)**: Este es el puerto en el que el servicio (por ejemplo, un servidor web como Nginx o Apache) está escuchando dentro del contenedor. Es el puerto "interno". El contenedor, en su configuración, está esperando recibir solicitudes en el puerto 80.  
* **Puerto 9090 (en la máquina host)**: Este es el puerto en tu computadora que Docker "escuchará" para redirigir el tráfico al puerto 80 dentro del contenedor. Es el puerto "externo".  
  
**Qué ocurre al cambiarlo:**  

Al cambiar el puerto, por ejemplo, a `docker run -p 8080:80`, entonces:  

1. **Acceso**: Ahora se accede al servicio a través de `localhost:8080` (o `127.0.0.1:8080` si `localhost` no está configurado) en el navegador o usando cualquier herramienta que haga peticiones HTTP. Ya no funcionaría `localhost:9090`.  
2. **Funcionamiento interno**: El contenedor sigue funcionando exactamente igual. El servicio dentro del contenedor sigue escuchando en el puerto 80. Lo que cambia es a través de qué puerto externo accedes a ese puerto 80 interno.  
  
**En resumen:**  

Cambiar el puerto en la parte izquierda de `-p puerto_externo:puerto_interno` modifica el puerto en la máquina host que se utiliza para acceder al servicio que se ejecuta dentro del contenedor. El servicio dentro del contenedor no se ve afectado; sigue escuchando en el puerto que fue configurado para usar.

### 4. Usos Profesionales De Docker En Desarrollo De Software

#### Entornos De Desarrollo Consistentes

Docker elimina el problema de "funciona en mi máquina" al crear entornos idénticos entre desarrolladores. Cada miembro del equipo puede ejecutar exactamente las mismas versiones de dependencias, bases de datos y servicios, sin importar su sistema operativo local.

#### Microservicios Y Arquitecturas Distribuidas

Los contenedores Docker son ideales para implementar arquitecturas de microservicios. Cada servicio puede ejecutarse en su propio contenedor con sus dependencias específicas, facilitando el escalado independiente y el mantenimiento de cada componente.

#### Integración Y Despliegue Continuo (CI/CD)

Docker se integra perfectamente en pipelines de CI/CD. Los contenedores pueden construirse automáticamente, probarse en entornos idénticos a producción y desplegarse de manera consistente a través de diferentes etapas del ciclo de desarrollo.

#### Aislamiento De Aplicaciones

Los contenedores proporcionan aislamiento a nivel de aplicación, permitiendo ejecutar múltiples aplicaciones con diferentes versiones de dependencias en el mismo servidor sin conflictos. Esto es especialmente útil para aplicaciones legacy que requieren versiones específicas de bibliotecas.

#### Escalabilidad Y Orquestación

Docker funciona como base para plataformas de orquestación como Kubernetes, Docker Swarm y Amazon ECS. Esto permite escalar aplicaciones automáticamente según la demanda y gestionar la distribución de cargas de trabajo.

#### Testing Y Quality Assurance

Los contenedores permiten crear entornos de prueba reproducibles. Los equipos de QA pueden ejecutar exactamente la misma versión de la aplicación que será desplegada en producción, eliminando discrepancias entre entornos.

#### Desarrollo De APIs Y Servicios Backend

Docker simplifica el desarrollo de APIs al permitir levantar rápidamente bases de datos, servicios de caché (Redis), message brokers (RabbitMQ) y otros componentes necesarios para el desarrollo backend.

#### Portabilidad Multi-Cloud

Los contenedores Docker pueden ejecutarse en cualquier plataforma que soporte Docker, desde servidores locales hasta servicios cloud como AWS, Google Cloud Platform o Azure, proporcionando verdadera portabilidad.

#### Optimización De Recursos

Docker permite mejor utilización de recursos del servidor al ejecutar múltiples contenedores ligeros en lugar de máquinas virtuales completas, reduciendo overhead y costos operativos.
