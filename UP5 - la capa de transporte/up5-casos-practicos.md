

**Práctica de PT**: https://examenredes.com/14-8-1-packet-tracer-comunicaciones-de-tcp-y-udp-respuestas/ 

Test de Capa transporte

1. ¿Cuáles son los tres campos que se utilizan en el encabezado de un segmento UDP? (Elija tres).

Tamaño de la ventana
Longitud
Número de secuencia
Puerto de origen
Checksum
Número de acuse de recibo
Explique: Un encabezado UDP consta solamente de los campos Puerto de origen, Puerto de destino, Longitud y Checksum. Número de secuencia, Número de acuse de recibo y Tamaño de la ventana son campos de encabezado TCP.
2. ¿Cuáles son dos roles de la capa de transporte en la comunicación de datos en una red? (Escoja dos opciones).

Identificar la aplicación apropiada para cada transmisión de comunicación
Hacer un seguimiento de las transmisiones de comunicación individuales entre las aplicaciones en los hosts de origen y de destino.
proporcionar delimitación de tramas para identificar los bits que componen una trama
realizar una comprobación de redundancia cíclica en la trama para detectar errores
proporcionar la interfaz entre las aplicaciones y la red subyacente a través de la cual se transmiten los mensajes
Explique: La capa de transporte tiene muchas responsabilidades. Algunas de las principales incluyen lo siguiente:
Hacer un seguimiento de las transmisiones de comunicación individuales entre las aplicaciones en los hosts de origen y de destino.
Segmentar los datos en el origen y volverlos a armar en el destino.
Identificar la aplicación apropiada para cada transmisión de comunicación mediante el uso de números de puerto.
3. ¿Qué información utiliza TCP para rearmar y reordenar los segmentos recibidos?

Números de fragmento
Números de acuse de recibo
Números de secuencia
Números de puerto
Explique: En la capa de transporte, TCP utiliza los números de secuencia en el encabezado de cada segmento TCP para rearmar los segmentos en el orden correcto.
4. ¿Qué información importante se agrega al encabezado de la capa de transporte TCP/IP para asegurar la comunicación y la conectividad a un dispositivo de red remoto?

Direcciones físicas de destino y origen
Números de puerto de destino y origen
Direcciones de red lógicas de destino y origen
Temporización y sincronización
Explique: Los números de puerto de destino y origen se utilizan para identificar exactamente qué protocolo y qué proceso están realizando o respondiendo una solicitud.
5. ¿Cuáles son las dos características relacionadas con las sesiones UDP? Elija dos opciones.

Se realiza el seguimiento de los segmentos de datos transmitidos.
Se vuelven a transmitir los paquetes de datos de los que no se realizó el acuse de recibo.
Los dispositivos de destino reciben el tráfico con una demora mínima.
No se realiza el acuse de recibo de los datos recibidos.
Los dispositivos de destino rearman los mensajes y los transfieren a una aplicación.
Explique: TCP:
· Proporciona el seguimiento de los segmentos de datos transmitidos.
· Los dispositivos de destino realizan el acuse de recibo de los datos recibidos.
Los dispositivos de origen vuelven a transmitir los datos de los que no se realizó el acuse de recibo.
UDP
· Los dispositivos de destino no realizan el acuse de recibo de los datos recibidos.
· Los encabezados utilizan muy poca sobrecarga y provocan una demora mínima.

6. Una aplicación cliente necesita finalizar una sesión de comunicación TCP con un servidor. Coloque los pasos del proceso de finalización en el orden en que suceden. (No se utilizan todas las opciones.)

Módulos 14 - 15 Examen de comunicaciones de aplicaciones de red 9
Módulos 14 – 15 Examen de comunicaciones de aplicaciones de red 9
Explique: Para finalizar una sesión TCP, el cliente envía al servidor un segmento con el indicador FIN establecido. El servidor envía al cliente un segmento con el indicador ACK establecido para dar acuse de recibo. El servidor envía un FIN al cliente para terminar la sesión de servidor a cliente. El cliente envía un segmento con el indicador ACK establecido para dar acuse de recibo de la finalización.
7. ¿Cuál es el indicador del encabezado TCP que se utiliza en respuesta a un FIN recibido para finalizar la conectividad entre dos dispositivos de red?

