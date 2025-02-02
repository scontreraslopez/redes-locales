# UP4. Dispositivos de la capa de red

## El router

### Introducción

El router es un dispositivo de red que opera en la capa de red del modelo OSI. Su función principal es la de encaminar paquetes de datos entre redes. Para ello, el router utiliza tablas de enrutamiento que le indican cómo encaminar los paquetes hacia su destino.

En empresas grandes con varias redes locales, el router es un dispositivo esencial para la comunicación entre las diferentes redes. En este caso, el router se encarga de encaminar los paquetes entre las redes locales y la red externa (Internet).

Otra característica de los routers es que crean un dominio de difusión para cada interfaz de red. Esto significa que los paquetes de difusión enviados por una interfaz no se transmiten a las demás interfaces del router. De esta forma, se evita la saturación de la red.

### Tablas de enrutamiento

La tabla de enrutamiento es el mecanismo que utiliza el router para determinar la ruta que deben seguir los paquetes de datos. En la tabla de enrutamiento, el router almacena información sobre las redes a las que está conectado y las rutas que debe seguir para llegar a otras redes.

[Coger foto de linux]

La tabla de enrutamiento se compone de varias columnas, entre las que destacan las siguientes:

- **Red de destino**: dirección IP de la red a la que se quiere llegar.
- **Máscara de subred**: máscara de subred que se aplica a la dirección IP de destino.
- **Gateway**: dirección IP del router que se utiliza para llegar a la red de destino.
- **Interfaz de salida**: interfaz de red por la que se envían los paquetes de datos.

Esta tabla puede ser creada por el administrador de red (enrutamiento estático) o generada automáticamente por el router mediante un protocolo de enrutamiento dinámico. Para esto último será preciso configurar el router para que utilice un protocolo de enrutamiento dinámico, como OSPF, RIP o EIGRP que le permita descubrir automáticamente las rutas a las diferentes redes.

Los routers en general almacenan la tabla de enrutamiento en la memoria RAM, por lo que si se reinicia el router, la tabla de enrutamiento se pierde. Algunos routers avanzados inocorporan una memoria no volátil (NVRAM, flash) que permite almacenar la configuración del router de manera persistente.

El trabajo del administrador de red es configurar la tabla de enrutamiento del router para que los paquetes de datos se encaminen correctamente hacia su destino. Para ello, el administrador debe conocer la topología de la red y las rutas que deben seguir los paquetes de datos, evitando que los paquetes se pierdan, que se produzcan bucles de enrutamiento o que se sature la red.

También podemos encontrar las tablas de enrutamiento en los propios dispositivos finales, como ordenadores o servidores. En estos casos, la tabla de enrutamiento se utiliza para determinar la ruta que deben seguir los paquetes de datos hacia su destino. Dependiendo del equipo en cuestión albergará unos valores u otros.

#### Dominando el comando 'ip route' en Linux

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

### Enrutamiento Estático y Dinámico

#### Enrutamiento Estático

El enrutamiento estático es como trazar una ruta fija en un mapa que nunca cambia. Aquí, el administrador de red introduce manualmente las rutas en la tabla de enrutamiento de cada router. Es decir, se le indica explícitamente al router por dónde debe enviar los paquetes para llegar a su destino.

##### Características principales:

- **Simplicidad en redes pequeñas:** Es fácil de configurar cuando la red es pequeña y no cambia con frecuencia.
- **Reducción del tráfico de red:** Los routers no necesitan intercambiar información para descubrir nuevas rutas, lo que disminuye el tráfico en la red.
- **Rutas predefinidas:** Los paquetes siempre siguen el mismo camino hacia un destino determinado.
- **Menor consumo de recursos:** Consume menos recursos del router y ahorra ancho de banda, ya que no hay necesidad de procesamiento adicional para descubrir rutas.
- **Mayor seguridad:** Las rutas fijas facilitan la monitorización y administración, aumentando la seguridad de la red.
- **Mantenimiento laborioso:** Si la topología de la red cambia, es necesario actualizar manualmente las tablas de enrutamiento, lo cual puede ser tedioso en redes grandes.

**Metáfora:** Imagina que siempre vas de tu casa al colegio por el mismo camino, sin importar si hay tráfico o si alguna calle está cerrada. Es sencillo pero poco flexible.

##### Enrutamiento Dinámico

El enrutamiento dinámico es como usar un GPS en tiempo real que te guía por la mejor ruta según las condiciones actuales. Los routers utilizan protocolos de enrutamiento para descubrir automáticamente las mejores rutas hacia cada destino, adaptándose a los cambios en la red.

### Tipos de protocolos según el algoritmo de enrutamiento:

- ### **Vector-Distancia:**
  - **Funcionamiento:** Cada router calcula la ruta basada en el número de saltos (routers intermedios) hasta el destino.
  - **Métrica:** Se utiliza el conteo de saltos; menos saltos significa una ruta preferida.
  - **Ejemplo de protocolo:** **RIP (Routing Information Protocol).**

- ### **Estado de Enlace:**
  - **Funcionamiento:** Los routers conocen el estado y costo de sus enlaces con routers vecinos y comparten esta información para construir un mapa completo de la red.
  - **Métrica:** Incluye factores como velocidad, capacidad y confiabilidad del enlace.
  - **Ejemplo de protocolo:** **OSPF (Open Shortest Path First).**

### Características del enrutamiento dinámico:

- **Actualización automática:** Las tablas de enrutamiento se ajustan en tiempo real sin intervención manual.
- **Flexibilidad en las rutas:** Los datagramas pueden seguir rutas distintas hacia el mismo destino según las condiciones de la red.
- **Ideal para redes grandes y complejas:** Evita la laboriosa tarea de actualizar manualmente las rutas en redes extensas.
- **Configuración más compleja:** Requiere un conocimiento profundo de los protocolos para evitar sobrecargas.
- **Mayor consumo de recursos:** Puede consumir más recursos del router y ancho de banda debido al intercambio constante de información.

**Metáfora:** Es como conductores que comparten información sobre el tráfico para encontrar la ruta más rápida en cada momento.

## **Protocolos de Enrutamiento Dinámico**

### **RIP (Routing Information Protocol)**

- **Simplicidad:** Presente en muchos routers y fácil de configurar.
- **Métrica basada en saltos:** Considera únicamente el número de saltos para determinar la mejor ruta.
- **Limitaciones:** No es ideal para redes grandes debido a su límite de 15 saltos y convergencia lenta.

### **OSPF (Open Shortest Path First)**

- **Complejidad y eficiencia:** Más complejo pero ofrece una visión detallada de la red.
- **Métrica basada en costo:** Tiene en cuenta factores como velocidad y calidad del enlace.
- **Adaptabilidad:** Construye un mapa completo de la red para calcular rutas óptimas.

## Para profundizar más:

- **Explora otros protocolos dinámicos:** Como EIGRP (Enhanced Interior Gateway Routing Protocol) o IS-IS (Intermediate System to Intermediate System).
- **Practica la configuración:** Utiliza simuladores de redes como Cisco Packet Tracer o GNS3 para experimentar con configuraciones estáticas y dinámicas.
- **Analiza casos reales:** Investiga cómo empresas grandes gestionan sus redes y qué protocolos utilizan.

**¿Sabías que...?**

- **BGP (Border Gateway Protocol):** Es el protocolo que mantiene unidas a todas las redes en Internet. Sin BGP, no podríamos navegar entre diferentes proveedores de servicios.
- **Enrutamiento híbrido:** Algunas redes utilizan una combinación de enrutamiento estático y dinámico para optimizar el rendimiento y la seguridad.