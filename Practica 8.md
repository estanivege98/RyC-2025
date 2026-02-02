1) a) Ip Origen: 10.0.0.20/24
   Ip Destino: 10.0.2.20/24
   Header: 20 bytes (cada fragmento lleva su propia cabecera IP)
   Tamaño total: 1500 Bytes (20 de cabecera IP + 1480 de datos)
   ID: 20543
   DF flag: 0
   MF flag: 0
   Frag flag: 0
   b) El paquete viaja bien desde el Router R1, pero el enlace entre R1 y R2 tiene un MTU de 600 bytes. Como 1500 > 600 debe fragmentar.
   c) Cada fragmento lleva su propia cabecera de 20 bytes, el tamaño de datos en cada fragmente debe ser múltiplo de 8 (a excepción del ultimo). MTU 600 - 20 = 580 bytes disponibles para datos. Como 580 no es divisible por 8 (580/8 = 72,5), el máximo de datos por fragmentos debe ser de 72 x 8 = 576 bytes.

| Fragmento | Tamaño total | Payload (datos) | Offset (Desplazamiento) | Bit MF |
| --------- | ------------ | --------------- | ----------------------- | ------ |
| Flag 1    | 596 B        | 576 B           | 0                       | 1      |
| Flag 2    | 596 B        | 576 B           | 72 (576/8)              | 1      |
| Flag 3    | 384 B        | 328 B *         | 144 (1152/8)            | 0      |
*Calculo ultimo payload: 1480 -576 - 576 = 328 Bytes*
d) Se reúnen de nuevo en los sistemas terminales. Si se pierde un fragmento, se deben retransmitir todos los fragmentos del paquete original. Sin embargo, IP no tiene mecanismos para comprobar la llegada de los fragmentos, así que depende de las decisiones de los protocolos de las capas superiores.
e) Lo vuelve a fragmentar.
2) El ruteo (o enrutamiento) es el proceso de la capa de red (Capa 3) que consiste en seleccionar el camino mas adecuado para reenviar los paquetes desde su origen hasta su destino final a través de redes interconectadas. Este proceso lo realizan principalemte los router, que mantienen una tabla de ruteo. 
   ¿Por que es necesario?: Es indispensable por las siguientes razones:
	1) Interconexion de redes distintas: Sin ruteo, una computadora solo podría comunicarse con otros dispositivos que estén en su misma red local (mismo switch o segmento físico). El ruteo permite que los datos "salten" de una red a otra (por ejemplo, de tu LAN doméstica a la red de tu proveedor de internet).
	2) Segmentación y Escalabilidad: Sería imposible tener a todos los dispositivos del mundo en una sola red gigante, ya que el tráfico de control (como los broadcasts de ARP) colapsaría el sistema. El ruteo permite dividir el mundo en millones de redes pequeñas administrables.
	3) Selección de la mejor ruta: En redes complejas (como Internet), existen múltiples caminos para llegar a un destino. El ruteo permite determinar cuál es el camino más corto, más rápido o menos congestionado.
	4) Aislamiento de tráfico: Ayuda a que la información circule solo por los segmentos necesarios, mejorando la seguridad y el rendimiento general de la red.
3) Ruteo Estático: El admin de red configura manualmente cada entrada en la tabla de ruteo de los routers
	1) Ventajas:
		1) Bajo consumo de recursos: No consume ciclos de CPU ni ancho de banda de red.
		2) Seguridad: El admin tiene control total sobre los caminos que sigue la información
		3) Previsibilidad: El camino que sigue un paquete es siempre el mismo y es fácil de debugear en redes pequeñas
	 2) Desventajas:
		 1) No es escalable: En redes grandes con decenas de routers, configurar cada router a mano es humanamente imposible y propenso a erroes.
		 2) No es adaptativo: Si un enlace se cae, el ruteo estático no sabe buscar un camino alternativo. El tráfico se pierde hasta que el administrador cambie la ruta manualmente.
		 3) Mantenimiento alto: Cualquier cambio en la topología (agregar una red nueva) requiere actualizar todos los routers involucrados.
	Ruteo Dinamico: Los routers utilizan protocolos de ruteo (como RIP, OSPF o BGP) para comunicarse entre ellos, aprender redes de forma automática y calcular el mejor camino.
	3) Ventajas:
		1) Escalabilidad: Es ideal para redes medianas y grandes. Una vez configurado el protocolo, los routers descubren nuevas redes sin intervención manual.
		2) Adaptabilidad (Resiliencia): Si un enlace falla, los routers detectan la caída y calculan automáticamente una ruta alternativa basándose en la nueva topología.
		3) Menor carga administrativa: El administrador solo configura el protocolo; el software se encarga de mantener las tablas de ruteo actualizadas.
	4) Desventajas:
		1) Consumo de recursos: Los protocolos consumen memoria RAM, ciclos de CPU y ancho de banda del enlace para enviar sus "actualizaciones" o "saludos" (hellos).
		2) Complejidad: Requiere conocimientos más avanzados para configurar correctamente el protocolo y evitar problemas como bucles de ruteo (routing loops).
		3) Seguridad: Es más vulnerable si no se utiliza autenticación, ya que un router extraño podría unirse a la red e inyectar rutas incorrectas para desviar el tráfico.
