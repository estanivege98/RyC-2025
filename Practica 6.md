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