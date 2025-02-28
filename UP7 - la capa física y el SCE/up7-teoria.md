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

![Conexión por cable al router inalámbrico](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084108.jpg)

Las tarjetas de interfaz de red (NIC) conectan un dispositivo a la red. Las NIC de Ethernet se usan para una conexión por cable, como se muestra en la figura, mientras que las NIC de la red de área local inalámbrica (WLAN) se usan para la conexión inalámbrica. Los dispositivos para usuarios finales pueden incluir un tipo de NIC o ambos. Una impresora de red, por ejemplo, puede contar solo con una NIC Ethernet y, por lo tanto, se debe conectar a la red mediante un cable Ethernet. Otros dispositivos, como las tabletas y los teléfono inteligentes, pueden contener solo una NIC WLAN y deben utilizar una conexión inalámbrica.

![Conexión por cable con una NIC Ethernet](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084136.jpg)

En términos de rendimiento, no todas las conexiones físicas son iguales a la hora de conectarse a una red.

### 2.2. La capa física

La capa física de OSI proporciona los medios de transporte de los bits que conforman una trama de la capa de enlace de datos a través de los medios de red. Esta capa acepta una trama completa desde la capa de enlace de datos y la codifica como una secuencia de señales que se transmiten en los medios locales. Un dispositivo final o un dispositivo intermediario recibe los bits codificados que componen una trama.

Haga clic en Reproducir en la figura para ver un ejemplo del proceso de encapsulación. La última parte de este proceso muestra los bits que se envían a través del medio físico. La capa física codifica las tramas y crea las señales eléctricas, ópticas o de ondas de radio que representan los bits en cada trama. Estas señales se envían por los medios, una a la vez.

La capa física del nodo de destino recupera estas señales individuales de los medios, las restaura a sus representaciones en bits y pasa los bits a la capa de enlace de datos en forma de trama completa.

