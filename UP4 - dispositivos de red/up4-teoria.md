# UP4. Dispositivos de la capa de red

## Índice

- [1. El router](#1-el-router)
  - [1.1. Introducción](#11-introducción)
  - [1.2. Tablas de enrutamiento](#12-tablas-de-enrutamiento)
  - [1.3. Dominando el comando 'ip route' en Linux](#13-dominando-el-comando-ip-route-en-linux)
  - [1.4. Enrutamiento Estático y Dinámico](#14-enrutamiento-estático-y-dinámico)
    - [1.4.1. Enrutamiento Estático](#141-enrutamiento-estático)
    - [1.4.2. Enrutamiento Dinámico](#142-enrutamiento-dinámico)
- [2. Hosts y sus Tablas de Enrutamiento](#2-hosts-y-sus-tablas-de-enrutamiento)
  - [2.1. Tablas de Enrutamiento](#21-tablas-de-enrutamiento)
    - [2.1.1. Profundización: Servidor Proxy](#211-profundización-servidor-proxy)
- [3. La conexión a Internet](#3-la-conexión-a-internet)
  - [3.1. Proveedores de Servicios de Internet (ISP)](#31-proveedores-de-servicios-de-internet-isp)
  - [3.2. Tecnologías de Acceso a Internet y Dispositivos Asociados](#32-tecnologías-de-acceso-a-internet-y-dispositivos-asociados)
    - [3.2.1. Tecnologías Actuales](#321-tecnologías-actuales)
    - [3.2.2. Breve Mención Histórica a Tecnologías Obsoletas](#322-breve-mención-histórica-a-tecnologías-obsoletas)

## 1. El router

### 1.1. Introducción

El router es un dispositivo de red que opera en la capa de red del modelo OSI. Su función principal es la de encaminar paquetes de datos entre redes. Para ello, el router utiliza tablas de enrutamiento que le indican cómo encaminar los paquetes hacia su destino.

En empresas grandes con varias redes locales, el router es un dispositivo esencial para la comunicación entre las diferentes redes. En este caso, el router se encarga de encaminar los paquetes entre las redes locales y la red externa (Internet).

Otra característica de los routers es que crean un dominio de difusión para cada interfaz de red. Esto significa que los paquetes de difusión enviados por una interfaz no se transmiten a las demás interfaces del router. De esta forma, se evita la saturación de la red.

### 1.2. Tablas de enrutamiento

La tabla de enrutamiento es el mecanismo que utiliza el router para determinar la ruta que deben seguir los paquetes de datos. En la tabla de enrutamiento, el router almacena información sobre las redes a las que está conectado y las rutas que debe seguir para llegar a otras redes.

![ROUTE PRINT - windows](/assets/images/show-routing-table-windows.webp)

La tabla de enrutamiento se compone de varias columnas, entre las que destacan las siguientes:

- **Red de destino**: dirección IP de la red a la que se quiere llegar.
- **Máscara de subred**: máscara de subred que se aplica a la dirección IP de destino.
- **Gateway**: dirección IP del router que se utiliza para llegar a la red de destino.
- **Interfaz de salida**: interfaz de red por la que se envían los paquetes de datos.
- **Métrica**: valor numérico que indica la distancia o coste de la ruta. Si existen varias rutas a la misma red, el router elegirá la ruta con la métrica más baja.

Esta tabla puede ser creada por el administrador de red (enrutamiento estático) o generada automáticamente por el router mediante un protocolo de enrutamiento dinámico. Para esto último será preciso configurar el router para que utilice un protocolo de enrutamiento dinámico, como OSPF, RIP o EIGRP que le permita descubrir automáticamente las rutas a las diferentes redes.

Los routers en general almacenan la tabla de enrutamiento en la memoria RAM, por lo que si se reinicia el router, la tabla de enrutamiento se pierde. Algunos routers avanzados incorporan una memoria no volátil (NVRAM, flash) que permite almacenar la configuración del router de manera persistente.

El trabajo del administrador de red es configurar la tabla de enrutamiento del router para que los paquetes de datos se encaminen correctamente hacia su destino. Para ello, el administrador debe conocer la topología de la red y las rutas que deben seguir los paquetes de datos, evitando que los paquetes se pierdan, que se produzcan bucles de enrutamiento o que se sature la red.

También podemos encontrar las tablas de enrutamiento en los propios dispositivos finales, como ordenadores o servidores. En estos casos, la tabla de enrutamiento se utiliza para determinar la ruta que deben seguir los paquetes de datos hacia su destino. Dependiendo del equipo en cuestión albergará unos valores u otros.

### 1.3. Dominando el comando 'ip route' en Linux

Fuente original: <https://commandmasters.com/commands/ip-route-linux/>

El comando `ip route` es una herramienta crucial para la gestión de tablas de enrutamiento IP en sistemas basados en Linux. Permite a los administradores y usuarios examinar y manipular las tablas de enrutamiento del kernel, que determinan cómo se reenvían los paquetes en la red. Este comando, parte del conjunto de herramientas `iproute2`, ofrece características de enrutamiento flexibles y sofisticadas en comparación con las utilidades tradicionales. Ya sea que necesites ver las rutas actuales, agregar nuevas rutas o solucionar problemas de red, ip route es un componente invaluable en tu kit de herramientas de red.

Casos de uso:

- Mostrar la tabla de enrutamiento:

```bash
ip route show
```

Muestra las entradas actuales de la tabla de enrutamiento.

- Agregar una ruta predeterminada usando un gateway:

```bash
ip route show
sudo ip route add default via 192.168.1.1
```

Añade una ruta predeterminada para que todos los paquetes no especificados se envíen a través del gateway indicado.

- Agregar una ruta predeterminada usando una interfaz específica:

```bash
sudo ip route add default dev eth0
```

Dirige el tráfico a través de una interfaz de red específica.

- Agregar una ruta estática:

```bash
sudo ip route add 10.0.0.0/24 via 192.168.1.1 dev eth0
```

Añade una ruta estática para un subred específica a través de un gateway.

- Eliminar una ruta estática:

```bash
sudo ip route del 10.0.0.0/24 dev eth0
```

Elimina una ruta estática de la tabla de enrutamiento.

- Cambiar o reemplazar una ruta estática:

```bash
sudo ip route change 10.0.0.0/24 via 192.168.1.1 dev eth0
```

Ajusta una ruta estática existente con nuevas propiedades.

- Mostrar la ruta que el kernel usará para llegar a una dirección IP específica:

```bash
ip route get 10.0.0.5
```

Proporciona la ruta que el kernel elegirá para llegar a una dirección IP específica.

### 1.4. Enrutamiento Estático y Dinámico

#### 1.4.1. Enrutamiento Estático

El enrutamiento estático es como trazar una ruta fija en un mapa que nunca cambia. Aquí, el administrador de red introduce manualmente las rutas en la tabla de enrutamiento de cada router. Es decir, se le indica explícitamente al router por dónde debe enviar los paquetes para llegar a su destino.

Características principales:

- **Simplicidad en redes pequeñas:** Es fácil de configurar cuando la red es pequeña y no cambia con frecuencia.
- **Reducción del tráfico de red:** Los routers no necesitan intercambiar información para descubrir nuevas rutas, lo que disminuye el tráfico en la red.
- **Rutas predefinidas:** Los paquetes siempre siguen el mismo camino hacia un destino determinado.
- **Menor consumo de recursos:** Consume menos recursos del router y ahorra ancho de banda, ya que no hay necesidad de procesamiento adicional para descubrir rutas.
- **Mayor seguridad:** Las rutas fijas facilitan la monitorización y administración, aumentando la seguridad de la red.
- **Mantenimiento laborioso:** Si la topología de la red cambia, es necesario actualizar manualmente las tablas de enrutamiento, lo cual puede ser tedioso en redes grandes.

**Metáfora:** Imagina que siempre vas de tu casa al colegio por el mismo camino, sin importar si hay tráfico o si alguna calle está cerrada. Es sencillo pero poco flexible.

#### 1.4.2. Enrutamiento Dinámico

El enrutamiento dinámico es como usar un GPS en tiempo real que te guía por la mejor ruta según las condiciones actuales. Los routers utilizan protocolos de enrutamiento para descubrir automáticamente las mejores rutas hacia cada destino, adaptándose a los cambios en la red.

Tipos de protocolos según el algoritmo de enrutamiento:

- **Vector-Distancia:**
  - **Funcionamiento:** Cada router calcula la ruta basada en el número de saltos (routers intermedios) hasta el destino.
  - **Métrica:** Se utiliza el conteo de saltos; menos saltos significa una ruta preferida.
  - **Ejemplo de protocolo:** **RIP (Routing Information Protocol).**

- **Estado de Enlace:**
  - **Funcionamiento:** Los routers conocen el estado y costo de sus enlaces con routers vecinos y comparten esta información para construir un mapa completo de la red.
  - **Métrica:** Incluye factores como velocidad, capacidad y confiabilidad del enlace.
  - **Ejemplo de protocolo:** **OSPF (Open Shortest Path First).**

Características del enrutamiento dinámico:

- **Actualización automática:** Las tablas de enrutamiento se ajustan en tiempo real sin intervención manual.
- **Flexibilidad en las rutas:** Los datagramas pueden seguir rutas distintas hacia el mismo destino según las condiciones de la red.
- **Ideal para redes grandes y complejas:** Evita la laboriosa tarea de actualizar manualmente las rutas en redes extensas.
- **Configuración más compleja:** Requiere un conocimiento profundo de los protocolos para evitar sobrecargas.
- **Mayor consumo de recursos:** Puede consumir más recursos del router y ancho de banda debido al intercambio constante de información.

**Metáfora:** Es como en el Waze cuando los conductores que comparten información sobre el tráfico para encontrar la ruta más rápida en cada momento.

Algunos Protocolos de Enrutamiento Dinámico son:

- **RIP (Routing Information Protocol)**:
  - **Simplicidad:** Presente en muchos routers y fácil de configurar.
  - **Métrica basada en saltos:** Considera únicamente el número de saltos para determinar la mejor ruta.
  - **Limitaciones:** No es ideal para redes grandes debido a su límite de 15 saltos y convergencia lenta.

- **OSPF (Open Shortest Path First)**:
  - **Complejidad y eficiencia:** Más complejo pero ofrece una visión detallada de la red.
  - **Métrica basada en costo:** Tiene en cuenta factores como velocidad y calidad del enlace.
  - **Adaptabilidad:** Construye un mapa completo de la red para calcular rutas óptimas.

 Para profundizar más:

- **Explora otros protocolos dinámicos:** Como EIGRP (Enhanced Interior Gateway Routing Protocol) o IS-IS (Intermediate System to Intermediate System).
- **Practica la configuración:** Utiliza simuladores de redes como Cisco Packet Tracer o GNS3 para experimentar con configuraciones estáticas y dinámicas.
- **Analiza casos reales:** Investiga cómo empresas grandes gestionan sus redes y qué protocolos utilizan.

**¿Sabías que...?**

- **BGP (Border Gateway Protocol):** Es el protocolo que mantiene unidas a todas las redes en Internet. Sin BGP, no podríamos navegar entre diferentes proveedores de servicios.
- **Enrutamiento híbrido:** Algunas redes utilizan una combinación de enrutamiento estático y dinámico para optimizar el rendimiento y la seguridad.

## 2. Hosts y sus Tablas de Enrutamiento

Los hosts también tienen una tabla de enrutamiento que les ayuda a determinar la mejor ruta para enviar paquetes.

### 2.1. Tablas de Enrutamiento:

Todos los dispositivos que usan TCP/IP tienen una tabla de enrutamiento con información básica para dirigir los paquetes. En los hosts, esta tabla suele ser más pequeña que en los routers, e incluye direcciones IP de la red local, la dirección de loopback y la puerta de enlace predeterminada.

Podemos añadir, modificar o borrar rutas estáticas en estas tablas, pero no dinámicas, ya que los hosts no comparten información de rutas entre sí. El sistema operativo consulta la tabla de enrutamiento antes de enviar cualquier paquete a la red local o a Internet.

Mención especial merece el concepto de **Puerta de Enlace Predeterminada**. La puerta de enlace predeterminada, o default gateway, es un nodo de red (como un router o servidor) que actúa como punto de acceso a redes externas. Los hosts envían los paquetes a la puerta de enlace cuando no encuentran una ruta en su tabla de enrutamiento, confiando en que esta encontrará la ruta correcta.

En grandes corporaciones, la puerta de enlace dirige el tráfico entre diferentes segmentos de red y suele conectar las redes internas con Internet. En estos casos, tiene una IP privada para la red interna y una IP pública para la red externa. Además, puede ofrecer servicios de proxy y cortafuegos para mejorar la seguridad.

Normalmente, la puerta de enlace tiene la dirección IP más baja disponible en la red, como 192.168.12.1 o 192.168.12.2 si la primera está ocupada. En hogares, el dispositivo que actúa como puerta de enlace suele ser el "router inalámbrico". A nivel doméstico este router es una combinación de router, switch, punto de acceso, cortafuegos y módem.

### 2.1.1. Profundización: Servidor Proxy

Un proxy actúa como un intermediario que intercepta tus solicitudes de comunicación y las gestiona de manera que parece que provienen de él mismo. Imagina al proxy como un agente secreto que recibe tus mensajes, los reescribe con su propia identidad y los envía al destino. Cuando el servidor de destino recibe la solicitud, cree que está interactuando directamente con el proxy, sin saber que tú eres el origen real de la comunicación.

Este proceso implica que el proxy recibe tus paquetes originales, los analiza y luego genera nuevos paquetes que envía al servidor. De esta forma, se establece una conexión entre el proxy y el servidor, independiente de la conexión entre tú y el proxy. Cuando el servidor responde, el proxy realiza el proceso inverso: recibe la respuesta, la interpreta y te envía nuevos paquetes como si fueran originados desde él. Lo que el proxy modifica es la información en la capa de aplicación, como las cabeceras HTTP en una navegación web.

- Recepción y Análisis: El proxy recibe los paquetes originales que envías desde tu dispositivo. En esta fase, el proxy analiza el contenido de estos paquetes para entender qué tipo de información contienen y hacia dónde se dirigen.
- Generación de Nuevos Paquetes: Luego, el proxy crea nuevos paquetes con la información relevante y los envía al servidor de destino. Esta nueva conexión es independiente de la original entre tu dispositivo y el proxy.
- Respuesta del Servidor: Cuando el servidor responde, devuelve los datos al proxy. El proxy entonces analiza esta respuesta y crea nuevos paquetes para enviártelos, haciendo parecer que estos paquetes se originaron desde el proxy.
- Modificación en la Capa de Aplicación: Aquí es donde entra en juego la modificación de la información en la capa de aplicación. El proxy puede cambiar las cabeceras HTTP, que son parte de los datos que se envían en la capa de aplicación. Estas cabeceras pueden incluir información como detalles del navegador, cookies, lenguaje preferido, etc. Al modificar estas cabeceras, el proxy puede ajustar la manera en que se presentan los datos o incluso proporcionar anonimato.
- Capa de Red: Efectivamente, el proxy también modifica la información en la capa de red al generar nuevos datagramas IP. Esto significa que el datagrama IP que llega al servidor parecerá haber sido enviado directamente desde el proxy, no desde tu dispositivo.

Para ilustrarlo mejor, piensa en una comunicación web típica:

Sin proxy:

- Tu PC envía una solicitud al servidor.
- El servidor ve tu dirección IP pública y responde directamente a ella.

Con proxy:

- Tu PC envía una solicitud al proxy.
- El proxy crea una nueva solicitud desde su propia dirección IP y la envía al servidor.
- El servidor responde al proxy, creyendo que es el origen.
- El proxy recibe la respuesta y te la reenvía.

Este esquema puede representarse así: [Tu PC] <---> [Proxy] <---> [Servidor]

Un ejemplo de un proxy en acción lo podemos encontrar en los filtros web (web filters).Un filtro web actúa como un proxy que intercepta y analiza las solicitudes web que haces desde tu dispositivo hacia Internet. Aquí están los pasos esenciales del proceso:

- Intercepción: Cuando intentas acceder a una página web, tu solicitud pasa primero por el filtro web.
- Evaluación: El filtro web revisa la solicitud y la compara con una base de datos de categorías y reglas predefinidas. Estas categorías pueden incluir temas como redes sociales, entretenimiento, noticias, contenido para adultos, etc.
- Acción: Basado en las reglas establecidas, el filtro web decide si permite o bloquea el acceso a la página solicitada. Si la página está en una categoría restringida, se bloquea y se te muestra un mensaje de bloqueo.

**Ejemplo Práctico**: Supongamos que estás en una red corporativa donde se ha configurado un filtro web que bloquea el acceso a sitios de redes sociales durante el horario laboral:

- Intentas acceder a Facebook.
- Tu solicitud pasa por el filtro web.
- El filtro detecta que Facebook pertenece a la categoría "Redes Sociales" y está bloqueado.
- Se te muestra un mensaje informándote que el acceso a Facebook está restringido.

**Proxy y Modificación de Datos**: En este caso, el filtro web actúa como un proxy, gestionando la conexión entre tu dispositivo y el servidor web de destino. También puede modificar las cabeceras HTTP u otros datos en la capa de aplicación para mejorar la seguridad, anonimato y cumplimiento de políticas internas de la organización.

En resumen, los filtros web son un tipo de proxy especializado en filtrar y controlar el acceso a Internet basándose en categorías y políticas predefinidas.

Beneficios de este enfoque:

- Anonimato y Privacidad: Tu dirección IP real permanece oculta para el servidor final, protegiendo tu identidad y ubicación.
- Control y Filtrado: Las organizaciones pueden implementar políticas de acceso, bloquear sitios no deseados y monitorear el uso de la red.
- Optimización: Los proxies pueden almacenar en caché contenido frecuente, reduciendo tiempos de carga y ancho de banda utilizado.

Un símil para entenderlo mejor: Imagina que quieres solicitar información a una empresa, pero en lugar de contactarlos directamente, le pides a un asistente que lo haga por ti. Tu asistente (el proxy) se comunica con la empresa, obtiene la información y luego te la entrega. La empresa solo interactúa con el asistente y no sabe que tú estás detrás de la petición.

El uso de proxies puede influir en la seguridad y eficiencia de las redes. Al actuar como intermediarios, no solo protegen la identidad de los usuarios, sino que también ofrecen capacidades adicionales como la inspección de tráfico y protección contra amenazas.

Además, existen diferentes tipos de proxies:

- Proxy Directo: Actúa en nombre del cliente, como hemos descrito.
- Proxy Inverso: Se coloca frente a uno o varios servidores, gestionando las solicitudes entrantes y distribuyéndolas según la carga o disponibilidad. Es común en servicios web para balancear carga y añadir capas de seguridad.

Con el creciente enfoque en la ciberseguridad y la privacidad en línea, los proxies juegan un papel crucial en la protección de datos y en el mantenimiento de redes robustas. Herramientas como las VPN (Redes Privadas Virtuales) también utilizan conceptos similares para crear túneles seguros entre dispositivos y redes.

## 3. La conexión a Internet

La conexión a Internet es el medio que permite a un ordenador o a una red de ordenadores acceder a la red global, facilitando la comunicación y el intercambio de información a nivel mundial.

### 3.1. Proveedores de Servicios de Internet (ISP)

Un Proveedor de Servicios de Internet (ISP) es una empresa que ofrece acceso a Internet a usuarios y organizaciones. El servicio se factura en función del ancho de banda contratado, es decir, de la velocidad y capacidad de transmisión de datos que el usuario necesita.

Los ISP se organizan en una jerarquía de tres niveles:

- **ISP de Nivel 1**: Constituyen la columna vertebral de Internet. Son empresas con infraestructura global que poseen enlaces troncales de alta velocidad, moviéndose en rangos desde 10 Gbps en adelante. Estos ISP tienen cobertura internacional y se conectan directamente entre sí y con numerosos ISP de nivel inferior, asegurando la interconectividad global.

- **ISP de Nivel 2**: Ofrecen cobertura regional o nacional. Se conectan a los ISP de Nivel 1 para acceder a la red global y proveen servicios a grandes empresas y a ISP de Nivel 3. Actúan como intermediarios, ampliando el alcance de los servicios de Internet.

- **ISP de Nivel 3**: Son los proveedores locales que ofrecen acceso directo a los usuarios finales, tanto hogares como pequeñas empresas. Se conectan a ISP de Nivel 2 para recibir el servicio y son los encargados de llevar Internet a la mayoría de los consumidores.

La interconexión entre estos niveles se realiza a través de **POP** (Puntos de Presencia), que son instalaciones donde los ISP alojan sus equipos de red, y **NAP** (Puntos de Acceso a la Red) o **IXP** (Internet Exchange Point), que facilitan la interconexión entre ISP de mismo nivel, permitiendo el flujo eficiente de datos a gran velocidad.

Internet es una red dinámica y en constante expansión. Gracias a la flexibilidad y escalabilidad de su arquitectura, continuamente se incorporan nuevos proveedores y tecnologías que enriquecen y mejoran la conectividad global.

### 3.2. Tecnologías de Acceso a Internet y Dispositivos Asociados

#### 3.2.1. Tecnologías Actuales

**Fibra Óptica**

La fibra óptica utiliza filamentos de vidrio o plástico para transmitir datos mediante pulsos de luz. Ofrece velocidades extremadamente altas, que pueden superar los 1 Gbps, baja latencia y gran estabilidad. Esta tecnología es ideal para soportar las crecientes demandas de ancho de banda en aplicaciones como streaming de alta definición, teletrabajo y servicios en la nube.

**Conexiones de Cable**

Utilizan la infraestructura de televisión por cable para proporcionar acceso a Internet de banda ancha. Ofrecen velocidades competitivas y son ampliamente utilizadas en zonas urbanas. La tecnología DOCSIS 3.1 permite velocidades que pueden alcanzar los 10 Gbps en condiciones óptimas.

**Redes Móviles 4G/5G**

Las redes móviles han evolucionado significativamente. La tecnología 4G LTE ofrece velocidades adecuadas para navegar, ver videos y usar aplicaciones en dispositivos móviles. Con la llegada del **5G**, se espera una revolución en la conectividad móvil, con velocidades que pueden superar los 20 Gbps, baja latencia y capacidad para conectar una gran cantidad de dispositivos simultáneamente, impulsando el Internet de las Cosas (IoT) y aplicaciones en tiempo real.

**Acceso Inalámbrico Fijo**

Esta tecnología proporciona acceso a Internet mediante señales inalámbricas desde una estación base fija a ubicaciones fijas (hogares, empresas). Es especialmente útil en áreas rurales o de difícil acceso donde las conexiones cableadas no son viables. Tecnologías como **WiMAX** y soluciones de radio enlace ofrecen alternativas eficientes para llevar conectividad a estas zonas.

#### 3.2.2. Breve Mención Histórica a Tecnologías Obsoletas

**Módem Analógico**

En sus inicios, los módems analógicos permitieron a los usuarios conectarse a Internet a través de líneas telefónicas convencionales, alcanzando velocidades máximas de 56 Kbps. Fueron fundamentales para la masificación de Internet en los hogares, aunque sus limitaciones de velocidad y estabilidad los hicieron obsoletos con la llegada de tecnologías superiores.

**RDSI (Red Digital de Servicios Integrados)**

La RDSI proporcionó conexiones digitales sobre líneas telefónicas, mejorando la calidad y velocidad con respecto a los módems analógicos, alcanzando hasta 192 Kbps en el acceso básico. Aunque representó un avance significativo en su momento, fue superada por tecnologías de banda ancha más eficientes.

**ADSL (Línea de Abonado Digital Asimétrica)**

El ADSL marcó un hito al permitir velocidades de varios Mbps utilizando las líneas telefónicas existentes, separando las frecuencias de voz y datos. Su naturaleza asimétrica, con mayor velocidad de descarga que de subida, se ajustaba a las necesidades de los usuarios domésticos. Sin embargo, las crecientes demandas de ancho de banda y la aparición de nuevas tecnologías llevaron a su progresivo desuso.

**ATM y Frame Relay**

Fueron tecnologías utilizadas principalmente en entornos empresariales para la transmisión de datos sobre redes de área amplia. ATM (Modo de Transferencia Asíncrona) y Frame Relay permitieron mejorar la eficiencia y velocidad en las comunicaciones. No obstante, la evolución de los protocolos de Internet y las nuevas necesidades de flexibilidad y escalabilidad hicieron que estas tecnologías quedaran obsoletas.

## 4. Redes Locales Virtuales (VLAN)

Imagina que en una empresa todos los departamentos están conectados a la misma red física. Sin embargo, no es conveniente que todos los empleados tengan acceso a toda la información que circula por esa red. Por ejemplo, no queremos que el departamento de Ventas vea los datos confidenciales de Contabilidad. Hasta ahora habíamos visto la técnica de subnetting, pero ¿qué impide a alguien cambiar su dirección IP y saltar de una subred a otra? Aquí es donde entran en juego las Redes Locales Virtuales, o VLAN por sus siglas en inglés.

Una VLAN es una forma de segmentar una red física en múltiples redes lógicas. Esto significa que, aunque todos los dispositivos estén conectados al mismo hardware físico, se comportan como si estuvieran en redes separadas. Así, la información que se genera dentro de una VLAN solo es accesible para los anfitriones (hosts) de esa misma VLAN, aumentando la seguridad y eficiencia de la red. A diferencia de con el subnetting, esta configuración se realiza a nivel de switch, asignando puertos a una VLAN específica.

Este es uno de los motivos que justifica la sensibilidad de los cuartos de comunicaciones y racks de servidores, ya que un acceso no autorizado a estos dispositivos podría comprometer la seguridad de toda la red. También la necesidad de proteger con contraseña los switches, para evitar que alguien pueda cambiar la configuración de las VLAN.

### 4.1 Características de las VLAN

Las VLAN ofrecen varias ventajas que mejoran el funcionamiento y gestión de las redes locales:

- Reducción de costos y facilidad administrativa: Al utilizar software para segmentar la red, eliminamos la necesidad de añadir routers físicos para crear dominios de difusión separados. Los switches VLAN permiten esta funcionalidad con un costo menor y una configuración más sencilla.
- Aumento de la eficiencia del ancho de banda: Al controlar los dominios de difusión, se reduce la cantidad de tráfico innecesario en la red. Los paquetes solo se envían a los dispositivos que pertenecen a la misma VLAN, optimizando el uso del ancho de banda y mejorando el rendimiento general.
- Mejora en la seguridad: Al separar la red en VLAN, podemos asegurarnos de que solo los usuarios autorizados tengan acceso a cierta información. Esto evita que datos sensibles estén al alcance de todos y facilita la implementación de políticas de seguridad específicas para cada segmento.
- Flexibilidad y escalabilidad: Los hosts pueden pertenecer a diferentes VLAN sin importar a qué puerto del switch estén conectados. Además, es posible que hosts en switches distintos formen parte de la misma VLAN. Esto simplifica la reorganización y expansión de la red sin cambios drásticos en la infraestructura física.

### 4.2 Configuración de Switches VLAN

Los switches que soportan VLAN nos permiten configurar estas redes virtuales de dos maneras.

#### 4.2.1. VLAN Estáticas

En las VLAN estáticas, asignamos manualmente cada puerto del switch a una VLAN específica. Esta asignación permanece igual a menos que se modifique la configuración. Es una forma sencilla y directa de gestionar las VLAN, pero requiere que el administrador esté atento a qué dispositivos se conectan y dónde, especialmente si hay cambios físicos en la red.

- Ventaja: Sencillez en la configuración y control directo sobre la asignación de puertos.
- Desventaja: Menos flexibilidad ante cambios o movimientos de dispositivos en la red.

#### 4.2.2. VLAN Dinámicas

En las VLAN dinámicas, la asignación de puertos a VLAN se realiza automáticamente según ciertos parámetros, como la dirección MAC del dispositivo o la autenticación del usuario. Esto permite que, sin importar en qué puerto se conecte un dispositivo, siempre forme parte de su VLAN asignada.

- Ventaja: Mayor flexibilidad y facilidad para usuarios móviles o dispositivos que cambian de ubicación.
- Desventaja: Configuración más compleja, ya que requiere mantener una base de datos con las direcciones MAC o credenciales de los dispositivos y usuarios.

#### 4.2.3. Comunicación entre VLANs

Aunque las VLAN están diseñadas para aislar el tráfico, a veces es necesario que se comuniquen entre sí. Para permitir esta comunicación, podemos utilizar:

- Routers: Conectamos las VLAN al router, que se encargará de dirigir el tráfico entre ellas. Cada VLAN se configura como una red independiente en el router, y se establecen reglas de enrutamiento para controlar el flujo de datos.
- Switches con Trunking: Los switches pueden utilizar una técnica llamada trunking, que implica configurar uno o más puertos como troncales. Estos puertos pueden transportar tráfico de múltiples VLAN simultáneamente. Al conectar los puertos troncales a un router o a otros switches, facilitamos la comunicación entre VLANs sin necesidad de configurar rutas específicas en el router.

#### 4.2.4. Otros beneficios de las VLAN

Las VLAN no solo mejoran la seguridad y eficiencia en redes empresariales, sino que también son fundamentales en tecnologías modernas como la virtualización y las redes definidas por software (SDN). Permiten una gestión más dinámica y adaptable de los recursos de red, lo cual es esencial en entornos donde la escalabilidad y flexibilidad son clave.
