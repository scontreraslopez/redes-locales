# Tema 1: Caracterización de las Redes Locales - Repaso y Ejercicios Prácticos

## 1. Definición de Red de Área Local y Principales Características

- **Red de Área Local (LAN):**  
  Una LAN es una red de comunicación que abarca un espacio geográfico reducido (por ejemplo, un edificio, una oficina, un hogar o un campus). Surgen por la necesidad de compartir recursos dentro de la organización. Se caracteriza por:
  - **Alta velocidad:** Uso de tecnologías como Ethernet y Wi-Fi.
  - **Baja latencia:** Las distancias cortas reducen significativamente el tiempo de propagación.
  - **Administración centralizada:** Normalmente, la red es gestionada por la propia organización o el propietario local, lo cual facilita su mantenimiento, seguridad y control.

---

## 2. Clasificación de Redes según su Ámbito de Aplicación

- **PAN (Personal Area Network):**
  - **Descripción:** Red personal que generalmente utiliza tecnologías como Bluetooth para conectar dispositivos cercanos (smartphones, auriculares, smartwatches, etc.).
  - **Operación:** Suele ser gestionada por el propio usuario, ya que conecta dispositivos personales.

- **LAN (Local Area Network):**
  - **Descripción:** Redes que cubren áreas limitadas (hogares, oficinas, escuelas).
  - **Operación:** Administradas y operadas internamente por la organización o el propietario local.

- **MAN (Metropolitan Area Network) o Red de Campus:**
  - **Descripción:** Redes que abarcan un área más extensa que una LAN, como campus universitarios o conjuntos de edificios en una misma zona urbana.
  - **Operación:** Generalmente gestionadas por la institución o por entidades colaborativas en el ámbito institucional o corporativo.

- **WAN (Wide Area Network):**
  - **Descripción:** Redes que se extienden a lo largo de grandes distancias, conectando ciudades, países o incluso continentes.
  - **Operación:** Normalmente operadas y administradas por proveedores de servicios de telecomunicaciones, quienes ofrecen enlaces de comunicación a nivel regional, nacional o internacional.

---

## 3. Modelos de Referencia en Redes

Los modelos de referencia son una forma de abstraer la complejidad de la interconexión de sistemas y permiten estudiar la interacción de protocolos y equipos. En redes, destacan los siguientes modelos:

- **Modelo OSI (Open Systems Interconnection):**
  - **Descripción:** Propuesto por la ISO, es un modelo académico que proporciona una aproximación teórica para comprender la transmisión de datos.
  - **Capas:**  
    1. **Capa Física:** Transmisión de bits a través del medio físico.  
    2. **Capa de Enlace de Datos:** Control de errores, detección de colisiones, acceso al medio.  
    3. **Capa de Red:** Encaminamiento y direccionamiento.  
    4. **Capa de Transporte:** Segmentación, control de flujo y reensamblaje.  
    5. **Capa de Sesión:** Gestión de la conexión y sesiones entre aplicaciones.  
    6. **Capa de Presentación:** Formato, cifrado y compresión de datos.  
    7. **Capa de Aplicación:** Interfaz y servicios directos al usuario.

- **Modelo TCP/IP:**
  - **Descripción:** Basado en la experiencia práctica y experimental, es un modelo más ingenieril y realista en la aplicación de protocolos.
  - **Capas:**  
    1. **Capa de Acceso a la Red:** Combina funciones de las capas física y de enlace.  
    2. **Capa de Internet:** Encargada del direccionamiento y del encaminamiento de paquetes (similar a la capa de red del OSI).  
    3. **Capa de Transporte:** Gestión de la comunicación punto a punto (TCP, UDP).  
    4. **Capa de Aplicación:** Implementa protocolos y servicios a nivel de usuario.

- **Modelo Híbrido (por Tanenbaum):**
  - **Descripción:** 
    Una aproximación que parte del modelo TCP/IP pero que separa la capa de acceso al medio en dos: **Capa Física** y **Capa de Enlace de Datos**. Esta separación facilita el estudio de ambas capas, dado que tienen funciones de naturaleza muy distinta.

---

## 4. Problemas del Tema 1

En el estudio de la transmisión de datos en redes es fundamental comprender y poder calcular los distintos tipos de retardo o demora que afectan a la entrega de la información. Entre ellos destacan:

### 4.1 Tiempo de Transmisión

- **Definición:** Es el tiempo que se necesita para insertar todos los bits de un paquete en el medio de transmisión.
- **Fórmula:**

![Tiempo de Transmisión](/assets/images/t1_f1.png)

### 4.2 Retraso de Propagación

- **Definición:** Es el tiempo que tarda un bit en recorrer el medio físico desde el emisor hasta el receptor.
- **Fórmula:**
  \[
t1_f2
  \]
  *Ejemplo:* En fibra óptica, la velocidad de propagación suele ser aproximadamente \(2 \times 10^8\) m/s. 

### 4.3 Retraso de Procesamiento

- **Definición:** Se refiere al tiempo adicional que requieren los equipos intermedios (como routers y switches) para procesar y reenviar el paquete. Este retardo depende de la capacidad del equipo y de la carga de trabajo en el momento.

