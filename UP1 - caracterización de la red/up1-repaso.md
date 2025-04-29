# Tema 1: Caracterización de las Redes Locales - Repaso y Ejercicios Prácticos

## 1. Definición de Red de Área Local y Principales Características

**Red de Área Local (LAN):**  Una LAN es una red de comunicación que abarca un espacio geográfico reducido (por ejemplo, un edificio, una oficina, un hogar o un campus). Surgen por la necesidad de compartir recursos dentro de la organización. 

Se caracteriza por:

- **Alta velocidad:** Uso de tecnologías como Ethernet y Wi-Fi.
- **Baja latencia:** Las distancias cortas reducen significativamente el tiempo de propagación.
- **Administración centralizada:** Normalmente, la red es gestionada por la propia organización o el propietario local, lo cual facilita su mantenimiento, seguridad y control.

---

## 2. Clasificación de Redes según su Ámbito de Aplicación

La clasificación más común de las redes es en función de su ámbito de aplicación (extensión). Distinguimos:

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
    - **L1: Capa Física:** Transmisión de bits a través del medio físico.  
    - **L2: Capa de Enlace de Datos:** Control de errores, detección de colisiones, acceso al medio.  
    - **L3: Capa de Red:** Encaminamiento y direccionamiento.  
    - **L4: Capa de Transporte:** Segmentación, control de flujo y reensamblaje.  
    - **L5: Capa de Sesión:** Gestión de la conexión y sesiones entre aplicaciones.  
    - **L6: Capa de Presentación:** Formato, cifrado y compresión de datos.  
    - **L7: Capa de Aplicación:** Interfaz y servicios directos al usuario.

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

### 4.1 Transmisiones de Datos

En el estudio de la transmisión de datos en redes es fundamental comprender y poder calcular los distintos tipos de retardo o demora que afectan a la entrega de la información. Entre ellos destacan los siguientes.

#### 4.1.1 Tiempo de Transmisión

- **Definición:** Es el tiempo que se necesita para insertar todos los bits de un paquete en el medio de transmisión.
- **Fórmula:**

```math
T_t = \frac{L}{R}
```

Donde:

- $T_t$: Tiempo de transmisión (en segundos).  
- $L$: Longitud del paquete (en bits).  
- $R$: Tasa de transmisión (en bits por segundo).

**Ejemplo:** Si un paquete tiene 1500 bytes y la tasa de transmisión es de 
1 Gbps:

```math
T_t = \frac{1500 \times 8}{1 \times 10^9} = 0.000012 \, \text{segundos} \quad (\approx 12 \, \mu s)
 ```

**Interpretación:** Esto significa que se tardará aproximadamente 12 microsegundos en transmitir el paquete de 1,500 bytes a una velocidad de 1 Gbps. Esta componente del tiempo de entrega es la que podemos optimar mejorando la velocidad de transmisión del medio físico. Por ejemplo, al pasar de una red Fast Ethernet (100 Mbps) a una Gigabit Ethernet (1 Gbps), el tiempo de transmisión se reduce diez veces.

Sin embargo, como veremos no es la única componente del tiempo de entrega. En redes de área local (LAN), el tiempo de transmisión es el factor dominante debido a las altas velocidades de conexión y a las cortas distancias. En cambio, en redes de área amplia (WAN), como Internet, el tiempo de propagación y el tiempo de procesamiento son más relevantes.

#### 4.1.2 Retraso de Propagación

- **Definición:** Es el tiempo que tarda un bit en recorrer el medio físico desde el emisor hasta el receptor.

- **Fórmula:**
  
```math
T_p = \frac{d}{v}
```
  
Donde:
  
- $T_p$: Tiempo de propagación (en segundos).
- $d$: Distancia entre emisor y receptor (en metros).
- $v$: Velocidad de propagación en el medio (en metros por segundo).
  
>[!NOTE]
> En fibra óptica, la velocidad de propagación suele ser aproximadamente $2 \times 10^8$ m/s. En el cable de cobre se considera que, corriente eléctrica su propaga entre un 60-95% de la velocidad de la luz en el vacío. Por conveniencia podemos considerar $2 \times 10^8$ m/s (67%) para nuestros cálculos.

Estas consideraciones justifican el uso de técnicas avanzadas como los **CDN**, que ayudan a minimizar la latencia trasladando el contenido a nodos más próximos al usuario final.

#### 4.1.3 Retraso de Procesamiento

- **Definición:** $T_{proc}$. Se refiere al tiempo adicional que requieren los equipos intermedios (como routers y switches) para procesar y reenviar el paquete. Este retardo depende de la capacidad del equipo y de la carga de trabajo en el momento.

#### 4.1.4 Tiempo de Entrega del Paquete

- **Definición:** Es la suma de todos los retardos (transmisión, propagación y procesamiento) que un paquete experimenta al ir desde el origen hasta el destino. 

>[!NOTE] 
> En redes es bastante común usar el RTT (Round Trip Time) como alternativa al tiempo de entrega del paquete. Este es el tiempo que un paquete de datos tarda en viajar de un origen hasta un destino, ida y vuelta. Este tiempo será el doble del tiempo de entrega del paquete.

