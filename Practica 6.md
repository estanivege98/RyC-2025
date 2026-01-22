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
