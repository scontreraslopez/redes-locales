# Casos Prácticos UP3

## Índice

- [1. Comprobar la conectividad entre máquinas](#1-comprobar-la-conectividad-entre-máquinas)
  - [1.1. El comando ping](#11-el-comando-ping)
  - [1.2. El comando traceroute](#12-el-comando-traceroute)
- [2. Configurar la dirección IP en Linux](#2-configurar-la-dirección-ip-en-linux)
  - [2.1. Tareas de setup para el ejercicio](#21-tareas-de-setup-para-el-ejercicio)
  - [2.2. Configuración de la dirección IP](#22-configuración-de-la-dirección-ip)
    - [2.2.1. Configuración de la dirección IP dinámica (Alpine)](#221-configuración-de-la-dirección-ip-dinámica-alpine)
    - [2.2.2. Configuración de la dirección IP estática (Alpine)](#222-configuración-de-la-dirección-ip-estática-alpine)
    - [2.2.3 Configuración de la dirección IP en Ubuntu-based distros (TBD)](#223-configuración-de-la-dirección-ip-en-ubuntu-based-distros-tbd)
- [3. Configurar router mediante CISCO Cli - Gigabit Ethernet Interface](#3-configurar-router-mediante-cisco-cli---gigabit-ethernet-interface)

## 1. Comprobar la conectividad entre máquinas

### 1.1. El comando ping

Para comprobar la conexión entre redes la herramienta más utilizada es el comando `ping`. Este comando envía mensajes de echo reply esperando el correspondiente mensaje de echo request de vuelta. En su expresión más simple el comando ping sigue la siguiente estructura:

```bash
ping <target-ip | url>
```

Una cuestión importante es que si al utilizar ping no recibimos mensajes de respuesta, esto no significa necesariamente que exista un problema, simplemente que no se ha conseguido la conexión a nivel de red. Muchos administradores deciden colocar cortafuegos que impiden el paso de mensajes ICMP para evitar ataques.

A continuación vemos un ejemplo de verificación de conectividad frente a google.com:

![Captura de pantalla del comando ping](assets/images/captura_ping1.png)

Se observa cómo el dispositivo responde correctamente en unos 20-50 milisegundos al envío de paquetes de 32 bytes. El tamaño y el número de paquetes que se envían desde ping se puede configurar modificando los parámetros del comando.

### 1.2. El comando traceroute

La otra herramienta típica es traceroute, que nos permite ver la ruta que sigue un paquete desde nuestro dispositivo hasta el destino. En el siguiente ejemplo se muestra la ruta que sigue un paquete desde un dispositivo hasta google.com:

![Captura de pantalla del comando traceroute](assets/images/captura_traceroute1.png)

```bash
traceroute [opciones] <destino>  --> Linux
tracert [opciones] <destino>  --> Windows
```

Se pueden observar todas las direcciones IP por donde pasan nuestros paquetes, en las que se nos indica el tiempo que se tarda en llegar a cada uno de los routers. Es importante notar que cada paquete tiene un máximo estipulado de 30 saltos (TTL=30). Si se sobrepasa este límite el paquete se descarta y aparece el error “Destino inalcanzable”.

Existen herramientas visuales que muestran los países por los que pasan nuestros paquetes y la ubicación final del servidor al que se dirige la traza. Un ejemplo de estas herramientas es [Open Visual Traceroute](https://gsuite.tools/traceroute). Es una herramienta de código abierto que permite visualizar gráficamente los saltos que toman los paquetes de datos de nuestro ordenador, mostrando un mapa mundial en 3D o 2D. Esta herramienta es muy útil para entender cómo se mueven los datos a través de la red y para identificar la ubicación final del servidor.

## 2. Configurar la dirección IP en Linux

### 2.1. Tareas de setup para el ejercicio

Esto lo vamos a hacer utilizando para ello la VM alpine que encontraréis en: smb://aquituuser@aulainfo2.local/share/Redes/
Copiad alpine1.ova e importarla.

[Información adicional para montar el directorio SAMBA](https://www.linode.com/docs/guides/linux-mount-smb-share/)

Ejecutar setup-alpine (la distribución por defecto del teclado es la en-us, por lo que se espera un poco de pericia para escribir el símbolo del guión '-' ). Instalar con las opciones por defecto excepto para distribución del teclado _es_ y para zona horaria _Europe/Madrid_.

## 2.2. Configuración de la dirección IP

Existen dos tipos de asignaciones de direcciones IP:

– IP dinámica: la dirección IP es asignada automáticamente por un servidor DHCP (Dynamic Host Configuration Protocol). Esta dirección puede variar cada vez que se inicia una nueva sesión en el sistema operativo.
– IP fija: la dirección IP y la máscara de subred son asignadas manualmente por el administrador de red. En principio, esta dirección es invariable, a no ser que el propio administrador vuelva a establecer una nueva configuración de red.

Para configurar la dirección IP en Linux desde la consola, debemos seguir los siguientes pasos:

### 2.2.1. Configuración de la dirección IP dinámica (Alpine)

1. Modificar el archivo `interfaces` que se encuentra en la ruta `/etc/network`. Podemos modificarlo con cualquier editor de texto. En el ejemplo, utilizamos `nano`:

```bash
sudo nano /etc/network/interfaces
```

2. Dentro del archivo, si queremos configurar una IP dinámica, incluiríamos las siguientes líneas:

```bash
# Utilizar DHCP para la configuración del adaptador
auto eth0
iface eth0 inet dhcp
```

3. Guardamos el archivo y reiniciamos la red:

```bash
sudo /etc/init.d/networking restart
```

4. El sistema debería responder con un mensaje indicando que los paquetes de intercambio del protocolo DHCP han tenido éxito.

5. Para comprobar que la configuración se ha realizado correctamente, podemos utilizar el comando `ifconfig`:

### 2.2.2. Configuración de la dirección IP estática (Alpine)

Para establecer una IP estática, también debemos modificar el archivo `/etc/network/interfaces`:

1. Si en el archivo existe alguna línea de configuración dinámica de la interfaz que queremos pasar a estática, deberemos borrarla o comentarla (símbolo `#`).

2. A continuación, especificamos nuestra configuración IP:

```bash
# Configuración de IP estática en eth0
auto eth0
iface eth0 inet static
address 192.168.12.5
gateway 192.168.12.1
netmask 255.255.255.0
network 192.168.12.0
broadcast 192.168.12.255
```

3. Guardamos el archivo y reiniciamos los servicios de red:

```bash
sudo /etc/init.d/networking restart
```

4. Para comprobar que la configuración se ha realizado correctamente, podemos utilizar el comando `ifconfig`:

### 2.2.3 Configuración de la dirección IP en Ubuntu-based distros (TBD)

Primero, puedes listar las conexiones disponibles que Network Manager conoce con el siguiente comando, esto es importante para encontrar el nombre, ya que el id del dispositivo no se usa:

```bash
nmcli con show
```

Esto te dará algo como:

NAME                UUID                                  TYPE            DEVICE 
Wired connection 1  7a3b674a-f346-3cfb-8b30-ff70e6db1b60  802-3-ethernet  enp0s3
You can then modify the connection with the following:

Si desea configurar la conexión para usar DHCP, puede usar lo siguiente.

```bash
nmcli con mod "Wired connection 1"
  ipv4.addresses ""
  ipv4.gateway ""
  ipv4.dns ""
  ipv4.dns-search ""
  ipv4.method "auto"
```

Cuando ingreses lo anterior, utilízalo en una sola línea. Lo he dividido en líneas separadas para que sea más claro. Necesitas todas las comillas vacías ya que eliminan cualquier configuración que hayan tenido previamente.

```bash
nmcli con mod "Wired connection 1"
  ipv4.addresses "HOST_IP_ADDRESS/IP_NETMASK_BIT_COUNT"
  ipv4.gateway "IP_GATEWAY"
  ipv4.dns "PRIMARY_IP_DNS,SECONDARY_IP_DNS"
  ipv4.dns-search "DOMAIN_NAME"
  ipv4.method "manual" 
```

To add a network, use:

```nmcli con add ...```

Con parámetros similares. Puedes revisar la [nmcli cheatsheet](https://www.golinuxcloud.com/nmcli-command-examples-cheatsheet-centos-rhel/) para más detalles.

Para activar la configuración, reinicia.

[Referencias](https://linuxconfig.org/setting-a-static-ip-address-in-ubuntu-24-04-via-the-command-line)

### Configurar router mediante CISCO Cli - Gigabit Ethernet Interface

Para configurar una interfaz Gigabit Ethernet en un router Cisco, siga estos pasos:

1. Acceda al modo de configuración global:

```bash
Router> enable
Router# configure terminal
```

2. Configure la interfaz:

```bash
Router(config)# interface gigabitethernet 0/0
```

3. Asigne una dirección IP y una máscara de subred. Por ejemplo

```bash
Router(config-if)# ip address 192.168.1.1 255.255.255.0
```

4. Habilite la interfaz:

```bash
Router(config-if)# no shutdown
```

5. Salga del modo de configuración de la interfaz:

```bash
Router(config-if)# exit
```

6. Guarde la configuración:

```bash
Router# copy running-config startup-config
```

[Referencias](https://www.netacad.com/es/courses/networking-basics?courseLang=es-XL)
