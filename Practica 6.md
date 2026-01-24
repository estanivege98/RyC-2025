1) 

| Servicio   | Protocolo de Aplicación | Puerto(s) por Defecto                            |
| ---------- | ----------------------- | ------------------------------------------------ |
| Web        | HTTP                    | 80 (TCP)                                         |
| SSH        | SSH                     | 22 (TCP)                                         |
| DNS        | DNS                     | 53 (UDP para consultas, TCP para transferencias) |
| Web Seguro | HTTPS                   | 443 (TCP)                                        |
| POP3       | POP3                    | 110 (TCP)                                        |
| IMAP       | IMAP                    | 143 (TCP)                                        |
| SMTP       | SMTP                    | 25 (TCP)                                         |
Tanto en Linux como en Windows mantienen un archivo de texto que funciona como una "guía de referencia" para que el sistema sepa que nombre corresponde a cada numero de puerto.
**En Linux**: la ruta es /etc/services. Para consultarlo se puede usar el comando 'cat /etc/services' o buscar uno con el comando 'grep'. Este archivo es esencial para comandos como 'ss' o 'netstat' puedan mostrar nombres de servicio en lugar de solo números.
**En Windows**: La ruta es C:\Windows\System32\drivers\etc\services. Se puede abrir este archivo en un bloc de notas, y al igual que en Linux contiene una extensa lista de nombres de servicio, números de puerto y el protocolo que utilizan.
2) El multicast es un método de direccionamiento de red que permite enviar datos desde un único emisor a un grupo específico de receptores simultáneamente, sin necesidad de duplicar el mensaje para cada uno. A diferencia del unicast (uno a uno) o el broadcast (uno a todos), el multicast es altamente eficiente porque el emisor envía una sola copia de los datos y la red se encarga de replicarla solo donde sea necesario para alcanzar a los miembros del grupo.
   El mutlicast funciona casi exclusivamente sobre UDP, esto se debe a que UDP no requiere mantener una conexión abierta ni realizar un seguimiento de quien recibió que y por eficiencia, es ideal para transmisiones de "uno a muchos".
   No es posible adaptarlo a TCP, porque varias razones:
	1) Orientación a la conexión: TCP requiere el three-way-handshake para establecer una sesión única entre dos puntos específicos. En TCP no existe un mecanismo para sincronizar números de secuencia (ISN) con miles de receptores a la vez de forma simultanea.
	2) Control y flujo de errores: TCP garantiza la entrega mediante confirmación (ACK). Si un emisor usa multicast usara TCP y tuviera 1000 receptores, recibiría 1000 ACKs por cada paquete enviado. Si un solo receptor perdiera un paquete, el emisor tendría que retransmitirlo, lo que causaría una "implosión de ACKs" y colapsaría el emisor.
	3) Control de congestión: TCP ajusta su velocidad basándose en la congestión detectada entre emisor y receptor. En un grupo multicast, cada receptor puede tener  una calidad de conexión distinta; TCP no sabría a qué velocidad transmitir para satisfacer a todos sin perjudicar a ninguno.
3) El FTP es diferente al resto de los protocolos en comparación, ya que usa dos canales de comunicación distintos para funcionar: uno para el control (comandos) y otro para la transferencia de datos.
   Funcionamiento del FTP: a diferencia del HTTP o del SSH, que se envia todo en una unica conexion, el FTP separa las tareas:
	1) Canal de control (puerto 21): Se utiliza para autenticación, navegación por carpetas y envío de comandos (como GET o PUT). Permanece abierto durante toda la sesión.
	2) Canal de datos: Se abre y se cierra dinámicamente cada vez que se transfiere un archivo o se solicita un listado de archivos.
   Modo pasivo vs modo activo: La diferencia principal radica en quién inicia la conexión para el canal de datos:
	3) Activo (Active Mode): Es el diseño original de FTP, donde el servidor debe conectarse al cliente para entregar los datos.
		1) Conexión de Control: El cliente se conecta desde un puerto aleatorio (6$N$) al puerto 21 del servidor.
		2) Comando PORT: El cliente envía el comando PORT, indicando al servidor su dirección IP y un puerto abierto (N+1) donde esperan los datos.
		3) Conexioin de datos: El servidor inicia una conexión desde su puerto 20 hacia el puerto $N+1$ del cliente.
		4) Problema: Los firewalls de los clientes suelen bloquear conexiones entrantes no solicitadas, lo que hace que el Modo Activo falle frecuentemente hoy en día.
	4) Pasivo (Passive Mode): Fue diseñado para solucionar problemas de firewalls, haciendo que el cliente inicie ambas conexiones.
		1) Conexión de Control: Igual que en el modo activo (Cliente al puerto 21).
		2) Comando PASV: El cliente envía el comando PASV. El servidor responde con una dirección IP y un puerto aleatorio alto (ej. 55000).
		3) Conexión de Datos: El cliente inicia la conexión desde su puerto 17$N+1$ hacia el puerto aleatorio indicado por el servidor.
		4) Ventaja: Como el tráfico es "saliente" desde la perspectiva del cliente, los firewalls domésticos suelen permitirlo sin problemas.
   ¿En que se diferencia FTP del resto de los protocolos?: FTP se distingue de protocolos como HTTP, SMTP o DNS por tres razones fundamentales: 
	5) Multiconexion: Es de los pocos protocolos que requiere abrir múltiples sockets simultáneos (uno de control y uno o más de datos) para completar una sola tarea de usuario.
	6) Negociación Dinámica de Puertos: Mientras que el puerto de control es fijo (21), los puertos de datos cambian constantemente, lo que complica la configuración de reglas de seguridad en routers y firewalls.
	7) Fuera de Banda (Out-of-band): Al separar el control de los datos, FTP permite enviar comandos (como "Abortar transferencia") a través del canal de control mientras el canal de datos está ocupado transfiriendo un archivo pesado. En protocolos de un solo canal, tendrías que esperar a que termine la descarga para que el servidor procese el siguiente comando.
