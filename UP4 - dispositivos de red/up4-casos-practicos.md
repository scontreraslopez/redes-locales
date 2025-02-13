# Casos Prácticos UP4

## Índice
- [1. Dominando el comando 'ip route' en Linux](#1-dominando-el-comando-ip-route-en-linux)
- [2. LAB: Configurando la tabla de enrutamiento de un router CISCO mediante el CLI](#2-lab-configurando-la-tabla-de-enrutamiento-de-un-router-cisco-mediante-el-cli)
  - [2.1. Configurar las interfaces de los routers](#21-configurar-las-interfaces-de-los-routers)
  - [2.2. Configurar las rutas estáticas para los routers](#22-configurar-las-rutas-estáticas-para-los-routers)
  - [2.3. Comprobación de la conectividad](#23-comprobación-de-la-conectividad)
  - [2.4. Memoria a entregar](#24-memoria-a-entregar)
- [3. LAB: Configuarando VLANs en un switch CISCO mediante el CLI](#3-lab-configuarando-vlans-en-un-switch-cisco-mediante-el-cli)
  - [3.1. Configuración de VLANs en Switches](#31-configuración-de-vlans-en-switches)
  - [3.2. Relación del diseño de VLANs con las Subredes IP](#32-relación-del-diseño-de-vlans-con-las-subredes-ip)
  - [3.3. Enlaces Troncales (Trunk Links)](#33-enlaces-troncales-trunk-links)
  - [3.4. Enunciado del Ejercicio](#34-enunciado-del-ejercicio)
  - [3.5. Objetivos de la Práctica](#35-objetivos-de-la-práctica)
  - [3.6. Pasos para la Práctica](#36-pasos-para-la-práctica)
    - [3.6.1. Paso 1: Diseño y Subnetting](#361-paso-1-diseño-y-subnetting)
    - [3.6.2. Paso 2: Configuración en Packet Tracer](#362-paso-2-configuración-en-packet-tracer)
    - [3.6.3. Paso 3: Configurar VLANs en los Switches](#363-paso-3-configurar-vlans-en-los-switches)
    - [3.6.4. Paso 4: Configurar Direcciones IP en los PCs](#364-paso-4-configurar-direcciones-ip-en-los-pcs)
    - [3.6.5. Paso 5: Verificar la Conectividad](#365-paso-5-verificar-la-conectividad)
    - [3.6.6. Paso 6: Explicación Breve del Protocolo 802.1Q](#366-paso-6-explicación-breve-del-protocolo-8021q)
    - [3.6.7. Paso 7: Configuración Adicional para Enrutamiento entre VLANs (Opcional)](#367-paso-7-configuración-adicional-para-enrutamiento-entre-vlans-opcional)
    - [3.6.8. Paso 8: Reflexión y Exploración Adicional](#368-paso-8-reflexión-y-exploración-adicional)

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

## 2. LAB: Configurando la tabla de enrutamiento de un router CISCO mediante el CLI

- Dificultad: Moderada
- Tiempo estimado: 120 minutos

Vamos a realizar la siguiente configuración en Cisco Packet Tracer. Aquí configuraremos las interfaces de los routers y las rutas estáticas para los routers. La topología de red es la siguiente:

![Router Configuration Exercise](/assets/images/router-config-up4-1.png)

### 2.1. Configurar las interfaces de los routers

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

**Checklist de configuración**:

Esto permite ir tachando según se vaya completando la configuración.

- [ ] Hostname de R0
- [ ] ip address de R0 Fa0/0
- [ ] no shutdown de R0 Fa0/0
- [ ] Hostname de R1
- [ ] ip address de R1 Fa0/0
- [ ] no shutdown de R1 Fa0/0
- [ ] ip address de R1 Fa0/1
- [ ] no shutdown de R1 Fa0/1
- [ ] Hostname de R2
- [ ] ip address de R2 Fa0/0
- [ ] no shutdown de R2 Fa0/0
- [ ] ip address de R2 Fa0/1
- [ ] no shutdown de R2 Fa0/1
- [ ] Hostname de R3
- [ ] ip address de R3 Fa0/0
- [ ] no shutdown de R3 Fa0/0

En este punto ya deberíamos ver todas las conexiones entre routers en verde.

### 2.2. Configurar las rutas estáticas para los routers

- Establecemos las rutas estáticas para permitir la comunicación entre los routers, comenzando con el router R0. Es fundamental que las tablas de enrutamiento de todos los routers sean coherentes. Esto implica que cada router debe contener la ruta adecuada para alcanzar la red adyacente en un solo salto. Una vez configuradas correctamente las tablas de enrutamiento de los routers, podremos acceder a cada uno de ellos desde los demás.

**No es preciso añadir entradas en las tablas de enrutamiento para las redes directamente conectadas**. Por ejemplo, no necesitamos añadir una entrada para la conexión entre R0 y R1, ya que esta conexión es directa y se añade automáticamente a la tabla de enrutamiento.

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

Como puede ser un poco difícil de seguir, quizá resulte útil este cuadro resumen: 

| Segmento de red | Dirección de red |
|-----------------|------------------|
| A: R0 - R1         | 10.0.0.0/30      |
| B: R1 - R2         | 10.0.1.0/30      |
| C: R2 - R3         | 10.0.2.0/30      |

Debemos configurar los siguientes saltos estáticos en cada router:

| Router | Red destino | Máscara de red | Próximo salto |
|--------|-------------|----------------|---------------|
| R0     | Dirección IP de red B | 255.255.255.252 | Dirección IP de R1 Fa0/0 |
| R0     | Dirección IP de red C | 255.255.255.252 | Dirección IP de R1 Fa0/0 |
| R1     | Dirección IP de red C | 255.255.255.252 | Dirección IP de R2 Fa0/0 |
| R2     | Dirección IP de red A | 255.255.255.252 | Dirección IP de R1 Fa0/1 |
| R3     | Dirección IP de red B | 255.255.255.252 | Dirección IP de R2 Fa0/1 |
| R3     | Dirección IP de red A | 255.255.255.252 | Dirección IP de R2 Fa0/1 |

Nótese que en estos routers en lugar de las direcciones de red, podemos usar el default gateway ip route como en el ejemplo de R0 ```Router(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2```

**Checklist de configuración**:

Esto permite ir tachando según se vaya completando la configuración.

- [ ] ip route de R0 a red B
- [ ] ip route de R0 a red C
- [ ] ip route de R1 a red C
- [ ] ip route de R2 a red A
- [ ] ip route de R3 a red B
- [ ] ip route de R3 a red A

### 2.3. Comprobación de la conectividad

 Ejecuta el comando `show ip route` en cada router para verificar que las rutas estáticas se han configurado correctamente. Como son los routers en los extremos, funcionará si se ha configurado correctamente todos los saltos.

- Por último, intenta hacer ping desde el router R0 al R3 para comprobar que la configuración de la red es correcta.

> [!TIP]
> Desde el modo de configuración interface `config-if` de dicha interfaz utiliza `no ip address` para borrar una dirección ip de una interfaz

> [!TIP]
> Desde el modo enable`Router#` o usuario `Router>` puedes ejecutar el comando `show ip interface brief` o `show ip interface`

### 2.4. Memoria a entregar

Las capturas de pantalla contendrán toda la pantalla, incluida la hora del PC.

- Generar un documento de texto, con nombre, curso, asignatura, fecha.
- Incluir las siguientes capturas de pantalla:
  - Capturas de pantalla de la configuración de las interfaces de los routers. Se deben ver las direcciones IP asignadas y el estado de las interfaces. Se puede ejecutar el comando `show ip interface brief` a este efecto.
  - Capturas de pantalla de la configuración de las rutas estáticas. Se deben ver las rutas estáticas añadidas y la puerta de enlace. Se puede ejecutar el comando `show ip route` a este efecto.
  - Captura de pantalla de la verificación de la conectividad entre los routers. Se debe ver el resultado del comando `ping` entre los routers.

## 3. LAB: Configuarando VLANs en un switch CISCO mediante el CLI

- Dificultad: Moderada
- Tiempo estimado: 90 minutos

### 3.1. Configuración de VLANs en Switches

Por defecto, todos los puertos de un switch pertenecen a la VLAN 1, la VLAN nativa. Si deseas segmentar tu red, necesitas:

- Crear Nuevas VLANs: Configura las VLANs que necesites directamente en el switch.
- Asignar Puertos a las VLANs: Mueve o asigna los puertos físicos del switch a las VLANs recién creadas. Esto determina qué dispositivos pertenecen a cada segmento de red.

Este proceso es fundamental para controlar quién puede comunicarse con quién dentro de tu infraestructura.

### 3.2. Relación del diseño de VLANs con las Subredes IP

El diseño e implementación de las VLANs deben alinearse con el esquema de subredes IP de tu red. Aquí tienes principios clave a seguir:

- Una Subred por VLAN: Cada VLAN debe tener su propia subred IP. Esto simplifica el enrutamiento y la gestión de direcciones.
- Dispositivos consistentes dentro de la VLAN: Todos los equipos en una VLAN deben pertenecer a la misma subred. Esto asegura una comunicación fluida y evita conflictos de direcciones.
- Comunicación entre VLANs: Para permitir que diferentes VLANs se comuniquen, necesitas un dispositivo de capa 3, como un router o un switch de capa 3 (Switch L3 o Switch Layer3). Este dispositivo actúa como intermediario, dirigiendo el tráfico entre las subredes asociadas a cada VLAN. Un switch de capa 3, nos permite definir interfaces virtuales para cada VLAN, asignarles rangos de subred específicos y gestionar el enrutamiento internamente.

### 3.3. Enlaces Troncales (Trunk Links)

Enlaces Troncales (Trunk Links): Son conexiones especiales que transportan tráfico de múltiples VLANs entre switches y dispositivos de capa 3. Utilizan protocolos como IEEE 802.1Q para etiquetar los marcos Ethernet y así identificar a qué VLAN pertenece cada uno.

### 3.4. Enunciado del Ejercicio

En esta práctica, configuraremos VLANs en switches Cisco utilizando Packet Tracer, combinando conceptos básicos de subnetting. Además, utilizaremos el protocolo de trunking 802.1Q, que es un estándar ampliamente usado para permitir que múltiples VLANs compartan un enlace troncal. Aunque nos enfocaremos en 802.1Q, es importante saber que existen otros protocolos como ISL (Inter-Switch Link), propietario de Cisco.

Imaginemos una empresa donde necesitamos segmentar la red en dos departamentos. Por simplicidad, consideraremos que en cada departamento se necesita tener el mismo número de equipos conectados. Los departamentos son:

- Departamento de Ventas
- Departamento de Contabilidad

Queremos que los equipos de cada departamento solo se comuniquen entre sí y estén aislados del otro departamento. Para ello, asignaremos a cada departamento una VLAN diferente:

- VLAN 10: Ventas
- VLAN 20: Contabilidad

Considera además que la Red Principal de la empresa es 192.168.0.0/24

### 3.5. Objetivos de la Práctica

- Configurar VLANs estáticas en switches.
- Asignar puertos a diferentes VLANs.
- Configurar enlaces troncales utilizando 802.1Q.
- Realizar subnetting sencillo para asignar direcciones IP.
- Verificar la comunicación entre hosts en la misma VLAN.
- Comprobar el aislamiento entre diferentes VLANs.

### 3.6. Pasos para la Práctica

#### 3.6.1. Paso 1: Diseño y Subnetting

Primero, vamos a planificar nuestras subredes a partir de la Red Principal: 192.168.0.0/24

Usando FLSM para subnetting, determinamos el rango de IP de cada una de las VLANs:

| Departamento | VLAN | Dirección de red (CIDR) | Broadcast | Rango de IPs host |
|--------------|--------|--------------|-------|------------|
| Ventas | VLAN 10 | 192.168.0.0/25 | 192.168.0.127 | 192.168.0.1 - 192.168.0.126 |
| Contabilidad | VLAN 20 | 192.168.0.128/25 | 192.168.0.255 | 192.168.0.129 - 192.168.0.254 |

#### 3.6.2. Paso 2: Configuración en Packet Tracer

- Abre Packet Tracer y crea un nuevo proyecto.
- Añade los dispositivos necesarios:
  - 2x Switches 2960
  - 4x PCs representando al primer y último host de cada departamento.
- Conecta los dispositivos:

Switch1:

- Conecta PC1 al puerto Fa0/1.
- Conecta PC2 al puerto Fa0/2.

Switch2:

- Conecta PC3 al puerto Fa0/1.
- Conecta PC4 al puerto Fa0/2.

Enlace Troncal:

- Conecta el puerto Gig0/1 de Switch1 al puerto Gig0/1 de Switch2.

#### 3.6.3. Paso 3: Configurar VLANs en los Switches

##### Configuración en Switch1

- Accede a la CLI de Switch1.
- Entra en modo privilegiado y luego en modo de configuración global:
```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname Switch1
```
- Crea la VLAN 10 para Ventas:
```bash
Switch(config)# vlan 10
Switch(config-vlan)# name Ventas
Switch(config-vlan)# exit
```
- Crea la VLAN 20 para Contabilidad:
```bash
Switch(config)# vlan 20
Switch(config-vlan)# name Contabilidad
Switch(config-vlan)# exit
```
- Asigna los puertos a las VLANs:

Asignar PC1 a VLAN 10:
```bash
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

Asignar PC2 a VLAN 20:
```bash
Switch(config)# interface FastEthernet0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
```

Configura el puerto troncal:

```bash
Switch(config)# interface Gig0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit
```

> Nota: Configuramos la VLAN nativa como VLAN 99 para mejorar la seguridad al evitar el uso de la VLAN predeterminada (VLAN 1) como nativa.

##### Configuración en Switch2

Repite los mismos pasos que hiciste en Switch1.

- Crea las VLANs 10 y 20.
- Asigna los puertos:
  - Asignar PC3 a VLAN 10 (puerto Fa0/1).
  - Asignar PC4 a VLAN 20 (puerto Fa0/2).
- Configura el puerto troncal en Fa0/24.
- Configurar Direcciones IP en los PCs

#### 3.6.4. Paso 4: Configurar las IPs en los PCs

Para los PCs en VLAN 10 (Ventas):

PC1:
- IP Address: 192.168.10.2
- Subnet Mask: 255.255.255.0
- Gateway: 192.168.10.1 (lo configuraremos más adelante)

PC3:
- IP Address: 192.168.10.3
- Subnet Mask: 255.255.255.0
- Gateway: 192.168.10.1

Para los PCs en VLAN 20 (Contabilidad):

PC2:
- IP Address: 192.168.20.2
- Subnet Mask: 255.255.255.0
- Gateway: 192.168.20.1

PC4:
- IP Address: 192.168.20.3
- Subnet Mask: 255.255.255.0
- Gateway: 192.168.20.1

Configuración en Packet Tracer:

- Abre cada PC, ve a la pestaña Desktop y selecciona IP Configuration.
- Introduce la IP Address y Subnet Mask correspondientes.

#### 3.6.5. Paso 5: Verificar la Conectividad

1. Comunicación dentro de la misma VLAN:

Desde PC1, realiza un ping a PC3:

``` bash
C:\> ping 192.168.10.3
```

Deberías recibir respuestas exitosas.

Desde PC2, realiza un ping a PC4:

``` bash
C:\> ping 192.168.20.3
```

2. Aislamiento entre VLANs:

Intenta hacer ping desde PC1 a PC2:
```bash
C:\> ping 192.168.20.2
```

No deberías recibir respuesta, ya que las VLANs están aisladas y no hay enrutamiento entre ellas.

#### 3.6.6. Paso 6: Explicación Breve del Protocolo 802.1Q

El estándar 802.1Q es un protocolo de trunking que permite transmitir tráfico de múltiples VLANs a través de un único enlace físico. Esto se logra añadiendo una etiqueta (tag) a las tramas Ethernet, indicando a qué VLAN pertenece cada una.

¿Por qué 802.1Q?

- Compatibilidad: Es un estándar abierto, lo que significa que funciona entre dispositivos de diferentes fabricantes, no solo Cisco.
- Eficiencia: Permite un uso más eficiente de los enlaces físicos, al transportar múltiples VLANs sin necesidad de cables separados.
- Flexibilidad: Facilita la expansión y reconfiguración de la red sin cambios significativos en la infraestructura física.

Otros Protocolos de Trunking:

- ISL (Inter-Switch Link): Protocolo propietario de Cisco, ahora en desuso debido a la popularidad y adopción de 802.1Q.
- VLAN Trunking Protocol (VTP): Aunque no es un protocolo de trunking per se, VTP es utilizado para propagar información de VLANs a través de la red conmutada. Es importante manejarlo con cuidado para evitar problemas de seguridad.

#### 3.6.7. Paso 7: Configuración Adicional para Enrutamiento entre VLANs 

Si se requiere comunicación entre VLANs, necesitamos un dispositivo de capa 3. Puedes utilizar un router o un switch multicapa (Capa 3).

Usando Router-on-a-Stick (ROAS):

1. Añade un Router al escenario.
2. Conecta el puerto GigabitEthernet0/0 del router al Switch1 (puerto Fa0/24).
3. Configura subinterfaces en el router para cada VLAN:

```bash
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config-if)# exit
```

Subinterfaz para VLAN 10:

```bash
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit
```

Subinterfaz para VLAN 20:

```bash
Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit
```

4. Configura el puerto del switch conectado al router como troncal:

``` bash
Switch1(config)# interface FastEthernet0/24
Switch1(config-if)# switchport mode trunk
Switch1(config-if)# switchport trunk allowed vlan 10,20
Switch1(config-if)# exit
```

5. Actualiza la configuración de gateway en los PCs para que apunten a las IPs del router (ya establecidas en el Paso 4).

6. Verifica la comunicación entre VLANs:

Desde PC1, realiza un ping a PC2. Ahora deberías recibir respuestas, ya que el router está ruteando el tráfico entre las VLANs.

#### 3.6.8. Paso 8: Reflexión y Exploración Adicional

Es posible profundizar en este campo por los siguientes caminos:

- Seguridad: Considera implementar ACLs (Listas de Control de Acceso) en el router para controlar qué tráfico puede pasar entre VLANs.
- Subnetting Avanzado: Experimenta con diferentes máscaras de subred para optimizar el uso de direcciones IP.
- VTP (VLAN Trunking Protocol): Investiga cómo VTP puede ayudarte a gestionar las VLANs en múltiples switches de manera centralizada, pero ten en cuenta las implicaciones de seguridad.
- Experimenta con VLANs dinámicas y ve cómo se pueden asignar dispositivos a VLANs basándose en criterios como direcciones MAC o autenticación de usuario.
- Investiga otros protocolos y tecnologías como Private VLANs, Q-in-Q tunneling, y cómo SDN (Software-Defined Networking) está cambiando la forma en que gestionamos las redes.
Pr- ueba modificar la topología añadiendo más switches y PCs.
- Crea VLANs adicionales y practica el subnetting con diferentes máscaras.
- Simula escenarios donde ciertos departamentos necesiten comunicarse y otros no, ajustando las ACLs en el router.

Recuerda: La práctica constante y la exploración son claves para dominar el mundo de las redes.

Prácticas de Mejores Configuraciones:
- Siempre documenta tus configuraciones.
- Cambia la VLAN nativa por defecto para evitar ataques VLAN hopping.
- Deshabilita puertos no utilizados y colócalos en una VLAN no utilizada.

### 3.7 Conclusión

En esta práctica, hemos aprendido a:

- Configurar VLANs estáticas y asignar puertos.
- Utilizar el protocolo 802.1Q para enlaces troncales.
- Implementar subnetting básico para segmentar la red.
- Configurar enrutamiento entre VLANs utilizando Router-on-a-Stick. (ROAS)

Estas habilidades son fundamentales para diseñar redes seguras y eficientes. La segmentación mediante VLANs no solo mejora el rendimiento sino que también proporciona una capa adicional de seguridad al aislar diferentes tipos de tráfico.
