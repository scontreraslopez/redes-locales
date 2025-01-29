# Casos Prácticos UP3

## Comprobar la conectividad entre máquinas

Para comprobar la conexión entre redes la herramienta más utilizada es el comando `ping`. Este comando envía mensajes de echo reply esperando el correspondiente mensaje de echo request de vuelta. En su expresión más simple el comando ping sigue la siguiente estructura:

```bash
ping <target-ip | url>
```

Una cuestión importante es que si al utilizar ping no recibimos mensajes de respuesta, esto no significa necesariamente que exista un problema, simplemente que no se ha conseguido la conexión a nivel de red. Muchos administradores deciden colocar cortafuegos que impiden el paso de mensajes ICMP para evitar ataques.

A continuación vemos un ejemplo de verificación de conectividad frente a google.com:

![Captura de pantalla del comando ping](assets\images\captura_ping1.png)

Se observa cómo el dispositivo responde correctamente en 2 milisegundos al envío de paquetes de 32 bytes. El tamaño y el número de paquetes que se envían desde ping se puede configurar modificando los parámetros del comando.
La otra herramienta de uso común es el traceroute, que nos permitirá seguir el itinerario que siguen nuestros paquetes y los routers por los que van saltando. Al igual que con ping, puede ocurrir que algunos routers no respondan a las solicitudes de eco entrantes.
Realizamos una traza a www.google.com.

Se pueden observar todas las direcciones IP por donde pasan nuestros paquetes, en las que se nos indica el tiempo que se tarda en llegar a cada uno de los routers. Es importante notar que cada paquete tiene un máximo estipulado de 30 saltos. Si se sobrepasa este límite el paquete se descarta y aparece el error “Destino inalcanzable”.
Existen herramientas visuales que indican incluso los países por donde están pasando nuestros paquetes y la ubicación final del servidor hacia donde se dirigía la traza.

## Configurar la dirección IP en Linux

Existen dos tipos de asignaciones de direcciones IP.

– IP dinámica: la dirección IP es asignada por medio de un servidor DHCP (dynamic host control protocol). Esta dirección puede cambiar en función del momento en el que se ha iniciado la sesión en el sistema operativo.

– IP fija: la dirección IP y la máscara de subred son asignadas manualmente por el administrador de red. En principio esta dirección es invariable, a no ser que el propio administrador vuelva a establecer una nueva configuración de red.

En Linux

Para configurar la dirección IP en Linux desde la consola debemos seguir los siguientes pasos:

1. Modificar el fichero Interfaces que se encuentra en la ruta /etc/network. Podemos modificarlo con cualquier editor de textos. En el ejemplo, utilizamos el nano:

2. Dentro del fichero, si queremos configurar IP dinámica, incluiríamos las siguientes líneas:
3. En el ejemplo hemos utilizado la interfaz de red eth0, si bien podría ser cualquiera de las interfaces y tantas como se quieran. A continuación guardamos el archivo, reiniciamos la red y ya lo tenemos configurado.
4. El sistema tiene que contestarnos con un mensaje parecido a este, donde nos indica que los paquetes de intercambio del protocolo DHCP han tenido éxito:
Si queremos establecer una IP estática, también hemos de modificar el fichero /etc/network/interfaces:
1. Si en el fichero existe alguna línea de configuración dinámica de la interfaz que queremos pasar a estática, deberemos borrarla o ponerla como un comentario (símbolo #).
2. A continuación especificamos, en el fichero, nuestra configuración IP:
3. Vemos que los parámetros a configurar son la dirección IP (address), la puerta de enlace predeterminada (gateway), la máscara de subred (netmask), la dirección de cable (network) y la dirección de difusión.
4. A continuación, guardando el archivo y volviendo a reiniciar los servicios de la red, la configuración debería resultar exitosa.

sudo nano /etc/network/interfaces
