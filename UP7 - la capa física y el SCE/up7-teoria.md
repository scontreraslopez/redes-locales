# UP7. La capa física y el Sistema de Cableado Estructurado (SCE)

## 1. Introducción

En esta unidad se abordará la capa física de la red, que incluye el medio de transmisión y los dispositivos de interconexión. Se estudiarán los distintos tipos de cables y conectores, así como las normativas que regulan la instalación de redes de cableado estructurado.

## 2. Propósito de la capa física

### 2.1. La conexión física

Para que se pueda producir cualquier comunicación es imprescindible contar con conexiones físicas, aunque irremediablemente pensemos en una conexión por cable (red cableada) estas también pueden ser conexiones inalámbricas mediante ondas de radio (red inalámbrica).

El tipo de conexión física utilizada depende de varios factores, como la facilidad de instalación y las necesidades específicas. Por ejemplo, las conexiones por cable son comunes en ordenadores de sobremesa en oficinas, mientras que las conexiones inalámbricas son más adecuadas para portátiles, tablets y smartphones debido a su movilidad y flexibilidad.

En el caso de los dispositivos inalámbricos, los datos se transmiten mediante ondas de radio. La conectividad inalámbrica es común a medida que las personas y las empresas descubren sus ventajas. Los dispositivos en una red inalámbrica deben estar conectados a un punto de acceso inalámbrico (AP) o router inalámbrico como el que se muestra en la figura.

#### Router inalámbrico

![Router inalámbrico](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084032.jpg)

Estos son los componentes de un punto de acceso:

- Las antenas inalámbricas (Estas están integradas dentro de la versión del router que se muestra en la figura anterior).
- Puerto Ethernet/LAN: Conecta el punto de acceso a la red principal (por ejemplo, un router o switch) y también permite la comunicación con otros dispositivos en la red.

Al igual que una oficina corporativa, la mayoría de los hogares ofrecen conectividad cableada e inalámbrica a la red. Las cifras muestran un router doméstico y una computadora portátil que se conectan a la red de área local (LAN).

#### Conexión por cable al router inalámbrico

![Tarjetas de interfaz de red](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084108.jpg)

Las tarjetas de interfaz de red (NIC) conectan un dispositivo a la red. Las NIC de Ethernet se usan para una conexión por cable, como se muestra en la figura, mientras que las NIC de la red de área local inalámbrica (WLAN) se usan para la conexión inalámbrica. Los dispositivos para usuarios finales pueden incluir un tipo de NIC o ambos. Una impresora de red, por ejemplo, puede contar solo con una NIC Ethernet y, por lo tanto, se debe conectar a la red mediante un cable Ethernet. Otros dispositivos, como las tabletas y los teléfono inteligentes, pueden contener solo una NIC WLAN y deben utilizar una conexión inalámbrica.

#### Conexión por cable con una NIC Ethernet

En términos de rendimiento, no todas las conexiones físicas son iguales a la hora de conectarse a una red.

### 2.2. La capa física

La capa física de OSI proporciona los medios de transporte de los bits que conforman una trama de la capa de enlace de datos a través de los medios de red. Esta capa acepta una trama completa desde la capa de enlace de datos y la codifica como una secuencia de señales que se transmiten en los medios locales. Un dispositivo final o un dispositivo intermediario recibe los bits codificados que componen una trama.

Haga clic en Reproducir en la figura para ver un ejemplo del proceso de encapsulación. La última parte de este proceso muestra los bits que se envían a través del medio físico. La capa física codifica las tramas y crea las señales eléctricas, ópticas o de ondas de radio que representan los bits en cada trama. Estas señales se envían por los medios, una a la vez.

La capa física del nodo de destino recupera estas señales individuales de los medios, las restaura a sus representaciones en bits y pasa los bits a la capa de enlace de datos en forma de trama completa.

![Proceso de encapsulación](https://examenredes.com/wp-content/uploads/2021/12/4.1.2a.gif)
https://examenredes.com/wp-content/uploads/2021/12/4.1.2a.gif

### 2.3. Estándares de la capa física

En el tema anterior, obtuvo una visión general de alto nivel de la capa física y su lugar en una red. Este tema profundiza un poco más en los detalles de la capa física. Esto incluye los componentes y los medios utilizados para construir una red, así como los estándares necesarios para que todo funcione en conjunto.

Los protocolos y las operaciones de las capas OSI superiores se llevan a cabo en software diseñado por ingenieros en software e informáticos. El grupo de trabajo de ingeniería de Internet (IETF) define los servicios y protocolos del conjunto TCP/IP.

La capa física consta de circuitos electrónicos, medios y conectores desarrollados por ingenieros. Por lo tanto, es necesario que las principales organizaciones especializadas en ingeniería eléctrica y en comunicaciones definan los estándares que rigen este hardware.

Existen muchas organizaciones internacionales y nacionales, organizaciones de regulación gubernamentales y empresas privadas que intervienen en el establecimiento y el mantenimiento de los estándares de la capa física. Por ejemplo, los estándares de hardware, medios, codificación y señalización de la capa física están definidos y regidos por estas organizaciones de estándares:

- Organización Internacional para la Estandarización (ISO)
- Asociación de las Industrias de las Telecomunicaciones (TIA) y Asociación de Industrias Electrónicas (EIA)
- Unión Internacional de Telecomunicaciones (ITU)
- Instituto Nacional Estadounidense de Estándares (ANSI)
- Instituto de Ingenieros Eléctricos y Electrónicos (IEEE)
- Autoridades nacionales reguladoras de las telecomunicaciones, incluida la Federal Communication Commission (FCC) de los Estados Unidos y el Instituto Europeo de Estándares de Telecomunicaciones (ETSI)

Además de estos, a menudo hay grupos de normas de cableado regionales como CSA (Asociación de Normas Canadienses), CENELEC (Comité Europeo de Normalización Electrotécnica) y JSA / JIS (Asociación de Normas Japonesas), que desarrollan especificaciones locales.

![Estándares de la capa física](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084438.jpg)