RST
FIN
SYN
ACK
Explique: En una sesión TCP, cuando un dispositivo no tiene más datos para enviar, envía un segmento con el indicador FIN establecido. El dispositivo conectado que recibe el segmento responde con un indicador ACK para acusar el recibo de ese segmente. Luego, el dispositivo que envió el indicador ACK envía un mensaje FIN para cerrar la conexión que tiene con el otro dispositivo. El envío del FIN debe ir seguido de la recepción de un indicador ACK proveniente del otro dispositivo.
8. ¿Qué protocolo o servicio utiliza UDP para una comunicación cliente a servidor y TCP para la comunicación servidor a servidor?

HTTP
SMTP
FTP
DNS
Explique: Algunas aplicaciones pueden utilizar TCP y UDP. DNS utiliza UDP cuando los clientes envían solicitudes a un servidor DNS, y TCP cuando dos servidores DNS se comunican directamente.
9. ¿Qué clase de puerto se le debe solicitar a la IANA para utilizar con una aplicación específica?

Puerto privado
Puerto registrado
Puerto de origen
Puerto dinámico
Explique: La IANA asigna puertos registrados (del 1024 al 49151) a una entidad solicitante para que los utilice con procesos o aplicaciones específicos. Principalmente, estos procesos son aplicaciones individuales que el usuario elige instalar en lugar de aplicaciones comunes que recibiría un número de puerto conocido. Por ejemplo, Cisco registró el puerto 1985 para su proceso de protocolo de routing de reserva activa (HRSP).
10. ¿Cuáles son los tres protocolos de la capa de aplicación que utilizan TCP? Elija tres opciones.

SMTP
DHCP
TFTP
HTTP
FTP
SNMP
Explique: Algunos protocolos requieren el transporte de datos confiable que proporciona TCP. Además, estos protocolos no tienen requisitos de comunicación en tiempo real y pueden tolerar cierto grado de pérdida de datos mientras minimizan la sobrecarga de protocolo. Algunos ejemplos de estos protocolos son SMTP, FTP y HTTP.
11. ¿Cuáles son las tres afirmaciones que caracterizan el protocolo UDP? Elija tres opciones.

UDP proporciona funciones básicas sin conexión de la capa de transporte.
UDP proporciona mecanismos de control de flujo sofisticados.
UDP es un protocolo de sobrecarga baja que no proporciona mecanismo de control del flujo o secuenciación.
UDP proporciona un transporte de datos rápido y orientado a la conexión en la capa 3.
UDP depende del protocolo IP para la detección de errores y la recuperación.
UDP se basa en los protocolos de la capa de aplicación para la detección de errores.
Explique: UDP es un protocolo simple que proporciona las funciones básicas de la capa de transporte. Tiene una sobrecarga mucho menor que TCP ya que no está orientado a la conexión y no proporciona los mecanismos sofisticados de retransmisión, secuenciación y control del flujo que ofrecen confiabilidad.
12. ¿Qué dos campos se incluyen en el encabezado TCP pero no en el encabezado UDP? (Escoja dos opciones).

Puerto de origen
ventana
número de secuencia
Puerto de destino
checksum
Explique: El número de secuencia y los campos de ventana se incluyen en el encabezado TCP, pero no en el encabezado UDP.
13. ¿Qué campo en el encabezado TCP indica el estado del three-way handshake?

checksum
ventana
control bits
reservado
Explique: Los bits de control en el encabezado TCP indican el progreso y estado de la conexión.
14. ¿Cómo se utilizan los números de puerto en el proceso de encapsulación TCP/IP?

Los números de puerto de origen y de puerto de destino se generan aleatoriamente.
Los números de puerto de destino se asignan automáticamente y no se pueden cambiar.
Los números de puerto de origen y los números de puerto de destino no son necesarios cuando UDP es el protocolo de capa de transporte que se utiliza para la comunicación.
Si se producen varias conversaciones que utilizan el mismo servicio, el número de puerto de origen se utiliza para realizar un seguimiento de las conversaciones separadas.
Explique: Tanto UDP como TCP utilizan números de puerto para proporcionar un identificador único para cada conversación. Los números de puerto de origen se generan aleatoriamente y se utilizan para rastrear diferentes conversaciones. Los números de puerto de destino identifican servicios específicos mediante un número de puerto predeterminado para el servicio o un número de puerto asignado manualmente por un administrador del sistema.
15. ¿Qué tres afirmaciones describen un mensaje de descubrimiento de DHCP? (Elija tres).

