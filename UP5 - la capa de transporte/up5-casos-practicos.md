## **Título de la Práctica:** Análisis de Protocolos Inseguros con Wireshark: Telnet vs. Protocolos Seguros

## Introducción

Dado que ya hemos estudiado cómo funcionan las sesiones TCP, en esta práctica vamos a profundizar en cómo se comunican dos equipos y, de paso, explorar la importancia de utilizar **protocolos seguros** en nuestras comunicaciones.

En la arquitectura de las redes de comunicación, la seguridad es un aspecto fundamental que debe ser considerado en cada capa del modelo OSI (Open Systems Interconnection). Aunque la capa de transporte es responsable de gestionar la entrega de datos de extremo a extremo y garantizar que estos lleguen correctamente a su destino mediante protocolos como **TCP (Transmission Control Protocol)** y **UDP (User Datagram Protocol)**, estos protocolos por sí solos no proporcionan mecanismos de seguridad.

Es aquí donde entran en juego los protocolos seguros como **HTTPS**, **SSH** y **sFTP**, que añaden capas adicionales de cifrado y autenticación para proteger la información. Por el contrario, sus alternativas inseguras como **HTTP**, **Telnet** y **FTP** transmiten datos en **texto plano**, lo que puede ser fácilmente interceptado y leído por terceros no autorizados.

En esta práctica, utilizaremos **Wireshark** para analizar el tráfico de red y visualizar cómo la información transmitida mediante protocolos inseguros puede ser capturada y comprendida sin dificultad. A través del análisis de capturas de tráfico, los estudiantes podrán ver de primera mano los riesgos asociados con el uso de protocolos no seguros y comprenderán la necesidad de adoptar prácticas de seguridad adecuadas en entornos de red.

Espero que esta introducción refleje adecuadamente tus intenciones y ayude a tus alumnos a entender la importancia de los protocolos seguros. Si necesitas ajustar algo más o añadir información adicional, ¡no dudes en decírmelo!

### **Objetivos:**

- Comprender cómo los protocolos inseguros transmiten información sensible en texto plano.
- Aprender a utilizar Wireshark para captar y analizar tráfico de red.
- Destacar la importancia de usar protocolos seguros en entornos de red.

### **Materiales Necesarios:**

- Computadora con Wireshark instalado.
- Archivo de captura **ch2.pcap** que contiene tráfico de autenticación Telnet.
- Conexión a Internet para consultar documentación si es necesario.

### **Procedimiento:**

#### **1. Introducción al Uso de Wireshark y TCP Stream**

- **Breve explicación de Wireshark:**
  - Es una herramienta de análisis de protocolos de red que permite capturar y examinar paquetes a nivel detallado.
- **Concepto de TCP Stream:**
  - Un flujo TCP agrupa todos los paquetes que pertenecen a una misma sesión de comunicación entre dos puntos.

#### **2. Apertura del Archivo de Captura**

- Abre Wireshark.
- Ve a **"File" > "Open"** y selecciona el archivo **ch2.pcap**.
- Observa que aparecen múltiples paquetes capturados en la interfaz.

#### **3. Filtrado del Tráfico Telnet**

- En la barra de filtro, escribe **`telnet`** y presiona **Enter**.
- Wireshark ahora muestra únicamente los paquetes relacionados con Telnet.

#### **4. Análisis del Flujo TCP**

- Selecciona cualquiera de los paquetes mostrados.
- Haz clic derecho sobre el paquete y selecciona **"Follow" > "TCP Stream"**.
- Se abrirá una nueva ventana que muestra la comunicación entre el cliente y el servidor Telnet.

#### **5. Identificación de Usuario y Contraseña**

- Observa la ventana del flujo TCP.
- Notarás que el texto está en **texto plano**, lo que significa que es legible y no está encriptado.
- Busca las partes donde se ingresan las credenciales:
  - El usuario suele enviarse después de una cadena como **"login:"**.
  - La contraseña sigue después de **"Password:"**.
- **Ejemplo:**

  ```
  login: usuario123
  Password: contraseñasegura
  ```

- Anota el nombre de usuario y la contraseña que encuentres.

#### **6. Discusión Sobre los Riesgos**

- Analiza con tus alumnos cómo cualquier persona con acceso a la red puede capturar este tipo de paquetes y obtener información sensible.
- Destaca que protocolos como Telnet no cifran los datos transmitidos.
- Muestra cómo protocolos seguros como **SSH** ofrecen encriptación, protegiendo la información de posibles interceptores.

#### **7. Comparación con Protocolos Seguros**

- Si es posible, muestra una captura de tráfico SSH.
- Repite los pasos anteriores y observa que, al seguir el flujo TCP, los datos aparecen en formato ilegible o encriptado.
- **Ejemplo de datos encriptados:**

  ```
  ̧��x#��K�+�/E�V���C��=C�
  ```

#### **8. Conclusiones**

- Reflexiona sobre la importancia de utilizar protocolos seguros en entornos donde se maneja información sensible.
- Fomenta la adopción de buenas prácticas en seguridad de la información.
- Invita a los alumnos a pensar en otras situaciones donde puedan aplicarse estos conocimientos.

### **Puntos Adicionales para Profundizar:**

- **Experimentar con FTP vs. SFTP:**
  - Realizar un análisis similar comparando FTP (inseguro) con SFTP (seguro).
- **Explorar Otros Protocolos Inseguros:**
  - Como **HTTP** frente a **HTTPS** y analizar las diferencias en la transmisión de datos.
- **Configurar un Pequeño Laboratorio:**
  - Montar sesiones de Telnet y SSH en un entorno controlado para capturar el tráfico en tiempo real.

TODO: **Práctica de PT**: https://examenredes.com/14-8-1-packet-tracer-comunicaciones-de-tcp-y-udp-respuestas/ 
Link: Podemos usar <http://poc.aquilasoftware.com/poclite/resources/cms/cms.html#/login> para hacer la práctica de TCP stream.
