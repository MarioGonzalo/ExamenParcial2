Link al repositorio: https://github.com/MarioGonzalo/ExamenParcial2.git

# Examen Final de Redes II: La Restauración de la HoloRed Galáctica

## Parte I – Misiones de Conocimiento Teórico (60%)

### Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

Partiendo de la dirección 172.16.0.0/24 tendremos que dividirla en 4 secciones capaces de albergar:

Comando Central: ~50 hosts (dispositivos)

Defensa Perimetral: ~30 hosts

Centro Médico: ~20 hosts

Hangar y Taller: ~14 hosts

Para poder albergar el número de hosts suficientes tenemos que reservar espacio igual o mayor al número de hosts que se requiere en cada zona en potencias de 2, quitando un host para red y otro para broadcast.

---

#### Comando central

Para el comando central reservaremos 62 direcciones de hosts (64-2) ya que 30 (32-2) no son suficientes para albergar los 50 hosts por lo que sus direcciones serían:

- Dirección de red: 172.16.0.0/26

- Rango de hosts: 172.16.0.1 – 172.16.0.62

- Broadcast: 172.16.0.63

---

#### Defensa perimetral

Para la defensa perimetral necesitaremos 30 hosts (32-2) por lo que sus direcciones serían:

- Dirección de red: 172.16.0.64/27

- Rango de hosts: 172.16.0.65 – 172.16.0.94

- Broadcast: 172.16.0.95

---

#### Centro médico

Para el centro médico reservaremos 30 direcciones de hosts (32-2) ya que 14 (16-2) no son suficientes para albergar los 20 hosts por lo que sus direcciones serían:

- Dirección de red: 172.16.0.96/27

- Rango de hosts: 172.16.0.97 – 172.16.0.126

- Broadcast: 172.16.0.127

---

#### Hangar y taller

Para el hangar y el taller tenemos que reservar 14 direcciones de hosts, lo que da suficiente con /28 (16-2 direcciones de host) por lo que sus direcciones serían:

- Dirección de red: 172.16.0.128/28

- Rango de hosts: 172.16.0.129 – 172.16.0.142

- Broadcast: 172.16.0.143

---

#### Enlace troncal

Por último para la antena de comunicaciones reservaremos únicamente dos direcciones de host para dos dispositivos de enlace troncal que necesitemos conectar por lo que sus direcciones serían:

- Dirección de red: 172.16.0.144/30

- Rango de hosts: 172.16.0.145 – 172.16.0.146

- Broadcast: 172.16.0.147

---

Hemos usado hasta 172.16.0.147, por lo que aún quedan direcciones libres entre 172.16.0.148 y 172.16.0.255 para futuras expansiones o reserva.

### Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas

#### Enrutamiento Estático

En el enrutamiento estático se definen manualmente las rutas de cada router

##### Ventajas:
- Simplicidad: Fácil de entender e implementar en redes pequeñas.
- Menor carga del router: No requiere procesamiento de protocolos de enrutamiento.
- Mayor control: Ideal para rutas específicas o políticas de seguridad estrictas.

##### Inconvenientes:
- No se adapta a cambios: Si una ruta falla, no hay ajuste automático.
- Escalabilidad limitada: Difícil de administrar en redes grandes.
- Alto mantenimiento: Cambios en la red requieren intervención manual.

---

#### Enrutamiento Dinámico

Los routers intercambian información automáticamente usando protocolos de enrutamiento para construir y actualizar sus tablas de rutas.

##### Ventajas:
- Adaptabilidad: Ajuste automático ante fallos o cambios en la red.
- Escalabilidad: Adecuado para redes grandes y complejas.
- Menor intervención manual: Disminuye la carga operativa.

##### Inconvenientes:
- Mayor uso de recursos: Más procesamiento, memoria y ancho de banda.
- Complejidad: Configuración y depuración más complejas.
- Posible inestabilidad: Configuraciones incorrectas pueden causar bucles o inconsistencias.


**Ejemplo de protocolo dinámico:**  
- RIP (Routing Information Protocol): protocolo de *vector de distancia* que usa el número de saltos para calcular la ruta más corta.

#### Diferencia entre vector de distancia y estado de enlace

Los protocolos de vector de distancia (como por ejemplo RIP), emplean un conteo de saltos para hallar la mejor ruta, similar a el protocolo de búsqueda por inundación mientras que los protocolos de estado de enlace (como por ejemplo OSPF) determinan la ruta más corta y eficiente mediante Djikstra.

### Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

#### ¿Qué es el DNS?

El **DNS (Domain Name System)** es el sistema que se encarga de traducir nombres de dominio (como holonet.rebelion.org) en direcciones IP (como 192.0.2.42) que las computadoras pueden entender. Este sistema es esencial para la comunicación en redes basadas en TCP/IP, ya que los dispositivos realmente se comunican usando direcciones IP, no nombres legibles para humanos.

---

#### ¿Cómo funciona la resolución de nombres?