Todos los hosts reciben el mensaje pero sólo responde un servidor de DHCP.
Solamente el servidor de DHCP recibe el mensaje.
La dirección IP de destino es 255.255.255.255.
El mensaje proviene de un cliente que busca una dirección IP.
El mensaje proviene de un servidor que ofrece una dirección IP.
La dirección MAC de origen tiene 48 bits (FF-FF-FF-FF-FF-FF).
Explique: Cuando un host configurado para utilizar DHCP se activa en una red, envía un mensaje DHCPDISCOVER. FF-FF-FF-FF-FF-FF es la dirección de broadcast de L2. Un servidor de DHCP responde al host con un mensaje unicast DHCPOFFER.
16. ¿Qué dos protocolos pueden utilizar los dispositivos en el proceso de solicitud que implica el envío de un correo electrónico? (Elija dos opciones).

IMAP
POP
HTTP
POP3
SMTP
DNS
Explique: Los protocolos POP, POP3 e IMAP se utilizan para recuperar mensajes de correo electrónico de los servidores. SMTP es el protocolo predeterminado que se utiliza para enviar correo electrónico. El servidor de correo electrónico del remitente puede utilizar DNS para encontrar la dirección del servidor de correo electrónico de destino.
17. Cual capa del modelo OSI proporcionar la interfaz entre las aplicaciones y la red subyacente a través de la cual se transmiten los mensajes?

Transporte
Presentación
Sesión
Aplicación
Explique: a capa de aplicación es la que se encuentra más cerca del usuario final y proporciona la interfaz entre aplicaciones y la red subyacente a través de la cual se transmiten los mensajes.
18. ¿Cuál de las siguientes es una característica clave del modelo de red entre pares?

Impresión en red por medio de un servidor de impresión
Redes sociales sin Internet
Uso compartido de recursos sin un servidor exclusivo
Red inalámbrica
Explique: El modelo de red entre pares (P2P) admite el uso compartido de datos, impresoras y recursos sin un servidor exclusivo.
19. La capa de aplicación del modelo TCP/IP realiza las funciones de tres capas del modelo OSI. ¿De cuáles? Elija tres opciones.

Transporte
Sesión
Red
Aplicación
Enlace de datos
Física
Presentación
Explique: La capa de acceso a la red del modelo TCP/IP realiza las mismas funciones que las capas física y de enlace de datos del modelo OSI. La capa de interconexión de redes equivale a la capa de red del modelo OSI. Las capas de transporte son iguales en ambos modelos. La capa de aplicación del modelo TCP/IP representa las capas de sesión, presentación y aplicación del modelo OSI.
20. ¿Cuál es la capa del modelo TCP/IP que se utiliza para dar formato a los datos, comprimirlos y cifrarlos?

Acceso a la red
Interconexión de redes
Aplicación
Sesión
Presentación
Explique: La capa de aplicación del modelo TCP/IP realiza las funciones de tres capas del modelo OSI: aplicación, presentación y sesión. La capa de aplicación del modelo TCP/IP proporciona la interfaz entre las aplicaciones, es responsable de dar formato a los datos, comprimirlos y cifrarlos, y se utiliza para crear y mantener diálogos entre las aplicaciones de origen y de destino.
21. Una compañía fabricante se suscribe a ciertos servicios alojados por parte de su ISP. Entre los servicios requeridos, se incluyen el alojamiento web, la transferencia de archivos y el correo electrónico. ¿Qué protocolos representan estas tres aplicaciones clave? Elija tres opciones.

DHCP
SMTP
FTP
SNMP
HTTP
DNS
Explique: El ISP utiliza el protocolo HTTP junto con el alojamiento de páginas web, el protocolo FTP con las transferencias de archivos y el protocolo SMTP con el correo electrónico. DNS se utiliza para traducir nombres de dominio en direcciones IP. SNMP se utiliza para el tráfico de administración de redes. DHCP se utiliza, normalmente, para administrar la asignación de direcciones IP.
22. ¿Qué protocolo de la capa de aplicación utiliza mensajes de tipo GET, PUT y POST?

