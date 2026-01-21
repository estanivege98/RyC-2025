1) La capa de transporte permite la comunicación lógica entre procesos. Los protocolos de esta capa son mecanismos para comunicar procesos. Hace uso de los sockets, que son una abstracción a través de la cual puede enviar o recibir información: cada SO tiene su implementación. Además, estos sockets pueden ser de multiplexación (La capa de transporte del emisor arma segmentos enviando en la cabecera los identificadores para el origen y destino) y demultiplexación (la capa de transporte del receptor revisa las cabeceras y de esta manera determina a cual socket debe entregarle los datos que contiene el segmento.)
2) TCP: La cabecera TCP es **mucho más compleja** que la de UDP, ya que debe gestionar la fiabilidad, el orden, el control de flujo y la detección de errores. UDP: La cabecera UDP es **mínima** (solo 8 bytes) porque no ofrece mecanismos de fiabilidad, orden o control de flujo. Se le conoce como un protocolo de "mejor esfuerzo" (_best-effort_). La principal diferencia en la estructura es que TCP requiere y contiene campos extensos (Secuencia, Reconocimiento, Ventana y Flags) para ser **confiable** y **orientado a la conexión**, mientras que UDP carece de estos campos y es **mucho más rápido** porque no tiene que gestionar ni verificar la entrega. 
3) El objetivo principal del uso de **puertos** en el modelo TCP/IP es permitir la **multiplexación de aplicaciones**, es decir, que un mismo dispositivo pueda mantener múltiples sesiones de comunicación simultáneas y dirigir los datos al proceso o aplicación correcta. Mientras que la dirección IP identifica a un host (computadora o servidor) en la red, el **número de puerto** identifica la aplicación específica dentro de ese host. 

Funciones claves de los puertos:
El uso de puertos cumple con tres propósitos fundamentales:

- **Diferenciación de servicios:** Permite que un servidor ofrezca distintos servicios al mismo tiempo (como una página web en el puerto 80 y un correo electrónico en el puerto 25) utilizando una única dirección IP.
    
- **Segmentación de procesos:** Garantiza que los datos que llegan desde la red se entreguen exactamente al programa que los solicitó (por ejemplo, que una respuesta de chat no termine en la ventana del navegador).
    
- **Establecimiento de sesiones:** Permite que un cliente abra múltiples pestañas o conexiones hacia el mismo servidor, diferenciándolas mediante "puertos efímeros" (puertos de origen aleatorios).
Categorías de puertos:

Los puertos están representados por números de 16 bits, lo que da un rango de **0 a 65,535**, divididos en:

1. **Puertos bien conocidos (0 - 1023):** Reservados para servicios estándar (HTTP: 80, HTTPS: 443, FTP: 21).
    
2. **Puertos registrados (1024 - 49151):** Asignados a aplicaciones específicas o empresas.
    
3. **Puertos dinámicos o privados (49152 - 65535):** Usados temporalmente por las aplicaciones cliente para conectarse a un servidor.
4) 

| Caracteristica        | TCP                                                         | UDP                                                         |
| --------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| Confiabilidad         | Alta: Garantiza que los datos lleguen completos y en orden. | Baja: No garantiza la entrega ("mejor esfuerzo").           |
| Multiplexación        | Mediante puertos; gestiona sesiones individuales.           | Mediante puertos; gestiona datagramas independientes.       |
| Orientación           | Orientado a la conexión: Requiere saludo de 3 vías.         | Sin conexión: Envía datos directamente                      |
| Control de Congestión | Sí: Ajusta la velocidad según el estado de la red.          | No: Envía datos a la máxima velocidad posible.              |
| Uso de Puertos        | Utiliza puertos para mantener estados de conexión.          | Utiliza puertos para identificar aplicaciones (sin estado). |
5) El término datagrama se utiliza específicamente en el siguiente contexto:
	1) Cuando se utiliza el protocolo UDP: en la capa de transporte, el nombre de la PDU depende directamente del protocolo que se este utilizando:
		1) Segmento: Se usa con TCP (Transmission Control Protocol). Se llama así porque TCP toma un flujo continuo de datos de la aplicación y lo "segmenta" en trozos manejables, añadiendo números de secuencia para reconstruirlos en orden.
		2) Datagrama (o Datagrama de Usuario): Se usa con UDP (User Datagram Protocol). A diferencia de TCP, UDP no fragmenta un flujo continuo ni garantiza el orden; envía cada unidad de datos como un bloque independiente y autónomo. De ahí su nombre técnico: User Datagram.
		

