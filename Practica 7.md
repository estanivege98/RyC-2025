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

| IP / Mascara     | Clase | Subred        | Broadcast     | Max. Hosts |
| ---------------- | ----- | ------------- | ------------- | ---------- |
| 172.16.58.223/26 | B     | 172.16.58.192 | 172.16.58.255 | 62         |
| 163.10.5.49/27   | B     | 163.10.5.32   | 163.10.5.63   | 30         |
| 128.10.1.0/23    | B     | 128.10.0.0    | 128.10.1.255  | 510        |
| 10.1.0.0/24      | A     | 10.1.0.0      | 10.1.0.255    | 245        |
| 8.40.11.179/12   | A     | 8.32.0.0      | 8.47.255.255  | 1,048,574  |

7) 
	1) Es una dirección de host, porque al ser de clase B, su mascara por defecto es /16. Esto significa que los primeros dos octetos (128.50) son la red y los últimos dos (10.0) son el host. En binario es 10000000 00110010 00001010 00000000 y la mascara es 11111111 11111111 00000000 00000000
	2) Clase B (su rango es de 128 a 191) y la mascara de clase es 255.255.0.0 (en CIDR: /16).
	3) La cantidad de host posibles es 32 - 16 = 16bits --> 2^16 -2 = 65534 hosts
	4) q
		1) Mascara necesaria: 255.255.255.192
		2) Cantidad de redes asignables: 1024
		3) Cantidad de hosts por subred: 62
		4) La subred 710 en binaria resia la 709 ya que se empieza a contar desde 0. 710 en binario es 10110001, por lo que la dirección para la subred seria: 100000000 00110010 10110001 01000000 (128.50.177.64)
		5) 128.50.177.127
8) a) Si uso la formula de 2^n >= subredes, donde n es la cantidad de bits que robaremos a los hosts
	1) Si robamos 3 bits: 2^3 = 8 subredes, no alcanza necesitamos 9
	2) Si robamos 4 bits: 2^4 = 16 subredes
   Debemos tomar 4 bits
   Para definir la nueva mascara, sabemos que la mascara original es /24, al sumar los 4 bits que tomamos prestados, la nueva mascarara es /28, 255.255.255.240 (el 240 viene de sumar los pesos de los 4 bits activamos en el ultimo octeto: 128 + 64 + 32 + 16 = 240)
   b) 

| Subred # | Direccion de Subred |
| -------- | ------------------- |
| 1        | 195.200.45.0        |
| 2        | 195.200.45.16       |
| 3        | 195.200.45.32       |
| 4        | 195.200.45.48       |
| 5        | 195.200.45.64       |
| 6        | 195.200.45.80       |
| 7        | 195.200.45.96       |
| 8        | 195.200.45.112      |
| 9        | 195.200.45.128      |
c) 195.200.45.0
Broadcast: 11111111 11111111 11111111 00001111 - 195.200.45.15
Min: 11111111 11111111 11111111 0000001 - 195.200.45.1
Max: 11111111 11111111 11111111 0001110 - 195.200.45.14

10) CIDR (Classless Inter-Domain Routing) es el sistema que jubiló al antiguo modelo de "redes por clases" (A, B y C) a principios de los años 90. Fue la solución de emergencia para evitar que las direcciones IPv4 se agotaran prematuramente y que las tablas de enrutamiento de Internet colapsaran por el exceso de información.
    En lugar de tener tamaños de red fijos y rígidos, CIDR permite usar máscaras de longitud variable (VLSM).CIDR es una estrategia para frenar algunos problemas que se habian comenzado a manifestar con el crecimiento de Internet. Algunos de estos son:
	1) Agotamiento del espacio de direcciones de clase B.
	2) Crecimiento de las tablas de enrutamiento mas alla de la capacidad del software y hardware disponibles
	3) Eventual agotamiento de las direcciones IP en general.
     CIDR consiste básicamente en permitir mascaras de subred de longitud variable (VLSM) para optimizar la asignación de direcciones IP y utilizar resumen de rutas para disminuir el tamaño de las tablas de enrutamiento.
 Este sistema resulta util porque no solo es "mas ordenado", es vital para la supervivencia de la red por dos razones:
 - Eficiencia en la asignacion de IPs: Elimina el desperdicio masivo. Permite a los proveedores de Internet (ISPs) parcelar sus bloques de direcciones de forma quirúrgica, entregando a cada cliente exactamente lo que necesita.
 - Agregación de rutas (supernetting): CIDR permite que un router anuncie una sola ruta resumen (ej: 192.10.0.0/22) en lugar de cuatro rutas individuales (/24).
	 - Menos memoria: Los routers de los "backbones" de Internet no tienen que memorizar miles de millones de rutas.
	 - Menos tráfico de control: Si una pequeña red dentro del bloque falla, el resto del mundo no necesita enterarse, porque la ruta resumida sigue siendo válida.