SMTP
POP3
DHCP
HTTP
DNS
Explique: El comando GET es una solicitud de datos de un servidor web por parte de un cliente. El comando PUT carga recursos y contenido, como imágenes, a un servidor web. El comando POST carga archivos de datos a un servidor web.
23. ¿Cuáles son los tres protocolos que funcionan en la capa de aplicación del modelo TCP/IP? (Elija tres opciones).

DHCP
FTP
POP3
TCP
ARP
UDP
Explique: FTP, DHCP y POP3 son protocolos de la capa de aplicación. TCP y UDP son protocolos de la capa de transporte. ARP es un protocolo de la capa de red.
24. ¿Cuál de estas situaciones describe una función proporcionada por la capa de transporte?

Un estudiante reproduce una película corta con sonido basada en Web. La película y el sonido están codificados dentro del encabezado de la capa de transporte.
Un alumno utiliza un teléfono VoIP del aula para llamar a su casa. El identificador único grabado en el teléfono es una dirección de capa de transporte utilizada para establecer contacto con otro dispositivo de red en la misma red.
Un alumno tiene dos ventanas de explorador Web abiertas a fin de acceder a dos sitios Web. La capa de transporte garantiza que se entregue la página Web correcta a la ventana de explorador adecuada.
Un trabajador de una empresa accede a un servidor Web ubicado en una red corporativa. La capa de transporte da formato a la pantalla para que la página Web se visualice de manera adecuada, independientemente del dispositivo que se utilice para ver el sitio Web.
Explique: Los números de puerto de origen y de destino se utilizan para identificar la aplicación y la ventana correctas en esa aplicación.
25. ¿Cuáles son las tres capas del modelo OSI que proporcionan servicios de red similares a los que proporciona la capa de aplicación del modelo TCP/IP? (Elija tres).

Capa de enlace de datos
Capa de presentación
Capa de transporte
Capa de aplicación
Capa física
Capa de sesión
Explique: Las tres capas superiores del modelo OSI, es decir, las capas de sesión, de presentación y de aplicación, proporcionan servicios de aplicación similares a los que brinda la capa de aplicación del modelo TCP/IP. Las capas inferiores del modelo OSI se relacionan más con el flujo de datos.
26. Un cliente crea un paquete para enviar a un servidor. El cliente está solicitando el servicio SSH. ¿Qué número se utilizará como número de puerto de destino en el paquete de envío?

69
67
22
80
27. Un equipo que se está comunicando con un servidor web tiene un tamaño de ventana TCP de 6.000 bytes al enviar datos y un tamaño de paquete de 1.500 bytes. ¿Qué byte de información confirmará el servidor web después de haber recibido tres paquetes de datos del PC?

4501
3000
6001
6000
28. ¿Cuál de los siguientes es un ejemplo de comunicación de red que utiliza el modelo cliente-servidor?

Una estación de trabajo inicia una solicitud de DNS cuando el usuario escribe www.cisco.com en la barra de direcciones de un explorador Web.
Un usuario imprime un documento con una impresora conectada por cable a la estación de trabajo de un compañero.
Un usuario utiliza eMule para descargar un archivo compartido por un amigo después de que se determina la ubicación del archivo.
Una estación de trabajo inicia un protocolo ARP para encontrar la dirección MAC del host receptor.
29. ¿En qué modelo de red se utilizarían eDonkey, eMule, BitTorrent, Bitcoin y LionShare?

Basada en clientes
Red entre pares
Punto a punto
Maestro/esclavo
Explique: En el modelo de red entre pares (P2P), se intercambian datos entre dos dispositivos de red sin utilizar un servidor exclusivo. Las aplicaciones entre pares como Shareaz, eDonkey y Bitcoin permiten que un dispositivo de red asuma el rol de servidor, mientras que uno o más dispositivos de red asumen el rol de cliente usando la aplicación peer-to-peer.
30. ¿Qué aplicaciones o servicios permiten que los hosts actúen como cliente y servidor al mismo tiempo?