| Protocolo | Nombre de la PDU | Razon del nombre                                                            |
| --------- | ---------------- | --------------------------------------------------------------------------- |
| TCP       | Segmento         | Los datos son parte de una "sesión" y están numerados para se reensamblados |
| UDP       | Datagrama        | Cada paquete es una entidad independiente que no depende de los anteriores  |
6) El saludo de tres vías (three-way-handshake) es el proceso mediante el cual el protocolo TCP establece una conexión lógica antes de comenzar a transferir datos. Su propósito es sincronizar los números de secuencia iniciales de ambos extremos y confirmar que el canal de comunicación está abierto y disponible.
Pasos del saludo de tres vías:
	1) Sincronización (SYN): el cliente envía un segmente con el bit SYN activado. En este paso, el cliente elige un numero de secuencia inicial aleatorio y se lo comunica al servidor.
	2) Sincronización y reconocimiento (SYN-ACK): El servidor recibe el segmente y responde con los bits SYN y ACK activados: El servidor reconoce el numero de secuencia del cliente enviando un ACK = x +1, mientras el servidor envía su propio numero de secuencia inicial.
	3) Reconocimiento (ACK): El cliente recibe la respuesta del servidor y envía un ultimo segmente con el bit ACK activado. Confirma la recepción del numero de secuencia del servidor enviando un ACK = y + 1.
	Una vez completado este ultimo paso, la conexión queda establecida y los datos pueden comenzar a fluir en ambas direcciones.
UDP no posee esta característica, ya que es un protocolo sin conexión (connectionless). Al eliminar el retraso que genera el intercambio de mensajes iniciales en el TCP, hace que el UDP sea mas rápido para aplicaciones en tiempo real como juegos en lineal o llamadas de voz.

7) El ISN (Initial Sequence Number) es un valoro numérico de 32 bits que se asigna a cada nueva conexión TCP. Su función principal es servir como el "punto de partida" para llevar la cuenta de los bytes enviados durante una sesión. En TCP cada byte de datos enviado tiene un numero de secuencia asociado. El ISN es el primero numero utilizado para esa secuencia. No comienza con 0 o 1 por razones de seguridad; en su lugar se genera un algoritmo que lo hace pseudoaleatorio y variable con el tiempo.
   El intercambio de los ISN es el objetico técnico central del saludo de las tres vías. Para que dos dispositivos se comuniquen de forma confiable, ambos deben "ponerse de acuerdo" en que numero van a empezar a contar. El proceso funciona así:
   i) SYN: El cliente envía su $ISN_{cliente}$ al servidor
   ii) SYN-ACK: El servidor recibe el numero, lo incrementa en 1 para confirmar la recepción (ACK = $ISN_{cliente}$ +1) y envía su propio $ISN_{servidor}$. 
   iii) ACK: El cliente recibe el numero del servidor, lo incrementa en 1 (ACK = $ISN_{servidor}$ +1) y lo envía de vuelta.
   El ISN debe ser aleatorio porque si se predice, la conexión seria vulnerable a ataques como la inyección de datos o superposición de sesiones.
8) El MSS (Maximum Segmente Size) es un parámetro critico del protocolo TCP que define la cantidad máxima de datos (en bytes) que un dispositivo puede recibir en un solo segmento de la capa de transporte. A diferencia de otras medidas, el MSS se refiere únicamente a la carga útil (de los datos reales), sin contar los encabezados de TCP o IP.
   Para entender el MSS, se debe entender primero el MTU, que es el tamaño maximo de la trama completa que puede viajar por la capa de enlace. La formula estandar para calcular el MSS es: 
$$
   MSS = MTU - (Cabecera IP + Cabecera TCP)
