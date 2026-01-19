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