# Cosas Q no Vi

- Microcontroladores

# SBC - Single Board Computer

Acá se encuentra las rasberry

- Tiene SO - Linux/Android/etc.
- Bajo costo
- Bajo consumo de energía
- Se puede expandir con módulos
- Una mini computadora
Rasperry PI Model B+

## Usos

Nodo Edge

Puesto de interacción con usuarios

Redes de sensores

Puesto de trabajo simples

### Beacons

Manda señales que son tomadas por un telefono y poder determinar su ubicacion y se comunique, entre el mocrocontrolador y el dispositivo movil. Podemos ubicar un telefono en un edificio. Manda UID y la detecta con una aplicacion/web movil.

# Redes De Sensores

Nodo Sensor: uno o mas sensores. Recolecta y transmite datos.

- Un microcontrolador
- Sensores
	- Temperatura, humedad, distancia, RFID, Enconders, Presencia, etc.
- Módulos de alimentación
- Módulo de comunicación
	- Alámbricas: usualmente usada en la industria para maximizar la mínima la perdida de información.
	- Inalámbricas
	- Mixtas
- Actuadores
	- Motores continuos
	- Servomotores
	- Buzzers
	- Valvulas
	- Etc
- 

Red de Comunicación: Red que une los sensores

Gateway: Nodo recolector/ el nodo principal que recibe los datos y devolver una accion o mandarlos a otro servicio.

Red de sensor ≠ wifi

- No siempre es pública

Diferencia entre usar LoRa a seco o un GetWay #Buscar

## Protocolos

### ESP

Se comunica directamente entre ellos sin un servidor

### HTTP

### MQTT

# 8/10

## IoT

### Internet De Las Cosas IoT

Es un paradigma que se refiere a la interconexión de objetos cotidianos a internet.

### Internet Industriales De Las Cosas IIoT

Es un subconjunto dentro de IoT especificado en la automatización y mejora de la eficiencia en la industria.

## Arquitectura Distribuida

### Cloud Computing

Vas del internet a la nube. Depender totalmente del cloud, genera cuellos de botella y alots costos.

### Edge Y Fog Computing

El objetivo no es sustituir el computo en la nube, sino complementarlo, proover niveles adicionales capaces de complementarlo.

Ayuda a solucionar problemas como:

- .
- .
- .

#### Fog Computing

Acercar los servicios a los nodos. Haria un preposesacmiento de los datos.

Internet (cloud computing)

Fog (Fog node/capa intermedia)

Nodo Final (end device)

Sigue estando dentro de internet pero en redes más cercanas a nuestros nodos finales.

#### Edge Computing

Conexiones en routers, gateway y/o servidores.

- Validacion de nodos / gestion de redes
- Procesamiento
- Seguridad
- Bases de datos
- Plataformas
- Visualizacion

 El objetivo es reducir la latencia y el ancho de banda, procesando los datos más cerca de la fuente.

Cloud Computing (internet)

Fog Computing (fog node) (sigue dentro de internet)

Edge Computing (edge node)

End Device (end devices)

#### End Device

Nodo sensor, dispositivo movil, robot, drones, etc

Esta compuesto por :

## Plataformas Y Servicios

Que podemos trasladar a capas mas cercanas?

(Todo lo de la diapositiva)

## Aplicaciones Y Resilencia

### Computo Heterogeneo

Planificacion: Algoritmo o servicios que me permitan mejorar la distribucion de la carga.

Pre Procesar: Intento que a la nube solo lleguen los datos finales o que menos procesamiento requieran.

### Computo Redundante

Buscamos que distintos nodos de distintas capas sean capaces de procesar y resolver una misma tarea. Así, ante cualquier fallo se prevé tener una estrategia para intentar siempre tener respuesta en mi arquitectura. Pruebo de hacer un Machine Learning en un nodo final, que aunque su objetivo no es hacer eso porque lo voy a derivar a otro nodo, debo saber si es capaz de procesarlo en caso de cualquier error.

## Nodos De Control

Node RED : Capa Edge

Thinger. Io: Capa fog - daba un dashboard

Usuario: pi

Contraseña: raspberry

Sudo raspi-config

- SSID
	- Wifilora
	- 12345678
- Enable SSH

IP: 192.168.1.110

IP: 192.168.1.113

# 9/10

- Thinger. Io
	- Open Source
	- Conexion Sencilla
	- Muchas integraciones nativas
	- APIs REST y MQTT
	- Data Buckets para alacenamiento
	- Rules Engine
- Thingsboard
- Home Assistant
- Kaa Project (Open Source parecido a Hombe assistant)

Servicios:

- Visualizacion: Grafana
- Motores de bases de datos: InfluxDB, Postgresql, Cassandra
- APIs
- .....

ESP 32 con el protocolo IOTMP

Codigo python:

Usuario

URL

Generar temperatura ramdom

Enviar datos al dispositivo de thiger. Io

Ciclo principal del programa

Credencial de ESP 32: D4hMBCVpKHGJ16@K

Usar Commmunity Edition de manera local

# 10/10

Thing Board

Lenguaje de Java VHL ?

## Edge Computing

<10 ms de Latencia

Ejemplo:

- Hacer el procesamiento en un auto Tesla.
- Control de insulina en un dispositivo inter body.

**Futuro**: Continum Cloud - Edge Hibrido
- El entrenamiento de una IA es en el cloud y su uso en el edge.

Deberiamos elegir el hardware en base al software y no al revez

Instalar Docker, Docker Compose no se

`docker images `

`docker ps -a`

Usar una virtual box con ubuntu

Virtual micro machine - Contenedores de sistemas

El docker es contenedor de aplicacion.

Diferencias?

Cubernetes?

Mini cube es un cubernete para una unica maquina

Python - Node. Js - manejo de bases de datos.

Mandandole la imagen del contenedor al cliente sin preocuparte de que sistema tiene el cliente.

Federal edge? Es un tipo de computación distribuida donde múltiples nodos de borde colaboran para procesar datos, a menudo manteniendo la privacidad y la soberanía de los datos. Agrupamos los servidores y se toman como un conjunto.

Al tener los edge federados, un colectivo autonomo va cambiando por los repetidores de los distintos edge.