- **Fórmula General:**

```math
T_t = T_p + T_p + T_{proc}
```

> [!NOTE]  
> En una red LAN, el **tiempo de transmisión** suele ser el factor dominante debido a las cortas distancias y altas velocidades de conexión. Por otro lado, en redes de mayor alcance como el Internet, el **retraso de propagación** adquiere mayor relevancia. Esto ha impulsado el desarrollo de tecnologías como las **CDN (Content Delivery Networks)**, que consisten en redes distribuidas diseñadas para acercar el contenido al usuario final, reduciendo la latencia y mejorando la experiencia en la entrega de información.

---

## 5. Ejercicios Prácticos

### Ejercicio 1: Transmisión de un archivo .OVA de 5GB en una red Gigabit Ethernet

**Datos:**
- **Tamaño del archivo:** 5GB.  
  Se considerará 1GB = $ 2^{30} $ bytes, por lo tanto, 5GB = $ (5 \times 2^{30}) $ **bytes**.
- **Velocidad de la red:** 1 Gbps = $ (1 \times 10^9) bits/s $.
- **Suposiciones:** No se consideran los retardos de propagación ni de procesamiento.

**Cálculos:**

1. **Conversión de bytes a bits:**
   
   ```math
   5 \, \text{GB} = 5 \times 2^{30} \text{bytes} \times 8 = 40 \times 10^9 \, \text{bits}
   ```

2. **Tiempo de Transmisión:**

   ```math
   T_t = \frac{40 \times 10^9 \, \text{bits}}{1 \times 10^9 \, \text{bits/s}} = 40 \, \text{segundos}
   ```

**Respuesta:** El archivo se transmitirá en 40 segundos.

---

### Ejercicio 2: Transmisión de un email de 70kB por fibra DIGI de 600Mbps

**Datos:**
- **Tamaño del email:** 70 kB
  ```math
  \text{Transformamos a bytes: } 70 kB = (70 \times 2^{10}) \, bytes = 560 \, \text{kbits} \\
  \text {y de ahí a bits: } 70000 \times 8 = 560000 \text \, bits.
  ```
- **Velocidad de la red:** 600 Mbps = $(600 \times 10^6) $ bits/s.
- **Distancia entre origen y destino:** 3000 km = $(3 \times 10^6)$ m.
- **Velocidad de propagación:**  $(2 \times 10^8)$ m/s.
- **Suposiciones:** No se añade retraso de procesamiento extra.

**Cálculos:**

1. **Tiempo de Transmisión:**
   ```math
   T_t = \frac{560\,000 \, \text{bits}}{600 \times 10^6 \, \text{bits/s}} \approx 0.000933 \, \text{segundos} \quad (\approx 0.933 \, \text{ms})
   ```

2. **Retraso de Propagación:**

```math
T_p = \frac{3\,000\,000 \, \text{m}}{2 \times 10^8 \, \text{m/s}} = 0.015 \, \text{segundos} \quad (15 \, \text{ms})
```

3. **Tiempo Total Sin Procesamiento Adicional:**
  
```math
T_{total} \approx 0.933 \text{ms} + 15 \text{ms} \approx 15.933  \text{ms}
```

**Respuesta:** El email se transmitiría en aproximadamente 16 ms.

---

### Ejercicio 3: Transmisión del mismo email considerando 5 routers, cada uno con 1 ms de retardo

**Datos adicionales:**
- Cada router introduce un retraso de 1 ms.
- **Total de retraso de procesamiento:** 
$(5 \times 1 \text{ ms} = 5 \text{ ms})$

**Cálculos:**

1. **Tiempo Total con Procesamiento:**
```math
   T_{total} \approx T_t + T_p + \text{Retraso de Procesamiento} \approx 0.933 \, \text{ms} + 15 \, \text{ms} + 5 \, \text{ms} \approx 20.933 \, \text{ms}
```

**Respuesta:** Teniendo en cuenta los retardos en cada router, el tiempo total sería aproximadamente de 21 ms.

---

### 4.2 Sistemas de representación de la información

#### 4.2.1. Sistema Decimal

El que usamos habitualmente. Los números se descomponen como sumas de potencias base 10.

Así
```math
754 = 7 \times 10^2 + 5 \times 10^1 + 4 \times 10⁰ = 700 + 50 + 4
```

#### 4.2.2. Sistema Binario

Fundamental en sistemas de computadores. Los números se descomponen como sumas de potencia base 2.

Así
```math
1001 = 2^3 + 2^0 = 9 \text { en decimal}
```

En redes no es habitual trabajar con números binarios cuya representación decimal sea superior a 255 (1 octeto), por lo que sobre todo trabajaremos estos.


#### 4.2.3. Sistema Hexadecimal

El sistema hexadecimal nos ayuda a representar de manera más cómoda números que en decimal serían excesivamente largos, dado que 1 carácter hexadecimal (nibble) equivale a un grupo de 4 bits.



