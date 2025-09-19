1) La capa de aplicación proporciona la interfaz directa entre el cliente y el servidor, definiendo protocolos de comunicación que permiten enviar, recibir datos y la comunicación. Su función principal es brindar servicios de red a las aplicaciones, gestionando tareas como la navegación web, el correo electrónico, la transferencia de archivos y la resolución de nombres de dominio (DNS)
2) a) Si dos procesos deben comunicarse y están en diferentes maquinas, se utilizan protocolos de comunicación que ambas computadoras entiendan. Esta es la función principal de los protocolos, la comunicación es independiente del sistema operativo de alguna de las computadoras.
   b) En el caso de que dos procesos quieran comunicarse y se encuentran en la misma maquina cosas como la memoria compartida.
3) Este modelo es el que mas utilizan las aplicaciones. La idea es que el cliente pone el procesamiento de interfaz, haciendo los requerimientos y/o los pedidos. Por eso Chrome ocupa mucha RAM.
- Es un modelo de carga compartida.
- El servidor pone el resto del procesamiento.
- Existen modelos en varios tiers.
- El servidor corre servicio esperando de forma pasiva la conexión.
- El cliente se conecta al servidor y se comunica a través de este.
- Ejemplos: File server vía NFS o FTP.
- Es un modelo asimétrico 1 a N, M a N (donde M<N).
  Si damos un ejemplo de la vida real, el cliente podría buscar en google, a traves de si navegador, y el servidor de google le responde.
  Un ejemplo mas técnico es: 
7) En curl, los parámetros sirven para lo siguiente:
	1) '-l': Muestra el sitio web en modo lista.
	2) '-H': Le envía un header diferente al servidor.
	3) '-X': Especifica un comando request al servidor.
	4) '-s': Modo silencioso, no muestra errores de comunicación entre el servidor y el cliente.
8) a) Realice un requerimiento (método GET) y recibí un HTML.
   b) El atributo href 