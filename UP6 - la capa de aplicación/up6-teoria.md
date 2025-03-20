# Todo lo que necesitas saber sobre DNS: Curso intensivo de diseño de sistemas #4

## Imagen principal


Fuente: https://www.youtube.com/watch?v=27r4Bzuj5NQ

DNS, o Sistema de Nombres de Dominio, es el directorio de Internet que traduce nombres de dominio legibles para humanos a direcciones IP legibles para máquinas. Es un componente crucial en la columna vertebral de Internet 

La jerarquía DNS se compone de diferentes tipos de servidores DNS, cada uno con una función única, incluyendo resolutores DNS, servidores raíz, servidores de nombres de dominio de nivel superior (TLD) y servidores de nombres autoritativos para dominios 

Cuando un navegador realiza una consulta DNS, solicita ayuda a un resolutor DNS, que puede ser proporcionado por un proveedor de servicios de Internet (ISP) o servicios populares como Cloudflare (1.1.1.1) o Google (8.8.8.8). Si el resolutor no tiene la respuesta en su caché, encuentra el servidor de nombres autoritativo correcto y le solicita la información 

El servidor de nombres autoritativo contiene la respuesta a la consulta DNS. Cuando se actualizan los registros DNS de un dominio, su servidor de nombres autoritativo también se actualiza 

El resolutor DNS encuentra el servidor de nombres autoritativo a través de un sistema de tres niveles principales de servidores DNS autoritativos: servidores raíz, servidores de nombres TLD y servidores de nombres autoritativos para dominios 

Los servidores raíz almacenan las direcciones IP de los servidores de nombres TLD. Hay 13 servidores raíz lógicos, cada uno con una dirección IP única asignada y múltiples servidores físicos detrás de cada dirección IP 

Los servidores de nombres TLD almacenan las direcciones IP de los servidores de nombres autoritativos para todos los dominios bajo su nivel. Existen muchos tipos de TLD, incluyendo .com, .org, .edu, y TLDs de código de país como .de y .uk 

Los servidores de nombres autoritativos para un dominio proporcionan respuestas definitivas a las consultas DNS. Cuando se registra un dominio, el registrador utiliza servidores de nombres autoritativos por defecto, pero pueden ser cambiados a otros, como los operados por proveedores en la nube como AWS y Cloudflare 

El diseño jerárquico de DNS lo hace altamente descentralizado y robusto. La vida de una consulta DNS típica incluye que el usuario escriba un nombre de dominio en un navegador, el navegador revise su caché y luego realice una llamada al sistema operativo para intentar obtener la respuesta, lo que puede implicar contactar con el resolutor DNS, el servidor raíz, el servidor de nombres TLD y finalmente el servidor de nombres autoritativo del dominio 

Al actualizar los registros DNS para un sistema de producción activo y de alto tráfico, es esencial considerar la propagación DNS, que puede ser lenta debido al tiempo de vida (TTL) de cada registro DNS. Para mitigar este riesgo, se recomienda reducir el TTL del registro a cambiar a un tiempo corto, como 60 segundos, con suficiente antelación a la actualización, y mantener el servidor funcionando en la dirección IP antigua por un tiempo después de la actualización 