4) Una maquina conectada, inclusive si no esta conectada a la internet, tiene una tabla de ruteo para gestionar la comunicación con la red local. La tabla de enrutamiento tiene informacion sobre  las rutas disponibles en la red y como alcanzar otras maquinas dentro de esa red.
5) a)

| Red Destino   | Mask | Next-Hop  | Iface |
| ------------- | ---- | --------- | ----- |
| 153.10.20.128 | /27  | -         | eth1  |
| 10.0.0.4      | /30  | -         | eth0  |
| 10.0.0.0      | /30  | -         | eth0  |
| 10.0.0.8      | /30  | -         | eth3  |
| 10.0.0.12     | /30  | 10.0.0.5  | eth0  |
| 10.0.0.16     | /30  | 10.0.0.10 | eth3  |
| 205.10.0.128  | /25  | 10.0.0.1  | eth5  |
| 205.20.0.192  | /26  | 10.0.0.5  | eth0  |
| 205.20.0.128  | /26  | 10.0.0.5  | eth0  |
| 163.10.5.64   | /27  | 10.0.0.10 | eth3  |
b) No, no tiene Internet porque la tabla de roteo no tien ninguna entrada que conecte con un ISP. Esto se puede solucionar con una default gateway que conecte con un ISP a traves de RTC-C
c) Entraría en loop hasta que finalice el TTL y se descarte el paquete
d) No, en el estado actual no se puede realizar la sumarizacion porque 10.0.0.4 y 10.0.0.8 no tienen la misma interfaz
e) No se podría aplicar ya que son redes que están directamente conectadas con interfaces distintas
f) 

| Red Destino   | Mask | Next-Hop  | IFace |
| ------------- | ---- | --------- | ----- |
| 205.20.0.192  | /26  | -         | eth0  |
| 205.20.0.128  | /26  | .         | eth2  |
| 10.0.0.4      | /30  | -         | eth1  |
| 10.0.0.12     | /30  | -         | eth3  |
| 10.0.0.0      | /30  | 10.0.0.13 | eth3  |
| 10.0.0.8      | /30  | 10.0.0.6  | eth1  |
| 10.0.0.16     | /30  | 10.0.0.13 | eth3  |
| 0.0.0.0       | /0   | 10.0.0.13 | eth3  |
| 153.10.20.128 | /27  | 10.0.0.6  | eth1  |
| 205.10.0.128  | /25  | 10.0.0.10 | eth3  |
| 163.10.5.54   | /27  | 10.0.0.6  | eth1  |
| 120.0.0.0     | /30  | 10.0.0.13 | eth3  |
| 130.0.10.0    | /30  | 10.0.0.13 | eth3  |
g) Se podria reestablecer el acceso a internet si los routers tienen en su tablaa de ruteo la red ISP-1, es decir, a la red destino 120.0.0.0/30 para la cual se debe pasar por el router A.
6)  a) router2 -> router1 -> router3 -> PC-C. router2 no conoce 10.0.7.0, usa default -> router1; router 1 si conoce 10.0.3.0 -> router3; router3 tiene a 10.0.7.0 ocnectada; El mensaje lleja dando 3 saltos, la respuesta es ICMP Echo Reply
	b) router3 -> router4 -> router2 -> PC-B. router3 usa default -> router4; router4 conoce 10.0.5.0; router2 tiene red directa con PC-B. El mensaje llega dando 3 saltos, con mensaje ICMP Echo Reply.
	c) Hay un loop de ruteo -> ningun router conoce a 8.8.8.8, todos usan default route, el paquete gira en ciclo entre routers y el TTL se agota. El resultado no llega y el emisor recibe ICMP Time Exceeded
	d) Pasa lo mismo que lo anterior