$$
¿Cuándo se negocia?: El MSS se negocia exclusivamente durante el saludo de tres vías. Una vez que la conexión está establecida y los datos comienzan a fluir, el valor del MSS no puede cambiarse -> momento exacto: ocurre en el intercambio de los paquetes SYN y SYN-ACK
¿Cómo se negocia?: En realidad es un intercambio de limites máximos. El proceso funciona así:
	i) El cliente envía un SYN: En el campo de "Opciones" del encabezado TCP, incluye si valor MSS. Esto le dice al servidor "No me envíes segmentes mas grandes que X bytes"
	ii) El servidor responde con un SYN-ACK: También incluye su propio valor MSS en las opciones (por ejemplo, Y bytes, si su red es distinta). Esto le dice al cliente: "No me envíes segmentos más grandes de Y bytes"
	iii) Acuerdo implícito: Cada extremo respetará el valor MSS informado por el otro. Si un host anunció un MSS de X y el otro uno de Y, la comunicación se ajustará para que nadie exceda el límite del receptor
Es importante el MSS porque si este llega a ser demasiado grade, el paquete resultante al llegar a la capa IP excederá el MTU de la red y causara fragmentación. Esta degrada el rendimiento de la red y aumenta el uso de CPU en los routers y dispositivos finales. El MSS bien negociado evita este problema desde el origen.
9) ![[Pasted image 20260121154757.png]] ![[Pasted image 20260121154859.png]]
	   Uso de los flags:
	   - -t: TCP
	   - -u: UDP
	   - -l: Listening (escucha)
	   - -p: Process (proceso/programa)
	   - -n: Numeric (direcciones y puertos numéricos)
10) Cuando un segmento TCP con el flag SYN activo llega a un host donde el puerto de destino no está en estado LISTEN (es decir, el puerto está cerrado), el protocolo TCP dicta que el receptor debe responder con un segmento que tenga el flag RST (Reset) y el flag ACK activados. Esto le indica al emisor que la conexión ha sido rechazada y que no debe intentar seguir con el saludo de tres vías.
	1) ![[Pasted image 20260121160554.png]] 'sudo hping3 -S -p 22 localhost'
	2) ![[Pasted image 20260121160745.png]] 'sudo hping3 -S -p 40 localhost'
	3) En el puerto 22 el host responde con el flags=SA, esto significa que el servidor reconoce el intento de conexión y está dispuesto a establecerla (procediendo al segundo del saludo de tres vías). En el puerto 40 el host responde con el flags=RA, esto significa que el paquete llego al host, pero el SO corto la comunicación de inmediato
	4) ¿A que se debe?: si ejecutamos el comando 'ss -ltn' en la maquina, vemos lo siguiente: ![[Pasted image 20260121161414.png]] Hay un proceso (quizá el servicio SSH) escuchando al puerto 22. Al recibir un SYN, el SO pasa el paquete al servicio y responde positivamente para iniciar una conexión. Por otro lado el puerto 40 no aparece en la lista al ejecutar el comando; como no hay ningún proceso "dueño" de ese puerto esperando datos, la pila TCP/IP del kernel del SO genera automáticamente un paquete RST para informar al cliente que "no hay nadie en casa" y que deje de consumir recursos.
11) A diferencia de TCP, que maneja sus propios errores mediante el flag RST, el protocolo UDP no tiene mecanismos integrados para señalizar errores. Por lo tanto, cuando un datagrama UDP llega a un puerto cerrado, el host receptor recurre al protocolo ICMP (Capa de Red) para informar del problema. El mensaje específico que se envía es un ICMP Type 3, Code 3 (Destination Unreachable - Port Unreachable).
	1) ![[Pasted image 20260121162726.png]]
	2) ![[Pasted image 20260121162930.png]] 
	3) En el puerto 5353 (abierto): no devuelve nada. La ausencia de mensajes suele ser "una buena noticia" en UDP, indicando que el paquete fue entregado a la pila de protocolos y no hubo errores de red inmediatos. En el puerto 40 (cerrado) se recibe un paquete ICMP de vuelta, el host destino nos está diciendo explícitamente: "recibí tu paquete, pero no tengo ninguna aplicación que sepa qué hacer con él"
	4) ¿A que se debe?: si se ejecuta el comando 'ss -uln' se puede ver lo siguiente: ![[Pasted image 20260121163450.png]] el sistema está escuchando al puerto 5353, como hay un proceso esperando, el kernel entrega el datagrama y no genera error. Por otro lado, el puerto 40 no aparece en la lista; al llegar el datagrama el kernel busca en su tabla de sockets activos; al no encontrar coincidencia para el puerto 40, genera el mensaje de error ICMP Port Unreachable.