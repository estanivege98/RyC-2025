1) Función de la capa de enlace: Su función principal es establecer una conexión entre cada nodo que separa a dos hosts finales. Se encarga de gestionar tramas dentro de una red local, las cuales sirven para mover los paquetes IP provenientes de la capa de red. Permite la comunicación mediante identificadores físicos conocidos como MAC ID.
   Servicios que presta esta capa: 
	- Direccionamiento físico: utiliza direcciones MAC de 49 bits grabadas en los adaptadores de red (NIC) para identificar de forma única a los dispositivos en una red local.
	- Control de acceso al medio: Gestiona como los dispositivos comparten el canal de comunicación
	- Detección de errores: implementa mecanismos para identificar si los datos han sido alterados durante la transmisión.
2) Alcance de comunicación:
	1) Capa de enlace: su objetivo es establecer una conexión entre cada nodo individual que separa a dos hosts finales (comunicación nodo a nodo o hop-to-hop).
	2) Capa de transporte: Se encarga de la comunicación lógica entre los dos hosts finales del proceso de comunicación (comunicación extremo a extremo).
	Direccionamiento:
	3) Capa de enlace: Utiliza direcciones físicas (MAC) de 48 bits, que están grabadas en el adaptador de red (NIC) y no cambian según la red.
	4) Capa de transporte: Aunque el documento no profundiza en sus detalles técnicos, se sitúa por encima de la capa de red (que usa IPs lógicas), enfocándose en la entrega a procesos específicos dentro del host final.
	Unidades de datos y servicios especificos:
	5) Capa de enlace: Gestiona tramas y presta servicios de detección de errores, control de acceso al medio y direccionamiento físico dentro de una red local.
	6) Capa de transporte: Provee servicios de comunicación lógica que permiten que las aplicaciones en los hosts finales se comuniquen de forma transparente a los nodos intermedios.
3) ´ñ
	1) ¿Cómo se identifican dos máquinas en una red Ethernet? Se identifican mediante identificadores físicos únicos conocidos como MAC ID o direcciones MAC (Media Access Control). Mientras que la capa de red usa direcciones IP lógicas, la capa de enlace utiliza estas direcciones físicas para mover las tramas entre nodos dentro de una misma red local.
	2) ¿Cómo se llaman y qué características poseen estas direcciones? Se llaman direcciones MAC. Sus características principales son: 
		1) Longitud: son direcciones de 48 bits.
		2) Representación: Generalmente se escriben en formato hexadecimal.
		3) Permanencia: Vienen grabadas de fabrica en el adaptador de red (NIC). A diferencia de las direcciones IP, no cambian aunque el dispositivo se conecte a una red distinta.
	3) ¿Cuál es la dirección de broadcast en la capa de enlace? ¿Qué función cumple?
		1) Dirección: Es FF:FF:FF:FF:FF:FF (todos los bits en 1).
		2) Función: Se utiliza para enviar una trama a todos los dispositivos que pertenecen al mismo dominio de broadcast (red local). Es fundamental para protocolos como ARP, donde un host necesita preguntar a todos los demás quién posee una dirección IP específica para poder obtener su dirección MAC correspondiente.
4) 
	1) Dispositivos de capa de enlace y sus diferencias:
		1) Hub (Concentrador): Es un dispositivo que actúa a nivel físico; su función es simplemente repetir las tramas que recibe por un puerto hacia todos los demás puertos. No tiene capacidad de "aprendizaje", por lo que amplía los dominios de colisión
		2) Switch (Conmutador): Es un dispositivo de capa de enlace que tiene la capacidad de aprender las direcciones MAC de origen de los dispositivos conectados a sus puertos. A diferencia del Hub, reenvía las tramas de forma selectiva únicamente al puerto donde se encuentra el destino si lo conoce en su tabla; de lo contrario, realiza una inundación (flooding).
		3) Router (Encaminador): Aunque opera principalmente en la capa de red, es el dispositivo encargado de separar de forma explícita los dominios de broadcast.
	2) ¿Qué es una colisión?: Técnicamente, una colisión ocurre cuando dos o más dispositivos intentan transmitir datos de forma simultánea por el mismo medio físico, lo que provoca que las señales eléctricas interfieran entre sí y los datos se corrompan.
	3) Dispositivos que dividen dominios de broadcast: Routers: Son los dispositivos que separan los dominios de broadcast. Esto significa que los mensajes de difusión (como los ARP Requests) tienen un límite explícito y no atraviesan el router hacia otras redes.
	4) Dispositivos que dividen dominios de colisión:
		1) Switches: Al reenviar tramas selectivamente basándose en las direcciones MAC, el switch crea dominios de colisión independientes en cada uno de sus puertos
		2) Routers: Al separar redes físicas distintas, también actúan como una barrera que divide los dominios de colisión entre sus interfaces.
5) El algoritmo de acceso al medio (históricamente conocido como CSMA/CD - Carrier Sense Multiple Access with Collision Detection) sirve para gestionar y organizar cómo los dispositivos comparten el canal físico de comunicación.
   Su función principal es evitar que dos o más dispositivos transmitan datos al mismo tiempo por el mismo cable, lo que provocaría una colisión y la pérdida de la información. El algoritmo dicta que:
	1) Un dispositivo debe "escuchar" el medio antes de transmitir.
	2) Si el medio está libre, transmite.
	3) Si detecta una colisión mientras transmite, se detiene, envía una señal de refuerzo, espera un tiempo aleatorio y vuelve a intentar la transmisión.
	¿Es orientado a conexión? -> No, Ethernet no es orientado a la conexión. Ethernet es un protocolo "Connectionless" (sin conexión) y de "Best Effort" (mejor esfuerzo).
6) La finalidad del Protocolo de Resolución de Direcciones (ARP - Address Resolution Protocol) es servir como un "puente" o traductor entre la capa de red (capa 3) y la capa de enlace (capa 2). Su función específica es descubrir la dirección MAC (física) de un host cuando solo se conoce su dirección IP (lógica) dentro de una misma red local. **¿Por qué es necesario?** Para que un dispositivo pueda enviar una trama Ethernet a otro, necesita conocer la MAC de destino. Si el dispositivo emisor sabe que el destino está en su misma red (porque comparó las IPs y máscaras), pero no tiene la MAC en su memoria, debe usar ARP para obtenerla. Sin ARP, la comunicación en redes Ethernet sería imposible porque las tramas quedarían incompletas.
7) ![[Pasted image 20260202191723.png]] Dado el siguiente esquema de red
	1) Estacion 2, Servidor 1, Estacion 4, Estación 5
	2) Estación 2, Estacion 3, Servidor 1, Estacion 4, Estacion 5, Estacion 11
	3) Estacion 2, Estacion 3, Servidor 1, Estacion 4, Estacion 5, Estacion 10, Estacion 9, Estacion 8
	4) Todos
	5) Estacion 7
	6) Estacion 10, Estacion 9 y 8
	7) Se pueden producir donde hay HUBs
8) .
	1) 5 -> Segundo puerto del switch 1 es todo un dominio donde hay un hub. También cuenta entre el switch 1 y 2 
	2) 1
	3) 