11) Análisis Binario:
     - a. 198.10.0.0: 198.10. 000000 00 .0
     - b. 198.10.1.0: 198.10. 000000 01 .0
     - c. 198.10.2.0: 198.10. 000000 10 .0
     - d. 198.10.3.0: 198.10. 000000 11 .0
    Bits Comunes:
	1) Primer octeto: 8 Bits
	2) Segundo octeto: 8 Bits
	3) Tercer octeto: 6 Bits comunes
	4) Total: 8 + 8 + 6 = 22
	Resultado: 198.10.0.0/22
12) Bloque: 200.56.168.0/21
	- Es un red de Clase C, con mascara /24
	- Cantidad de redes: 2^3 = 8 redes
	- Las redes involucradas van desde 200.56.168.0/24 hasta 200.56.175.0/24
	Bloque: 195.24.0.0/13:
	- Red de Clase B, con mascara /16
	- Cantidad de redes: 2^3 = 8 redes tipo C
	- Las redes involucradas van desde 195.24.0.0/16 hasta 195.31.0.0/16
    Bloque: 195.24/13:
    - Abreviado del anterior -> en el estándar CIDR es común omitir los octetos que son todos ceros al final.
    - Significado: 195.24/13 es exactamente lo mismo que 195.24.0.0/13
    - Las redes involucradas son las mismas que en el bloque anterior.
13) En CIDR si, es equivalente a listar todas las direcciones de clase B.
	- Para demostrarlo, se debe mirar los bits mas significativos:
		- Históricamente, se definió que toda la dirección de clase B debe comenzar obligatoriamente con los bits binarios 10.
		- El numero 128 en binario es 10000000
		- La mascara /12 le dice al router: "Solo me importan los primeros 2 bits, el resto puede ser lo que sea".
		- Esos dos primeros bits son 10
	Por lo tanto, abarca absolutamente todas las direcciones que comienzan con 10, lo cual  es exactamente el rango que va desde 128.0.0.0 hasta 191.255.255.255 (todas las direcciones de la clase B).
	Por otro lado, siguiendo la misma logica binaria, podemos agrupar toda la clase A en un unico bloque:
	- Regla de la clase A: el primer bit debe ser 0
	- Rango: va desde 0.0.0.0 hasta 127.255.255.255
	- Bloque CIDR: para fijar solo el primer bit como 0, necesitamos una mascara de 1 bit.
	- Bloque clase A: 0.0.0.0/1 (o simplemente 0/1)
	Esto representa la primera mitad exacta de todo el universo de direcciones IPv4.
14) VLSM (Variable Length Subnet Masking) es la evolución técnica del subnetting tradicional. si el subnetting es dividir una red en partes iguales, VLSM la divide en tamaños diferentes según la necesidad real de cada segmento.
    Para aplicar VLSM correctamente, siempre se debe seguir una jerarquía de necesidades. No se puede dividir al azar; se debe empezar por la subred que requiere la mayor cantidad de hosts y terminar con la mas pequeña.
15) Si el subnetting, es cortar como cortar una pizza en 8 porciones iguales, el VLSM es como cortarla según el hambre de cada comensal: a uno le das media pizza, a otro dos porciones y al ultimo solo una puntita.
    El mecanismo para hacerlo y no morir en el intento es el siguiente:
	1) El inventario (¿Quien necesita que?): Lo primero es hacer una lista de todas las redes que necesitás y cuántos hosts (dispositivos) va a tener cada una.
	2) La Regla de Oro: Ordenar de Mayor a Menor Este es el paso donde la mayoría se equivoca. Siempre tenés que empezar a asignar direcciones a la subred que necesite más hosts. Si empezás por la red más chica, vas a "fragmentar" el bloque de IPs y después no te van a quedar espacios contiguos lo suficientemente grandes para las redes grandes.
	3) Encontrar la "Horma" (La Máscara ideal)Para la red más grande de tu lista, buscás la máscara que mejor le quede.Si necesitás 50 hosts, buscás la potencia de 2 que lo cubra: $2^6 = 64$.Como $64 - 2$ (red y broadcast) es $62$, esa máscara te sirve perfectamente.Esa máscara sería una /26 (porque $32 - 6 = 26$).
	4) Asignar y "Cortar" Tomas tu bloque de IP original y le asignás ese primer pedazo. Ejemplo: Si empezás en la .0, y tu bloque es de 64, esa subred va de la .0 a la .63.
	5) Repetir con el "Sobrante" Ahora mirás cuál es la siguiente red más grande en tu lista. Su dirección de subred va a ser la que sigue inmediatamente después de donde terminó la anterior. En el ejemplo anterior, la siguiente red empezaría en la .64. Volvés al Paso 3 para calcular su máscara y seguís así hasta terminar con los enlaces de los routers (que suelen ser los últimos por ser los más chiquitos, de máscara /30).
16) 