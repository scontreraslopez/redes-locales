# UP5. La capa de transporte

## Índice

- [1. Funciones de la Capa de Transporte](#1-funciones-de-la-capa-de-transporte)
- [2. Transmission Control Protocol (TCP)](#2-transmission-control-protocol-tcp)
  - [2.1. Características de TCP](#21-características-de-tcp)
  - [2.2. Encabezado TCP](#22-encabezado-tcp)
    - [2.2.1. Campos de encabezado TCP](#221-campos-de-encabezado-tcp)
  - [2.3. Aplicaciones que usan TCP](#23-aplicaciones-que-usan-tcp)
  - [2.4. Procesos del Servidor TCP](#24-procesos-del-servidor-tcp)
    - [2.4.1. Clientes que envían solicitudes TCP](#241-clientes-que-envían-solicitudes-tcp)
    - [2.4.2. Solicitar puertos de destino](#242-solicitar-puertos-de-destino)
    - [2.4.3. Solicitar puertos de origen](#243-solicitar-puertos-de-origen)
    - [2.4.4. Respuesta puertos destino](#244-respuesta-puertos-destino)
    - [2.4.5. Respuesta puertos de origen](#245-respuesta-puertos-de-origen)
  - [2.5. Establecimiento de Conexión TCP](#25-establecimiento-de-conexión-tcp)
  - [2.6. Terminación de Sesión](#26-terminación-de-sesión)
  - [2.7. Análisis del Enlace de Tres Vías TCP](#27-análisis-del-enlace-de-tres-vías-tcp)
  - [2.8. Fiabilidad y control de flujo](#28-fiabilidad-y-control-de-flujo)
    - [2.8.1. Fiabilidad I: Entrega Garantizada y Ordenada](#281-fiabilidad-i-entrega-garantizada-y-ordenada)
    - [2.8.2. Fiabilidad II: Pérdida y Retransmisión de Datos](#282-fiabilidad-ii-pérdida-y-retransmisión-de-datos)
    - [2.8.3. Control de flujo I: Tamaño de Ventana y Acuses de Recibo](#283-control-de-flujo-i-tamaño-de-ventana-y-acuses-de-recibo)
    - [2.8.4. Control de flujo II: Tamaño Máximo de Segmento (MSS)](#284-control-de-flujo-ii-tamaño-máximo-de-segmento-mss)
    - [2.8.5. Control de flujo III: Prevención de Congestiones](#285-control-de-flujo-iii-prevención-de-congestiones)
- [3. User Datagram Protocol (UDP)](#3-user-datagram-protocol-udp)
  - [3.1. Casos de uso de UDP vs TCP](#31-casos-de-uso-de-udp-vs-tcp)
  - [3.2. Comparación de Baja Sobrecarga y Confiabilidad de UDP](#32-comparación-de-baja-sobrecarga-y-confiabilidad-de-udp)
  - [3.3. Reensamblaje de Datagramas UDP](#33-reensamblaje-de-datagramas-udp)
  - [3.4. Procesos y Solicitudes del Servidor UDP](#34-procesos-y-solicitudes-del-servidor-udp)
  - [3.5. Procesos de Cliente UDP](#35-procesos-de-cliente-udp)
- [4. Puertos: Identificando Procesos en Comunicación](#4-puertos-identificando-procesos-en-comunicación)
  - [4.1. Comunicaciones Múltiples Separadas](#41-comunicaciones-múltiples-separadas)
  - [4.2. Pares de Socket](#42-pares-de-socket)
  - [4.3. Grupos de número de puerto](#43-grupos-de-número-de-puerto)
  - [4.4. El Comando netstat](#44-el-comando-netstat)
- [5. Otros protocolos Emergentes](#5-otros-protocolos-emergentes)
  - [5.1. Internet de las Cosas (IoT)](#51-internet-de-las-cosas-iot)
  - [5.2. Redes 5G y Futuras Generaciones](#52-redes-5g-y-futuras-generaciones)
  - [5.3. Protocolo Rápido de Internet Basado en UDP (QUIC)](#53-protocolo-rápido-de-internet-basado-en-udp-quic)
  - [5.4. Stream Control Transmission Protocol (SCTP)](#54-stream-control-transmission-protocol-sctp)
- [6. Seguridad Integrada en la Capa de Transporte](#6-seguridad-integrada-en-la-capa-de-transporte)
- [7. Conclusión](#7-conclusión)
- [8. Referencias](#8-referencias)

## 1. Funciones de la Capa de Transporte

La capa de transporte gestiona las comunicaciones lógicas entre las aplicaciones que operan en distintos hosts. Su principal objetivo es facilitar el intercambio de datos entre estas aplicaciones, asegurando que los requerimientos específicos de cada una sean satisfechos.

Esta capa se encarga de proporcionar varios servicios, entre los cuales se incluyen:

- **Establecimiento de Conexiones**: Permite la creación de sesiones temporales entre dos hosts para la transmisión de datos.
- **Transmisión Confiable**: Garantiza que la información se entregue sin errores y en el orden correcto.

La capa de transporte actúa como un puente esencial entre la capa de aplicación y las capas inferiores responsables de la transmisión a través de la red. Diferentes aplicaciones tienen diferentes requisitos de fiabilidad, lo que motiva la existencia de varios protocolos en esta capa.

![Protocolos de capa de transporte](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_090920.jpg)

Los protocolos de capa de transporte más utilizados son **TCP (Transmission Control Protocol)** y **UDP (User Datagram Protocol)**, cada uno diseñado para manejar distintos tipos de tráfico. IP, por su parte, se centra en la estructura y el direccionamiento de paquetes, pero no especifica cómo se entregan estos datos.

A continuación, se definen los dos tipos de **Unidad de Datos de Protocolo (PDU)** en la capa de transporte:

- **Segmento**: Utilizado por TCP.
- **Datagrama**: Utilizado por UDP.

Las funciones clave de la capa de transporte se pueden clasificar de la siguiente manera:

1. **Segmentación y Reensamblado**: Divide los datos de las aplicaciones en segmentos adecuados para su transmisión y los reensambla en el destino.
2. **Multiplexación y Demultiplexación**: Permite que múltiples procesos utilicen la red simultáneamente, identificando cada conexión mediante números de puerto.
3. **Control de Flujo**: Gestión de la velocidad de envío de datos para prevenir la saturación del receptor.
4. **Control de Congestión**: Regulación del tráfico para evitar congestiones en la red.
5. **Entrega Confiable**: Asegura la entrega correcta y en orden de los segmentos, incluyendo la detección y retransmisión de segmentos perdidos.
6. **Establecimiento de Sesiones**: Facilita la creación, mantenimiento y cierre de conexiones entre procesos en diferentes dispositivos.

La capa de transporte juega un papel fundamental en la comunicación eficiente y confiable entre procesos que se ejecutan en distintas máquinas, permitiendo que múltiples procesos se comuniquen de forma simultánea sin interferencias.

## 2. Transmission Control Protocol (TCP)

**TCP** es un protocolo orientado a conexión que proporciona comunicación fiable:

- **Establecimiento de Conexión**: Utiliza un proceso de *handshake* de tres vías para iniciar la comunicación.
- **Entrega Fiable y Ordenada**: Garantiza que los datos lleguen sin errores y en el orden correcto.
- **Control de Flujo y Congestión**: Ajusta el envío de datos según la capacidad del receptor y las condiciones de la red.
- **Características Adicionales**: Soporta retransmisiones, control de duplicados y temporización.

**TCP** es algo así como enviar una carta certificada. El remitente recibe confirmación de que la carta ha sido entregada, y si se pierde, se envía de nuevo. Es seguro, pero puede ser más lento debido a los protocolos de confirmación. Así, el transporte TCP es análogo a un envío que se rastrea desde el origen hasta el destino, incluso si este envío se divide en varios paquetes, llamados segmentos en TCP.

TCP se considera un protocolo de capa de transporte confiable y con todas las funciones, que garantiza que todos los datos lleguen al destino. TCP incluye campos que aseguran la entrega de los datos de la aplicación. Estos campos requieren un procesamiento adicional por parte de los hosts de envío y recepción. Para mantener el estado de una conversación y rastrear la información, TCP primero debe establecer una conexión entre el remitente y el receptor. Es por eso que TCP se conoce como un protocolo orientado a la conexión.

![Protocolo de Control de Transmisión TCP](https://examenredes.com/wp-content/uploads/2021/12/14.1.4.gif)

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

Puedes obtener más información sobre TCP en el documento RFC 793.

### 2.2. Encabezado TCP

TCP es un protocolo con estado, lo que significa que realiza un seguimiento del estado de la sesión de comunicación. Para rastrear el estado de una sesión, TCP registra qué información ha enviado y qué información ha sido reconocida. La sesión con estado comienza con el establecimiento de la sesión y termina con la finalización de la sesión.

Un segmento TCP agrega 20 bytes (es decir, 160 bits) de sobrecarga al encapsular los datos de la capa de aplicación. La imagen muestra los campos en un encabezado TCP.

![Encabezado TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Encabezado-TCP.png)

#### 2.2.1. Campos de encabezado TCP

La tabla identifica y describe los campos en un encabezado TCP. Como el campo Opciones no está siempre presente generalmente se dice que el encabezado TCP presenta 10 campos.

| Campo de encabezado TCP | Descripción |
|------------------------|-----------------------------------------------------------------------------|
| Puerto de origen       | Un campo de 16 bits utilizado para identificar la aplicación de origen por número de puerto. |
| Puerto de destino      | Un campo de 16 bits utilizado para identificar la aplicación de destino por número de puerto. |
| Secuencia de números   | Un campo de 32 bits utilizado para fines de reensamblado de datos.           |
| Número de acuse de recibo | Un campo de 32 bits utilizado para indicar que se han recibido datos y que se espera el siguiente byte de la fuente. |
| Longitud del encabezado | Un campo de 4 bits conocido como “desplazamiento de datos” que indica la longitud del encabezado del segmento TCP. |
| Reservado              | Un campo de 6 bits que está reservado para uso futuro.                      |
| Bits de control        | Un campo de 6 bits utilizado que incluye códigos de bits o banderas (FIN, ACK, SYN, RST, PSH y URG), que indican el propósito y la función del segmento TCP. |
| Tamaño de ventana      | Un campo de 16 bits utilizado para indicar el número de bytes que se pueden aceptar a la vez. |
| Suma de comprobación    | Un campo de 16 bits utilizado para la verificación de errores del encabezado y los datos del segmento. |
| Urgente                | Un campo de 16 bits utilizado para indicar si los datos contenidos son urgentes. |
| Opciones               | Un campo de longitud variable utilizado para varios propósitos, como el ajuste del tamaño máximo de segmento (MSS) y el uso de timestamps. |

### 2.3. Aplicaciones que usan TCP

TCP es un buen ejemplo de cómo las diferentes capas del conjunto de protocolos TCP/IP tienen roles específicos. TCP maneja todas las tareas asociadas con la división del flujo de datos en segmentos, proporcionando confiabilidad, controlando el flujo de datos y reordenando segmentos.

TCP libera a la aplicación de tener que administrar cualquiera de estas tareas. Las aplicaciones, como las que se muestran en la figura, simplemente pueden enviar el flujo de datos a la capa de transporte y utilizar los servicios de TCP.

![Aplicaciones que usan TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Aplicaciones-que-usan-TCP.png)

### 2.4. Procesos del Servidor TCP

Cada proceso de aplicación que se ejecuta en un servidor está configurado para usar un número de puerto. El número de puerto se asigna automáticamente o se configura manualmente por un administrador del sistema.

Un servidor individual no puede tener dos servicios asignados al mismo número de puerto dentro de los mismos servicios de capa de transporte. Por ejemplo, un host que ejecuta una aplicación de servidor web y una aplicación de transferencia de archivos no puede tener ambos configurados para usar el mismo puerto, como el puerto TCP 80.

Una aplicación de servidor activa asignada a un puerto específico se considera **abierta**, lo que significa que la capa de transporte acepta y procesa segmentos dirigidos a ese puerto. Se acepta cualquier solicitud de cliente entrante dirigida al socket correcto, y los datos se pasan a la aplicación del servidor. Puede haber muchos puertos abiertos simultáneamente en un servidor, uno para cada aplicación de servidor activa.

#### 2.4.1. Clientes que envían solicitudes TCP

![Clientes envían solicitudes TCP](https://ccnadesdecero.es/wp-content/uploads/2020/04/Clientes-env%C3%ADan-solicitudes-TCP.png)

En la imagen se observa como el cliente 1 solicita servicios web y el cliente 2 solicita servicio de correo electrónico utilizando puertos conocidos (es decir, servicios web en el puerto 80, servicios de correo electrónico en el puerto 25).

#### 2.4.2. Solicitar puertos de destino

Las solicitudes generan dinámicamente un número de puerto de origen. En este caso, el Cliente 1 está utilizando el puerto de origen 49152 y el Cliente 2 está utilizando el puerto de origen 51152.

![Solicitar puertos de destino](https://ccnadesdecero.es/wp-content/uploads/2020/04/Solicitar-puertos-de-destino.png)

#### 2.4.3. Solicitar puertos de origen

Cuando el servidor responde a las solicitudes del cliente, invierte el destino y los puertos de origen de la solicitud inicial.

![Solicitar puertos de origen](https://ccnadesdecero.es/wp-content/uploads/2020/04/Solicitar-puertos-de-origen.png)

#### 2.4.4. Respuesta puertos destino

Observa que la respuesta del servidor a la solicitud web ahora tiene el puerto de destino 49152 y la respuesta de correo electrónico ahora tiene el puerto de destino 51152.

![Respuesta puertos de destino](https://ccnadesdecero.es/wp-content/uploads/2020/04/Respuesta-Puertos-de-destino.png)

#### 2.4.5. Respuesta puertos de origen

El puerto de origen en la respuesta del servidor es el puerto de destino original en las solicitudes iniciales.

![Solicitar puertos de origen](https://ccnadesdecero.es/wp-content/uploads/2020/04/Respuesta-Puertos-de-origen.png)

### 2.5. Establecimiento de Conexión TCP

En algunas culturas, cuando dos personas se encuentran, a menudo se saludan dándose la mano. Ambas partes entienden el acto de estrechar la mano como una señal de saludo amistoso. Las conexiones en la red son similares. En las conexiones TCP, el cliente host establece la conexión con el servidor mediante el proceso de enlace de tres vías (*three-way handshake*).

- **Paso 1. SYN**
- **Paso 2. ACK y SYN**
- **Paso 3. ACK**

El cliente que inicia solicita una sesión de comunicación de cliente a servidor con el servidor.

**Paso 1 SYN**:

El protocolo de enlace de tres vías valida que el host de destino esté disponible para comunicarse. En este ejemplo, el host A ha validado que el host B está disponible.

![Paso 1 SYN](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-1-SYN.png)

**Paso 2 ACK y SIN SYN**:

El servidor reconoce la sesión de comunicación de cliente a servidor y solicita una sesión de comunicación de servidor a cliente.

![Paso 2 ACK y SYN](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-2-ACK-y-SYN.png)

**Paso 3. ACK**:

El cliente que inicia reconoce la sesión de comunicación de servidor a cliente.

![Paso 3 ACK](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-3-ACK.png)

El protocolo de enlace de tres vías valida que el host de destino esté disponible para comunicarse. En este ejemplo, el host A ha validado que el host B está disponible.

### 2.6. Terminación de Sesión

Para cerrar una conexión, el indicador de control Finish (FIN) debe establecerse en el encabezado del segmento. Para finalizar cada sesión TCP unidireccional, se utiliza un protocolo de enlace bidireccional, que consta de un segmento FIN y un segmento de acuse de recibo (ACK). Por lo tanto, para finalizar una sola conversación compatible con TCP, se necesitan cuatro intercambios para finalizar ambas sesiones. Tanto el cliente como el servidor pueden iniciar la terminación.

En el ejemplo, los términos "cliente" y "servidor" se utilizan como referencia por simplicidad, pero dos hosts que tengan una sesión abierta pueden iniciar el proceso de finalización.

Haga clic en cada botón para obtener más información sobre los pasos de finalización de la sesión.

- **Paso 1. FIN**
- **Paso 2. ACK**
- **Paso 3. FIN**
- **Paso 4. ACK**

Cuando el cliente no tiene más datos para enviar en la secuencia, envía un segmento con el indicador FIN establecido.

**Paso 1 FIN**:
Cuando todos los segmentos han sido reconocidos, la sesión se cierra.

![Paso 1 FIN](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-1-FIN.png)

**Paso 2 ACK**:

El servidor envía un ACK para acusar recibo del FIN para finalizar la sesión del cliente al servidor.

![Paso 2 ACK](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-2-ACK.png)

**Paso 3 FIN**:

El servidor envía un FIN al cliente para finalizar la sesión de servidor a cliente.

![Paso 3 FIN](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-3-FIN.png)

**Paso 4 ACK**:

El cliente responde con un ACK para reconocer el FIN del servidor.

![Paso 4 ACK](https://ccnadesdecero.es/wp-content/uploads/2020/04/Paso-4-ACK.png)

### 2.7. Análisis del Enlace de Tres Vías TCP

Los hosts mantienen el estado, rastrean cada segmento de datos dentro de una sesión e intercambian información sobre qué datos se reciben utilizando la información en el encabezado TCP. TCP es un protocolo *full-duplex*, donde cada conexión representa dos sesiones de comunicación unidireccionales. Para establecer la conexión, los hosts realizan un protocolo de enlace de tres vías. Como se muestra en la imagen, los bits de control en el encabezado TCP indican el progreso y el estado de la conexión.

Estas son las funciones del **handshake** de tres vías:

- Establece que el dispositivo de destino está presente en la red.
- Verifica que el dispositivo de destino tenga un servicio activo y esté aceptando solicitudes en el número de puerto de destino que el cliente iniciador pretende utilizar.
- Informa al dispositivo de destino que el cliente de origen tiene la intención de establecer una sesión de comunicación en ese número de puerto.

Una vez completada la comunicación, las sesiones se cierran y la conexión finaliza. Los mecanismos de conexión y sesión permiten la función de confiabilidad TCP.

**Campo de bits de control**:

Se muestra los campos de encabezado del segmento TCP con el campo de bits de control de 6 bits resaltado. Los seis bits en el campo Bits de control del encabezado del segmento TCP también se conocen como banderas. Una bandera es un bit que está activado o desactivado.

![Campo de bits de control](https://ccnadesdecero.es/wp-content/uploads/2020/04/Campo-de-bits-de-control.png)

Los seis indicadores de bits de control son los siguientes:

- **URG**: campo de puntero urgente significativo.
- **ACK**: indicador de reconocimiento utilizado en el establecimiento de la conexión y la finalización de la sesión.
- **PSH**: función de empuje.
- **RST**: restablece la conexión cuando se produce un error o un tiempo de espera.
- **SYN**: sincroniza los números de secuencia utilizados en el establecimiento de la conexión.
- **FIN**: no hay más datos del remitente y se utilizan en la finalización de la sesión.

[Vídeo: Protocolo de Enlace TCP de 3 Vías](https://www.youtube.com/watch?v=cm_2Jp7dQP8)

### 2.8. Fiabilidad y control de flujo

#### 2.8.1. Fiabilidad I: Entrega Garantizada y Ordenada

La razón por la que TCP es el mejor protocolo para algunas aplicaciones es porque, a diferencia de UDP, reenvía paquetes descartados y paquetes numerados para indicar su orden correcto antes de la entrega. TCP también puede ayudar a mantener el flujo de paquetes para que los dispositivos no se sobrecarguen. En este tema se tratan detalladamente estas características de TCP.

Puede haber ocasiones en que los segmentos TCP no lleguen a su destino. Otras veces, los segmentos TCP pueden llegar desordenados. Para que el destinatario entienda el mensaje original, se deben recibir todos los datos y los datos de estos segmentos deben volver a ensamblarse en el mensaje original. Los números de secuencia se asignan en el encabezado de cada paquete para lograr este objetivo. El número de secuencia representa el primer byte de datos del segmento TCP.

Durante la configuración de la sesión, se establece un número de secuencia inicial (ISN). Este ISN representa el valor inicial de los bytes que se transmiten a la aplicación receptora. A medida que los datos se transmiten durante la sesión, el número de secuencia se incrementa por el número de bytes que se han transmitido. Este seguimiento de bytes de datos permite que cada segmento se identifique y reconozca de forma única. Así, podemos identificar los segmentos que no se hayan entregado.

El ISN no comienza en uno, sino que es un número aleatorio. Esto es así para prevenir ciertos tipos de ataques maliciosos. No obstante, en muchos ejemplos se suelen emplear el número 1 por simplicidad.

Los números de secuencia de segmento indican cómo volver a armar y reordenar los segmentos recibidos, como se muestra en la imagen.

![Segmentos TCP se reordenan en destino](https://ccnadesdecero.es/wp-content/uploads/2020/04/Segmentos-TCP-se-reordenan-en-destino.png)

Aunque los segmentos pueden tomar diferentes rutas y llegar desordenados al destino, TCP tiene la capacidad de reordenar los segmentos.

El proceso TCP receptor coloca los datos del segmento en un búfer de recepción. Los segmentos se colocan en el orden de secuencia adecuado y se pasan a la capa de aplicación cuando se vuelven a montar. Todos los segmentos que lleguen con números de secuencia desordenados se retienen para su posterior procesamiento. A continuación, cuando llegan los segmentos con bytes faltantes, tales segmentos se procesan en orden.

Una de las funciones de TCP es garantizar que cada segmento llegue a su destino. Los servicios TCP en el host de destino reconocen los datos que ha recibido la aplicación de origen.

[Serie de videos acerca de TCP](https://www.youtube.com/watch?v=eNuC80Mzy0I)

[Video Fiabilidad de TCP](https://www.youtube.com/watch?v=ScXoIKcOwP8)

#### 2.8.2. Fiabilidad II: Pérdida y Retransmisión de Datos

No importa cuán bien diseñada esté una red, ocasionalmente se produce la pérdida de datos. TCP proporciona métodos para administrar la pérdida de segmentos. Entre estos está un mecanismo para retransmitir segmentos para los datos sin reconocimiento.

El número de secuencia (SEQ) y el número de acuse de recibo (ACK) se utilizan juntos para confirmar la recepción de los bytes de datos contenidos en los segmentos transmitidos. El número SEQ identifica el primer byte de datos en el segmento que se transmite. TCP utiliza el número de ACK reenviado al origen para indicar el próximo byte que el receptor espera recibir. Esto se llama acuse de recibo de expectativa.

Antes de mejoras posteriores, TCP solo podía reconocer el siguiente byte esperado. Por ejemplo, en la figura, utilizando números de segmento para simplificar, el host A envía los segmentos del 1 al 10 al host B. Si llegan todos los segmentos excepto los segmentos 3 y 4, el host B respondería con acuse de recibo especificando que el siguiente segmento esperado es el segmento 3. El host A no tiene idea de si algún otro segmento llegó o no. Por lo tanto, el host A reenviaría los segmentos 3 a 10. Si todos los segmentos de reenvío llegan correctamente, los segmentos 5 a 10 serían duplicados. Esto puede provocar retrasos, congestión e ineficiencias.

![Segmentos duplicados](https://ccnadesdecero.es/wp-content/uploads/2020/04/Segmentos-duplicados.png)

Los sistemas operativos actualmente suelen emplear una característica TCP opcional llamada reconocimiento selectivo (SACK), negociada durante el protocolo de enlace de tres vías. Si ambos hosts admiten SACK, el receptor puede reconocer explícitamente qué segmentos (bytes) se recibieron, incluidos los segmentos discontinuos. Por lo tanto, el host emisor solo necesitaría retransmitir los datos faltantes. Por ejemplo, en la siguiente figura, utilizando de nuevo números de segmento para simplificar, el host A envía los segmentos 1 a 10 al host B. Si llegan todos los segmentos excepto los segmentos 3 y 4, el host B puede reconocer que ha recibido los segmentos 1 y 2 (ACK 3) y reconocer selectivamente los segmentos 5 a 10 (SACK 5-10). El host A solo necesitaría reenviar los segmentos 3 y 4.

![Segmentos sin duplicar](https://ccnadesdecero.es/wp-content/uploads/2020/04/Segmentos-sin-duplicar.png)

Nota: TCP normalmente envía ACK para cualquier otro paquete, pero otros factores que están más allá del alcance de este tema pueden alterar este comportamiento.

TCP usa temporizadores para saber cuánto tiempo esperar antes de reenviar un segmento.

[Video Fiabilidad de TCP II](https://www.youtube.com/watch?v=8_em-0tkY5Y)

#### 2.8.3 Control de flujo I: Tamaño de Ventana y Acuses de Recibo

TCP también proporciona mecanismos para el control de flujo, que es la cantidad de datos que el destino puede recibir y procesar de manera confiable. Este control de flujo garantiza la confiabilidad de la transmisión de TCP mediante el ajuste de la velocidad del flujo de datos entre el origen y el destino para una sesión determinada. Para lograr esto, el encabezado TCP incluye un campo de 16 bits llamado "tamaño de la ventana".

En la figura se muestra un ejemplo de tamaño de ventana y reconocimientos.

![Ejemplo de tamaño de ventana TCP](https://ccnadesdecero.es/wp-content/uploads/2020/04/Ejemplo-de-tama%C3%B1o-de-ventana-TCP.png)

El tamaño de la ventana determina la cantidad de bytes que se pueden enviar antes de recibir un reconocimiento. El número de reconocimiento es el número del siguiente byte esperado.

El tamaño de la ventana es la cantidad de bytes que el dispositivo de destino de una sesión TCP puede aceptar y procesar al mismo tiempo. En este ejemplo, el tamaño de la ventana inicial de la PC B para la sesión TCP es de 10,000 bytes. A partir del primer byte, el byte 1, el último byte que la PC A puede enviar sin recibir un reconocimiento es el byte 10,000. Esto se conoce como la ventana de envío de la PC A. El tamaño de la ventana se incluye en cada segmento TCP para que el destino pueda modificar el tamaño de la ventana en cualquier momento, dependiendo de la disponibilidad del búfer.

El tamaño inicial de la ventana se acuerda cuando se establece la sesión TCP durante el establecimiento del enlace de tres vías. El dispositivo de origen debe limitar el número de bytes enviados al dispositivo de destino en función del tamaño de la ventana del destino. El dispositivo de origen puede continuar enviando más datos para la sesión solo cuando recibe un reconocimiento de los bytes enviados. Por lo general, el destino no esperará a que se reciban todos los bytes de su tamaño de ventana antes de responder con un acuse de recibo. A medida que se reciben y procesan los bytes, el destino envía reconocimientos para informar al origen que puede continuar enviando bytes adicionales.

Por ejemplo, es típico que la PC B no espere a recibir los 10,000 bytes completos antes de enviar un acuse de recibo. Esto significa que la PC A puede ajustar su ventana de envío a medida que recibe confirmaciones de la PC B. Como se muestra en la figura, cuando la PC A recibe una confirmación con el número de reconocimiento 2,921, que es el siguiente byte esperado, la ventana de envío de la PC A se incrementará en 2,920 bytes. Esto cambia la ventana de envío de 10,000 bytes a 12,920 bytes.

Un destino que envía confirmaciones a medida que procesa los bytes recibidos y el ajuste continuo de la ventana de envío del origen se conoce como "ventanas deslizantes". En el ejemplo anterior, la ventana de envío de la PC A se incrementa o desliza en 2,921 bytes, de 10,000 a 12,920 bytes.

Si disminuye la disponibilidad de espacio de búfer del destino, este puede reducir su tamaño de ventana para informar al origen que debe reducir el número de bytes enviados sin recibir un reconocimiento.

Nota: Los dispositivos actuales usan el protocolo de ventanas deslizantes (Sliding window protocol). El receptor generalmente envía un acuse de recibo después de cada dos segmentos que recibe. El número de segmentos recibidos antes de ser reconocido puede variar. La ventaja de las ventanas deslizantes es que permite al emisor transmitir segmentos continuamente, siempre que el receptor reconozca segmentos anteriores. Los detalles de las ventanas deslizantes están más allá del alcance de este curso.

#### 2.8.4 Control de flujo II: Tamaño Máximo de Segmento (MSS)

En la imagen, la fuente está transmitiendo 1.460 bytes de datos dentro de cada segmento TCP. Este suele ser el tamaño máximo de segmento (MSS) que puede recibir el dispositivo de destino. El MSS es parte del campo de opciones en el encabezado TCP que especifica la mayor cantidad de datos, en bytes, que un dispositivo puede recibir en un solo segmento TCP. El tamaño de MSS no incluye el encabezado TCP. El MSS generalmente se incluye durante el protocolo de enlace de tres vías.

![Tamaño máximo de segmento MSS](https://ccnadesdecero.es/wp-content/uploads/2020/04/Tama%C3%B1o-m%C3%A1ximo-de-segmento-MSS.png)

Un MSS común es de 1,460 bytes cuando se usa IPv4. Un host determina el valor de su campo MSS restando los encabezados IP y TCP de la unidad de transmisión máxima de Ethernet (MTU). En una interfaz Ethernet, la MTU predeterminada es 1500 bytes. Restando el encabezado IPv4 de 20 bytes y el encabezado TCP de 20 bytes, el tamaño predeterminado de MSS será 1460 bytes, como se muestra en la imagen.

![Tamaño predeterminado de MSS](https://ccnadesdecero.es/wp-content/uploads/2020/04/Tama%C3%B1o-predeterminado-de-MSS.png)

#### 2.8.5 Control de flujo III: Prevención de Congestiones

Cuando se produce congestión en una red, el Router sobrecargado descarta los paquetes. Cuando los paquetes que contienen segmentos TCP no llegan a su destino, se dejan sin confirmar. Al determinar la velocidad a la que se envían los segmentos TCP pero no se reconoce, la fuente puede asumir un cierto nivel de congestión de la red.

Siempre que haya congestión, se producirá la retransmisión de segmentos TCP perdidos desde la fuente. Si la retransmisión no se controla adecuadamente, la retransmisión adicional de los segmentos TCP puede empeorar la congestión. No solo se introducen nuevos paquetes con segmentos TCP en la red, sino que el efecto de retroalimentación de los segmentos TCP retransmitidos que se perdieron también aumentará la congestión. Para evitar y controlar la congestión, TCP emplea varios mecanismos, temporizadores y algoritmos para el manejo de la congestión.

Si la fuente determina que los segmentos TCP no se reconocen o no se reconocen de manera oportuna, entonces puede reducir el número de bytes que envía antes de recibir un reconocimiento. Como se ilustra en la imagen, la PC A detecta que hay congestión y, por lo tanto, reduce la cantidad de bytes que envía antes de recibir un acuse de recibo de la PC B.

![Control de congestión TCP](https://ccnadesdecero.es/wp-content/uploads/2020/04/Control-de-congesti%C3%B3n-TCP.png)

Los números de acuse de recibo corresponden al siguiente byte esperado y no a un segmento. Los números de segmento utilizados se simplifican con fines ilustrativos.

Ten en cuenta que es la fuente la que está reduciendo el número de bytes no reconocidos que envía y no el tamaño de ventana determinado por el destino.

#### 2.8.6. Resumen de Fiabilidad y Control de Flujo

Resumimos a continuación los conceptos clave de fiabilidad y control de flujo de TCP:

- El tamaño de ventana en TCP es un mecanismo esencial de control de flujo que determina la cantidad de datos que un emisor puede enviar sin recibir un reconocimiento (ACK) del receptor. Este tamaño sí sube y baja durante una sesión, adaptándose dinámicamente a las condiciones de la red y al estado del receptor.
- Control de Flujo: El receptor informa al emisor cuántos bytes puede recibir sin sobresaturarse mediante el campo de ventana de recepción en el encabezado TCP. Si el receptor está ocupado o tiene un búfer limitado, puede reducir el tamaño de ventana, indicándole al emisor que disminuya la tasa de envío.
- Control de Congestión: TCP implementa algoritmos como Slow Start, Congestion Avoidance, Fast Retransmit y Fast Recovery para detectar y responder a la congestión en la red. Por ejemplo:
  - Slow Start: Al iniciar una conexión, TCP comienza enviando paquetes lentamente y aumenta el tamaño de ventana exponencialmente hasta detectar pérdidas o alcanzar un umbral.
  - Congestion Avoidance: Después de alcanzar el umbral, el tamaño de ventana aumenta linealmente para evitar congestión.
  - Respuesta a Pérdidas: Si se detecta pérdida de paquetes, TCP reduce drásticamente el tamaño de ventana para aliviar la congestión. Este comportamiento dinámico permite que TCP ajuste eficientemente el flujo de datos, aumentando la ventana cuando la red es rápida y estable, y reduciéndola cuando hay congestión o problemas.
- Máximo Tamaño de Segmento (MSS): El MSS es el tamaño máximo de segmento de datos que un dispositivo está dispuesto a recibir en una sola unidad TCP. A diferencia del tamaño de ventana, el MSS no cambia durante una sesión; se establece al inicio y permanece constante para evitar fragmentación y garantizar eficiencia.

## 3. User Datagram Protocol (UDP)

El **UDP** es un protocolo sin conexión y sin garantías de entrega (*best effort*):

- **Baja Sobrecarga**: Menos control y gestión que TCP, lo que permite mayor velocidad.
- **Sin Control de Flujo ni Congestión**: No ajusta la tasa de envío ni retransmite datos perdidos.
- **Uso Ideal**: Aplicaciones donde la velocidad es crítica y se tolera la pérdida de algunos datos, como streaming de video o voz, y juegos en línea.

Las características UDP incluyen lo siguiente:

- Los datos se reconstruyen en el orden en que se recibieron.
- Los segmentos perdidos no se vuelven a enviar.
- No hay establecimiento de sesión.
- El envío no está informado sobre la disponibilidad de recursos.

**UDP** es como enviar una postal. No hay confirmación de recepción, pero es rápido y sencillo. Ideal para mensajes breves donde la pérdida ocasional es tolerable.

UDP es un protocolo de capa de transporte más simple que TCP. No proporciona confiabilidad y control de flujo, lo que significa que requiere menos campos de encabezado. Debido a que los procesos UDP del emisor y del receptor no tienen que administrar la confiabilidad y el control de flujo, esto significa que los datagramas UDP pueden procesarse más rápido que los segmentos TCP. UDP proporciona las funciones básicas para entregar datagramas entre las aplicaciones apropiadas, con muy poca sobrecarga y verificación de datos.

Nota: UDP divide los datos en datagramas que también se denominan segmentos.

UDP es un protocolo sin conexión. Debido a que UDP no proporciona confiabilidad o control de flujo, no requiere una conexión establecida. Debido a que UDP no rastrea la información enviada o recibida entre el cliente y el servidor, UDP también se conoce como un protocolo sin estado.

UDP también se conoce como un protocolo de entrega de mejor esfuerzo porque no hay reconocimiento de que los datos se reciben en el destino. Con UDP, no hay procesos de capa de transporte que informen al remitente de una entrega exitosa.

UDP es como colocar una carta regular, no registrada, en el correo. El remitente de la carta no tiene conocimiento de la disponibilidad del receptor para recibir la carta. La oficina de correos tampoco es responsable de rastrear la carta o informar al remitente si la carta no llega al destino final.

![Protocolo de datagramas de usuario UDP](https://examenredes.com/wp-content/uploads/2021/12/14.1.5.gif)

### 3.1. Casos de uso de UDP vs TCP

Algunas aplicaciones pueden tolerar cierta pérdida de datos durante la transmisión a través de la red, pero los retrasos en la transmisión son inaceptables. Para estas aplicaciones, UDP es la mejor opción porque requiere menos sobrecarga de red. UDP es preferible para aplicaciones como Voz sobre IP (VoIP). Los reconocimientos y la retransmisión retrasarían la entrega y harían inaceptable la conversación de voz.

UDP también es utilizado por las aplicaciones de solicitud y respuesta donde los datos son mínimos y la retransmisión se puede hacer rápidamente. Por ejemplo, el servicio de nombres de dominio (DNS) usa UDP para este tipo de transacción. El cliente solicita direcciones IPv4 e IPv6 para un nombre de dominio conocido de un servidor DNS. Si el cliente no recibe una respuesta en un período de tiempo predeterminado, simplemente envía la solicitud nuevamente.

Por ejemplo, si uno o dos segmentos de una transmisión de video en vivo no llegan, se crea una interrupción momentánea en la transmisión. Esto puede aparecer como una distorsión en la imagen o el sonido, pero puede que el usuario no lo note. Si el dispositivo de destino tuviera que dar cuenta de la pérdida de datos, la transmisión podría retrasarse mientras se esperaban las retransmisiones, por lo que la imagen o el sonido se degradarían mucho. En este caso, es mejor renderizar los mejores medios posibles con los segmentos recibidos y renunciar a la fiabilidad.

Para otras aplicaciones, es importante que lleguen todos los datos y que puedan procesarse en su secuencia adecuada. Para este tipo de aplicaciones, TCP se utiliza como protocolo de transporte. Por ejemplo, las aplicaciones como bases de datos, navegadores web y clientes de correo electrónico requieren que todos los datos enviados lleguen al destino en su estado original. Cualquier dato faltante podría corromper una comunicación, haciéndola incompleta o ilegible. Por ejemplo, es importante cuando se accede a la información bancaria a través de la web para asegurarse de que toda la información se envíe y reciba correctamente.

Los desarrolladores de aplicaciones deben elegir qué tipo de protocolo de transporte es apropiado en función de los requisitos de las aplicaciones. El video puede enviarse a través de TCP o UDP. Las aplicaciones que transmiten audio y video almacenado generalmente usan TCP. La aplicación utiliza TCP para realizar almacenamiento en búfer, sondeo de ancho de banda y control de congestión, a fin de controlar mejor la experiencia del usuario.

El video y la voz en tiempo real generalmente usan UDP, pero también pueden usar TCP, o tanto UDP como TCP. Una aplicación de videoconferencia puede usar UDP de manera predeterminada, pero debido a que muchos firewalls bloquean UDP, la aplicación también se puede enviar a través de TCP.

Las aplicaciones que transmiten audio y video almacenado usan TCP. Por ejemplo, si tu red de repente no puede soportar el ancho de banda necesario para ver una película a pedido, la aplicación detiene la reproducción. Durante la pausa, es posible que vea un mensaje de “almacenamiento en búfer …” mientras TCP trabaja para restablecer la transmisión. Cuando todos los segmentos están en orden y se restaura un nivel mínimo de ancho de banda, se reanuda la sesión TCP y se reanuda la reproducción de la película.

La imagen resume las diferencias entre UDP y TCP.

![Diferencias entre UDP y TCP](https://ccnadesdecero.es/wp-content/uploads/2017/11/Diferencias-entre-UDP-y-TCP.png)

### 3.2. Comparación de Baja Sobrecarga y Confiabilidad de UDP

Como se explicó anteriormente, UPD es perfecto para comunicaciones que necesitan ser rápidas, como VoIP. Este tema explica en detalle por qué UDP es perfecto para algunos tipos de transmisiones. Como se muestra en la figura, UDP no establece una conexión. UDP suministra transporte de datos con baja sobrecarga debido a que posee un encabezado de datagrama pequeño sin tráfico de administración de red.

![UDP de baja sobrecarga frente a fiabilidad](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_182709.jpg)

### 3.3. Reensamblaje de Datagramas UDP

Al igual que los segmentos con TCP, cuando los datagramas UDP se envían a un destino, a menudo toman diferentes caminos y llegan en el orden incorrecto. UDP no rastrea los números de secuencia como lo hace TCP. UDP no tiene forma de reordenar los datagramas en su orden de transmisión, como se muestra en la imagen.

Por lo tanto, UDP simplemente vuelve a ensamblar los datos en el orden en que se recibieron y los reenvía a la aplicación. Si la secuencia de datos es importante para la aplicación, la aplicación debe identificar la secuencia adecuada y determinar cómo se deben procesar los datos.

UDP sin conexión y no confiable

![UDP sin conexión y no confiable](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_182742.jpg)

### 3.4. Procesos y Solicitudes del Servidor UDP

Al igual que las aplicaciones basadas en TCP, a las aplicaciones de servidor basadas en UDP se les asignan números de puerto conocidos o registrados, como se muestra en la imagen. Cuando estas aplicaciones o procesos se ejecutan en un servidor, aceptan los datos que coinciden con el número de puerto asignado. Cuando UDP recibe un datagrama destinado a uno de estos puertos, reenvía los datos de la aplicación a la aplicación adecuada en función de su número de puerto.

![UDP sin conexión y no confiable](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_182815.jpg)

Nota: El Remote Authentication Dial-in User Service (RADIUS) que se muestra en la imagen proporciona servicios de autenticación, autorización y contabilidad para administrar el acceso de los usuarios. El funcionamiento de RADIUS está más allá del alcance de este curso.

### 3.5. Procesos de Cliente UDP

Como en TCP, la comunicación cliente-servidor es iniciada por una aplicación cliente que solicita datos de un proceso de servidor. El proceso de cliente UDP selecciona dinámicamente un número de puerto del intervalo de números de puerto y lo utiliza como puerto de origen para la conversación. Por lo general, el puerto de destino es el número de puerto bien conocido o registrado que se asigna al proceso de servidor.

Después de que un cliente ha seleccionado los puertos de origen y destino, se utiliza el mismo par de puertos en el encabezado de todos los datagramas en la transacción. Para la devolución de datos del servidor al cliente, se invierten los números de puerto de origen y destino en el encabezado del datagrama.

Abajo se presenta una ilustración de dos hosts que solicitan servicios del servidor de autenticación DNS y RADIUS.

**Clientes Mandando Solicitudes UDP**: El cliente 1 está enviando una solicitud DNS utilizando el conocido puerto 53, mientras que el cliente 2 solicita servicios de autenticación RADIUS mediante el puerto registrado 1812.

![Solicitud UDP de Puertos de Origen](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_183011.jpg)

**Solicitud UDP de Puertos de Origen**: Las solicitudes de los clientes generan dinámicamente números de puerto de origen. En este caso, el cliente 1 está utilizando el puerto de origen 49152 y el cliente 2 está utilizando el puerto de origen 51152.

![UDP Solicitud de Puertos de Origen](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_183053.jpg)

**UDP Solicitud de Puertos de Origen**: Cuando el servidor responde a las solicitudes del cliente, invierte los puertos de destino y origen de la solicitud inicial.

![Destino de respuesta UDP](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_183150.jpg)

**Destino de respuesta UDP**: En la respuesta del servidor a la solicitud DNS ahora es el puerto de destino 49152 y la respuesta de autenticación RADIUS ahora es el puerto de destino 51152.

![UDP Respuesta de Puertos de Origen](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_183215.jpg)

**UDP Respuesta de Puertos de Origen**: Los puertos de origen en la respuesta del servidor son los puertos de destino originales en las solicitudes iniciales.

![UDP Communication](https://examenredes.com/wp-content/uploads/2021/12/2021-12-29_183240.jpg)

## 4. Puertos: Identificando Procesos en Comunicación

Los **puertos** son números que identifican de manera única a los procesos dentro de un dispositivo. Funcionan como puntos finales de comunicación en la capa de transporte. Gracias a los puertos:

- Se puede especificar exactamente qué proceso en el dispositivo destino debe recibir los datos.
- Es posible la **multiplexación**, permitiendo que múltiples conexiones existan simultáneamente.
- Se organiza y gestiona el tráfico de red de manera eficiente.

Los números de puerto se dividen en rangos:

- **Puertos Bien Conocidos (0-1023)**: Reservados para servicios y aplicaciones estándar (por ejemplo, el puerto 80 para HTTP).
- **Puertos Registrados (1024-49151)**: Asignados para aplicaciones y procesos específicos.
- **Puertos Dinámicos o Privados (49152-65535)**: Utilizados temporalmente por aplicaciones cliente al establecer conexiones.

### 4.1. Comunicaciones Múltiples Separadas

Hay algunas situaciones en las que TCP es el protocolo adecuado para el trabajo, y otras situaciones en las que se debe utilizar UDP. No importa qué tipo de datos se transporten, tanto TCP como UDP usan números de puerto.

Los protocolos de capa de transporte TCP y UDP utilizan números de puerto para administrar múltiples conversaciones simultáneas. Como se muestra en la figura, los campos de encabezado TCP y UDP identifican un número de puerto de aplicación de origen y destino.

Puerto de origen (16) | Puerto de destino (16)

El número de puerto de origen está asociado con la aplicación de origen en el host local, mientras que el número de puerto de destino está asociado con la aplicación de destino en el host remoto.

Por ejemplo, supón que un host está iniciando una solicitud de página web desde un servidor web. Cuando el host inicia la solicitud de la página web, el host genera dinámicamente el número de puerto de origen para identificar de forma exclusiva la conversación. Cada solicitud generada por un host utilizará un número de puerto de origen creado dinámicamente diferente. Este proceso permite que se produzcan múltiples conversaciones simultáneamente.

En la solicitud, el número de puerto de destino es lo que identifica el tipo de servicio que se solicita del servidor web de destino. Por ejemplo, cuando un cliente especifica el puerto 80 en el puerto de destino, el servidor que recibe el mensaje sabe que se están prestando servicios web pedido.

Un servidor puede ofrecer más de un servicio simultáneamente, como servicios web en el puerto 80, mientras que ofrece el establecimiento de conexión de Protocolo de transferencia de archivos (FTP) en el puerto 21.

### 4.2. Pares de Socket

Los puertos de origen y destino se colocan dentro del segmento. Los segmentos se encapsulan dentro de un paquete IP. El paquete IP contiene la dirección IP de origen y destino. La combinación de la dirección IP de origen y el número de puerto de origen, o la dirección IP de destino y el número de puerto de destino se conoce como socket.

En el ejemplo de la imagen, la PC solicita simultáneamente servicios FTP y web del servidor de destino.

![Pares de Socket](https://ccnadesdecero.es/wp-content/uploads/2020/04/Pares-de-Socket.png)

En el ejemplo, la solicitud FTP generada por la PC incluye las direcciones MAC de capa 2 y las direcciones IP de capa 3. La solicitud también identifica el número de puerto de origen 1305 (es decir, generado dinámicamente por el host) y el puerto de destino, identificando los servicios FTP en el puerto 21. El host también ha solicitado una página web del servidor utilizando las mismas direcciones de Capa 2 y Capa 3 . Sin embargo, está utilizando el número de puerto de origen 1099 (es decir, generado dinámicamente por el host) y el puerto de destino que identifica el servicio web en el puerto 80.

El socket se utiliza para identificar el servidor y el servicio que solicita el cliente. Un socket de cliente podría verse así, con 1099 representando el número de puerto de origen: 192.168.1.5:1099. Por su parte, el socket en un servidor web puede ser 192.168.1.7:80.

Juntos, estos dos sockets se combinan para formar un par de sockets: 192.168.1.5:1099, 192.168.1.7:80

Los sockets permiten que múltiples procesos, que se ejecutan en un cliente, se distingan entre sí, y que múltiples conexiones a un proceso de servidor se distingan entre sí.

El número de puerto de origen actúa como una dirección de retorno para la aplicación solicitante. La capa de transporte realiza un seguimiento de este puerto y la aplicación que inició la solicitud para que cuando se devuelva una respuesta, se pueda reenviar a la aplicación correcta.

### 4.3. Grupos de número de puerto

La Internet Assigned Numbers Authority (IANA) es la organización de estándares responsable de asignar varios estándares de direccionamiento, incluidos los números de puerto de 16 bits. Los 16 bits utilizados para identificar los números de puerto de origen y destino proporcionan un rango de puertos de 0 a 65535.

La IANA ha dividido el rango de números en los siguientes tres grupos de puertos.

| Grupo de puertos | Rango | Descripción |
|------------------|-------|-------------|
| Puertos Bien Conocidos | 0-1023 | Estos números de puerto están reservados para servicios y aplicaciones comunes o populares, como navegadores web, clientes de correo electrónico y clientes de acceso remoto. Los puertos bien conocidos definidos para aplicaciones de servidor comunes permiten a los clientes identificar fácilmente el servicio asociado requerido |
| Puertos registrados | 1024-49151 | La IANA asigna estos números de puerto a una entidad solicitante para usar con procesos o aplicaciones específicos. Estos procesos son principalmente aplicaciones individuales que un usuario ha elegido instalar, en lugar de aplicaciones comunes que recibirían un número de puerto conocido. Por ejemplo, Cisco ha registrado el puerto 1812 para su proceso de autenticación del servidor RADIUS |
| Puertos privados y/o dinámicos | 49152 a 65535 | Estos puertos también se conocen como puertos efímeros. El sistema operativo del cliente generalmente asigna números de puerto dinámicamente cuando se inicia una conexión a un servicio. El puerto dinámico se utiliza para identificar la aplicación del cliente durante la comunicación. |

> [!NOTE]
> Algunos sistemas operativos de clientes pueden usar números de puerto registrados en lugar de números de puerto dinámicos para asignar puertos de origen.

La tabla muestra algunos números de puerto conocidos y sus aplicaciones asociadas.

| Número de puerto | Protocolo | Solicitud |
|------------------|-----------|-----------|
| 20               | TCP       | Protocolo de transferencia de archivos (FTP) - Datos |
| 21               | TCP       | Protocolo de transferencia de archivos (FTP) - Control |
| 22               | TCP       | Shell seguro (SSH) |
| 23               | TCP       | Telnet |
| 25               | TCP       | Protocolo simple de transferencia de correo (SMTP) |
| 53               | UDP, TCP  | Servicio de nombres de dominio (DNS) |
| 67               | UDP       | Protocolo de configuración dinámica de host (DHCP): servidor |
| 68               | UDP       | Protocolo de configuración dinámica de host: cliente |
| 69               | UDP       | Protocolo trivial de transferencia de archivos (TFTP) |
| 80               | TCP       | Protocolo de transferencia de hipertexto (HTTP) |
| 110              | TCP       | Protocolo de oficina de correos versión 3 (POP3) |
| 143              | TCP       | Protocolo de acceso a mensajes de Internet (IMAP) |
| 161              | UDP       | Protocolo simple de administración de red (SNMP) |
| 443              | TCP       | Protocolo de transferencia de hipertexto seguro (HTTPS) |

Algunas aplicaciones pueden usar tanto TCP como UDP. Por ejemplo, DNS usa UDP cuando los clientes envían solicitudes a un servidor DNS. Sin embargo, la comunicación entre dos servidores DNS siempre usa TCP.

El el sitio web de la IANA se puede encontrar una lista completa de los números de puerto asignados.

### 4.4. El Comando netstat

Las conexiones TCP no descritas pueden representar una gran amenaza de seguridad. Pueden indicar que algo o alguien está conectado al host local. A veces es necesario saber qué conexiones TCP activas están abiertas y ejecutándose en un host en red. Netstat es una importante utilidad de red que se puede usar para verificar esas conexiones. Como se muestra a continuación, ingresa el comando netstat para enumerar los protocolos en uso, la dirección local y los números de puerto, la dirección extranjera y los números de puerto y el estado de la conexión.

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

De manera predeterminada, el comando `netstat` intentará resolver las direcciones IP para nombres de dominio y números de puerto para aplicaciones conocidas. La opción `-n` se puede usar para mostrar las direcciones IP y los números de puerto en su forma numérica.

## 5. Otros protocolos Emergentes

Los desarrollos tecnológicos recientes y las crecientes demandas de aplicaciones avanzadas han impulsado la evolución de la capa de transporte. Entre estas necesidades se destacan:

### 5.1. Internet de las Cosas (IoT)

- **Proliferación de Dispositivos**: La conexión de millones de dispositivos requiere protocolos eficientes y escalables.
- **Protocolos Ligeros**: Como **MQTT** y **CoAP**, ideales para dispositivos con recursos limitados y comunicaciones de baja potencia.
- **Seguridad**: La protección de datos y dispositivos es esencial, especialmente por el volumen y la sensibilidad de la información manejada.

### 5.2. Redes 5G y Futuras Generaciones

- **Alta Velocidad y Baja Latencia**: Estas redes demandan protocolos de transporte que maximicen estas características.
- **Aplicaciones en Tiempo Real**: Tecnologías como la realidad aumentada, vehículos autónomos y telemedicina requieren comunicaciones rápidas y fiables.
- **Edge Computing**: El procesamiento de datos cercano a su origen reduce la carga en la red central y mejora los tiempos de respuesta.

### 5.3. Protocolo Rápido de Internet Basado en UDP (QUIC)

Ante estas necesidades, han surgido protocolos innovadores como **QUIC**. Desarrollado por Google, **QUIC** combina las ventajas de TCP y UDP:

- **Basado en UDP**: Utiliza UDP para evitar limitaciones en redes donde TCP puede ser bloqueado o manipulado.
- **Establecimiento de Conexión Rápido**: Reduce la latencia al combinar el handshake de transporte y seguridad en un solo paso.
- **Cifrado Incorporado**: Integra TLS 1.3 para ofrecer seguridad desde el diseño.
- **Multiplexación de Flujos**: Permite múltiples flujos independientes en una sola conexión, evitando bloqueos.
- **Optimización para Móviles**: Diseñado para adaptarse a cambios frecuentes de conexión en dispositivos móviles.

**Analogía**: **QUIC** se asemeja a un mensaje instantáneo cifrado a través de una aplicación de mensajería segura: rápido, seguro y eficiente.

### 5.4. Stream Control Transmission Protocol (SCTP)

Otro protocolo emergente es el **SCTP**, que proporciona características avanzadas frente a TCP y UDP:

- **Multistreaming**: Permite múltiples flujos de datos independientes apilados dentro de una única conexión.
- **Multihoming**: Un solo punto final puede tener varias direcciones IP, mejorando la tolerancia a fallos.
- **Entrega Fiable y Ordenada**: Aunque similar a TCP, **SCTP** ofrece mayor flexibilidad en la gestión de flujos.

## 6. Seguridad Integrada en la Capa de Transporte

La seguridad es fundamental en las comunicaciones de red, y la capa de transporte actúa como el punto de control para garantizar la confidencialidad, integridad y autenticación de los datos. Las tecnologías clave en este ámbito incluyen:

### **TLS (Transport Layer Security) y SSL (Secure Sockets Layer)**

- **Cifrado de Datos**: Protege la confidencialidad de la información transmitida.
- **Autenticación**: Verifica la identidad de las partes que se comunican.
- **Integridad**: Asegura que los datos no sean alterados durante la transmisión.

**SSL** fue el precursor de **TLS**, ofreciendo inicialmente cifrado y autenticación en las comunicaciones en red. Aunque **SSL** ya no se considera seguro y ha sido reemplazado por **TLS**, su legado es significativo en la evolución de la seguridad de la capa de transporte.

La seguridad ya no es una opción adicional; es una necesidad integrada. Protocolos como **QUIC** incorporan **TLS** de forma nativa, garantizando conexiones seguras sin pasos adicionales.

## 7. Conclusión

La capa de transporte es fundamental en las comunicaciones de red, y su comprensión es esencial para cualquier profesional en informática. Los avances tecnológicos y las nuevas demandas de aplicaciones requieren una actualización constante de los conocimientos.

La capa de transporte es el enlace entre la capa de aplicación y las capas inferiores que son responsables de la transmisión a través de la red. La capa de transporte es responsable de las comunicaciones lógicas entre aplicaciones que se ejecutan en diferentes hosts. La capa de transporte incluye los protocolos TCP y UDP. Los protocolos de capa de transporte especifican cómo transferir mensajes entre hosts y es responsable de administrar los requisitos de fiabilidad de una conversación. La capa de transporte es responsable del seguimiento de conversaciones (sesiones), la segmentación de datos y el reensamblaje de segmentos, la adición de información de encabezado, la identificación de aplicaciones y la multiplexación de conversaciones. TCP is stateful, reliable, acknowledges data, resends lost data, and delivers data in sequenced order. Utilice TCP para el correo electrónico y la web. UDP no tiene estado, es rápido, tiene una sobrecarga baja, no requiere acuses de recibo, no reenvía los datos perdidos y entrega los datos en el orden en que llegan. Use UDP para VoIP y DNS.

TCP establece sesiones, asegura confiabilidad, proporciona entrega del mismo pedido y admite control de flujo. Un segmento TCP agrega 20 bytes de sobrecarga como información de encabezado al encapsular los datos de capa de aplicación. Los campos de encabezado TCP son los puertos de origen y destino, número de secuencia, número de reconocimiento, longitud del encabezado, reservado, bits de control, tamaño de ventana, suma de verificación y urgente. Las aplicaciones que usan TCP son HTTP, FTP, SMTP y Telnet.

UDP reconstruye los datos en el orden en que se reciben, los segmentos perdidos no se vuelven a enviar, no se establece la sesión y UPD no informa al remitente de la disponibilidad de recursos. Los campos de encabezado UDP son puertos de origen y destino, longitud y suma de verificación. Las aplicaciones que utilizan UDP son DHCP, DNS, SNMP, TFTP, VoIP y videoconferencias.

Los protocolos de capa de transporte TCP y UDP utilizan números de puerto para administrar múltiples conversaciones simultáneas. Esta es la razón por la que los campos de encabezado TCP y UDP identifican un número de puerto de aplicación de origen y destino. Los puertos de origen y de destino se colocan dentro del segmento. Los segmentos se encapsulan dentro de un paquete IP. El paquete IP contiene la dirección IP de origen y de destino. Se conoce como socket a la combinación de la dirección IP de origen y el número de puerto de origen, o de la dirección IP de destino y el número de puerto de destino. El socket se utiliza para identificar el servidor y el servicio que solicita el cliente. Hay un rango de números de puerto entre 0 y 65535. Esta gama se divide en grupos: Puertos conocidos, Puertos Registrados, Puertos Privados y/o Dinámicos. Hay algunos números de puerto conocidos que están reservados para aplicaciones comunes como FTP, SSH, DNS, HTTP y otros. A veces es necesario conocer las conexiones TCP activas que están abiertas y en ejecución en el host de red. Netstat es una utilidad de red importante que puede usarse para verificar esas conexiones.

Cada proceso de aplicación que se ejecuta en el servidor para utilizar un número de puerto. El número de puerto es asignado automáticamente o configurado manualmente por un administrador del sistema. Los procesos del servidor TCP son los siguientes: clientes que envían solicitudes TCP, solicitan puertos de destino, solicitan puertos de origen, responden a solicitudes de puerto de destino y puerto de origen. Para terminar una conversación simple admitida por TCP, se requieren cuatro intercambios para finalizar ambas sesiones. El cliente o el servidor pueden iniciar la terminación. El protocolo de enlace de tres vías establece que el dispositivo de destino está presente en la red, verifica que el dispositivo de destino tiene un servicio activo y acepta solicitudes en el número de puerto de destino que el cliente iniciador pretende utilizar, e informa al dispositivo de destino que el cliente de origen tiene la intención de establecer una sesión de comunicación sobre ese número de puerto. Los seis indicadores de bits de control son: URG, ACK, PSH, RST, SYN y FIN.

Para que el receptor comprenda el mensaje original, los datos en estos segmentos se vuelven a ensamblar en el orden original. Se asignan números de secuencia en el encabezado de cada paquete. No importa cuán bien diseñada esté una red, ocasionalmente se produce la pérdida de datos. TCP proporciona formas de administrar pérdidas de segmentos. Hay un mecanismo para retransmitir segmentos para datos no reconocidos. Los sistemas operativos host actualmente suelen emplear una característica TCP opcional llamada reconocimiento selectivo (SACK), negociada durante el protocolo de enlace de tres vías. Si ambos hosts admiten SACK, el receptor puede reconocer explícitamente qué segmentos (bytes) se recibieron, incluidos los segmentos discontinuos. Por lo tanto, el host emisor solo necesitaría retransmitir los datos faltantes. El control de flujo permite mantener la confiabilidad de la transmisión de TCP mediante el ajuste de la velocidad del flujo de datos entre el origen y el destino. Para lograr esto, el encabezado TCP incluye un campo de 16 bits llamado “tamaño de la ventana”. El proceso en el que el destino envía reconocimientos a medida que procesa los bytes recibidos y el ajuste continuo de la ventana de envío del origen se conoce como ventanas deslizantes. El origen está transmitiendo 1460 bytes de datos dentro de cada segmento TCP. Este es el MSS típico que puede recibir un dispositivo de destino. Para evitar y controlar la congestión, TCP emplea varios mecanismos de manejo de congestión. Es la fuente la que está reduciendo el número de bytes no reconocidos que envía y no el tamaño de ventana determinado por el destino.

UDP es un protocolo simple que proporciona las funciones básicas de la capa de transporte. Cuando los datagramas UDP se envían a un destino, a menudo toman caminos diferentes y llegan en el orden incorrecto. UDP no realiza un seguimiento de los números de secuencia de la manera en que lo hace TCP. UDP no puede reordenar los datagramas en el orden de la transmisión. UDP simplemente reensambla los datos en el orden en que se recibieron y los envía a la aplicación. Si la secuencia de datos es importante para la aplicación, esta debe identificar la secuencia adecuada y determinar cómo se deben procesar los datos. A las aplicaciones de servidor basadas en UDP se les asignan números de puerto conocidos o registrados. Cuando UDP recibe un datagrama destinado a uno de esos puertos, envía los datos de aplicación a la aplicación adecuada en base a su número de puerto. El proceso de cliente UDP selecciona dinámicamente un número de puerto del intervalo de números de puerto y lo utiliza como puerto de origen para la conversación. Por lo general, el puerto de destino es el número de puerto bien conocido o registrado que se asigna al proceso de servidor. Después de que un cliente ha seleccionado los puertos de origen y destino, se utiliza el mismo par de puertos en el encabezado de todos los datagramas utilizados en la transacción. Para la devolución de datos del servidor al cliente, se invierten los números de puerto de origen y destino en el encabezado del datagrama.

## 8. Referencias

- <https://ccnadesdecero.es/ccna-1/#Modulo_14_Capa_de_Transporte_CCNA_1_v7>
- <https://examenredes.com/ccna-1-version-7-modulo-14-capa-de-transporte/>