aplicaciones de correo electrónico
Aplicaciones P2P
Aplicaciones de cliente-servidor
Servicios de autenticación
31. ¿Cuál es la función del mensaje HTTP GET?

Recuperar el correo electrónico del cliente desde un servidor de correo electrónico mediante el puerto TCP 110.
Cargar contenido de un cliente web a un servidor web.
Enviar información de errores de un servidor web a un cliente web.
Solicitar una página HTML de un servidor web.
32. ¿Qué protocolo utiliza un cliente para comunicarse en forma segura con el servidor web?

SMTP
HTTPS
IMAP
SMB
33. Una PC está descargando un archivo grande de un servidor. La ventana TCP es de 1000 bytes. El servidor envía el archivo utilizando segmentos de100 bytes. ¿Cuántos segmentos enviará el servidor antes de requerir un acuse de recibo de la PC?

10 segmentos
100 segmentos
1000 segmentos
1 segmento
Explique: Con una ventana de 1000 bytes, el host de destino acepta segmentos hasta que se hayan recibido los 1000 bytes de datos. Luego, el host de destino envía un acuse de recibo.
34. ¿Cuál de las siguientes es una característica de UDP?

UDP solamente transfiere los datos a la red cuando el destino está listo para recibirlos.
Las aplicaciones que utilizan UDP siempre se consideran poco confiables.
Los datagramas UDP pueden tomar la misma ruta y llegar al destino en el orden correcto.
UDP rearma los datagramas recibidos en el orden en que se recibieron.
Explique: UDP no tiene manera de reordenar los datagramas por orden de transmisión, por lo que, simplemente, los rearma en el orden en que se recibieron y los reenvía a la aplicación.
35. ¿Por qué HTTP utiliza TCP como protocolo de la capa de transporte?

Porque se pueden tolerar fácilmente errores de transmisión.
Porque HTTP es un protocolo de máximo esfuerzo.
Porque HTTP requiere entrega confiable.
Para asegurar la mayor velocidad de descarga posible.
Explique: Cuando un host solicita una página Web, se deben garantizar la confiabilidad y la integridad de la transmisión. Por lo tanto, HTTP utiliza TCP como protocolo de la capa de transporte.
36. ¿Qué tipos de aplicaciones son los más adecuados para el uso de UDP? (Escoja dos opciones).

Las aplicaciones que necesitan una entrega confiable
Aplicaciones que pueden tolerar cierta pérdida de datos, pero requieren demoras breves o que no haya demoras.
aplicaciones que necesitan el reordenamiento de segmentos
aplicaciones que manejan la confiabilidad por su cuenta.
aplicaciones que necesitan control de flujo de datos
Explique: Las aplicaciones que pueden tolerar cierta pérdida de datos, requieren una solicitudes y respuestas simples, y manejan la fiabilidad por sí mismas son las más adecuadas para UDP. UDP tiene una sobrecarga baja y no requiere confiabilidad. TCP proporciona servicios de confiabilidad, control del flujo de datos y reordenamiento de segmentos.
37. ¿Cuáles de las siguientes son tres responsabilidades de la capa de transporte? (Elija tres opciones.)

Identificar las aplicaciones y los servicios que deben manejar los datos transmitidos en el servidor y el cliente.
Dar a los datos un formato compatible para que los reciban los dispositivos de destino.
Realizar una detección de errores del contenido de las tramas.
Cumplir con los requisitos de confiabilidad de las aplicaciones, si corresponde.
Dirigir paquetes hacia la red de destino.
Realizar la multiplexación de varias transmisiones de comunicación desde muchos usuarios o aplicaciones en la misma red.
Explique: La capa de transporte tiene muchas responsabilidades. Algunas de las principales incluyen lo siguiente:
Hacer un seguimiento de las transmisiones de comunicación individuales entre las aplicaciones en los hosts de origen y de destino.
Segmentar los datos en el origen y volverlos a armar en el destino.
Identificar la aplicación apropiada para cada transmisión de comunicación mediante el uso de números de puerto.
Realizar la multiplexación de las comunicaciones de varios usuarios o aplicaciones en una misma red.
Administrar los requisitos de confiabilidad de las aplicaciones.
