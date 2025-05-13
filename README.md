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






