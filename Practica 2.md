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
   b) El atributo href en la etiqueta <link> se utiliza para enlazar recursos externos y el atributo src en la etiqueta <img> se utiliza para especificar la ubicación de la imagen que se mostrará en la página web. En los dos casos el navegador realiza solicitudes HTTP para descargar los recursos especificados en las URL de los atributos. Después, dependiendo del recurso, realiza acciones como aplicar estilos en el caso de las hojas de estilo o mostrar las imágenes en el caso de las etiquetas <img>.
   c) No alcanza con un nuico requerimiento. Cada recurso se solicita por separa el recurso al servidor. Se necesitarán 1 requerimiento para el archivo base HTML, 1 requerimiento para el favicon, 2 requerimientos para el CSS, 2 requerimientos para el Javascript, y 3 requerimientos para las 3 imágenes. Si el HTML tiene algún atributo href también se realizan los requerimientos correspondiente para cada atributo. Curl solo realizará un solo requerimiento (archivo base HTML), requiere solicitudes manuales. 
9)  -v Muestra información del intercambio que se está haciendo, información detallada de la comunicación entre el cliente y el servidor. La diferencia se debe a > /dev/null que redirige la salida estandar (la respuesta enviada por el servidor) a /dev/null (que la descarta).
> GET / HTTP/1.1
> Host: www.redes.unlp.edu.ar
> User-Agent: curl/7.74.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 19 Sep 2025 19:51:33 GMT
< Server: Apache/2.4.56 (Unix)
< Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
< ETag: "1322-5f7457bd64f80"
< Accept-Ranges: bytes
< Content-Length: 4898
< Content-Type: text/html
< 
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>.::.Redes y Comunicaciones.::.Facultad de Inform&aacute;tica.::.UNLP.::.</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="">
    <meta name="author" content="">

    <!-- Le styles -->
    <link href="./bootstrap/css/bootstrap.css" rel="stylesheet">
    <link href="./css/style.css" rel="stylesheet">
    <link href="./bootstrap/css/bootstrap-responsive.css" rel="stylesheet">

    <!-- HTML5 shim, for IE6-8 support of HTML5 elements -->
    <!--[if lt IE 9]>
      <script src="./bootstrap/js/html5shiv.js"></script>
    <![endif]-->
  </head>

  <body>
      
    <div id="wrap">
    <div class="navbar navbar-inverse navbar-fixed-top">
      <div class="navbar-inner">
        <div class="container">
          <a class="brand" href="./index.html"><i class="icon-home icon-white"></i></a>
          <a class="brand" href="https://catedras.info.unlp.edu.ar" target="_blank">Redes y Comunicaciones</a>
          <a class="brand" href="http://www.info.unlp.edu.ar" target="_blank">Facultad de Inform&aacute;tica</a>
          <a class="brand" href="http://www.unlp.edu.ar" target="_blank">UNLP</a>
        </div>
      </div>
    </div>

    <div class="container">

      <!-- Main hero unit for a primary marketing message or call to action -->
      <div class="hero-unit">
        <h2>Bienvenidos a Redes y Comunicaciones!</h2>
        <p>Este CD es parte de los enunciados pr&aacute;cticos de la materia Redes y Comunicaciones de la carrera de Licenciatura en Inform&aacute;tica de la UNLP para la cursada del presente a&ntilde;o y servir&aacute; como herramienta para la realizaci&oacute;n de los trabajos pr&aacute;cticos.</p>
      </div>

       <div class="row">
           <div class="span12">
                <h3>Acerca de la VM</h3>
                <p>Esta m&aacute;quina virtual est&aacute; basada en Debian GNU/Linux y fue creada por la c&aacute;tedra de Redes y Comunicaciones de la carrera de Licenciatura en Inform&aacute;tica de la UNLP para incluir las herramientas y configuraciones que se utilizar&aacute;n a lo largo de la cursada.</p>
                <p>Se ha configurado al usuario <em><strong>root</strong></em> y al usuario <em><strong>redes</strong></em> con la misma contrase&ntilde;a: <strong>redes</strong>.</p>
            </div>
       </div>
       <div class="row">
           <div class="span12">
             <h3>Ejercicios Pr&aacute;cticos</h3>
             <p>Todo el material se va a encontrar publicado en el sitio de la c&aacute;tedra en <a href="https://catedras.info.unlp.edu.ar/" target="_blank">https://catedras.info.unlp.edu.ar/</a>.</p>
            </div>
       </div>
      <div class="row">
          
        <div class="span2">
          <h4>Introducci&oacute;n</h4>
          <p>
             <ul>
                <li>Nociones b&aacute;sicas</li>
            </ul>
          </p>
        </div>
        <div class="span3">
          <h4>Capa de Aplicaci&oacute;n</h4>
          <p>
            <ul>
                <li><a href="http/protocolos.html">Protocolos HTTP</a></li>
                <li><a href="http/metodos.html">M&eacute;todos HTTP</a></li>
            </ul>
          </p>
       </div>
        <div class="span3">
          <h4>Capa de Transporte</h4>
          <p>
            <ul>
                <li>TCP</li>
                <li>UDP</li>
            </ul>
          </p>
        </div>
        <div class="span2">
          <h4>Capa de Red</h4>
          <p>
            <ul>
                <li>IP</li>
                <li>
                    Algoritmos de ruteo:<br/>
                    Topolog&iacute;as CORE:
                    <ul>
                        <li><a href="./core/1-ruteo-estatico.xml" target="_blank">Est&aacute;tico</a></li>
                        <li><a href="./core/2-ruteo-RIP.xml" target="_blank">RIP</a></li>
                        <li><a href="./core/3-ruteo-OSPF.xml" target="_blank">OSPF</a></li>
                    </ul>
                </li>
                <li>ICMP</li>
            </ul>
          </p>
        </div>
        <div class="span2">
          <h4>Capa de Enlace</h4>
            <p>
            <ul>
                <li>ARP</li>
                <li>
                    Switch - Hub
                </li>
            </ul>
            </p>
        </div>
      </div>

      <div class="row">
      <hr>
         <p>Desarrollado originalmente por Christian Rodriguez y Paula Venosa en el año 2007, modificado en 2013 por el grupo de desarrollo de Lihuen GNU/Linux y en 2016 y 2020 por Leandro Di Tommaso.</p>
        <br/>
      </div>
    </div> 
    
    </div>
    
    <div id="footer">
      <div class="container">
        <p class="muted credit">Redes y Comunicaciones</p>
      </div>
    </div>


  </body>
