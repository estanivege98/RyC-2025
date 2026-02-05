1) El IPv6 el la version mas nueva del protocol IP. Esta proporciona mayor espacio de direcciones (128 bits), un formato de cabecera simplificado y menor overhead de procesamiento. Es necesaria su implementacion para solucionar las limitaciones(en cuanto a direcciones IP) que traía IPv4. Garantiza que haya suficientes direcciones IP únicas para todos los dispositivos. Ademas, IPv6 proporciona mejoras en seguridad y eficiencia en comparación com IPv4.
2) Porque en IPv4 había un campo opcional cuyo tamaño podía variar, haciendo que varia la longitud del encabezado. En IPv6 todos los campos tienen un tamaño fijo, haciendo que el encabezado tenga una longitud constante.
3) El checksum se utiliza para verificar que no haya corrupciones en el paquete IP. En IPv6, el campo de checksum es eliminado para simplificar el procesamiento de los paquetes en los routers y dispositivos, dejando esta verificación a las capas superiores (TCP y UDP). En cuanto a estas, su obligatoriedad no ha cambiado.
4) Se reemplazaron por las extenisones de encabezado:
	1) Permiten la extensibilidad del protocolo
	2) Se encuentran a continuación del header
	3) En general, son procesadas por los extremos
5) Se implementaría como una extension del encabezado.
6) En IPv6, a diferencia de IPv4, ICMP es obligatorio. En IPv6 cumple funciones similares que en IPv4, pero con diferencias
	1) Descubrimientos de vecinos: ICMPv6 ND reemplaza ARP en IPv4, mapea direcciones IPv6 a direcciones de enlace para envió de paquetes
	2) Gestión de errores: ICMPv6 informa sobre errores de entrega, como paquetes demasiado grandes, tiempo de vida agotado y destino inalcanzable.
	3) Redireccion de rutas: ICMPv6 informa a los hosts sobre rutas mas eficientes en la red.
	4) Pruebas de conectividad: ICMPv6 informa a los hosts sobre rutas mas eficientes en la red.
	5) MLD (Multicast Listener Discovery): ICMPv6 se utiliza para el descubrimiento de escuchadores de multidifusion en redes IPv6.
7) Neighbour Discovery (ND) es un protocolo de IPv6 (definido en la RFC 4861) que reemplaza y amplía varias funciones que en IPv4 estaban separadas (ARP, ICMP Router Discovery, etc.). Funciona sobre ICMPv6.
   Funciones que cumple:
	1) Resolución de direcciones (reemplaza ARP): Traduce IPv6 → MAC
	2) Descubrimiento de routers: Permite que un host descubra: qué routers hay en la red y cuál es el gateway por defecto
	3) Autoconfiguración de direcciones (SLAAC): Gracias a los RA, el host puede: Obtener el prefijo de red y Generar su IPv6 global automáticamente
	4) Detección de direcciones duplicadas (DAD): Antes de usar una dirección IPv6, el host verifica que nadie más la esté usando, Se hace enviando NS a la propia dirección. Evita conflictos de IP.
	5) Detección de vecinos alcanzables: Permite saber si un vecino o router: sigue activo y es alcanzable. Mantiene actualizada la tabla de los vecinos.
   El Neighbour Discovery no puede funcionar sin IPv6, IPv6 depende directamente de ND para:
	- Resolver direcciones MAC
	- Encontrar routers
	- Autoconfigurarse
	- Evitar direcciones duplicadas
   Sin ND:
	- No hay gateway
	- No hay resolución de direcciones
	- No hay SLAAC
   IPv6 no es funcional sin Neighbour Discovery.
   Asimismo, IPv6 tampoco puede funcionar sin direcciones de tipo link-local, dado que Neighbour Discovery utiliza exclusivamente este tipo de direcciones para el intercambio de mensajes ICMPv6.
8)  Direcciones IPv6 **NO válidas**:
    - `2001::1871::4` (uso doble de `::`)
    - `3ffg:8712:0:1:0000:aede:aaaa:1211` (carácter no hexadecimal)
    - `3ffe:1080:1212:56ed:75da:43ff:fe90:affe:1001` (exceso de grupos)
9) 3f80:0:0:a00::845 (la 4ta)
10) |Dirección|Tipo|
	|---|---|
	|fe80::1/64|Link-local|
	|3ffe:4543:2:100:4398::1/64|Global unicast|
	|::|Unspecified|
	|::1|Loopback|
	|ff02::2|Multicast (link-local)|
	|2818:edbc:43e1::8721:122|Global unicast|
	|ff02::9|Multicast (link-local)|

11) Esto se hace principalmente para evitar el rastreo de dispositivos a través de redes, usando direcciones estables pero aleatorias o temporales para la navegación