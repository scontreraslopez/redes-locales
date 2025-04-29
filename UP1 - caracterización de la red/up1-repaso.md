# Tema 1: Caracterización de las Redes Locales - Repaso y Ejercicios Prácticos

## Índice

- [1. Definición de Red de Área Local y Principales Características](#1-definición-de-red-de-área-local-y-principales-características)
- [2. Clasificación de Redes según su Ámbito de Aplicación](#2-clasificación-de-redes-según-su-ámbito-de-aplicación)
- [3. Modelos de Referencia en Redes](#3-modelos-de-referencia-en-redes)
- [4. Problemas del Tema 1](#4-problemas-del-tema-1)
  - [4.1 Transmisiones de Datos](#41-transmisiones-de-datos)
    - [4.1.1 Tiempo de Transmisión](#411-tiempo-de-transmisión)
    - [4.1.2 Retraso de Propagación](#412-retraso-de-propagación)
    - [4.1.3 Retraso de Procesamiento](#413-retraso-de-procesamiento)
    - [4.1.4 Tiempo de Entrega del Paquete](#414-tiempo-de-entrega-del-paquete)
  - [4.2 Sistemas de representación de la información](#42-sistemas-de-representación-de-la-información)
    - [4.2.1 Sistema Decimal](#421-sistema-decimal)
    - [4.2.2 Sistema Binario](#422-sistema-binario)
    - [4.2.3 Sistema Hexadecimal](#423-sistema-hexadecimal)
- [5. Ejercicios Prácticos](#5-ejercicios-prácticos)
- [6. Ejercicios de Repaso Propuestos: Transmisiones de Datos y Sistemas de Representación](#6-ejercicios-de-repaso-propuestos-transmisiones-de-datos-y-sistemas-de-representación)


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

Gracias a esto, podemos usar un método simplificado para convertir de decimal a binario.

Podemos convertir un octeto binario a decimal de forma rápida usando restas, aprovechando que el número máximo de un octeto es 255 (es decir, en binario: 11111111). La idea es “partir” de 255 y, por cada bit que esté en 0, restar su valor correspondiente (la potencia de 2 que le toca). De esta manera, al omitir las posiciones activas (con 1) y “quitar” solo lo que falta, obtenemos la suma de los bits en 1.

##### Pasos a seguir (decimal a binario usando restas)

Vamos a explicar cómo convertir un número decimal a binario usando restas, aprovechando que en redes solemos trabajar con octetos (8 bits). La idea es iniciar con el número decimal y, a partir de la mayor potencia de 2 (para un octeto, la mayor es 128), restar sucesivamente las potencias de 2 cuando sean menores o iguales al número o al residuo que tengamos. Cada vez que podamos restar esa potencia, asignamos un 1 en la posición correspondiente; si no podemos restarla, colocamos 0.

Imagina que queremos convertir el número decimal **172** a binario (en un octeto). Vamos a usar las potencias de 2 correspondientes a cada bit:

- **Bit 7:** 128  
- **Bit 6:** 64  
- **Bit 5:** 32  
- **Bit 4:** 16  
- **Bit 3:** 8  
- **Bit 2:** 4  
- **Bit 1:** 2  
- **Bit 0:** 1  

Procederemos de la siguiente forma:

1. **Empiezas con 172 y la mayor potencia: 128**  
   - ¿172 es mayor o igual que 128? Sí.  
   - Asignamos 1 al Bit 7 y restamos 128.  
   - **Residuo:** 172 − 128 = 44.

2. **Siguiente potencia: 64 (Bit 6)**  
   - ¿44 es mayor o igual que 64? No.  
   - Asignamos 0 al Bit 6, sin restar ningún valor.  
   - **Residuo sigue siendo:** 44.

3. **Ahora la potencia: 32 (Bit 5)**  
   - ¿44 ≥ 32? Sí.  
   - Ponemos 1 en el Bit 5 y restamos 32.  
   - **Residuo:** 44 − 32 = 12.

4. **Siguiente: 16 (Bit 4)**  
   - ¿12 ≥ 16? No.  
   - Asignamos 0 en el Bit 4.  
   - **Residuo:** sigue siendo 12.

5. **Luego: 8 (Bit 3)**  
   - ¿12 es mayor o igual que 8? Sí.  
   - Ponemos 1 en el Bit 3 y restamos 8.  
   - **Residuo:** 12 − 8 = 4.

6. **La siguiente potencia: 4 (Bit 2)**  
   - ¿4 es mayor o igual que 4? Sí.  
   - Asignamos 1 en el Bit 2 y restamos 4.  
   - **Residuo:** 4 − 4 = 0.

7. **Ahora: 2 (Bit 1)**  
   - ¿0 es mayor o igual que 2? No.  
   - Ponemos 0 en el Bit 1.

8. **Finalmente: 1 (Bit 0)**  
   - ¿0 es mayor o igual que 1? No.  
   - Ponemos 0 en el Bit 0.

Resumiendo en una tabla:

| Bit (posición) | Valor (potencia de 2) | ¿Se resta?          | Resto   | Bit asignado |
|----------------|-----------------------|---------------------|---------|--------------|
| Bit 7          | 128                   | 172 ≥ 128 → Sí      | 172-128=44 | 1            |
| Bit 6          | 64                    | 44 < 64 → No        | 44      | 0            |
| Bit 5          | 32                    | 44 ≥ 32 → Sí        | 44-32=12 | 1            |
| Bit 4          | 16                    | 12 < 16 → No        | 12      | 0            |
| Bit 3          | 8                     | 12 ≥ 8 → Sí         | 12-8=4  | 1            |
| Bit 2          | 4                     | 4 ≥ 4 → Sí          | 4-4=0   | 1            |
| Bit 1          | 2                     | 0 < 2 → No          | 0       | 0            |
| Bit 0          | 1                     | 0 < 1 → No          | 0       | 0            |

Al final, la secuencia de bits (de Bit 7 a Bit 0) es: **1 0 1 0 1 1 0 0**, es decir, **10101100**.

###### ¿Por Qué Es Útil Este Método en Redes?

Cuando trabajas con direcciones IP o máscaras de red, habitualmente manejas números en formato de octetos. Este método te permite desglosar mentalmente el número decimal en sus componentes binarios de forma intuitiva, solo restando lo que falta para alcanzar el valor total del octeto.

#### 4.2.3. Sistema Hexadecimal

El sistema hexadecimal nos ayuda a representar de manera más compacta números que en decimal serían excesivamente largos, dado que 1 carácter hexadecimal (nibble) equivale a un grupo de 4 bits. Así 8 bits (un byte) se pueden representar con 2 caracteres hexadecimales. Por ejemplo, el número binario **10101100** se puede representar como **AC** en hexadecimal.

Para trabajar en redes resulta muy práctico convertir hexadecimal a decimal (y viceversa) usando el enfoque nibble a nibble. Esto significa convertir cada dígito hexadecimal en su equivalente en binario (4 bits) y luego deducir su valor decimal. Aquí te explico paso a paso para ambos procesos:

##### Conversión de Hexadecimal a Decimal

**Concepto básico:**  
Cada dígito hexadecimal equivale a un nibble (4 bits). Por ejemplo, el dígito hexadecimal "A" equivale al binario `1010` y su valor decimal es 10. Al convertir un número hexadecimal mayor (generalmente un byte, compuesto por dos nibbles) se sigue este método:

**Pasos:**

1. **Divide el número en nibbles:**  
   Por ejemplo, para convertir el byte hexadecimal **AC**, separa en dos dígitos:  
   - Primer nibble: `A`  
   - Segundo nibble: `C`

2. **Convierte cada dígito a binario:**  
   Utiliza la siguiente tabla para cada nibble:

   | Hexadecimal | Binario | Decimal |
   |-------------|---------|---------|
   | 0           | 0000    | 0       |
   | 1           | 0001    | 1       |
   | 2           | 0010    | 2       |
   | 3           | 0011    | 3       |
   | 4           | 0100    | 4       |
   | 5           | 0101    | 5       |
   | 6           | 0110    | 6       |
   | 7           | 0111    | 7       |
   | 8           | 1000    | 8       |
   | 9           | 1001    | 9       |
   | A           | 1010    | 10      |
   | B           | 1011    | 11      |
   | C           | 1100    | 12      |
   | D           | 1101    | 13      |
   | E           | 1110    | 14      |
   | F           | 1111    | 15      |

   Así, para nuestro ejemplo:  
   - `A` → 1010 (valor 10)  
   - `C` → 1100 (valor 12)

3. **Concatena los valores binarios:**  

Juntando los dos nibbles, obtenemos el binario completo: `10101100`, que ya podemos traducir de binario a decimal por el método general.    Esto equivale a 172 en decimal.

Por lo tanto, el hexadecimal **AC** equivale al decimal **172**.

---

##### Conversión de Decimal a Hexadecimal

**Concepto básico:**

Para convertir un número decimal a hexadecimal, se puede proceder a convertir el decimal a binario (en forma de octeto) y luego agrupar los bits en nibbles. Otra vía (más directa y equivalente) es dividir el número decimal en partes correspondientes a la división entera y el residuo con 16 pero nos centraremos en el primer método que es más intuitivo.

**Método usando nibbles:**

1. **Convierte el número decimal a binario (dentro de un byte, si se trabaja en redes):**

  Por ejemplo, para el decimal **111**, se obtiene el octeto binario `01101111`. Nótese la importancia de hacer padding (rellenar con 0s) a la izquierda para tener el octeto entero siempre.

2. **Separa el octeto en dos nibbles:**  
   - Primer nibble (bits más significativos): `0110`  
   - Segundo nibble (bits menos significativos): `1111`

3. **Convierte cada nibble a su valor hexadecimal usando la tabla anterior:**  
   - `0110` → 6 → **6**  
   - `1111` → 15 → **F**

   Así, el número decimal **111** se representa como **6F** en hexadecimal.

**Método directo (división por 16):**

1. Divide el número decimal entre 16:  
   - 111 ÷ 16 = 6 (cociente) con residuo 15.
2. El cociente 6 se convierte a hexadecimal → **6**  
   El residuo 15 se convierte a hexadecimal → **F**.
3. Junta ambos resultados: **6F**

---

En redes, especialmente cuando se trabaja con IPv6 o con configuraciones de hardware que exigen manipulación de direcciones en distintos sistemas numéricos, este método nibble a nibble es muy efectivo. La correspondencia directa entre un dígito hexadecimal y 4 bits facilita la conversión y minimiza errores al interpretar direcciones, máscaras de subred o identificadores de hardware.

## 5. Ejercicios Prácticos

### Ejercicio 1: Transmisión de un archivo .OVA de 5GB en una red Gigabit Ethernet

**Datos:**

- **Tamaño del archivo:** 5GB.  
  1GB = $ 2^{30} $ bytes, por lo tanto, 5GB = $ (5 \times 2^{30}) $ **bytes**.
- **Velocidad de la red:** 1 Gbps = $ (1 \times 10^9) \, bits/s $.
- **Suposiciones:** No se consideran los retardos de propagación ni de procesamiento.

**Cálculos:**

1. **Conversión de bytes a bits:**

```math
5 \, \text{GB} = 5 \times 2^{30} \text{bytes} \times 8 = 42949672960 \approx \, 4,295 \times 10^{10}\text{bits}
```

2. **Tiempo de Transmisión:**

   ```math
   T_t = \frac{4,295 \times 10^{10}\text{bits}}{1 \times 10^9 \, \text{bits/s}} = 42,95 \, \text{segundos}
   ```

**Respuesta:** El archivo se transmitirá en aproximadamente 43 segundos.

---

### Ejercicio 2: Transmisión de un email de 70kB por fibra DIGI de 600Mbps a 3000 km de distancia

**Datos:**

- **Tamaño del email:** 70 kB

  ```math
  \text{Transformamos a bytes: } 70 kB = (70 \times 2^{10}) \, bytes = 71680 \, \text{bytes} \\
  \text {y de ahí a bits: } 71680 \times 8 = 573440 \text \, bits.
  ```

- **Velocidad de la red:** 600 Mbps = $(600 \times 10^6) $ bits/s.
- **Distancia entre origen y destino:** 3000 km = $(3 \times 10^6)$ m.
- **Velocidad de propagación:**  $(2 \times 10^8)$ m/s.
- **Suposiciones:** No se añade retraso de procesamiento extra.

**Cálculos:**

1. **Tiempo de Transmisión:**

   ```math
   T_t = \frac{573440 \, \text{bits}}{600 \times 10^6 \, \text{bits/s}} \approx 0.000956 \, \text{segundos} \quad ( 0.956 \, \text{ms})
   ```

2. **Retraso de Propagación:**

  ```math
   T_p = \frac{3\,000\,000 \, \text{m}}{2 \times 10^8 \, \text{m/s}} = 0.015 \, \text{segundos} \quad (15 \, \text{ms})
  ```

3. **Tiempo Total Sin Procesamiento Adicional:**

  ```math
   T_{total} \approx 0.956 \text{ms} + 15 \text{ms} \approx 15.956  \text{ms}
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
   T_{total} = T_t + T_p + T_{proc} \approx 0.933 \, \text{ms} + 15 \, \text{ms} + 5 \, \text{ms} \approx 20.933 \, \text{ms}
```

**Respuesta:** Teniendo en cuenta los retardos en cada router, el tiempo total sería aproximadamente de 21 ms.

---

## 6. Ejercicios de Repaso Propuestos: Transmisiones de Datos y Sistemas de Representación**

**Instrucciones:** Resuelve los siguientes ejercicios aplicando las fórmulas y métodos explicados en el Tema 1. Presta atención a las unidades y realiza las conversiones necesarias. Usa la velocidad de propagación $v = 2 \times 10^8$ m/s cuando sea necesario.

**Bloque 1: Transmisiones de Datos**

1.  **Tiempo de Transmisión (Foto HD):** Calcula el tiempo de transmisión ($T_t$) necesario para enviar una fotografía de 8 Megabytes (MB) a través de una conexión de red con una tasa de transmisión (R) de 100 Mbps.
    *   *Recuerda:* 1 MB = $2^{20}$ bytes, 1 byte = 8 bits, 1 Mbps = $10^6$ bits/s.

2.  **Retraso de Propagación (Fibra Ciudad):** Calcula el retraso de propagación ($T_p$) para un bit que viaja a través de un cable de fibra óptica de 50 km de longitud entre dos puntos de una ciudad.

3.  **Tiempo de Entrega (Paquete Pequeño WAN):** Se envía un paquete de 500 bytes a través de un enlace WAN de 2000 km con una velocidad de transmisión de 2 Mbps. Asumiendo que no hay retraso de procesamiento, ¿cuál es el tiempo total de entrega del paquete?
    *   Calcula $T_t$ y $T_p$ y súmalos.

4.  **Tiempo de Entrega con Procesamiento (Similar al anterior):** Considera el mismo escenario del ejercicio 3 (paquete de 500 bytes, enlace de 2000 km a 2 Mbps), pero ahora el paquete debe atravesar 4 routers, y cada router introduce un retraso de procesamiento ($T_{proc}$) de 0.5 milisegundos (ms). Calcula el nuevo tiempo total de entrega.
    *   *Recuerda:* 1 ms = 0.001 segundos.

5.  **Comparativa de Tecnologías (Mismo Archivo):** Tienes un archivo de 20 MB. ¿Cuánto tiempo de transmisión ($T_t$) tardaría en enviarse por:
    *   a) Una conexión ADSL de 20 Mbps?
    *   b) Una conexión Gigabit Ethernet (1 Gbps)?
    *   Compara los resultados. ¿Qué tecnología es significativamente más rápida para la transmisión pura?

6.  **RTT Básico (Ping LAN):** Envías un paquete de ping (considera 64 bytes de tamaño) a un servidor en tu misma red local (LAN), situado a 100 metros de distancia a través de un cable Ethernet a 1 Gbps. Ignorando el tiempo de procesamiento, ¿cuál sería el RTT (Round Trip Time) esperado?
    *   Calcula el tiempo de entrega de ida ($T_t + T_p$) y multiplícalo por 2.

**Bloque 2: Sistemas de Representación**

7.  **Decimal a Binario (Octetos):** Convierte los siguientes números decimales a su representación binaria de 8 bits (octeto), usando el método de restas sucesivas si te ayuda:
    *   a) 145
    *   b) 68
    *   c) 250
    *   d) 15

8.  **Binario a Decimal (Octetos):** Convierte los siguientes octetos binarios a su valor decimal:
    *   a) `11010010`
    *   b) `01011100`
    *   c) `10001111`
    *   d) `00101010`

9.  **Hexadecimal a Binario y Decimal:** Convierte los siguientes valores hexadecimales (representando un byte cada uno) a su equivalente binario de 8 bits y a su valor decimal:
    *   a) `B7`
    *   b) `2E`
    *   c) `F1`
    *   d) `88`
    *   *Pista:* Usa el método nibble a nibble (cada dígito hex son 4 bits).

10. **Decimal a Hexadecimal:** Convierte los siguientes números decimales a su representación hexadecimal de 2 dígitos:
    *   a) 199
    *   b) 85
    *   c) 23
    *   d) 172 (¡Comprueba si coincide con el ejemplo del texto!)
    *   *Pista:* Puedes pasar primero a binario (octeto) y luego agrupar en nibbles, o usar la división por 16.

11. **Aplicación en Redes (Máscara):** Una máscara de subred común es `255.255.255.0`. Convierte el número `255` a binario (octeto) y a hexadecimal. ¿Qué patrón observas en la representación binaria de 255?

12. **Aplicación en Redes (Dirección IP):** Un componente de una dirección IPv4 es `11000000` en binario. ¿Cuál es su valor decimal y hexadecimal? (Este es el primer octeto de una dirección IP Clase C muy común).

---