![Proceso de encapsulación](https://examenredes.com/wp-content/uploads/2021/12/4.1.2a.gif)

## 3. Características de la capa física

### 3.1. Estándares de la capa física

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

### 3.2. Componentes físicos

Los estándares de la capa física abarcan tres áreas funcionales:

- Componentes físicos
- Codificación
- Señalización

#### Componentes físicos

Los componentes físicos son los dispositivos de hardware electrónico, medios y otros conectores que transmiten las señales que representan los bits. Todos los componentes de hardware, como NIC, interfaces y conectores, materiales y diseño de los cables, se especifican en los estándares asociados con la capa física. Los diversos puertos e interfaces de un router Cisco 1941 también son ejemplos de componentes físicos con conectores y diagramas de pines específicos derivados de los estándares.

#### 3.3. Codificación

La codificación, o codificación de línea, es un método que se utiliza para convertir una transmisión de bits de datos en un “código” predefinido. Los códigos son grupos de bits utilizados para ofrecer un patrón predecible que pueda reconocer tanto el emisor como el receptor. En otras palabras, la codificación es el método o patrón utilizado para representar la información digital. Similar a la forma en que el código Morse codifica un mensaje con una serie de puntos y guiones.

Por ejemplo, en la codificación Manchester los 0 se representan mediante una transición de voltaje de alto a bajo y los 1 se representan como una transición de voltaje de bajo a alto. Un ejemplo de codificación Manchester se ilustra en la figura. La transición se produce en el medio de cada período de bit. Este tipo de codificación se usa en Ethernet de 10 Mbps. Las velocidades de datos más rápidas requieren codificación más compleja. La codificación Manchester se utiliza en estándares Ethernet más antiguos, como 10BASE-T. Ethernet 100BASE-TX usa codificación 4B / 5B y 1000BASE-T usa codificación 8B / 10B.

![Componentes físicos](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084527.jpg)

La transición se produce en el medio de cada período de bit.

#### 3.4. Señalización

La capa física debe generar las señales inalámbricas, ópticas o eléctricas que representan los “1” y los “0” en los medios. La forma en que se representan los bits se denomina método de señalización. Los estándares de la capa física deben definir qué tipo de señal representa un “1” y qué tipo de señal representa un “0”. Esto puede ser tan simple como un cambio en el nivel de una señal eléctrica o de un pulso óptico. Por ejemplo, un pulso largo podría representar un 1 mientras que un pulso corto podría representar un 0.

Esto es similar al método de señalización que se utiliza en el código Morse, que puede utilizar una serie de tonos de encendido/apagado, luces o clics para enviar texto a través de cables telefónicos o entre barcos en el mar.

Las figuras muestran señalización

Cable de Cobre: Señales eléctricas sobre cable

![Señalización](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084643.jpg)

Cable de fibra óptica: Pulsos de luz sobre cable de fibra óptica

![Medios inalámbricos](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084707.jpg)

Medios inalámbricos: Señales de microondas sobre medios inalámbricos

![Medios inalámbricos](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_084738.jpg)

#### 3.5. Ancho de banda

Los diferentes medios físicos admiten la transferencia de bits a distintas velocidades. La transferencia de datos generalmente se discute en términos de ancho de banda. El ancho de banda es la capacidad a la que un medio puede transportar datos. El ancho de banda digital mide la cantidad de datos que pueden fluir desde un lugar hacia otro en un período de tiempo determinado. El ancho de banda generalmente se mide en kilobits por segundo (kbps), megabits por segundo (Mbps) o gigabits por segundo (Gbps). En ocasiones, el ancho de banda se piensa como la velocidad a la que viajan los bits, sin embargo, esto no es adecuado. Por ejemplo, tanto en Ethernet a 10 Mbps como a 100 Mbps, los bits se envían a la velocidad de la electricidad. La diferencia es el número de bits que se transmiten por segundo.

Una combinación de factores determina el ancho de banda práctico de una red:

- Las propiedades de los medios físicos
- Las tecnologías seleccionadas para la señalización y la detección de señales de red
- Las propiedades de los medios físicos, las tecnologías actuales y las leyes de la física desempeñan una función al momento de determinar el ancho de banda disponible.

En la tabla, se muestran las unidades de medida comúnmente utilizadas para el ancho de banda.

| Unidad de ancho de banda | Abreviatura | Equivalencia                          |
|--------------------------|-------------|---------------------------------------|
| Bits por segundo         | bps         | 1 bps = unidad fundamental de ancho de banda |
| Kilobits por segundo     | Kbps        | 1 Kbps = 1,000 bps = 10³ bps          |
| Megabits por segundo     | Mbps        | 1 Mbps = 1,000,000 bps = 10⁶ bps      |
| Gigabits por segundo     | Gbps        | 1 Gbps = 1,000,000,000 bps = 10⁹ bps  |
| Terabits por segundo     | Tbps        | 1 Tbps = 1,000,000,000,000 bps = 10¹² bps |

#### 3.6. Terminología del ancho de banda

Los términos utilizados para medir la calidad del ancho de banda incluyen:

- Latencia
- Rendimiento
- Capacidad de transferencia útil

##### Latencia

El concepto de latencia se refiere a la cantidad de tiempo, incluidas las demoras, que les toma a los datos transferirse desde un punto determinado hasta otro.

En una internetwork o una red con múltiples segmentos, el rendimiento no puede ser más rápido que el enlace más lento de la ruta de origen a destino. Incluso si todos los segmentos o gran parte de ellos tienen un ancho de banda elevado, solo se necesita un segmento en la ruta con un rendimiento inferior para crear un cuello de botella en el rendimiento de toda la red.

##### Rendimiento

El rendimiento es la medida de transferencia de bits a través de los medios durante un período de tiempo determinado.

Debido a diferentes factores, el rendimiento generalmente no coincide con el ancho de banda especificado en las implementaciones de la capa física. El rendimiento suele ser menor que el ancho de banda. Hay muchos factores que influyen en el rendimiento:

- La cantidad de tráfico
- El tipo de tráfico
- La latencia creada por la cantidad de dispositivos de red encontrados entre origen y destino

Existen muchas pruebas de velocidad en línea que pueden revelar el rendimiento de una conexión a Internet. En la figura, se proporcionan resultados de ejemplo de una prueba de velocidad.

##### Capacidad de transferencia útil (Goodput)

Existe una tercera medición para evaluar la transferencia de datos utilizables, que se conoce como capacidad de transferencia útil. La capacidad de transferencia útil es la medida de datos utilizables transferidos durante un período determinado. La capacidad de transferencia útil es el rendimiento menos la sobrecarga de tráfico para establecer sesiones, acuses de recibo, encapsulación y bits retransmitidos. La capacidad de transferencia útil siempre es menor que el rendimiento, que generalmente es menor que el ancho de banda.

![Prueba de velocidad](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_085951.jpg)

## 4. Cableado de cobre

### 4.1. Características del cableado de cobre

El cableado de cobre es el tipo más común de cableado utilizado en las redes hoy en día. De hecho, el cableado de cobre no es solo un tipo de cable. Hay tres tipos diferentes de cableado de cobre que se utilizan cada uno en situaciones específicas.

Las redes utilizan medios de cobre porque son económicos y fáciles de instalar, y tienen baja resistencia a la corriente eléctrica. Sin embargo, estos medios están limitados por la distancia y la interferencia de señal.

Los datos se transmiten en cables de cobre como impulsos eléctricos. Un detector en la interfaz de red de un dispositivo de destino debe recibir una señal que pueda decodificarse exitosamente para que coincida con la señal enviada. No obstante, cuanto más lejos viaja una señal, más se deteriora. Esto se denomina atenuación de señal. Por este motivo, todos los medios de cobre deben seguir limitaciones de distancia estrictas según lo especifican los estándares que los rigen.

Los valores de temporización y voltaje de los pulsos eléctricos también son vulnerables a las interferencias de dos fuentes:

- Interferencia electromagnética (EMI) o interferencia de radiofrecuencia (RFI): las señales de EMI y RFI pueden distorsionar y dañar las señales de datos que transportan los medios de cobre. Las posibles fuentes de EMI y RFI incluyen las ondas de radio y dispositivos electromagnéticos, como las luces fluorescentes o los motores eléctricos.
- Crosstalk - Crosstalk se trata de una perturbación causada por los campos eléctricos o magnéticos de una señal de un hilo a la señal de un hilo adyacente. En los circuitos telefónicos, el crosstalk puede provocar que se escuche parte de otra conversación de voz de un circuito adyacente. En especial, cuando una corriente eléctrica fluye por un hilo, crea un pequeño campo magnético circular alrededor de dicho hilo, que puede captar un hilo adyacente.

En la figura, se muestra la forma en que la interferencia puede afectar la transmisión de datos.

![Interferencia electromagnética (EMI) o interferencia de radiofrecuencia (RFI)](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090136.jpg)

1. Se transmite una señal digital pura
2. En el medio, hay una señal de interferencia
3. La señal digital está dañada por la señal de interferencia.
4. El equipo receptor lee una señal cambiada. Observe que un bit 0 ahora se interpreta como un bit 1.

Para contrarrestar los efectos negativos de la EMI y la RFI, algunos tipos de cables de cobre se empaquetan con un blindaje metálico y requieren una conexión a tierra adecuada.

Para contrarrestar los efectos negativos del crosstalk, algunos tipos de cables de cobre tienen pares de hilos de circuitos opuestos trenzados que cancelan dicho tipo de interferencia en forma eficaz.

La susceptibilidad de los cables de cobre al ruido electrónico también se puede limitar utilizando estas recomendaciones:

- La elección del tipo o la categoría de cable más adecuados a un entorno de red determinado.
- El diseño de una infraestructura de cables para evitar las fuentes de interferencia posibles y conocidas en la estructura del edificio.
- El uso de técnicas de cableado que incluyen el manejo y la terminación apropiados de los cables.

### 4.2. Tipos de cableado de cobre

Existen tres tipos principales de medios de cobre que se utilizan en las redes.

![Tipos de cableado de cobre](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090249.jpg)

#### 4.3.3. Par trenzado no blindado (UTP)

El cableado de par trenzado no blindado (UTP) es el medio de red más común. El cableado UTP, que se termina con conectores RJ-45, se utiliza para interconectar hosts de red con dispositivos intermediarios de red, como switches y routers.

En las redes LAN, el cable UTP consta de cuatro pares de hilos codificados por colores que están trenzados entre sí y recubiertos con un revestimiento de plástico flexible que los protege contra daños físicos menores. El trenzado de los hilos ayuda a proteger contra las interferencias de señales de otros hilos.

Como se muestra en la figura, los códigos por colores identifican los pares individuales con sus alambres y sirven de ayuda para la terminación de cables.

![Par trenzado no blindado (UTP)](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090324.jpg)

Los números en la figura identifican algunas características clave del cable de par trenzado sin blindaje:

1. La cubierta exterior protege los cables de cobre del daño físico.
2. Los pares trenzados protegen la señal de interferencia.
3. El aislamiento de plástico codificado por colores aísla eléctricamente los cables entre sí e identifica cada par.

#### 4.3.4. Par trenzado blindado (STP)

El par trenzado blindado (STP) proporciona una mejor protección contra ruido que el cableado UTP. Sin embargo, en comparación con el cable UTP, el cable STP es mucho más costoso y difícil de instalar. Al igual que el cable UTP, el STP utiliza un conector RJ-45.

El cable STP combina las técnicas de blindaje para contrarrestar la EMI y la RFI, y el trenzado de hilos para contrarrestar el crosstalk. Para obtener los máximos beneficios del blindaje, los cables STP se terminan con conectores de datos STP blindados especiales. Si el cable no se conecta a tierra correctamente, el blindaje puede actuar como antena y captar señales no deseadas.

El cable STP que se muestra utiliza cuatro pares de hilos. Cada uno de estos pares está empaquetado primero con un blindaje de hoja metálica y, luego, el conjunto se empaqueta con una malla tejida o una hoja metálica.

![Par trenzado blindado (STP)](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090405.jpg)

Los números en la figura identifican algunas características clave del cable de par trenzado blindado:

1. Cubierta exterior
2. Escudo trenzado o de aluminio
3. Escudos de aluminio
4. Pares trenzados

#### 4.3.5. Cable coaxial

El cable coaxial obtiene su nombre del hecho de que hay dos conductores que comparten el mismo eje. Como se muestra en la figura, el cable coaxial consta de lo siguiente:

- Se utiliza un conductor de cobre para transmitir las señales electrónicas.
- Una capa de aislamiento plástico flexible que rodea al conductor de cobre.
- Sobre este material aislante, hay una malla de cobre tejida o una hoja metálica que actúa como segundo hilo en el circuito y como blindaje para el conductor interno. La segunda capa o blindaje reduce la cantidad de interferencia electromagnética externa.
- La totalidad del cable está cubierta por un revestimiento para evitar daños físicos menores.

Existen diferentes tipos de conectores con cable coaxial. Los conectores Bayoneta Neill—Concelman (BNC), tipo N y tipo F se muestran en la figura.

Aunque el cable UTP ha reemplazado esencialmente el cable coaxial en las instalaciones de Ethernet modernas, el diseño del cable coaxial se usa en las siguientes situaciones:

- **Instalaciones inalámbricas**: Los cables coaxiales conectan antenas a los dispositivos inalámbricos. También transportan energía de radiofrecuencia (RF) entre las antenas y el equipo de radio.
- **Instalaciones de Internet por cable**: Los proveedores de servicios de cable proporcionan conectividad a Internet a sus clientes mediante el reemplazo de porciones del cable coaxial y la admisión de elementos de amplificación con cables de fibra óptica. Sin embargo, el cableado en las instalaciones del cliente sigue siendo cable coaxial.

![Conectores con cable coaxial](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090452.jpg)

Los números en la figura identifican algunas características clave del cable coaxial:

1. Cubierta exterior
2. Blindaje de cobre trenzado
3. Aislamiento plástico
4. Conductor de cobre

#### 4.4. Cableado UTP

#### 4.4.1. Propiedades del cableado UTP

En el tema anterior, aprendió un poco sobre el cableado de cobre de par trenzado sin blindaje (UTP). Dado que el cableado UTP es el estándar para su uso en las LAN, en este tema se detallan sus ventajas y limitaciones, y qué se puede hacer para evitar problemas.

Cuando se utiliza como medio de red, el cableado (UTP) consta de cuatro pares de hilos codificados por colores que están trenzados entre sí y recubiertos con un revestimiento de plástico flexible. Su tamaño pequeño puede ser una ventaja durante la instalación.

Los cables UTP no utilizan blindaje para contrarrestar los efectos de la EMI y la RFI. En cambio, los diseñadores de cable han descubierto otras formas de limitar el efecto negativo del crosstalk:

- **Anulación**: Los diseñadores ahora emparejan los hilos en un circuito. Cuando dos hilos en un circuito eléctrico están cerca, los campos magnéticos son exactamente opuestos entre sí. Por lo tanto, los dos campos magnéticos se anulan y también anulan cualquier señal de EMI y RFI externa.
- **Variando el número de vueltas por par de hilos**: Para mejorar aún más el efecto de anulación de los pares de hilos del circuito, los diseñadores cambian el número de vueltas de cada par de hilos en un cable. Los cables UTP deben seguir especificaciones precisas que rigen cuántas vueltas o trenzas se permiten por metro (3,28 ft) de cable. Observe en la figura que el par naranja y naranja/blanco está menos trenzado que el par azul y azul/blanco. Cada par coloreado se trenza una cantidad de veces distinta.
Los cables UTP dependen exclusivamente del efecto de anulación producido por los pares de hilos trenzados para limitar la degradación de la señal y proporcionar un autoblindaje eficaz de los pares de hilos en los medios de red.

![Cableado UTP](https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_090602.jpg)

#### 4.4.2. Conectores y estándares de cableado UTP

El cableado UTP cumple con los estándares establecidos en conjunto por la TIA/EIA. En particular, la TIA/EIA-568 estipula los estándares comerciales de cableado para las instalaciones LAN y es el estándar de mayor uso en entornos de cableado LAN. Algunos de los elementos definidos son los siguientes:

Tipos de cables Longitudes del cable Conectores Terminación del cable Métodos para realizar pruebas de cable

El Instituto de Ingenieros Eléctricos y Electrónicos (IEEE) define las características eléctricas del cableado de cobre. IEEE califica el cableado UTP según su rendimiento. Los cables se dividen en categorías según su capacidad para transportar datos de ancho de banda a velocidades mayores. Por ejemplo, el cable de Categoría 5 se utiliza comúnmente en las instalaciones de FastEthernet 100BASE-TX. Otras categorías incluyen el cable de categoría 5 mejorada, la categoría 6 y la categoría 6a.

Los cables de categorías superiores se diseñan y fabrican para admitir velocidades superiores de transmisión de datos. A medida que se desarrollan y adoptan nuevas tecnologías Ethernet de velocidad gigabit, la categoría 5e es ahora el tipo de cable mínimamente aceptable, y la categoría 6 es el tipo recomendado para nuevas instalaciones de edificios.

La figura muestra tres categorías de cable UTP:

La categoría 3 se utilizó originalmente para la comunicación de voz a través de líneas de voz, pero más tarde para la transmisión de datos.
Las categorías 5 y 5e se utilizan para la transmisión de datos. La categoría 5 soporta 100Mbps y la categoría 5e soporta 1000 Mbps
La categoría 6 tiene un separador añadido entre cada par de cables para soportar velocidades más altas. Categoría 6 soporta hasta 10 Gbps.
Categoría 7 también soporta 10 Gbps.
Categoría 8 soporta 40 Gbps.
Algunos fabricantes producen cables que exceden las especificaciones de la categoría 6a de la TIA/EIA y se refieren a estos como cables de Categoría 7.

https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_092608-768x523.jpg

Los cables UTP generalmente se terminan con un conector RJ-45. El estándar TIA/EIA-568 describe las asignaciones de los códigos por colores de los hilos a la asignación de pines (diagrama de pines) de los cables Ethernet.

Como se muestra en la figura, el conector RJ-45 es el componente macho, engarzado al final del cable.

Conectores RJ-45 para UTP

https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_092741-768x239.jpg

El socket, que se muestra en la figura, es el componente hembra de un dispositivo de red, pared, salida de partición de cubículo o panel de conexiones. Cuando se realizan las terminaciones de manera incorrecta, cada cable representa una posible fuente de degradación del rendimiento de la capa física.

Socket RJ-45 para UTP

https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_092805-768x310.jpg

Esta figura muestra un ejemplo de un cable UTP mal terminado. Este conector defectuoso tiene cables que están expuestos, sin torcer y no cubiertos completamente por la funda..

Cable UTP mal terminado

https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_092835-768x265.jpg

La siguiente figura muestra un cable UTP correctamente terminado. Es un buen conector, los hilos están sin trenzar solo en el trecho necesario para unir el conector.

Cable UTP correctamente terminado

https://examenredes.com/wp-content/uploads/2021/12/2021-12-25_092901-768x269.jpg

Nota: La terminación incorrecta de los cables puede afectar el rendimiento de la transmisión.

4.4.3. Cables UTP directos y cruzados


## 7. Conclusiones

### Propósito de la capa física

Antes de que pueda ocurrir cualquier comunicación de red, se debe establecer una conexión física a una red local. Una conexión física puede ser una conexión por cable o una conexión inalámbrica mediante ondas de radio. Las tarjetas de interfaz de red (NIC) conectan un dispositivo a la red. Las NIC Ethernet se utilizan para una conexión por cable, mientras que las NIC WLAN (red de área local inalámbrica) se utilizan para la conexión inalámbrica. La capa física de OSI proporciona los medios de transporte de los bits que conforman una trama de la capa de enlace de datos a través de los medios de red. Esta capa acepta una trama completa desde la capa de enlace de datos y la codifica como una secuencia de señales que se transmiten en los medios locales. Un dispositivo final o un dispositivo intermediario recibe los bits codificados que componen una trama.

### Característica de la capa física

La capa física consta de circuitos electrónicos, medios y conectores desarrollados por ingenieros. Los estándares de la capa física abordan tres áreas funcionales: componentes físicos, codificación y señalización. El ancho de banda es la capacidad a la que un medio puede transportar datos. El ancho de banda digital mide la cantidad de datos que pueden fluir desde un lugar hacia otro en un período de tiempo determinado. El rendimiento es la medida de la transferencia de bits a través de los medios durante un período de tiempo determinado y generalmente es menor que el ancho de banda. El concepto de latencia se refiere a la cantidad de tiempo, incluidas las demoras, que les toma a los datos transferirse desde un punto determinado hasta otro. La capacidad de transferencia útil es la medida de datos utilizables transferidos durante un período determinado. La capa física produce la representación y las agrupaciones de bits para cada tipo de medio de la siguiente manera:

Cable de cobre – Las señales son patrones de pulsos eléctricos.
Cable de fibra óptica – Las señales son patrones de luz.
Conexión inalámbrica – Las señales son patrones de transmisiones de microondas.

### Cableado de cobre

Las redes utilizan medios de cobre porque son económicos y fáciles de instalar, y tienen baja resistencia a la corriente eléctrica. Sin embargo, estos medios están limitados por la distancia y la interferencia de señal. Los valores de tiempo y voltaje de los pulsos eléctricos también son susceptibles a la interferencia de dos fuentes: EMI y el crosstalk. Tres tipos de cableado de cobre son: UTP, STP y cable coaxial (coaxial). UTP tiene una cubierta exterior para proteger los cables de cobre de daños físicos, pares trenzados para proteger la señal de interferencias y aislamiento plástico codificado por colores que aísla eléctricamente los cables unos de otros e identifica cada par. El cable STP utiliza cuatro pares de cables, cada uno envuelto en un blindaje de aluminio, que luego se envuelve en una trenza o lámina metálica general. El cable coaxial obtiene su nombre del hecho de que hay dos conductores que comparten el mismo eje. Coaxial se utiliza para conectar antenas a dispositivos inalámbricos. Los proveedores de Internet por cable utilizan coaxial dentro de las instalaciones de sus clientes.

### UTP Cabling

Consta de cuatro pares de hilos codificados por colores que están trenzados entre sí y recubiertos con un revestimiento de plástico flexible. Los cables UTP no utilizan blindaje para contrarrestar los efectos de la EMI y la RFI. En cambio, los diseñadores de cables han descubierto otras formas de limitar el efecto negativo del crosstalk: la cancelación y la variación del número de giros por par de cables. El cableado UTP cumple con los estándares establecidos en conjunto por la TIA/EIA. El Instituto de Ingenieros Eléctricos y Electrónicos (IEEE) define las características eléctricas del cableado de cobre. Los cables UTP generalmente se terminan con un conector RJ-45. Los principales tipos de cables que se obtienen mediante el uso de convenciones de cableado específicas son Ethernet Directo y Ethernet Cruzado. Cisco tiene un cable UTP propietario llamado rollover que conecta una estación de trabajo a un puerto de consola del router.

### Fiber-Optic Cabling

El cable de fibra óptica transmite datos a distancias más largas y con anchos de banda más altos que cualquier otro medio de red. El cable de fibra óptica puede transmitir señales con menos atenuación que el cable de cobre y es completamente inmune a EMI y RFI. La fibra óptica es un hilo flexible, pero extremadamente delgado y transparente de vidrio muy puro, no mucho más grueso que un cabello humano. Los bits se codifican en la fibra como impulsos de luz. El cableado de fibra óptica se está utilizando ahora en cuatro tipos de industria: redes empresariales, FTTH, redes de largo recorrido y redes de cable submarino. Hay cuatro tipos de conectores de fibra óptica: ST, SC, LC y LC multimodo dúplex. Los cables de conexión de fibra óptica incluyen SC-SC multimodo, LC-LC monomodo, ST-LC multimodo y SC-ST monomodo. En la mayoría de los entornos empresariales, la fibra óptica se utiliza principalmente como cableado de red troncal para conexiones punto a punto de alto tráfico entre instalaciones de distribución de datos y para la interconexión de edificios en campus de varios edificios.

### Cableado Fibra óptica

Los medios inalámbricos transportan señales electromagnéticas que representan los dígitos binarios de las comunicaciones de datos mediante frecuencias de radio y de microondas. La tecnología inalámbrica tiene algunas limitaciones, entre ellas: área de cobertura, interferencia, seguridad y los problemas que se producen con cualquier medio compartido. Los estándares inalámbricos incluyen los siguientes: Wi-Fi (IEEE 802.11), Bluetooth (IEEE 802.15), WiMAX (IEEE 802.16) y Zigbee (IEEE 802.15.4). LAN inalámbrica (WLAN) requiere un AP inalámbrico y adaptadores NIC inalámbricos.

## 8. Referencias

- <https://https://examenredes.com/ccna-1-version-7-modulo-4-capa-fisica/>