7) .
	1) (Captura iniciada en Wireshark)
	2) ![[Pasted image 20260201121659.png]] 
	3) ![[Pasted image 20260201121756.png]] El archivo de dhclient.leases mantiene una base de datos persistentes de asignaciones de direcciones IP que fueron adquiridos y que siguen siendo validos. La base de datos es un archivo ASCII que contiene una declaración valida por declaración. Si mas de una declaración aparece para cada uno, se utiliza el ultimo que se encuentra en el archivo. Este archivo se escribe como un log. 
 
	4) ![[Pasted image 20260201122711.png]] 
	5) ![[Pasted image 20260201122816.png]] En el inciso 8b el cliente DHCP utiliza la información almacenada en dhclient.leases para renovar una concesión previa, por lo que no se observa el proceso completo de descubrimiento. En cambio, en el inciso 8e, al eliminar dicho archivo, el cliente no posee información previa y debe iniciar el proceso completo de DHCP (Discover, Offer, Request, ACK), lo que explica la diferencia en los paquetes observados en Wireshark.
	6) En ambos casos, el servidor DHCP le entrega, mediante las DHCP Options, al menos la siguiente informacion:
		 - **Máscara de subred** (`Subnet Mask – Option 1`)
        - **Gateway por defecto** (`Router – Option 3`)
        - **Servidor(es) DNS** (`Domain Name Server – Option 6`)
        - **Tiempo de concesión (lease time)** (`Option 51`)
        - **Tiempo de renovación (T1)** (`Option 58`)
	    - **Tiempo de rebinding (T2)** (`Option 59`)
	    - **Dirección del servidor DHCP** (`Server Identifier – Option 54`)
	    - (A veces) **nombre de dominio** (`Option 15`)
	    Todo esto se puede ver en el DHCPack en Wireshark.
8) NAT es un proceso que permite traducir direcciones IP de un espacio de direccionamiento a otro. Principalmente, se utiliza para mapear IP privadas (no enrutables en internet) a una IP publica (enrutable).
   Esto sirve para el ahorro de direcciones IPv4, siendo una solución "parche" exitosa ante el agotamiento de direcciones de 32 bits. Ademas da seguridad al ocultar las IPs reales de los hosts internos, actúa como barrera básica, ya que desde afuera no se puede iniciar una conexión directa hacia un host privado si no hay mapeo previo. Por ultimo, da flexibilidad cambiando de ISP sin tener que reconfigurar las IPs de todos los dispositivos de la red interna.
9) La normativa RFC 1918 reserva tres bloques de direcciones IPv4 para ser utilizados exclusivamente dentro de redes privadas. Lo mas importante es que estas direcciones son no enrutables en la internet publica. Esto significa que los routers de los proveedores de servicios (ISPs) descartan cualquier paquete que provenga de o vaya hacia una de estas direcciones fuera de su red local.
   Estas tres son:

| Rango                         | Mascara de Red (CIDR) | Descripcion                          |
| ----------------------------- | --------------------- | ------------------------------------ |
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8            | Grandes empresas y corporaciones     |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12         | Redes de tamaño mediano              |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16        | Redes domesticas y pequeñas oficinas |
La relación con NAT es dependencia mutua. Dado que hay miles de millones de dispositivos pero solo unos 4300 millones de direcciones IPv4, no todos pueden tener una dirección publica única. La solucion conjunta
- Ahorro de direcciones: miles de dispositivos pueden usar la misma dirección en diferentes redes privadas alrededor del mundo sin conflictos.
- Traducción (NAT): Cuando un dispositivo con una IP privada (RFC 1918) quiere salir a Internet, el router utiliza NAT para cambiar esa dirección privada por la única dirección IP pública que te asignó tu ISP.
- Seguridad Básica: Al no ser enrutables, las direcciones RFC 1918 están "escondidas" del mundo exterior. Un atacante en Internet no puede enviar un paquete directamente a tu IP 10.0.0.5 porque esa dirección no existe en el mapa global de la red
10) Si usamos ipconfig (en Windows) salen las Ip Privadas, mientra en el sitio www.cualesmiip.com sale la IPv4 publica.
11) ![[Pasted image 20260201125034.png]]
	1) `PC-A (ss)`
	`Local Address:Port Peer Address:Port`
	`192.168.1.2:49273 190.50.10.63:80 `
	`192.168.1.2:37484 190.50.10.63:25`
	`192.168.1.2:51238 190.50.10.81:8080`
	`PC-B (ss)`
	`Local Address:Port Peer Address:Port`
	`192.168.1.3:52734 190.50.10.81:8081`
	`192.168.1.3:39275 190.50.10.81:8080`
	`RTR-1 (Tabla de NAT)`
	`Lado LAN Lado WAN`
	`192.168.1.2:49273 205.20.0.29:25192`
	`192.168.1.2:51238 205.20.0.29:16345`
	`192.168.1.3:52734 205.20.0.29:51091`
	`192.168.1.2:37484 205.20.0.29:41823`
	`192.168.1.3:39275 205.20.0.29:9123`
	`SRV-A (ss)`
	`Local Address:Port Peer Address:Port`
	`190.50.10.63:80 205.20.0.29:25192`
	`190.50.10.63:25 205.20.0.29:41823`
	`SRV-B (ss)`
	`Local Address:Port Peer Address:Port`
	`190.50.10.81:8080 205.20.0.29:16345`
	`190.50.10.81:8081 205.20.0.29:51091`
	`190.50.10.81:8080 205.20.0.29:9123`
	2) Hay establecidas en total 5 conexiones:
		1) PC-A -> SRV-A: 2 Conexiones (puertso 80 y 25)
		2) PC-A -> SRV-B: 1 Conexión 
		3) PC-B -> SRV-B: 2 Conexiones
	3) Las que iniciaron las conexiones son las PCs, los Servers solo responden ya que están detrás de NAT y no tienen forma de iniciar una conexión hacia ips privadas. No se podría iniciar al revés sin una configuración adicional. El port forwarding es una tecnica NAT en donde se mapea un puerto fijo publico a una IP:puerto privado. Ejemplo: 
