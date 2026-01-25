1) Los servicios de la capa de red son los siguientes: 
	1) Direccionamiento Logico: Asigna a cada dispositivo una dirección única y jerárquica (dirección IP). A diferencia de la dirección MAC (física), la IP permite saber en qué red se encuentra el host.
	2) Enrutamiento (routing): Es la funcion más crítica, Consiste en determinar la mejor ruta que debe seguir un dato para llegar a su destino, basandose en tablas de entutamiento y protocolos (Header) con las direcciones IP de origen y destino, convirtiendolo en un paquete.
	3) Fragmentación y Re ensamblaje: si un paquete es demasiado grande para un medio físico intermedio (MTU pequeño), la capa de red puede dividirlo en trozos mas pequeño y volver a juntarlos en el destino.
   La PDU (Protocol Data Unit): La unidad de datos característica de esta capa es el paquete (Packet). En el contexto especifico del protocolo IP, a menudo se le denomina Datagrama IP. Cuando los datos bajan de la capa de transporte (segmentos) se "envuelven" en la capa de red con la información de direccionamiento necesaria, dando lugar al paquete.
   Dispositivo de la capa de red: El dispositivo por excelencia es el enrutador (Router): 
	4) ¿Por que?: Un router es capaz de leer las direcciones IP de los paquetes y tomar decisiones de envío basadas en su tabla de enrutamiento. A diferencia de un switch de capa 2 (que solo mira direcciones MAC), el router puede conectar redes de diferentes tecnologías y arquitecturas.
	5) Dato importante: Aunque existen los "Switches de Capa 3", el router sigue siendo el dispositivo diseñado fundamentalmente para operar en esta capa y servir de frontera entre distintas redes.
2) Se considera que IP (Internet Protocol) es un protocolo de "mejor esfuerzo" (Best-Effort) porque no garantiza que los datos lleguen a su destino, ni que lo hagan en el orden correcto o sin errores. Su única "promesa" es que el router hará lo mejor que pueda con los recursos que tiene en ese momento para reenviar el paquete.
3) 

| Clase   | Rango del primer octeto | Redes posibles           | Host por red                  |
| ------- | ----------------------- | ------------------------ | ----------------------------- |
| Clase A | 1 - 126                 | **128** ($2^7$)          | **16,777,214** ($2^{24} - 2$) |
| Clase B | 128 - 191               | **16,384** ($2^{14}$)    | **65,534** ($2^{16} - 2$)     |
| Clase C | 192 - 223               | **2,097,152** ($2^{21}$) | **254** ($2^8 - 2$)           |
4) Las subredes son el resultado de dividir una red física grande en varias redes lógicas más pequeñas. Es, básicamente, el arte de segmentar el espacio de direcciones IP para que la red sea más manejable, segura y eficiente. 
   Técnicamente, una subred se crea "tomando prestados" bits de la porción de host de una dirección IP y asignándolos a la porción de red. Esto crea una estructura de tres niveles:
	1) Red: La identidad principal
	2) Subred: el segmento especifico dentro de esa red
	3) Host: el dispositivo final
   Sirven para:
	4) Reducción del tráfico de Broadcast: En una red gigante, los mensajes de difusión (broadcast) saturarían los enlaces. Las subredes confinan ese tráfico a un área pequeña.
	5) Seguridad: Permiten aislar departamentos. Por ejemplo, puedes evitar que los hosts de la subred "Invitados" tengan acceso a la subred "Servidores Contables".
	6) Eficiencia: Ayudan a no desperdiciar direcciones IP. Con técnicas como VLSM (Máscara de Subred de Tamaño Variable), puedes asignar redes de 2 hosts para enlaces entre routers y redes de 100 hosts para oficinas, optimizando cada bit.
   Es importante especificar siempre la mascara de red porque, sin la máscara, una dirección IP es solo un número incompleto. La máscara de subred es lo que le da contexto a la IP. Es un número de 32 bits que indica exactamente dónde termina la red y dónde empieza el host:
	7) Define los límites: Si te doy la IP 192.168.1.1, no sabes si pertenece a una red de 254 hosts (máscara /24) o a una de solo 6 hosts (máscara /29). La máscara define el tamaño del "vecindario".
	8) Decisiones de enrutamiento: Cuando una computadora quiere enviar un paquete, realiza una operación lógica AND entre su propia IP y su máscara, y luego entre la IP de destino y su máscara. 
	9) Si los resultados coinciden: El destino está en la misma subred (entrega directa).
	10) Si no coinciden: El paquete debe enviarse al Gateway (Router) para salir de la red.
	11) Identifica la dirección de Red y Broadcast: La máscara permite calcular matemáticamente cuál es la primera dirección de la subred (red) y la última (broadcast).
5) Finalidad: Su función principal es la demultiplexación. Dado que la capa de red (IP) puede transportar datos de muchos protocolos diferentes de las capas superiores, necesita una forma de etiquetar el paquete para que el receptor sepa qué protocolo de transporte debe procesar la carga útil (payload):
	1) Ubicacion: es un campo de 8 bits en la cabecera IPv4.
	2) Funcionamiento: cuando un host recibe un paquete IP, mira este número. Si lee un 6, sabe que debe pasarle datos al modulo TCP; si lee 17, de los pasa a UDP

| Valor decimal | Protocolo |
| ------------- | --------- |
| 1             | ICMP      |
| 6             | TCP       |
| 17            | UDP       |
| 89            | OSPF      |
¿A qué campos de la capa de transporte se asemeja?
En cuanto a su funcionalidad, el campo Protocol de la capa de red es el equivalente directo a los Números de Puerto (Port Numbers) de la capa de transporte.
6) 