</html>
* Connection #0 to host www.redes.unlp.edu.ar left intact
10) a) No, no establece todas las cabeceras posibles porque se pueden utilizar cabeceras personalizadas, pero proporciona una lista de cabeceras estándar y comunes que se utilizan en el protocolo HTTP. Los desarrolladores pueden definir cabeceras según lo necesitado, pero se esperan que  se sigan las convenciones y estándares definidos en la RFC.
    b) 3 en el requerimiento y 7 en la respuesta.
    c) Si, la cabecera "Date" es una de la cabeceras definidas en la RFC. Esta indica la fecha y hora que se generó la solicitud o respuesta HTTP.
11) a) La primera línea brinda la versión de HTTP (HTTP/1.1), el código de estado 200 y la reason phrase (OK).
    b) 7
    c) Apache/2.4.56 (Unix)
    d) Si, lo indica el código 200.
    e) Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
12) En HTTP 1.0 El cliente se da cuenta de que ha recibido todo el objeto cuando el servidor cierra la conexión después de enviar la repuesta. En HTTP 1.1 en cambio se utiliza el encabezado "Content-Length" para indicar al cliente la longitud en bytes del objeto en la respuesta, permitiendo saber cuentos datos se esperan. El encabezado "Transfer-Encoding" con valor "chunked" divide la respuesta en trozos, y el cliente detecta el final de la respuesta cuándo recibe un trozo de tamaño 0.
13) 