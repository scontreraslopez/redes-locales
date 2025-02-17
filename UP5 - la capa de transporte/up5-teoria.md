# UP5. La capa de transporte

## Índice

1. [Funciones de la Capa de Transporte](#1-funciones-de-la-capa-de-transporte)
2. [Transmission Control Protocol (TCP)](#2-transmission-control-protocol-tcp)
    - [Características de TCP](#1-características-de-tcp)
    - [Encabezado TCP](#2-encabezado-tcp)
    - [Campos de encabezado TCP](#3-campos-de-encabezado-tcp)
    - [Aplicaciones que usan TCP](#4-aplicaciones-que-usan-tcp)
    - [Verifica tu comprensión – Descripción general de TCP](#5-verifica-tu-comprensión--descripción-general-de-tcp)
    - [Procesos del Servidor TCP](#1-procesos-del-servidor-tcp)
    - [Establecimiento de Conexión TCP](#2-establecimiento-de-conexión-tcp)
    - [Terminación de Sesión](#3-terminación-de-sesión)
    - [Análisis del Enlace de Tres Vías TCP](#4-análisis-del-enlace-de-tres-vías-tcp)
    - [Vídeo: Protocolo de Enlace TCP de 3 Vías](#5-vídeo-protocolo-de-enlace-tcp-de-3-vías)
    - [Comprueba tu comprensión – Proceso de comunicación TCP](#6-comprueba-tu-comprensión--proceso-de-comunicación-tcp)
    - [Fiabilidad de TCP: Entrega Garantizada y Ordenada](#1-fiabilidad-de-tcp-entrega-garantizada-y-ordenada)
    - [Vídeo: Confiabilidad de TCP: Números de Secuencia y Acuses de Recibo](#2-vídeo-confiabilidad-de-tcp-números-de-secuencia-y-acuses-de-recibo)
    - [Fiabilidad de TCP: Pérdida y Retransmisión de Datos](#3-fiabilidad-de-tcp-pérdida-y-retransmisión-de-datos)
    - [Vídeo: Confiabilidad de TCP: Pérdida y Retransmisión de Datos](#4-vídeo-confiabilidad-de-tcp-pérdida-y-retransmisión-de-datos)
    - [Control de flujo TCP: tamaño de ventana y agradecimientos](#5-control-de-flujo-tcp-tamaño-de-ventana-y-agradecimientos)
    - [Control de flujo TCP: Tamaño Máximo de Segmento (MSS)](#6-control-de-flujo-tcp-tamaño-máximo-de-segmento-mss)
    - [Control de Flujo TCP: Evitar la Congestión](#7-control-de-flujo-tcp-evitar-la-congestión)
    - [Comprueba tu Comprensión – Fiabilidad y Control de Flujo](#8-comprueba-tu-comprensión--fiabilidad-y-control-de-flujo)
3. [User Datagram Protocol (UDP)](#3-user-datagram-protocol-udp)
    - [Protocolo Adecuado de Capa de Transporte para la Aplicación Correcta](#6-protocolo-adecuado-de-capa-de-transporte-para-la-aplicación-correcta)
    - [Comprueba tu comprensión – Transporte de datos](#7-comprueba-tu-comprensión--transporte-de-datos)
    - [Comparación de Baja Sobrecarga y Confiabilidad de UDP](#1-comparación-de-baja-sobrecarga-y-confiabilidad-de-udp)
    - [Reensamblaje de Datagramas UDP](#2-reensamblaje-de-datagramas-udp)
    - [Procesos y Solicitudes del Servidor UDP](#3-procesos-y-solicitudes-del-servidor-udp)
    - [Procesos de Cliente UDP](#4-procesos-de-cliente-udp)
    - [Comprueba tu comprensión – Comunicación UDP](#5-comprueba-tu-comprensión--comunicación-udp)
4. [Otros protocolos Emergentes](#4-otros-protocolos-emergentes)
5. [Manejo Avanzado de Congestión y Control de Flujo](#3-manejo-avanzado-de-congestión-y-control-de-flujo)
6. [Impacto de Tecnologías Emergentes](#4-impacto-de-tecnologías-emergentes)
    - [Internet de las Cosas (IoT)](#internet-de-las-cosas-iot)
    - [Redes 5G y Futuras Generaciones](#redes-5g-y-futuras-generaciones)
    - [Protocolo Rápido de Internet basado en UDP (QUIC)](#41-protocolo-rápido-de-internet-basado-en-udp-quic)
    - [Stream Control Transmission Protocol (SCTP)](#42-stream-control-transmission-protocol-sctp)
7. [Seguridad Integrada en la Capa de Transporte](#5-seguridad-integrada-en-la-capa-de-transporte)
    - [TLS (Transport Layer Security) y SSL (Secure Sockets Layer)](#tls-transport-layer-security-y-ssl-secure-sockets-layer)
8. [PDU de la Capa de Transporte](#5-pdu-de-la-capa-de-transporte)
    - [Estructura General de un Segmento TCP](#estructura-general-de-un-segmento-tcp)
9. [Metáforas para Facilitar la Comprensión](#6-metáforas-para-facilitar-la-comprensión)
10. [Conclusión](#9-conclusión)
11. [Puertos: Identificando Procesos en Comunicación](#12-puertos-identificando-procesos-en-comunicación)
    - [Comunicaciones Múltiples Separadas](#1-comunicaciones-múltiples-separadas)
    - [Pares de Socket](#2-pares-de-socket)
    - [Grupos de número de puerto](#3-grupos-de-número-de-puerto)
    - [El Comando netstat](#4-el-comando-netstat)
    - [Verifica tu comprensión – Números de puerto](#5-verifica-tu-comprensión--números-de-puerto)
12. [Referencias](#referencias)

## 1. Funciones de la Capa de Transporte

Los programas de capa de aplicación generan datos que deben intercambiarse entre los hosts de origen y de destino. La capa de transporte es responsable de las comunicaciones lógicas entre las aplicaciones que se ejecutan en diferentes hosts. Esto puede incluir servicios como el establecimiento de una sesión temporal entre dos hosts y la transmisión confiable de información para una aplicación.

Como se muestra en la imagen, la capa de transporte es el enlace entre la capa de aplicación y las capas inferiores, que son responsables de la transmisión de la red. Las diferentes aplicaciones tienen diferentes requisitos de fiabilidad de transporte. Por lo tanto, TCP/IP proporciona los siguientes dos protocolos de capa de transporte

![Protocolos de capa de transporte](https://ccnadesdecero.es/wp-content/uploads/2017/11/Protocolos-de-capa-de-transporte.png)

IP solo se refiere a la estructura, direccionamiento y enrutamiento de paquetes. IP no especifica cómo se realiza la entrega o el transporte de los paquetes. Los protocolos de la capa de transporte especifican cómo transferir mensajes entre hosts y son responsables de administrar los requisitos de confiabilidad de una conversación. La capa de transporte incluye los protocolos TCP y UDP.

La **capa de transporte** actúa como un puente esencial entre las capas de red y las orientadas a la aplicación, facilitando una comunicación eficiente y confiable entre procesos que se ejecutan en diferentes máquinas.

En un dispositivo terminal pueden ejecutarse múltiples **procesos** simultáneamente. Un proceso es una instancia en ejecución de una aplicación. Algunos programas permiten múltiples instancias concurrentes, cada una considerada un proceso distinto. Estos procesos necesitan comunicarse con procesos en otros dispositivos, y la capa de transporte facilita esta comunicación de extremo a extremo.

En líneas generales, las **funciones clave de la Capa de Transporte** son las siguientes:

- **Segmentación y Reensamblado**: Divide los datos de las aplicaciones en segmentos adecuados para la transmisión y los reensambla en el destino.
- **Multiplexación y Demultiplexación**: Permite que múltiples procesos utilicen simultáneamente la red, identificando de manera única cada conexión mediante números de puerto.
- **Control de Flujo**: Gestiona la velocidad de envío de datos para prevenir la saturación del receptor.
- **Control de Congestión**: Regula el tráfico en la red para evitar y recuperarse de congestiones.
- **Entrega Confiable**: Asegura la entrega correcta y en orden de los segmentos, detectando y retransmitiendo los que se pierden.
- **Establecimiento de Sesión**: Crea, mantiene y cierra conexiones entre procesos en dispositivos distintos.

## 2. Transmission Control Protocol (TCP)

**TCP** es un protocolo orientado a conexión que proporciona comunicación fiable:

- **Establecimiento de Conexión**: Utiliza un proceso de *handshake* de tres vías para iniciar la comunicación.
- **Entrega Fiable y Ordenada**: Garantiza que los datos lleguen sin errores y en el orden correcto.
- **Control de Flujo y Congestión**: Ajusta el envío de datos según la capacidad del receptor y las condiciones de la red.
- **Características Adicionales**: Soporta retransmisiones, control de duplicados y temporización.

**TCP** es algo así como enviar una carta certificada. El remitente recibe confirmación de que la carta ha sido entregada, y si se pierde, se envía de nuevo. Es seguro, pero puede ser más lento debido a los protocolos de confirmación. Así, el transporte TCP es análogo a un envío que se rastrea desde el origen hasta el destino, incluso si este envío se divide en varios paquetes, llamados segmentos en TCP.

TCP se considera un protocolo de capa de transporte confiable y con todas las funciones, que garantiza que todos los datos lleguen al destino. TCP incluye campos que aseguran la entrega de los datos de la aplicación. Estos campos requieren un procesamiento adicional por parte de los hosts de envío y recepción. Para mantener el estado de una conversación y rastrear la información, TCP primero debe establecer una conexión entre el remitente y el receptor. Es por eso que TCP se conoce como un protocolo orientado a la conexión.

![Protocolo de Control de Transmisión TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Protocolo-de-Control-de-Transmisi%C3%B3n-TCP.png)

TCP proporciona confiabilidad y control de flujo utilizando estas operaciones básicas:

- Numerar y rastrear segmentos de datos transmitidos a un host específico desde una aplicación específica.
- Confirmar datos recibidos.
- Volver a transmitir cualquier información no reconocida después de un cierto período de tiempo.
- Secuenciar datos que pueden llegar en orden incorrecto.
- Enviar datos a una velocidad eficiente que sea aceptable para el receptor.

### 2.1. Características de TCP

Además de admitir las funciones básicas de segmentación y reensamblado de datos, TCP también proporciona los siguientes servicios:

- **Establece una sesión**: TCP es un protocolo orientado a la conexión que negocia y establece una conexión permanente (o sesión) entre los dispositivos de origen y destino antes de reenviar cualquier tráfico. A través del establecimiento de la sesión, los dispositivos negocian la cantidad de tráfico que se puede reenviar en un momento dado, y los datos de comunicación entre los dos se pueden administrar de cerca.
- **Garantiza una entrega confiable**: Por muchas razones, es posible que un segmento se corrompa o se pierda por completo, ya que se transmite a través de la red. TCP asegura que cada segmento que envía la fuente llega al destino.
- **Proporciona entrega en el mismo orden**: Dado que las redes pueden proporcionar múltiples rutas que pueden tener diferentes velocidades de transmisión, los datos pueden llegar en el orden incorrecto. Al numerar y secuenciar los segmentos, TCP garantiza que los segmentos se vuelvan a ensamblar en el orden correcto.
- **Admite control de flujo**: Los hosts de red tienen recursos limitados (es decir, memoria y potencia de procesamiento). Cuando TCP es consciente de que estos recursos están sobrecargados, puede solicitar que la aplicación de envío reduzca la velocidad del flujo de datos. Esto se hace mediante TCP que regula la cantidad de datos que transmite la fuente. El control de flujo puede evitar la necesidad de retransmitir los datos cuando los recursos del host receptor se ven desbordados.

Para obtener más información sobre TCP, busca en Internet el RFC 793.

### 2.2. Encabezado TCP

TCP es un protocolo con estado, lo que significa que realiza un seguimiento del estado de la sesión de comunicación. Para rastrear el estado de una sesión, TCP registra qué información ha enviado y qué información ha sido reconocida. La sesión con estado comienza con el establecimiento de la sesión y termina con la finalización de la sesión.

Un segmento TCP agrega 20 bytes (es decir, 160 bits) de sobrecarga al encapsular los datos de la capa de aplicación. La imagen muestra los campos en un encabezado TCP.

![Encabezado TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Encabezado-TCP.png)

#### 2.2.1. Campos de encabezado TCP

La tabla identifica y describe los diez campos en un encabezado TCP.

| Campo de encabezado TCP | Descripción |
|------------------------|-----------------------------------------------------------------------------|
| Puerto de origen       | Un campo de 16 bits utilizado para identificar la aplicación de origen por número de puerto. |
| Puerto de destino      | Un campo de 16 bits utilizado para identificar la aplicación de destino por número de puerto. |
| Secuencia de números   | Un campo de 32 bits utilizado para fines de reensamblado de datos.           |
| Número de acuse de recibo | Un campo de 32 bits utilizado para indicar que se han recibido datos y que se espera el siguiente byte de la fuente. |
| Longitud del encabezado | Un campo de 4 bits conocido como “desplazamiento de datos” que indica la longitud del encabezado del segmento TCP. |
| Reservado              | Un campo de 6 bits que está reservado para uso futuro.                      |
| Bits de control        | Un campo de 6 bits utilizado que incluye códigos de bits o banderas, que indican el propósito y la función del segmento TCP. |
| Tamaño de ventana      | Un campo de 16 bits utilizado para indicar el número de bytes que se pueden aceptar a la vez. |
| Suma de comprobación    | Un campo de 16 bits utilizado para la verificación de errores del encabezado y los datos del segmento. |
| Urgente                | Un campo de 16 bits utilizado para indicar si los datos contenidos son urgentes. |
| Opciones               | Un campo de longitud variable utilizado para varios propósitos, como el ajuste del tamaño máximo de segmento (MSS) y el uso de timestamps. |

### 2.3. Aplicaciones que usan TCP

TCP es un buen ejemplo de cómo las diferentes capas del conjunto de protocolos TCP/IP tienen roles específicos. TCP maneja todas las tareas asociadas con la división del flujo de datos en segmentos, proporcionando confiabilidad, controlando el flujo de datos y reordenando segmentos. TCP libera a la aplicación de tener que administrar cualquiera de estas tareas. Las aplicaciones, como las que se muestran en la figura, simplemente pueden enviar el flujo de datos a la capa de transporte y utilizar los servicios de TCP.

![Aplicaciones que usan TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Aplicaciones-que-usan-TCP.png)


5. Verifica tu comprensión – Descripción general de TCP
Comprueba tu comprensión de TCP eligiendo la MEJOR respuesta a las siguientes preguntas.

¿Qué protocolo de capa de transporte garantiza la entrega fiable del mismo pedido?
ICMP
IP
TCP
UDP
Ver también
CCNA 1
MAC e IP Red local y remota
MAC e IP
¿Qué enunciado de encabezado TCP es verdadero?
Se compone de 4 campos en un encabezado de 8 bytes.
Se compone de 8 campos en un encabezado de 10 bytes.
Se compone de 10 campos en un encabezado de 20 bytes.
Se compone de 20 campos en un encabezado de 40 bytes.
¿Qué dos aplicaciones usarían el protocolo de capa de transporte TCP? (Escoja dos opciones).
FTP
HTTP
ICMP
TFTP
VoIP

https://ccnadesdecero.es/proceso-de-comunicacion-tcp/

1. Procesos del Servidor TCP
Ya conoces los fundamentos de TCP. Comprender el papel de los números de puerto te ayudará a comprender los detalles del proceso de comunicación TCP. En este tema, también aprenderás acerca de los procesos de enlace de tres vías TCP y terminación de sesión.

Cada proceso de aplicación que se ejecuta en un servidor está configurado para usar un número de puerto. El número de puerto se asigna automáticamente o se configura manualmente por un administrador del sistema.

Un servidor individual no puede tener dos servicios asignados al mismo número de puerto dentro de los mismos servicios de capa de transporte. Por ejemplo, un host que ejecuta una aplicación de servidor web y una aplicación de transferencia de archivos no puede tener ambos configurados para usar el mismo puerto, como el puerto TCP 80.

Una aplicación de servidor activa asignada a un puerto específico se considera abierta, lo que significa que la capa de transporte acepta y procesa segmentos dirigidos a ese puerto. Se acepta cualquier solicitud de cliente entrante dirigida al socket correcto, y los datos se pasan a la aplicación del servidor. Puede haber muchos puertos abiertos simultáneamente en un servidor, uno para cada aplicación de servidor activa.

Clientes que envían solicitudes TCP
Solicitar puertos de destino
Solicitar puertos de origen
Respuesta Puertos de destino
Respuesta Puertos de origen
El cliente 1 solicita servicios web y el cliente 2 solicita servicio de correo electrónico utilizando puertos conocidos (es decir, servicios web es puerto 80, servicios de correo electrónico es puerto 25).

Clientes envían solicitudes TCP
Clientes envían solicitudes TCP
2. Establecimiento de Conexión TCP
En algunas culturas, cuando dos personas se encuentran, a menudo se saludan dándose la mano. Ambas partes entienden el acto de estrechar la mano como una señal de saludo amistoso. Las conexiones en la red son similares. En las conexiones TCP, el cliente host establece la conexión con el servidor mediante el proceso de enlace de tres vías (three-way handshake).

Paso 1. SYN
Paso 2. ACK y SYN
Paso 3. ACK
El cliente que inicia solicita una sesión de comunicación de cliente a servidor con el servidor.

Paso 1 SYN
Paso 1 SYN
El protocolo de enlace de tres vías valida que el host de destino esté disponible para comunicarse. En este ejemplo, el host A ha validado que el host B está disponible.

3. Terminación de Sesión
Para cerrar una conexión, el indicador de control Finish (FIN) debe establecerse en el encabezado del segmento. Para finalizar cada sesión TCP unidireccional, se utiliza un protocolo de enlace bidireccional, que consta de un segmento FIN y un segmento de acuse de recibo (ACK). Por lo tanto, para finalizar una sola conversación compatible con TCP, se necesitan cuatro intercambios para finalizar ambas sesiones. Tanto el cliente como el servidor pueden iniciar la terminación.

En el ejemplo, los términos cliente y servidor se utilizan como referencia por simplicidad, pero dos hosts que tengan una sesión abierta pueden iniciar el proceso de finalización.

Haga clic en cada botón para obtener más información sobre los pasos de finalización de la sesión.

Paso 1. FIN
Paso 2. ACK
Paso 3. FIN
Paso 4. ACK
Cuando el cliente no tiene más datos para enviar en la secuencia, envía un segmento con el indicador FIN establecido.

Paso 1 FIN
Paso 1 FIN
Cuando todos los segmentos han sido reconocidos, la sesión se cierra.

Ver también
CCNA 1

Direccionamiento de Red IPv6
4. Análisis del Enlace de Tres Vías TCP
Los hosts mantienen el estado, rastrean cada segmento de datos dentro de una sesión e intercambian información sobre qué datos se reciben utilizando la información en el encabezado TCP. TCP es un protocolo full-duplex, donde cada conexión representa dos sesiones de comunicación unidireccionales. Para establecer la conexión, los hosts realizan un protocolo de enlace de tres vías. Como se muestra en la imagen, los bits de control en el encabezado TCP indican el progreso y el estado de la conexión.

Estas son las funciones del apretón de manos de tres vías:

Establece que el dispositivo de destino está presente en la red.
Verifica que el dispositivo de destino tenga un servicio activo y esté aceptando solicitudes en el número de puerto de destino que el cliente iniciador pretende utilizar.
Informa al dispositivo de destino que el cliente de origen tiene la intención de establecer una sesión de comunicación en ese número de puerto.
Una vez completada la comunicación, las sesiones se cierran y la conexión finaliza. Los mecanismos de conexión y sesión permiten la función de confiabilidad TCP.

Campo de bits de control
Se muestra los campos de encabezado del segmento TCP con el campo de bits de control de 6 bits resaltado
Los seis bits en el campo Bits de control del encabezado del segmento TCP también se conocen como banderas. Una bandera es un bit que está activado o desactivado.

Los seis indicadores de bits de control son los siguientes:

URG: campo de puntero urgente significativo
ACK: indicador de reconocimiento utilizado en el establecimiento de la conexión y la finalización de la sesión
PSH: función de empuje
RST: restablece la conexión cuando se produce un error o un tiempo de espera
SYN: sincroniza los números de secuencia utilizados en el establecimiento de la conexión
FIN: no hay más datos del remitente y se utilizan en la finalización de la sesión
5. Vídeo: Protocolo de Enlace TCP de 3 Vías
Haz clic en Reproducir en la figura para ver una demostración en video del protocolo de enlace TCP de 3 vías, utilizando Wireshark.


6. Comprueba tu comprensión – Proceso de comunicación TCP
Verifica tu comprensión del proceso de comunicación TCP eligiendo la MEJOR respuesta a las siguientes preguntas.

¿Cuáles de los siguientes puertos serían válidos de origen y destino para un host que se conecta a un servidor de correo electrónico?
A. Origen: 25, Destino: 49152
B. Origen: 80, Destino: 49152
C. Origen: 49152, Destino: 25
D. Origen: 49152, Destino: 80
¿Qué indicadores de bits de control se utilizan durante el apretón de manos de tres vías?
A. ACK y FIN
B. FIN y RESET
C. RESET y SYN
D. SYN y ACK
¿Cuántos intercambios se necesitan para finalizar ambas sesiones entre dos hosts?
A. un intercambio
B. dos intercambios
C. tres intercambios
D. cuatro intercambios
E. cinco intercambios


https://ccnadesdecero.es/fiabilidad-y-control-de-flujo-tcp/


1. Fiabilidad de TCP: Entrega Garantizada y Ordenada
Puede haber ocasiones en que los segmentos TCP no lleguen a su destino. Otras veces, los segmentos TCP pueden llegar fuera de servicio. Para que el destinatario entienda el mensaje original, se deben recibir todos los datos y los datos de estos segmentos deben volver a ensamblarse en el pedido original. Los números de secuencia se asignan en el encabezado de cada paquete para lograr este objetivo. El número de secuencia representa el primer byte de datos del segmento TCP.

Durante la configuración de la sesión, se establece un número de secuencia inicial (ISN). Este ISN representa el valor inicial de los bytes que se transmiten a la aplicación receptora. A medida que los datos se transmiten durante la sesión, el número de secuencia se incrementa por el número de bytes que se han transmitido. Este seguimiento de bytes de datos permite que cada segmento se identifique y reconozca de forma única. Los segmentos faltantes se pueden identificar.

El ISN no comienza en uno, pero es efectivamente un número aleatorio. Esto es para prevenir ciertos tipos de ataques maliciosos. Para simplificar, utilizaremos un ISN de 1 para los ejemplos de este capítulo.

Los números de secuencia de segmento indican cómo volver a armar y reordenar los segmentos recibidos, como se muestra en la imagen.

Segmentos TCP se reordenan en destino
Segmentos TCP se reordenan en destino: Aunque los segmentos pueden tomar diferentes rutas y llegar fuera de servicio al destino, TCP tiene la capacidad de reordenar los segmentos
El proceso TCP receptor coloca los datos de un segmento en un búfer receptor. Los segmentos se colocan en el orden de secuencia adecuado y se pasan a la capa de aplicación cuando se vuelven a montar. Los segmentos que llegan con números de secuencia que están fuera de servicio se retienen para su posterior procesamiento. Luego, cuando llegan los segmentos con los bytes faltantes, estos segmentos se procesan en orden.

2. Vídeo: Confiabilidad de TCP: Números de Secuencia y Acuses de Recibo
Una de las funciones de TCP es garantizar que cada segmento llegue a su destino. Los servicios TCP en el host de destino reconocen los datos que ha recibido la aplicación de origen.

Haz clic en Reproducir en la figura para ver una lección acerca de los números de secuencia y los acuses de recibo del TCP.


3. Fiabilidad de TCP: Pérdida y Retransmisión de Datos
No importa cuán bien diseñada esté una red, ocasionalmente se produce pérdida de datos. TCP proporciona métodos para gestionar estas pérdidas de segmento. Entre estos se encuentra un mecanismo para retransmitir segmentos para datos no reconocidos.

Antes de las mejoras posteriores, TCP solo podía reconocer el siguiente byte esperado. Por ejemplo, en la imagen, usando los números de segmento para simplificar, el host A envía los segmentos 1 a 10 al host B. Si todos los segmentos llegan excepto los segmentos 3 y 4, el host B responderá con acuse de recibo especificando que el siguiente segmento esperado es el segmento 3. El host A no tiene idea de si llegaron otros segmentos o no. El host A, por lo tanto, reenviaría los segmentos 3 a 10. Si todos los segmentos reenviados llegaran con éxito, los segmentos 5 a 10 serían duplicados. Esto puede provocar demoras, congestión e ineficiencias.

Segmentos duplicados
Segmentos duplicados
Los sistemas operativos host de hoy en día suelen emplear una función TCP opcional llamada reconocimiento selectivo (SACK), negociada durante el protocolo de enlace de tres vías. Si ambos hosts admiten SACK, el receptor puede reconocer explícitamente qué segmentos (bytes) se recibieron, incluidos los segmentos discontinuos. Por lo tanto, el host emisor solo necesitaría retransmitir los datos faltantes. Por ejemplo, en la siguiente imagen, nuevamente usando números de segmento para simplificar, el host A envía los segmentos 1 a 10 al host B. Si todos los segmentos llegan excepto los segmentos 3 y 4, el host B puede confirmar que ha recibido los segmentos 1 y 2 (ACK 3) y reconoce selectivamente los segmentos 5 a 10 (SACK 5-10). El host A solo necesitaría reenviar los segmentos 3 y 4.

Segmentos sin duplicar
Segmentos sin duplicar
Nota: TCP normalmente envía ACK para cualquier otro paquete, pero otros factores que están más allá del alcance de este tema pueden alterar este comportamiento.

TCP usa temporizadores para saber cuánto tiempo esperar antes de reenviar un segmento.

4. Vídeo: Confiabilidad de TCP: Pérdida y Retransmisión de Datos
Haz clic en Reproducir en la figura para ver una lección acerca de la retransmisión TCP.


5. Control de flujo TCP: tamaño de ventana y agradecimientos
TCP también proporciona mecanismos para el control de flujo. El control de flujo es la cantidad de datos que el destino puede recibir y procesar de manera confiable. El control de flujo ayuda a mantener la confiabilidad de la transmisión TCP al ajustar la velocidad del flujo de datos entre el origen y el destino para una sesión determinada. Para lograr esto, el encabezado TCP incluye un campo de 16 bits llamado tamaño de ventana.

La imagen muestra un ejemplo de tamaño de ventana y acuses de recibo.

Ejemplo de tamaño de ventana TCP
Ejemplo de tamaño de ventana TCP
El tamaño de la ventana determina el número de bytes que se pueden enviar antes de esperar un acuse de recibo. El número de reconocimiento es el número del siguiente byte esperado.

El tamaño de la ventana es el número de bytes que el dispositivo de destino de una sesión TCP puede aceptar y procesar al mismo tiempo. En este ejemplo, el tamaño de la ventana inicial de la PC B para la sesión TCP es de 10,000 bytes. Comenzando con el primer byte, byte número 1, el último byte que la PC A puede enviar sin recibir un acuse de recibo es el byte 10,000. Esto se conoce como la ventana de envío de la PC A. El tamaño de la ventana se incluye en cada segmento TCP para que el destino pueda modificar el tamaño de la ventana en cualquier momento dependiendo de la disponibilidad del búfer.

El tamaño inicial de la ventana se acuerda cuando la sesión TCP se establece durante el protocolo de enlace de tres vías. El dispositivo de origen debe limitar el número de bytes enviados al dispositivo de destino en función del tamaño de la ventana del destino. Solo después de que el dispositivo fuente recibe un acuse de recibo de que se han recibido los bytes, puede continuar enviando más datos para la sesión. Por lo general, el destino no esperará a que se reciban todos los bytes para el tamaño de su ventana antes de responder con un acuse de recibo. A medida que se reciben y procesan los bytes, el destino enviará acuses de recibo para informar a la fuente que puede continuar enviando bytes adicionales.

Por ejemplo, es típico que la PC B no espere hasta que se hayan recibido los 10,000 bytes antes de enviar un acuse de recibo. Esto significa que la PC A puede ajustar su ventana de envío a medida que recibe confirmaciones de la PC B. Como se muestra en la imagen, cuando la PC A recibe una confirmación con el número de confirmación 2,921, que es el siguiente byte esperado. La ventana de envío de la PC A incrementará 2.920 bytes. Esto cambia la ventana de envío de 10,000 bytes a 12,920. La PC A ahora puede continuar enviando hasta otros 10,000 bytes a la PC B siempre que no envíe más de su nueva ventana de envío a 12,920.

Un destino que envía confirmaciones a medida que procesa los bytes recibidos, y el ajuste continuo de la ventana de envío de origen, se conoce como ventanas deslizantes. En el ejemplo anterior, la ventana de envío de la PC A aumenta o se desliza sobre otros 2,921 bytes de 10,000 a 12,920.

Si la disponibilidad del espacio de almacenamiento intermedio del destino disminuye, puede reducir el tamaño de su ventana para informar a la fuente que reduzca el número de bytes que debe enviar sin recibir un acuse de recibo.

Nota: Los dispositivos actuales usan el protocolo de ventanas deslizantes (Sliding window protocol). El receptor generalmente envía un acuse de recibo después de cada dos segmentos que recibe. El número de segmentos recibidos antes de ser reconocido puede variar. La ventaja de las ventanas deslizantes es que permite al emisor transmitir segmentos continuamente, siempre que el receptor reconozca segmentos anteriores. Los detalles de las ventanas deslizantes están más allá del alcance de este curso.

6. Control de flujo TCP: Tamaño Máximo de Segmento (MSS)
En la imagen, la fuente está transmitiendo 1.460 bytes de datos dentro de cada segmento TCP. Este suele ser el tamaño máximo de segmento (MSS) que puede recibir el dispositivo de destino. El MSS es parte del campo de opciones en el encabezado TCP que especifica la mayor cantidad de datos, en bytes, que un dispositivo puede recibir en un solo segmento TCP. El tamaño de MSS no incluye el encabezado TCP. El MSS generalmente se incluye durante el protocolo de enlace de tres vías.

Tamaño máximo de segmento MSS
Tamaño máximo de segmento MSS
Un MSS común es de 1,460 bytes cuando se usa IPv4. Un host determina el valor de su campo MSS restando los encabezados IP y TCP de la unidad de transmisión máxima de Ethernet (MTU). En una interfaz Ethernet, la MTU predeterminada es 1500 bytes. Restando el encabezado IPv4 de 20 bytes y el encabezado TCP de 20 bytes, el tamaño predeterminado de MSS será 1460 bytes, como se muestra en la imagen.

Tamaño predeterminado de MSS
Tamaño predeterminado de MSS
7. Control de Flujo TCP: Evitar la Congestión
Cuando se produce congestión en una red, el Router sobrecargado descarta los paquetes. Cuando los paquetes que contienen segmentos TCP no llegan a su destino, se dejan sin confirmar. Al determinar la velocidad a la que se envían los segmentos TCP pero no se reconoce, la fuente puede asumir un cierto nivel de congestión de la red.

Ver también
CCNA 1
Tramas Ethernet CCNA
Tramas de Ethernet
Siempre que haya congestión, se producirá la retransmisión de segmentos TCP perdidos desde la fuente. Si la retransmisión no se controla adecuadamente, la retransmisión adicional de los segmentos TCP puede empeorar la congestión. No solo se introducen nuevos paquetes con segmentos TCP en la red, sino que el efecto de retroalimentación de los segmentos TCP retransmitidos que se perdieron también aumentará la congestión. Para evitar y controlar la congestión, TCP emplea varios mecanismos, temporizadores y algoritmos para el manejo de la congestión.

Si la fuente determina que los segmentos TCP no se reconocen o no se reconocen de manera oportuna, entonces puede reducir el número de bytes que envía antes de recibir un reconocimiento. Como se ilustra en la imagen, la PC A detecta que hay congestión y, por lo tanto, reduce la cantidad de bytes que envía antes de recibir un acuse de recibo de la PC B.

Control de congestión TCP
Control de congestión TCP
Los números de acuse de recibo corresponden al siguiente byte esperado y no a un segmento. Los números de segmento utilizados se simplifican con fines ilustrativos.

Ten en cuenta que es la fuente la que está reduciendo el número de bytes no reconocidos que envía y no el tamaño de ventana determinado por el destino.

8. Comprueba tu Comprensión – Fiabilidad y Control de Flujo
Verifica tu conocimiento del proceso de fiabilidad y flujo TCP escogiendo la mejor respuesta a las siguientes preguntas.

¿Qué campo utiliza el host de destino para volver a ensamblar segmentos en el orden original?
Bits de Control
Puerto de Destino
Número de Secuencia
Puerto de Origen
Tamaño de la ventana
¿Qué campo se utiliza para proporcionar control de flujo?
Bits de Control
Puerto de Destino
Número de Secuencia
Puerto de Origen
Tamaño de la Ventana
¿Qué sucede cuando un host de envío detecta que hay congestión?
El host receptor aumenta el número de bytes que envía antes de recibir una confirmación del host remitente.
El host receptor reduce el número de bytes que envía antes de recibir una confirmación del host remitente.
El host de envío aumenta el número de bytes que envía antes de recibir una confirmación del host de destino.
El host de envío reduce el número de bytes que envía antes de recibir una confirmación del host de destino.
¿Aprendiste lo suficiente? Déjanos saber tus respuestas en los comentarios 🙂

Nota: Las explicaciones de los mecanismos, temporizadores y algoritmos de manejo de congestión reales están más allá del alcance de este curso.

Glosario: Si tienes dudas con algún término especial, puedes consultar este diccionario de redes informáticas.

¡Listo! Sigue visitando nuestro blog de curso de redes, dale Me Gusta a nuestra fanpage; y encontrarás más herramientas y conceptos que te convertirán en todo un profesional de redes.


## 3. User Datagram Protocol (UDP)

El **UDP** es un protocolo sin conexión y sin garantías de entrega:

- **Baja Sobrecarga**: Menos control y gestión que TCP, lo que permite mayor velocidad.
- **Sin Control de Flujo ni Congestión**: No ajusta la tasa de envío ni retransmite datos perdidos.
- **Uso Ideal**: Aplicaciones donde la velocidad es crítica y se tolera la pérdida de algunos datos, como streaming de video o voz, y juegos en línea.

- **UDP**: Es como enviar una postal. No hay confirmación de recepción, pero es rápido y sencillo. Ideal para mensajes breves donde la pérdida ocasional es tolerable.


UDP es un protocolo de capa de transporte más simple que TCP. No proporciona confiabilidad y control de flujo, lo que significa que requiere menos campos de encabezado. Debido a que los procesos UDP del emisor y del receptor no tienen que administrar la confiabilidad y el control de flujo, esto significa que los datagramas UDP pueden procesarse más rápido que los segmentos TCP. UDP proporciona las funciones básicas para entregar datagramas entre las aplicaciones apropiadas, con muy poca sobrecarga y verificación de datos.

Nota: UDP divide los datos en datagramas que también se denominan segmentos.

UDP es un protocolo sin conexión. Debido a que UDP no proporciona confiabilidad o control de flujo, no requiere una conexión establecida. Debido a que UDP no rastrea la información enviada o recibida entre el cliente y el servidor, UDP también se conoce como un protocolo sin estado.

UDP también se conoce como un protocolo de entrega de mejor esfuerzo porque no hay reconocimiento de que los datos se reciben en el destino. Con UDP, no hay procesos de capa de transporte que informen al remitente de una entrega exitosa.

UDP es como colocar una carta regular, no registrada, en el correo. El remitente de la carta no tiene conocimiento de la disponibilidad del receptor para recibir la carta. La oficina de correos tampoco es responsable de rastrear la carta o informar al remitente si la carta no llega al destino final.


![Protocolo de datagramas de usuario UDP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Protocolo-de-datagramas-de-usuario-UDP.png)


6. Protocolo Adecuado de Capa de Transporte para la Aplicación Correcta
Algunas aplicaciones pueden tolerar cierta pérdida de datos durante la transmisión a través de la red, pero los retrasos en la transmisión son inaceptables. Para estas aplicaciones, UDP es la mejor opción porque requiere menos sobrecarga de red. UDP es preferible para aplicaciones como Voz sobre IP (VoIP). Los reconocimientos y la retransmisión retrasarían la entrega y harían inaceptable la conversación de voz.

UDP también es utilizado por las aplicaciones de solicitud y respuesta donde los datos son mínimos y la retransmisión se puede hacer rápidamente. Por ejemplo, el servicio de nombres de dominio (DNS) usa UDP para este tipo de transacción. El cliente solicita direcciones IPv4 e IPv6 para un nombre de dominio conocido de un servidor DNS. Si el cliente no recibe una respuesta en un período de tiempo predeterminado, simplemente envía la solicitud nuevamente.

Por ejemplo, si uno o dos segmentos de una transmisión de video en vivo no llegan, se crea una interrupción momentánea en la transmisión. Esto puede aparecer como una distorsión en la imagen o el sonido, pero puede que el usuario no lo note. Si el dispositivo de destino tuviera que dar cuenta de la pérdida de datos, la transmisión podría retrasarse mientras se esperaban las retransmisiones, por lo que la imagen o el sonido se degradarían mucho. En este caso, es mejor renderizar los mejores medios posibles con los segmentos recibidos y renunciar a la fiabilidad.

Para otras aplicaciones, es importante que lleguen todos los datos y que puedan procesarse en su secuencia adecuada. Para este tipo de aplicaciones, TCP se utiliza como protocolo de transporte. Por ejemplo, las aplicaciones como bases de datos, navegadores web y clientes de correo electrónico requieren que todos los datos enviados lleguen al destino en su estado original. Cualquier dato faltante podría corromper una comunicación, haciéndola incompleta o ilegible. Por ejemplo, es importante cuando se accede a la información bancaria a través de la web para asegurarse de que toda la información se envíe y reciba correctamente.

Los desarrolladores de aplicaciones deben elegir qué tipo de protocolo de transporte es apropiado en función de los requisitos de las aplicaciones. El video puede enviarse a través de TCP o UDP. Las aplicaciones que transmiten audio y video almacenado generalmente usan TCP. La aplicación utiliza TCP para realizar almacenamiento en búfer, sondeo de ancho de banda y control de congestión, a fin de controlar mejor la experiencia del usuario.

El video y la voz en tiempo real generalmente usan UDP, pero también pueden usar TCP, o tanto UDP como TCP. Una aplicación de videoconferencia puede usar UDP de manera predeterminada, pero debido a que muchos firewalls bloquean UDP, la aplicación también se puede enviar a través de TCP.

Las aplicaciones que transmiten audio y video almacenado usan TCP. Por ejemplo, si tu red de repente no puede soportar el ancho de banda necesario para ver una película a pedido, la aplicación detiene la reproducción. Durante la pausa, es posible que vea un mensaje de “almacenamiento en búfer …” mientras TCP trabaja para restablecer la transmisión. Cuando todos los segmentos están en orden y se restaura un nivel mínimo de ancho de banda, se reanuda la sesión TCP y se reanuda la reproducción de la película.

La imagen resume las diferencias entre UDP y TCP.

![Diferencias entre UDP y TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Diferencias-entre-UDP-y-TCP.png)

Diferencias entre UDP y TCP
Diferencias entre UDP y TCP
7. Comprueba tu comprensión – Transporte de datos
Verifica tu comprensión de la capa de transporte eligiendo la MEJOR respuesta a las siguientes preguntas.

¿Qué capa es responsable de establecer una sesión de comunicación temporal entre las aplicaciones host de origen y destino?
A. Capa de aplicación
B. Capa de enlace de datos
C. Capa de red
D. Capa física
E. Capa de transporte
¿Cuáles son las tres responsabilidades de la capa de transporte? (Escoja tres opciones).
A. Multiplexión de conversaciones
B. identificación de marcos
C. identificación de información de enrutamiento
D. segmentación de datos y reensamblado de segmentos
E. Seguimiento de conversaciones individuales
¿Qué declaración de protocolo de capa de transporte es verdadera?
A. TCP tiene menos campos que UDP.
B. TCP es más rápido que UDP.
C. UDP es un protocolo de entrega de mejor esfuerzo.
D. UDP proporciona fiabilidad.
¿Qué protocolo de capa de transporte se usaría para aplicaciones VoIP?
A. Protocolo de información de sesión (SIP)
B. Protocolo de control de transmisión (TCP)
C. Protocolo de datagramas de usuario (UDP)
D. Protocolo de transferencia de VoIP

https://ccnadesdecero.es/comunicacion-udp/

1. Comparación de Baja Sobrecarga y Confiabilidad de UDP
Como se explicó anteriormente, UPD es perfecto para comunicaciones que necesitan ser rápidas, como VoIP. Este tema explica en detalle por qué UDP es perfecto para algunos tipos de transmisiones. Como se muestra en la figura, UDP no establece una conexión. UDP suministra transporte de datos con baja sobrecarga debido a que posee un encabezado de datagrama pequeño sin tráfico de administración de red.

UDP de baja sobrecarga frente a fiabilidad
UDP de baja sobrecarga frente a fiabilidad
2. Reensamblaje de Datagramas UDP
Al igual que los segmentos con TCP, cuando los datagramas UDP se envían a un destino, a menudo toman diferentes caminos y llegan en el orden incorrecto. UDP no rastrea los números de secuencia como lo hace TCP. UDP no tiene forma de reordenar los datagramas en su orden de transmisión, como se muestra en la imagen.

Por lo tanto, UDP simplemente vuelve a ensamblar los datos en el orden en que se recibieron y los reenvía a la aplicación. Si la secuencia de datos es importante para la aplicación, la aplicación debe identificar la secuencia adecuada y determinar cómo se deben procesar los datos.

UDP sin conexión y no confiable
UDP sin conexión y no confiable. Se muestra datagramas UDP que se envían en orden, pero que llegan fuera de servicio debido a la posibilidad de que diferentes rutas lleguen al destino.
3. Procesos y Solicitudes del Servidor UDP
Al igual que las aplicaciones basadas en TCP, a las aplicaciones de servidor basadas en UDP se les asignan números de puerto conocidos o registrados, como se muestra en la imagen. Cuando estas aplicaciones o procesos se ejecutan en un servidor, aceptan los datos que coinciden con el número de puerto asignado. Cuando UDP recibe un datagrama destinado a uno de estos puertos, reenvía los datos de la aplicación a la aplicación adecuada en función de su número de puerto.

Servidor UDP escuchando solicitudes
Servidor UDP escuchando solicitudes. Una aplicación de servidor RADIUS usa UDP para escuchar las solicitudes en el puerto 53
Nota: El Remote Authentication Dial-in User Service (RADIUS) que se muestra en la imagen proporciona servicios de autenticación, autorización y contabilidad para administrar el acceso de los usuarios. El funcionamiento de RADIUS está más allá del alcance de este curso.

4. Procesos de Cliente UDP
Al igual que con TCP, la comunicación cliente-servidor es iniciada por una aplicación cliente que solicita datos de un proceso del servidor. El proceso del cliente UDP selecciona dinámicamente un número de puerto del rango de números de puerto y lo utiliza como puerto de origen para la conversación. El puerto de destino suele ser el número de puerto conocido o registrado asignado al proceso del servidor.

Después de que un cliente ha seleccionado los puertos de origen y destino, se utiliza el mismo par de puertos en el encabezado de todos los datagramas en la transacción. Para los datos que regresan al cliente desde el servidor, se invierten los números de puerto de origen y destino en el encabezado del datagrama.

Haz clic en cada botón para ver una ilustración de dos hosts que solicitan servicios del servidor de autenticación DNS y RADIUS.

Clientes que envían solicitudes UDP
Puertos de destino de solicitud UDP
Puertos de origen de solicitud UDP
Destino de respuesta UDP
Puertos de origen de respuesta UDP
El Cliente 1 está enviando una solicitud DNS utilizando el conocido puerto 53, mientras que el Cliente 2 está solicitando servicios de autenticación RADIUS utilizando el puerto registrado 1812.

Clientes que envían solicitudes UDP
Clientes que envían solicitudes UDP
5. Comprueba tu comprensión – Comunicación UDP
Comprueba tu comprensión de la comunicación UDP eligiendo la MEJOR respuesta a las siguientes preguntas.

¿Por qué es conveniente UDP para los protocolos que hacen una simple solicitud y responden transacciones?
A. Control de flujo
B. Baja sobrecarga
C. Confianza
D. Entrega en el mismo pedido
¿Qué declaración de reensamblaje de datagramas UDP es verdadera?
A. UDP no vuelve a ensamblar los datos.
B. UDP vuelve a ensamblar los datos en el orden en que fueron recibidos.
C. UDP vuelve a ensamblar los datos utilizando bits de control.
D. UDP vuelve a ensamblar los datos utilizando números de secuencia.
¿Cuáles de los siguientes puertos serían válidos de origen y destino para un host que se conecta a un servidor DNS?
A. Origen: 53, Destino: 49152
B. Origen: 1812, Destino: 49152
C. Origen: 49152, Destino: 53
D. Origen: 49152, Destino: 1812


## 4. Otros protocolos Emergentes

## 3. Manejo Avanzado de Congestión y Control de Flujo

Con el incremento del tráfico y las demandas de alta velocidad, se han desarrollado nuevos algoritmos:

- **BBR (Bottleneck Bandwidth and Round-trip propagation time)**: Estima la capacidad real de la red y ajusta el envío de datos para maximizar el rendimiento sin causar congestión.
- **Algoritmos Adaptativos**: Protocolos que ajustan dinámicamente sus parámetros basándose en las condiciones actuales de la red.

Estos avances permiten un uso más eficiente de la infraestructura existente y mejoran la experiencia del usuario.

## 4. Impacto de Tecnologías Emergentes

### **Internet de las Cosas (IoT)**

- **Proliferación de Dispositivos**: Millones de dispositivos conectados requieren protocolos eficientes y escalables.
- **Protocolos Ligeros**: Como **MQTT** o **CoAP**, optimizados para dispositivos con recursos limitados y comunicaciones de baja potencia.
- **Seguridad**: La protección de datos y dispositivos es crítica, dado el volumen y sensibilidad de la información manejada.

### **Redes 5G y Futuras Generaciones**

- **Alta Velocidad y Baja Latencia**: Requieren protocolos de transporte que puedan aprovechar estas características.
- **Aplicaciones en Tiempo Real**: Como realidad aumentada, vehículos autónomos y telemedicina, que dependen de comunicaciones rápidas y fiables.
- **Edge Computing**: Procesamiento cercano al origen de los datos, reduciendo la carga en la red central y mejorando tiempos de respuesta.

### 4.1. Protocolo Rápido de Internet basado en UDP (QUIC)

Desarrollado por Google, **QUIC** es un protocolo moderno que combina lo mejor de TCP y UDP:

- **Basado en UDP**: Utiliza UDP para evitar limitaciones en redes donde TCP puede ser bloqueado o manipulado.
- **Establecimiento de Conexión Rápido**: Reduce la latencia al combinar el handshake de transporte y seguridad en un solo paso.
- **Cifrado Incorporado**: Integra TLS 1.3, ofreciendo seguridad desde el diseño.
- **Multiplexación de Flujo**: Permite múltiples flujos independientes dentro de una conexión para evitar bloqueos.
- **Mejora en Móviles**: Diseñado para lidiar con cambios frecuentes en la conexión, como en dispositivos móviles en movimiento.

- **QUIC**: Sería como enviar un mensaje instantáneo cifrado por una aplicación de mensajería segura. Rápido, seguro y eficiente.


### 4.2. Stream Control Transmission Protocol (SCTP)

El **SCTP** es un protocolo que incorpora características de TCP y UDP:

- **Multistreaming**: Permite múltiples flujos de datos independientes dentro de una única conexión.
- **Multihoming**: Un único punto final puede tener múltiples direcciones IP, aumentando la tolerancia a fallos.
- **Entrega Fiable y Ordenada**: Similar a TCP, pero con mayor flexibilidad en la gestión de flujos.

## 5. Seguridad Integrada en la Capa de Transporte

### **TLS (Transport Layer Security) y SSL (Secure Sockets Layer)**

- **Cifrado de Datos**: Protege la confidencialidad de la información transmitida.
- **Autenticación**: Verifica la identidad de las partes comunicantes.
- **Integridad**: Asegura que los datos no sean alterados durante la transmisión.

**SSL** fue el precursor de **TLS** y proporcionó las primeras implementaciones de cifrado y autenticación en las comunicaciones en red. Aunque **SSL** ya no se considera seguro y ha sido reemplazado por **TLS**, su legado sigue siendo importante en la evolución de la seguridad en la capa de transporte.

La seguridad ya no es una opción adicional; es una necesidad integrada. Protocolos como **QUIC** incorporan **TLS** de forma nativa, garantizando conexiones seguras sin pasos adicionales.

## 5. PDU de la Capa de Transporte

La **Unidad de Datos de Protocolo (PDU)** en la capa de transporte se conoce como:

- **Segmento** en TCP.
- **Datagrama** en UDP.

### Estructura General de un Segmento TCP

| Campo                | Tamaño (bits) |
|----------------------|---------------|
| Puerto de Origen     | 16            |
| Puerto de Destino    | 16            |
| Número de Secuencia  | 32            |
| Número de Acuse      | 32            |
| Offset de Datos      | 4             |
| Reservado            | 6             |
| Banderas             | 6             |
| Ventana              | 16            |
| Checksum             | 16            |
| Puntero Urgente      | 16            |
| Opciones y Relleno   | Variable      |
| Datos                | Variable      |

Esta estructura permite a TCP gestionar la comunicación de manera eficiente y fiable.

## 6. Metáforas para Facilitar la Comprensión



## 9. Conclusión

La capa de transporte es fundamental en las comunicaciones de red, y su comprensión es esencial para cualquier profesional en informática. Los avances tecnológicos y las nuevas demandas de aplicaciones requieren una actualización constante de los conocimientos.


## 1.2. Puertos: Identificando Procesos en Comunicación

Los **puertos** son números que identifican de manera única a los procesos dentro de un dispositivo. Funcionan como puntos finales de comunicación en la capa de transporte. Gracias a los puertos:

- Se puede especificar exactamente qué proceso en el dispositivo destino debe recibir los datos.
- Es posible la **multiplexación**, permitiendo que múltiples conexiones existan simultáneamente.
- Se organiza y gestiona el tráfico de red de manera eficiente.

Los números de puerto se dividen en rangos:

- **Puertos Bien Conocidos (0-1023)**: Reservados para servicios y aplicaciones estándar (por ejemplo, el puerto 80 para HTTP).
- **Puertos Registrados (1024-49151)**: Asignados para aplicaciones y procesos específicos.
- **Puertos Dinámicos o Privados (49152-65535)**: Utilizados temporalmente por aplicaciones cliente al establecer conexiones.

1. Comunicaciones Múltiples Separadas
Como has aprendido, hay algunas situaciones en las que TCP es el protocolo adecuado para el trabajo, y otras situaciones en las que se debe utilizar UDP. No importa qué tipo de datos se transporten, tanto TCP como UDP usan números de puerto.

Los protocolos de capa de transporte TCP y UDP utilizan números de puerto para administrar múltiples conversaciones simultáneas. Como se muestra en la figura, los campos de encabezado TCP y UDP identifican un número de puerto de aplicación de origen y destino.

Puerto de origen (16) | Puerto de destino (16)
El número de puerto de origen está asociado con la aplicación de origen en el host local, mientras que el número de puerto de destino está asociado con la aplicación de destino en el host remoto.

Por ejemplo, supón que un host está iniciando una solicitud de página web desde un servidor web. Cuando el host inicia la solicitud de la página web, el host genera dinámicamente el número de puerto de origen para identificar de forma exclusiva la conversación. Cada solicitud generada por un host utilizará un número de puerto de origen creado dinámicamente diferente. Este proceso permite que se produzcan múltiples conversaciones simultáneamente.

En la solicitud, el número de puerto de destino es lo que identifica el tipo de servicio que se solicita del servidor web de destino. Por ejemplo, cuando un cliente especifica el puerto 80 en el puerto de destino, el servidor que recibe el mensaje sabe que se están prestando servicios web pedido.

Un servidor puede ofrecer más de un servicio simultáneamente, como servicios web en el puerto 80, mientras que ofrece el establecimiento de conexión de Protocolo de transferencia de archivos (FTP) en el puerto 21.

2. Pares de Socket
Los puertos de origen y destino se colocan dentro del segmento. Los segmentos se encapsulan dentro de un paquete IP. El paquete IP contiene la dirección IP de origen y destino. La combinación de la dirección IP de origen y el número de puerto de origen, o la dirección IP de destino y el número de puerto de destino se conoce como socket.

En el ejemplo de la imagen, la PC solicita simultáneamente servicios FTP y web del servidor de destino.

![Pares de Socket](https://ccnadesdecero.es/wp-content/uploads/2020/04/Pares-de-Socket.png)

Pares de Socket
Pares de Socket
En el ejemplo, la solicitud FTP generada por la PC incluye las direcciones MAC de capa 2 y las direcciones IP de capa 3. La solicitud también identifica el número de puerto de origen 1305 (es decir, generado dinámicamente por el host) y el puerto de destino, identificando los servicios FTP en el puerto 21. El host también ha solicitado una página web del servidor utilizando las mismas direcciones de Capa 2 y Capa 3 . Sin embargo, está utilizando el número de puerto de origen 1099 (es decir, generado dinámicamente por el host) y el puerto de destino que identifica el servicio web en el puerto 80.

El socket se utiliza para identificar el servidor y el servicio que solicita el cliente. Un socket de cliente podría verse así, con 1099 representando el número de puerto de origen: 192.168.1.5:1099

El socket en un servidor web puede ser 192.168.1.7:80

Juntos, estos dos sockets se combinan para formar un par de sockets: 192.168.1.5:1099, 192.168.1.7:80

Los sockets permiten que múltiples procesos, que se ejecutan en un cliente, se distingan entre sí, y que múltiples conexiones a un proceso de servidor se distingan entre sí.

El número de puerto de origen actúa como una dirección de retorno para la aplicación solicitante. La capa de transporte realiza un seguimiento de este puerto y la aplicación que inició la solicitud para que cuando se devuelva una respuesta, se pueda reenviar a la aplicación correcta.

3. Grupos de número de puerto
La Internet Assigned Numbers Authority (IANA) es la organización de estándares responsable de asignar varios estándares de direccionamiento, incluidos los números de puerto de 16 bits. Los 16 bits utilizados para identificar los números de puerto de origen y destino proporcionan un rango de puertos de 0 a 65535.

La IANA ha dividido el rango de números en los siguientes tres grupos de puertos.

Grupo portuario	Rango de números	Descripción
Puertos conocidos	0 a 1,023	
Estos números de puerto están reservados para servicios y aplicaciones comunes o populares, como navegadores web, clientes de correo electrónico y clientes de acceso remoto.
Los puertos bien conocidos definidos para aplicaciones de servidor comunes permiten a los clientes identificar fácilmente el servicio asociado requerido.
Puertos registrados	1.024 a 49.151	
La IANA asigna estos números de puerto a una entidad solicitante para usar con procesos o aplicaciones específicos.
Estos procesos son principalmente aplicaciones individuales que un usuario ha elegido instalar, en lugar de aplicaciones comunes que recibirían un número de puerto conocido.
Por ejemplo, Cisco ha registrado el puerto 1812 para su proceso de autenticación del servidor RADIUS.
Puertos privados y/o dinámicos	49,152 a 65,535	
Estos puertos también se conocen como puertos efímeros.
El sistema operativo del cliente generalmente asigna números de puerto dinámicamente cuando se inicia una conexión a un servicio.
El puerto dinámico se utiliza para identificar la aplicación del cliente durante la comunicación.
Nota: Algunos sistemas operativos de clientes pueden usar números de puerto registrados en lugar de números de puerto dinámicos para asignar puertos de origen.

La tabla muestra algunos números de puerto conocidos y sus aplicaciones asociadas.

Número de puerto	Protocolo	Solicitud
20	TCP	Protocolo de transferencia de archivos (FTP) – Datos
21	TCP	Protocolo de transferencia de archivos (FTP) – Control
22	TCP	Shell seguro (SSH)
23	TCP	Telnet
25	TCP	Protocolo simple de transferencia de correo (SMTP)
53	UDP, TCP	Servicio de nombres de dominio (DNS)
67	UDP	Protocolo de configuración dinámica de host (DHCP): servidor
68	UDP	Protocolo de configuración dinámica de host: cliente
69	UDP	Protocolo trivial de transferencia de archivos (TFTP)
80	TCP	Protocolo de transferencia de hipertexto (HTTP)
110	TCP	Protocolo de oficina de correos versión 3 (POP3)
143	TCP	Protocolo de acceso a mensajes de Internet (IMAP)
161	UDP	Protocolo simple de administración de red (SNMP)
443	TCP	Protocolo de transferencia de hipertexto seguro (HTTPS)
Algunas aplicaciones pueden usar tanto TCP como UDP. Por ejemplo, DNS usa UDP cuando los clientes envían solicitudes a un servidor DNS. Sin embargo, la comunicación entre dos servidores DNS siempre usa TCP.

Ver también
CCNA 1
Administración de Archivos de Configuración IOS
Administración de Archivos de Configuración IOS
4. El Comando netstat
Las conexiones TCP inexplicadas pueden representar una gran amenaza de seguridad. Pueden indicar que algo o alguien está conectado al host local. A veces es necesario saber qué conexiones TCP activas están abiertas y ejecutándose en un host en red. Netstat es una importante utilidad de red que se puede usar para verificar esas conexiones. Como se muestra a continuación, ingresa el comando netstat para enumerar los protocolos en uso, la dirección local y los números de puerto, la dirección extranjera y los números de puerto y el estado de la conexión.

```bash
C:\> netstat
Active Connections
Proto Local Address Foreign Address State
TCP 192.168.1.124:3126 192.168.0.2:netbios-ssn ESTABLISHED
TCP 192.168.1.124:3158 207.138.126.152:http ESTABLISHED
TCP 192.168.1.124:3159 207.138.126.169:http ESTABLISHED
TCP 192.168.1.124:3160 207.138.126.169:http ESTABLISHED
TCP 192.168.1.124:3161 sc.msn.com:http ESTABLISHED
TCP 192.168.1.124:3166 www.cisco.com:http ESTABLISHED
```

De manera predeterminada, el comando netstat intentará resolver las direcciones IP para nombres de dominio y números de puerto para aplicaciones conocidas. La opción -n se puede usar para mostrar las direcciones IP y los números de puerto en su forma numérica.

5. Verifica tu comprensión – Números de puerto
Verifica tu comprensión de los números de puerto eligiendo la MEJOR respuesta a las siguientes preguntas.

Supongamos que un host con dirección IP 10.1.1.10 desea solicitar servicios web desde un servidor en 10.1.1.254. ¿Cuál de los siguientes mostraría para corregir el par de socket?
A. 1099:10 .1.1.10, 80:10 .1.1.254
B. 10.1.1. 10:80, 10.1.1. 254:1099
C. 10.1.1. 10:1099, 10.1.1. 254:80
D. 80:10 .1.1.10, 1099:10 .1.1.254
¿Qué grupo de puertos incluye números de puerto para aplicaciones FTP, HTTP y TFTP?
A. Puertos dinámicos
B. Puertos privados
C. Puertos registrados
D. Puertos bien conocidos
¿Qué comando de Windows mostrará los protocolos en uso, la dirección local y los números de puerto, la dirección extranjera y los números de puerto y el estado de la conexión?
A. ipconfig /all
B. ping
C. netstat
D. traceroute

## Referencias

https://ccnadesdecero.es/ccna-1/#Modulo_14_Capa_de_Transporte_CCNA_1_v7