Cuando un equipo de la **red rebelde** (o cualquier otra red TCP/IP) quiere comunicarse con un servidor usando su nombre (por ejemplo, holonet.rebelion.org), sigue estos pasos:

1. **El dispositivo (cliente)** consulta su caché local
2. Si no está en caché, **envía una consulta DNS** a su **servidor DNS configurado** (normalmente uno proporcionado por el router o la red local).
3. El **servidor DNS** consulta a otros servidores si no tiene la respuesta:
   - Primero al **servidor raíz**, luego al **servidor TLD** (.org), y finalmente al **servidor autoritativo** para rebelion.org.
4. El **servidor autoritativo** responde con un **registro A** (Address Record), que contiene la dirección IP asociada al nombre.
5. El cliente recibe la IP y establece la comunicación con el servidor usando la dirección IP obtenida.

---

#### ¿Qué es un servidor DNS?

Un **servidor DNS** es un equipo que almacena una **base de datos jerárquica** de nombres de dominio y sus direcciones IP correspondientes. Puede ser:

- **Recurrente**: consulta a otros servidores si no tiene la respuesta.
- **Autoritativo**: tiene la respuesta definitiva para un dominio específico.

---

#### ¿Qué es un registro DNS?
Un registro DNS es una entrada en la base de datos del sistema de nombres de dominio (DNS) que asocia un nombre de dominio con algún tipo de información. Hay distintos tipos de registros, según la función que cumplan.

---

#### ¿Qué es un registro A?
Un registro A (de “Address”) es un tipo específico de registro DNS. Asocia un nombre de dominio con una dirección IPv4.

---

#### Ejemplo: Resolución de nombre en la red de la Alianza
Supongamos que un piloto rebelde quiere acceder al sistema de inteligencia en holonet.rebelion.org.

1. El ordenador del piloto necesita saber la IP de holonet.rebelion.org para conectarse.

2. Envía una consulta al servidor DNS configurado (por ejemplo, dns.rebelion.org).

3. El servidor DNS busca un registro A para ese dominio (Por ejemplo 192.0.2.42).

4. El servidor DNS responde al ordenador del piloto con esa IP.

5. El dispositivo ya puede establecer conexión directa con el servidor de la Holonet en 192.0.2.42.

---

#### ¿Qué pasa si el servidor DNS no está disponible?
Si el servidor DNS está caído o inaccesible, los dispositivos de la red no podrán resolver nombres de dominio. Es decir:

- Al intentar acceder a holonet.rebelion.org, no se podrá obtener la IP correspondiente.

- Como resultado, no se establecerá la comunicación, incluso si el servidor de destino sigue funcionando.

### Misión 4: “Es una trampa… de protocolos!” – TCP vs UDP en las transmisiones

#### TCP (Transmission Control Protocol)

##### Características clave

- **Confiable**: garantiza la entrega de los datos completos y sin errores.
- **Orientado a conexión**: antes de enviar datos, establece una conexión entre emisor y receptor (three-way handshake).
- **Ordenado**: los paquetes llegan en el mismo orden en que fueron enviados.
- **Control de flujo y congestión**: ajusta la velocidad según la capacidad de la red y del receptor.
- **Mayor sobrecarga**: introduce más latencia y consumo de recursos debido a sus mecanismos de control.

##### ¿Por qué es confiable?

TCP incluye:
- Verificación de errores (checksum).
- Reenvío de paquetes perdidos (retransmisión).
- Confirmación de recepción (ACKs).
- Reensamblado en orden correcto.

##### Implicaciones en rendimiento

- **Más lento** que UDP debido a su complejidad.
- Ideal cuando **la integridad de los datos es prioritaria**, no la velocidad.

##### Ejemplos en la Alianza Rebelde

- **Transmisión de planes estratégicos cifrados** desde el Comando Central.
- **Actualizaciones de software** en los droides de combate.
- **Comunicaciones seguras** entre bases rebeldes.

---

#### UDP (User Datagram Protocol)

##### Características clave

- **No confiable**: no garantiza entrega, orden ni corrección de errores.
- **Sin conexión**: no requiere handshake previo.
- **Menor sobrecarga**: envía paquetes directamente, sin controles adicionales.
- **Más rápido**: baja latencia, ideal para comunicaciones en tiempo real.

##### ¿Por qué se considera no confiable?

- No espera confirmación de recepción.
- No reenvía paquetes perdidos.
- No ordena los datos.
- No gestiona el flujo.

##### ¿Por qué usarlo entonces?

Cuando es **más importante la velocidad que la precisión**, como en:
- Transmisiones en tiempo real.
- Comunicaciones donde perder algunos datos es tolerable.

##### Ejemplos en la Alianza Rebelde

- **Coordenadas de combate en tiempo real** entre pilotos en medio de una batalla.
- **Vídeo en directo desde sondas** que envían imágenes desde sistemas hostiles.
- **Mensajes de estado rápidos** entre naves en formación.

---















