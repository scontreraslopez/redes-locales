# Casos Prácticos UP4

## Índice

--TODO

## 1. Dominando el comando 'ip route' en Linux

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

## LAB: Configurando la tabla de enrutamiento de un router CISCO mediante el CLI

- Dificultad: Baja
- Tiempo estimado: 50 minutos

Vamos a realizar la siguiente configuración en Cisco Packet Tracer. Aquí configuraremos las interfaces de los routers y las rutas estáticas para los routers. La topología de red es la siguiente:

![Router Configuration Exercise](/assets/images/router-config-up4-1.png)

1. Configurar las interfaces de los routers:

- Ponemos los 4 routers 1841 en Cisco Packet Tracer y los conectamos entre sí con cables cruzados. Asegúrate de que las interfaces de los routers están conectadas de la siguiente manera:
  - R0: Fa0/0 a R1: Fa0/0
  - R1: Fa0/1 a R2: Fa0/0
  - R2: Fa0/1 a R3: Fa0/0
- Empezamos por R0, hacemos doble click y nos vamos a la pestaña CLI.
- Rechazamos el initial configuration dialog con `no`.
- Pulsamos la tecla intro para abrir el terminal.

```bash
Router> enable
Router# configure terminal
Router# hostname R0
Router(config)# interface FastEthernet0/0
Router(config-if)# ip address 10.0.0.1 255.255.255.252
Router(config-if)# no shutdown
```

Repetimos en R1 con la siguiente configuración. Nótese como esta vez abreviamos el nombre de la interfaz.

```bash
Router> enable
Router# configure terminal
Router# hostname R1
Router(config)# interface Fa0/0
Router(config-if)# ip address 10.0.0.2 255.255.255.252
Router(config-if)# no shutdown
Router(config-if)# interface Fa0/1
Router(config-if)# ip address 10.0.1.1 255.255.255.252
Router(config-if)# no shutdown
```

Se deja la configuración de R2 y R3 como ejercicio para el lector.

2. Configurar las rutas estáticas para los routers:

- Establecemos las rutas estáticas para permitir la comunicación entre los routers, comenzando con el router R0. Es fundamental que las tablas de enrutamiento de todos los routers sean coherentes. Esto implica que cada router debe contener la ruta adecuada para alcanzar la red adyacente en un solo salto. Una vez configuradas correctamente las tablas de enrutamiento de los routers, podremos acceder a cada uno de ellos desde los demás.

No es preciso añadir entradas en las tablas de enrutamiento para las redes directamente conectadas. Por ejemplo, no necesitamos añadir una entrada para la conexión entre R0 y R1, ya que esta conexión es directa y se añade automáticamente a la tabla de enrutamiento.

```bash
Router> enable
Router# configure terminal
Router(config)# ip route 10.0.1.0 255.255.255.252 10.0.0.2
Router(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Con la primera configuración ip route le estamos especificando a nuestro router R0 que para alcanzar la red 10.0.1.0/30 debe hacerlo mediante el router R1, cuya dirección IP es 10.0.0.2. Con la segunda configuración ip route le estamos diciendo a nuestro router R0 que para alcanzar cualquier red que no esté en su tabla de enrutamiento, lo haga a través del router R1.

- Comprueba que se ha configurado correctamente saliendo del modo configure y mostrando la tabla de enrutamiento.

```bash
Router(config)# exit
Router# show ip route

Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is 10.0.0.2 to network 0.0.0.0

     10.0.0.0/30 is subnetted, 2 subnets
C       10.0.0.0 is directly connected, FastEthernet0/0
S       10.0.1.0 [1/0] via 10.0.0.2
S*   0.0.0.0/0 [1/0] via 10.0.0.2

```

Observamos como nos indica que una de las interfaces está directamente conectada y las dos rutas estáticas que acabamos de definir.

Repetimos la operación con el resto de routers.

3. Comprobación de la conectividad:

- Ejecuta el comando `ip route show` en cada router para verificar que las rutas estáticas se han configurado correctamente.
- Por último, intenta hacer ping desde el router R0 al R3 para comprobar que la configuración de la red es correcta.

### Memoria a entregar

Las capturas de pantalla contendrán toda la pantalla, incluida la hora del PC.

- Generar un documento de texto, con nombre, curso, asignatura, fecha.
- Incluir las siguientes capturas de pantalla:
  - Capturas de pantalla de la configuración de las interfaces de los routers. Se deben ver las direcciones IP asignadas y el estado de las interfaces. Se puede ejecutar el comando `show ip interface brief` a este efecto.
  - Capturas de pantalla de la configuración de las rutas estáticas. Se deben ver las rutas estáticas añadidas y la puerta de enlace. Se puede ejecutar el comando `show ip route` a este efecto.
  - Captura de pantalla de la verificación de la conectividad entre los routers. Se debe ver el resultado del comando `ping` entre los routers.
