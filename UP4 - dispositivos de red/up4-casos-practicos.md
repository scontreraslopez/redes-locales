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

## Configurando la tabla de enrutamiento de un router CISCO mediante el CLI

Vamos a realizar la siguiente configuración en Cisco Packet Tracer. Aquí configuraremos las interfaces de los routers y las rutas estáticas para los routers. La topología de red es la siguiente:

![Router Configuration Exercise](/assets/images/router-config-up4-1.png)

1. Configurar las interfaces de los routers:

- Ponemos los 3 routers 1841 en Cisco Packet Tracer y los conectamos entre sí con cables cruzados. Hacemos doble click y nos vamos a la pestaña CLI.
- Nos aseguramos que la Fa0/0 de R0 conecta con la Fa0/0 de R1, la Fa0/1 de R1 con la Fa0/0 de R2.
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

Se deja la configuración de R2 como ejercicio para el lector.

2. Configurar las rutas estáticas para los routers:

- Configuramos las rutas estáticas para que los routers puedan comunicarse entre sí. Comenzamos con R0. Un aspecto crucial es que las tablas de enrutamiento de todos los routers deben ser consistentes. Esto significa que cada router debe incluir la ruta correcta que permita llegar a la red vecina en un solo salto. Una vez que las tablas de enrutamiento de los routers estén configuradas adecuadamente, podremos acceder desde cada router a todos los demás.

```bash
Router> enable
Router# configure terminal
Router(config)# ip route