### 4.4 Tiempo de Entrega del Paquete

- **Definición:** Es la suma de todos los retardos (transmisión, propagación y procesamiento) que un paquete experimenta al ir desde el origen hasta el destino.
- **Fórmula General:**
  \[
t1_f3
  \]

    > [!NOTE]  
    > En una red LAN, el **tiempo de transmisión** suele ser el factor dominante debido a las cortas distancias y altas velocidades de conexión. Por otro lado, en redes de mayor alcance como el Internet, el **retraso de propagación** adquiere mayor relevancia. Esto ha impulsado el desarrollo de tecnologías como las **CDN (Content Delivery Networks)**, que consisten en redes distribuidas diseñadas para acercar el contenido al usuario final, reduciendo la latencia y mejorando la experiencia en la entrega de información.

---

## 5. Ejercicios Prácticos

### Ejercicio 1: Transmisión de un archivo .OVA de 5GB en una red Gigabit Ethernet

**Datos:**
- **Tamaño del archivo:** 5GB  
  (Se considerará 1GB = \(10^9\) bytes, por lo tanto, 5GB = \(5 \times 10^9\) bytes).
- **Velocidad de la red:** 1 Gbps (\(1 \times 10^9\) bits/s).
- **Suposiciones:** No se consideran los retardos de propagación ni de procesamiento.

**Cálculos:**

1. **Conversión de bytes a bits:**
   \[
   5 \, \text{GB} = 5 \times 10^9 \, \text{bytes} \times 8 = 40 \times 10^9 \, \text{bits}
   \]

2. **Tiempo de Transmisión:**
   \[
   T_t = \frac{40 \times 10^9 \, \text{bits}}{1 \times 10^9 \, \text{bits/s}} = 40 \, \text{segundos}
   \]

**Respuesta:** El archivo se transmitirá en 40 segundos.

---

### Ejercicio 2: Transmisión de un email de 70kB por fibra DIGI de 600Mbps

**Datos:**
- **Tamaño del email:** 70 kB  
  (Se considera 70 kB = \(70 \times 10^3\) bytes ≈ 560 kbits, ya que \(70\,000 \times 8 = 560\,000\) bits).
- **Velocidad de la red:** 600 Mbps (\(600 \times 10^6\) bits/s).
- **Distancia entre origen y destino:** 3000 km = 3,000,000 m.
- **Velocidad de propagación:** Aproximadamente \(2 \times 10^8\) m/s.
- **Suposiciones:** No se añade retraso de procesamiento extra.

**Cálculos:**

1. **Tiempo de Transmisión:**
   \[
   T_t = \frac{560\,000 \, \text{bits}}{600 \times 10^6 \, \text{bits/s}} \approx 0.000933 \, \text{segundos} \quad (\approx 0.933 \, \text{ms})
   \]

2. **Retraso de Propagación:**
   \[
   T_p = \frac{3\,000\,000 \, \text{m}}{2 \times 10^8 \, \text{m/s}} = 0.015 \, \text{segundos} \quad (15 \, \text{ms})
   \]

3. **Tiempo Total Sin Procesamiento Adicional:**
   \[
   T_{total} \approx 0.933 \, \text{ms} + 15 \, \text{ms} \approx 15.933 \, \text{ms}
   \]

**Respuesta:** El email se transmitiría en aproximadamente 16 ms.

---

### Ejercicio 3: Transmisión del mismo email considerando 5 routers, cada uno con 1 ms de retardo

**Datos adicionales:**
- Cada router introduce un retraso de 1 ms.
- **Total de retraso de procesamiento:** \(5 \times 1 \, \text{ms} = 5 \, \text{ms}\).

**Cálculos:**

1. **Tiempo Total con Procesamiento:**
   \[
   T_{total} \approx T_t + T_p + \text{Retraso de Procesamiento} \approx 0.933 \, \text{ms} + 15 \, \text{ms} + 5 \, \text{ms} \approx 20.933 \, \text{ms}
   \]

**Respuesta:** Teniendo en cuenta los retardos en cada router, el tiempo total sería aproximadamente de 21 ms.

---

## Reflexión Final

Comprender y calcular estos retardos es fundamental para optimizar el rendimiento de las redes. Mientras que en las LANs la transmisión del paquete (debido a los altos anchos de banda y a las cortas distancias) es el factor dominante, en enlaces de larga distancia (como en Internet) el retraso de propagación y el de procesamiento se vuelven cruciales. Estas consideraciones justifican el uso de técnicas avanzadas como los **CDN**, que ayudan a minimizar la latencia trasladando el contenido a nodos más próximos al usuario final.

Además, entender estos conceptos permite analizar casos prácticos y diseñar estrategias de mejora en redes, lo que es vital en entornos donde la eficiencia y la rapidez de la comunicación son esenciales.

---

¿Te gustaría profundizar en la simulación de estos problemas con herramientas de red o explorar más sobre la administración de LAN versus WAN? ¡Hay un mundo de aplicaciones prácticas que podemos analizar!