4) 
	1) ACK 0: El Host B recibe el paquete 0 correctamente y confirma su recepción individual.
	2) ACK 1: El Host B recibe el paquete 1 correctamente y lo confirma.
	3) Sin ACK (Paquete 2): El mensaje llega con errores (E). El Host B detecta el error, descarta el paquete y no envía ningún ACK.
	4) ACK 3: El Host B recibe el paquete 3. Aunque el 2 falta, Selective Repeat permite confirmar paquetes fuera de orden. Envía el ACK 3 y almacena el paquete en su buffer.
	5) ACK 4: El Host B recibe el paquete 4 correctamente y envía el ACK 4.
	6) ACK 5: El Host B recibe el paquete 5 correctamente y envía el ACK 5.
	7) ACK 2 (Reintento tras Timeout): El Host A detecta que el tiempo para el paquete 2 se agotó (Timeout 2) y reenvía solo ese paquete. Al recibirlo correctamente esta vez, el Host B envía el ACK 2.
5) En el protocolo Selective Repeat, existe una restricción fundamental sobre el tamaño de la ventana para evitar que el receptor confunda paquetes nuevos con duplicados de una ventana anterior debido al "envolvimiento" (wrap-around) de los números de secuencia. La restriccion técnica establece que el tamaño de la ventana (W) debe ser menor o igual a la mitad del espacio total de numeros de secuencia (N), esto se expresa como W<=N/2. Si los números de secuencia se definen mediante k bits, el espacio de números es N=2^k, por lo que la restricción es: $$W_{sender} + W_{receiver} \leq 2^k$$ ¿Por qué existe esta restricción?
   Si la ventana fuera más grande que la mitad del espacio de secuencias, ocurriría un escenario de ambigüedad catastrófico:

    1. **Escenario de fallo:** Supongamos que tenemos números de secuencia del 0 al 3 ($N=4$) y un tamaño de ventana de 3 ($W=3$).
    
    2. El emisor envía los paquetes 0, 1 y 2.
    
    3. El receptor los recibe todos y envía los ACKs correspondientes, moviendo su ventana para esperar los paquetes 3, 0 y 1.
    
    4. **El problema:** Si todos los ACKs se pierden en la red, el emisor agotará su tiempo de espera y **reenviará el paquete 0**.
    
    5. **La confusión:** El receptor, que ahora está esperando un **nuevo** paquete 0 (de la siguiente vuelta), recibirá el paquete 0 **viejo** y lo aceptará como si fuera información nueva, ya que el 0 sigue cayendo dentro de su ventana actual.
6) Source: 172.20.1.1; Destination: 172.20.1.100; SYN; Seq=3933822137; 41749 > vce; ACK; Seq=3933822138; Ack=1047471502.
7) .
8) El RTT es el tiempo que transcurre desde que un emisor envía un segmento hasta que recibe el correspondiente reconocimiento (ACK) del receptor. Es, literalmente, el tiempo de "ida y vuelta". Calcular el RTT no es tan simple como medir un solo paquete, ya que el tráfico en la red es muy volátil. Por eso, TCP utiliza un RTT suavizado ($SRTT$) mediante el algoritmo de Jacobson para evitar reaccionar exageradamente a picos de latencia momentáneos: $$SRTT = (1 - \alpha) \cdot SRTT + \alpha \cdot RTT_{sample}$$ Donde **$RTT_{sample}$**: Es el tiempo medido del último paquete y **$\alpha$**: Es un factor de suavizado (típicamente **0.125** o **1/8**).
   Originalmente, TCP solo medía un RTT por cada ventana de datos, lo cual era poco preciso para redes modernas de alta velocidad. Para solucionar esto, se introdujo la opción de Timestamps en el encabezado TCP.
   Esta opción permite que cada segmento lleve una marca de tiempo, lo que proporciona una medición del RTT mucho más frecuente y exacta.
   Cuando la opción de Timestamps está activa, el encabezado TCP añade 10 bytes adicionales donde destacan estos dos campos:
   TSval (Timestamp Value): Es el valor actual del reloj del emisor en el momento de enviar el segmento.
   TSecr (Timestamp Echo Reply): Es el "eco". Aquí, el emisor coloca el último valor de TSval que recibió del receptor.
9) -
	1) ![[Pasted image 20260124175059.png]] 6
	2) ![[Pasted image 20260124175139.png]] ![[Pasted image 20260124175153.png]] 
	3) ![[Pasted image 20260124175224.png]] Para diferenciarlos, los exitosos tienen los flags SYN/ACK en 1, y los fallidos RST/ACK en 1
	4) 
		1) La conexion es iniciada por 10.0.2.10:46907. El cliente es 10.0.2.10:46907 y el servidor es 10.0.4.10:7002. ![[Pasted image 20260124175953.png]]
		2) ![[Pasted image 20260124181310.png]] ![[Pasted image 20260124181337.png]] ![[Pasted image 20260124181402.png]] 
		3) ![[Pasted image 20260124181500.png]]
		4) 10.0.2.10:46907, incrementa su numero de secuencia (cuando se envian datos), mientras que 10.0.4.10:7002 nunca lo incrementa (salvo en el 3WH). 10.0.2.10:46907 termina con el ISN relativo de 786458 y 10.0.4.10:7002 con 1
	 5) depues lo sigo
10) Sobre el mecanismo de control
	1) El control de flujo lo activa el receptor enviando ventanas mas chicas