```
	205.20.0.29: 80 -> 192.168.1.2:80
```

Con port forwarding los servidores se podrían conectar a las ip privadas.
12) ![[Pasted image 20260201131644.png]] Usando los bloques:
```
226.10.20.128/27
200.30.55.64/26
127.0.0.0/24
192.168.10.0/29
224.10.0.128/27
224.10.0.64/26
192.168.10.0/24
10.10.10.0/27
```
Con las siguientes condiciones:
- **Red C y Red D deben ser públicas**
- **Enlaces entre routers → redes privadas**
- **Desperdiciar la menor cantidad de IPs**
- **Asignar primero las redes con más hosts**
- **Las redes deben ser válidas**
De ese bloque descartamos:
- 127.0.0.0/24 Ya que es un loopback, no es ruteable
- 224.10.0.128/27 y 224.10.0.64/26 Por ser multicast, no se pueden asignar a hosts
Si clasificamos los restantes:
- Redes publicas (no RFC1918): 226.10.20.128/27 y 200.30.55.64/26
- Redes privadas (RFC1918): 192.168.10.0/24 ; 192.168.10.0/29 ; 10.10.10.0/27
**Red A**: Necesita 100 hosts -> necesita 7 bits que generarían 128 hosts. Se utilizara 192.168.10.0/24:
192.168.10. 00000000
255.255.255. 00000000 Mascara de red
255.255.255. 1 000000 Mascara de subred
Queda un bit para ser usado en subredes
192.168.10.00000000/25 - 192.168.10.0/25 Asignado a la red A, 192.168.10.128/25 libre para hacer subnetting.
**Red B**: necesita 70 hosts -> 7 bits que generarían 128 host, uso la subred de 192.168.10.128/25 que me quedo libre
**Red D**: Necesita 16 hosts -> necesita 5 bits que generarían 32 hosts y que la red sea publica, la unica que puedo utilizar es la 200.30.55.64/26
200.30.55.01000000
255.255.255.11000000 Mascara de red
255.255.255.11100000 Mascara de subres
queda 1 bit para ser usado en subredes. 200.30.55.01000000/27 - 200.30.55.64/27 Asignado a la red D; 200.30.55.01100000/27 libres para seguir haciendo subnetting
**Red C**: necesita 14 hosts -> 4 bits que generarían 16 -> seguir subnettinando 200.30.55.96/27
200.30.55.011000000
255.255.255.11100000 Mascara de red
255.255.255.11110000 Mascara de subred
Queda 1 bit para ser usado en subredes
200.30.55.01100000/28 - 200.30.55.96/28 Asignado a la red C
200.30.55.01110000/28 - 200.30.55.112/28 Libre para seguir haciendo subnetting
**Router D - Router C**: necesitan 4 hosts por lo que necesitan 3 bits que generarian 6 hosts -> uso 10.10.10.0/27
10.10.10.00000000
255.255.255.11100000 (/27)
255.255.255.11111000 (/29)
Asigno de los routers D y C 10.10.10.0/29