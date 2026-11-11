# Computer Networks

## Índice

- [Resumen Ejecutivo](#resumen-ejecutivo)
- [Mapa Conceptual de las Capas de Abstracción](#mapa-conceptual-de-las-capas-de-abstracción)
- [Capítulo 1: Introducción](#capítulo-1-introducción)
- [Capítulo 2: The Physical Layer](#capítulo-2-the-physical-layer)
- [Capítulo 3: The Data Link Layer](#capítulo-3-the-data-link-layer)
- [Capítulo 4: The Medium Access Control Sublayer](#capítulo-4-the-medium-access-control-sublayer)
- [Capítulo 5: The Network Layer](#capítulo-5-the-network-layer)
- [Capítulo 6: The Transport Layer](#capítulo-6-the-transport-layer)
- [Capítulo 7: The Application Layer](#capítulo-7-the-application-layer)
- [Capítulo 8: Network Security](#capítulo-8-network-security)
- [Capítulo 9: Reading List and Bibliography](#capítulo-9-reading-list-and-bibliography)

## Resumen Ejecutivo

El diseño de las redes de computadoras modernas responde a la transición paradigmática desde los antiguos centros de cómputo centralizados hacia sistemas distribuidos e interconectados compuestos por computadoras autónomas. Mientras que un sistema distribuido se presenta ante el usuario como un sistema único y coherente mediante capas de *middleware*, una red de computadoras mantiene explícita la autonomía e interconexión de sus nodos mediante tecnologías de comunicación heterogéneas.

Para gestionar la complejidad inherente a la transferencia confiable de información entre sistemas independientes, la arquitectura de red se organiza en una jerarquía de capas o niveles de abstracción. Cada capa actúa como una máquina virtual que ofrece servicios bien definidos a la capa superior a través de interfaces estandarizadas, ocultando los detalles internos de implementación y los algoritmos empleados. Se establece así una distinción fundamental entre el **servicio** (las operaciones semánticas disponibles en la interfaz entre capas) y el **protocolo** (las reglas y convenciones que rigen el intercambio de mensajes entre entidades par en máquinas distintas).

A nivel metodológico, la obra adopta un **modelo de referencia híbrido de 5 capas** que sintetiza el rigor teórico del modelo de 7 capas OSI (*Open Systems Interconnection*) y la aplicabilidad práctica del modelo de 4 capas TCP/IP. A través de esta estructura, se abordan los problemas transversales del diseño de redes: direccionamiento e identificación de procesos, multiplexación de canales, control de errores y de flujo, algoritmos de enrutamiento y control de congestión en la subred, garantías de calidad de servicio (QoS), y los mecanismos de seguridad criptográfica distribuidos verticalmente en la pila.

---

## Mapa Conceptual de las Capas de Abstracción

El siguiente esquema representa la arquitectura de la pila de protocolos de 5 capas utilizada como hilo conductor de la obra, detallando la unidad de datos (*PDU*), la función principal y los protocolos esenciales de cada nivel:

```text
=================================================================================
 CAPA DE APLICACIÓN (Application Layer)
 PDU: Mensaje / Datos de Aplicación
 Función: Interfaz directa con procesos de usuario y servicios de red.
 Protocolos: HTTP, DNS, SMTP, POP3, IMAP, RTP, SIP
=================================================================================
        | (Interfaz de Servicio de Transporte - Sockets / Puertos)
        v
=================================================================================
 CAPA DE TRANSPORTE (Transport Layer)
 PDU: Segmento / TPDU (Transport Protocol Data Unit)
 Función: Comunicación lógica proceso a proceso extremo a extremo y control de flujo.
 Protocolos: TCP (orientado a conexión, confiable), UDP (sin conexión)
=================================================================================
        | (Interfaz de Servicio de Red - IP Addresses)
        v
=================================================================================
 CAPA DE RED (Network Layer)
 PDU: Paquete / Datagrama IP
 Función: Enrutamiento salto a salto, interconexión de redes y control de congestión.
 Protocolos: IP (IPv4, IPv6), ICMP, ARP, OSPF, BGP
=================================================================================
        | (Interfaz de Servicio de Enlace)
        v
=================================================================================
 CAPA DE ENLACE DE DATOS (Data Link Layer)
 PDU: Trama (Frame)
 Función: Transferencia de tramas sin errores locales y control de acceso al medio (MAC).
 Protocolos/Estándares: Ethernet (802.3), Wi-Fi (802.11), PPP, HDLC
=================================================================================
        | (Interfaz con el Medio Físico)
        v
=================================================================================
 CAPA FÍSICA (Physical Layer)
 PDU: Flujo puro de bits
 Función: Transmisión de señales eléctricas, ópticas o electromagnéticas sobre el medio.
 Medios/Tecnologías: Par trenzado, Fibra óptica, Coaxial, Radiofrecuencia, DMT/ADSL
=================================================================================
```

### Desglose Estructural por Capas

#### 1. Capa de Aplicación (Capa 5)
* **PDU**: Mensaje.
* **Alcance**: Extremo a extremo (*End-to-End*).
* **Propósito**: Aloja los protocolos de alto nivel directamente requeridos por las aplicaciones de usuario para la transferencia de documentos, correo, resolución de nombres y multimedia en tiempo real.
* **Conceptos Fundamentales**: Base de datos jerárquica y distribuida en DNS; transferencias sin estado basadas en texto en HTTP; sesiones multimedia sobre RTP y SIP.

#### 2. Capa de Transporte (Capa 4)
* **PDU**: Segmento o TPDU (*Transport Protocol Data Unit*).
* **Alcance**: Extremo a extremo (*End-to-End*) entre procesos (*Socket to Socket*).
* **Propósito**: Aislar a las capas superiores de las imperfecciones y cambios tecnológicos de la subred de comunicación, proporcionando un canal transparente y seguro.
* **Conceptos Fundamentales**: Multiplexación mediante puertos (*TSAPs*); establecimiento de conexión mediante *Three-Way Handshake*; control de flujo adaptativo y control de congestión (*Slow Start*, *Congestion Avoidance*).

#### 3. Capa de Red (Capa 3)
* **PDU**: Paquete o Datagrama.
* **Alcance**: Salto a salto a través de la subred de routers (*Host-to-Router / Router-to-Router*).
* **Propósito**: Transportar paquetes desde la fuente hasta el destino final atravesando múltiples routers y redes heterogéneas.
* **Conceptos Fundamentales**: Conmutación de datagramas frente a circuitos virtuales; algoritmos de enrutamiento por Vector de Distancia y Estado de Enlace (*Dijkstra*); direccionamiento jerárquico (*CIDR*); tunelización y fragmentación.

#### 4. Capa de Enlace de Datos (Capa 2)
* **PDU**: Trama (*Frame*).
* **Alcance**: Local entre nodos adyacentes conectados por un canal físico o compartido.
* **Propósito**: Transformar un medio de transmisión físico no confiable en una línea de comunicación libre de errores detectados para la capa de red.
* **Conceptos Fundamentales**: Delimitación de tramas (*framing* y *bit/byte stuffing*); detección de errores mediante comprobación de redundancia cíclica (*CRC*); protocolos de ventana deslizante (*Stop-and-Wait*, *Go-Back-N*, *Selective Repeat*); arbitraje de acceso al medio compartido en la subcapa MAC (*CSMA/CD*, *CSMA/CA*).

#### 5. Capa Física (Capa 1)
* **PDU**: Flujo continuo de bits puros.
* **Alcance**: Punto a punto a través del medio de transmisión físico.
* **Propósito**: Transmitir bits individuales a través del canal de comunicación asegurando la fidelidad de los niveles eléctricos, ópticos o radioeléctricos.
* **Conceptos Fundamentales**: Ancho de banda y límites teóricos de capacidad (*Teorema de Nyquist* para canales sin ruido y *Teorema de Shannon* para canales ruidosos); medios guiados (par trenzado, coaxial, fibra óptica) e inalámbricos; técnicas de modulación y multiplexación (*FDM*, *TDM*, *WDM*, *CDMA*).

---

## Capítulo 1: Introducción

### Idea Central
Una red de computadoras se define formalmente como una colección de computadoras autónomas interconectadas mediante una única tecnología que les permite intercambiar información y compartir recursos. La evolución tecnológica desplazó el antiguo modelo de centros de cómputo centralizados hacia sistemas distribuidos y arquitecturas cliente-servidor estructuradas mediante jerarquías de protocolos en capas.

### Conceptos Clave
* **Computer Network (Red de computadoras)**: Conjunto de sistemas de cómputo autónomos interconectados por un medio físico o inalámbrico capaz de transferir datos.
* **Client-Server Model (Modelo Cliente-Servidor)**: Arquitectura donde los datos y servicios residen en máquinas de alto rendimiento (*servers*), a las cuales acceden máquinas de usuario (*clients*) para ejecutar tareas.
* **Broadcast vs. Point-to-Point Links**: Clasificación según tecnología de transmisión; los enlaces de difusión comparten un único canal de comunicación entre todas las máquinas, mientras que los enlaces punto a punto conectan pares individuales de nodos.
* **Network Scale (Escala de red)**: Clasificación por dimensión geográfica: PAN (*Personal Area Network*), LAN (*Local Area Network*), MAN (*Metropolitan Area Network*), WAN (*Wide Area Network*) e Internetwork.
* **Protocol Stack (Pila de protocolos)**: Estructura jerárquica de capas donde cada nivel ofrece servicios abstractos a la capa superior mediante interfaces, ocultando los detalles de implementación interna.
* **OSI vs. TCP/IP Reference Models**: El modelo OSI define 7 capas conceptuales (Física, Enlace, Red, Transporte, Sesión, Presentación, Aplicación) para la estandarización, mientras que TCP/IP implementa 4 capas prácticas (Host-to-Network, Internet, Transport, Application) centradas en la interconexión de redes heterogéneas.

### Mecanismos y Procesos
* **Encapsulación y Comunicación Virtual entre Entidades Par (Peers)**: Cada capa $n$ en la máquina emisora agrega información de control (cabecera/tráiler) a los datos recibidos de la capa $n+1$ y los transmite a la capa $n-1$. En el receptor, cada capa remueve su cabecera correspondiente, entregando la carga útil a la capa superior; las entidades de la misma capa se comunican de forma lógica a través del protocolo de capa $n$.
* **Conmutación de Paquetes en la Subred (Subnet)**: En redes de área amplia, los hosts se conectan a una subred de comunicación compuesta por líneas de transmisión y routers. La subred encamina paquetes discretos de un router a otro mediante algoritmos de enrutamiento hasta llegar al destino.
* **Servicios Orientados a Conexión vs. Sin Conexión**: Los servicios orientados a conexión (*connection-oriented*) requieren tres fases: establecimiento de la conexión, transferencia ordenada de datos y liberación de la conexión. Los servicios sin conexión (*connectionless*) envían cada paquete (datagrama) de forma independiente con dirección de destino completa, sin garantía preestablecida de orden o entrega.

### Ejemplos e Ilustraciones
* **Analogía Telefónica vs. Postal**: El servicio orientado a conexión equivale al sistema telefónico (marcar, establecer circuito, hablar secuencialmente y colgar); el servicio no orientado a conexión se asemeja al correo postal (cada carta viaja de forma independiente y puede llegar por rutas distintas).
* **El perro San Bernardo (St. Bernard)**: Caso hipotético ideado para ilustrar la relación entre ancho de banda y latencia; un perro entrenado que transporta cintas magnéticas de alta densidad posee una tasa de transferencia de datos gigantesca (ancho de banda), pero con un tiempo de propagación (latencia) de horas.
* **Protocolo Multicapa Corporativo**: Analogía donde directores, abogados e ingenieros de dos empresas negocian a través de sus equivalentes jerárquicos (peers), utilizando reglas de comunicación internas entre niveles inmediatos.

### Conexión Lógica y Relevancia
El Capítulo 1 establece la taxonomía fundamental, los límites conceptuales del área de conocimiento y la justificación del diseño en capas (adoptando un modelo híbrido de 5 capas: Física, Enlace, Red, Transporte y Aplicación). Este diseño modular sustenta el desglose estructurado del resto de la obra desde el nivel físico hasta el nivel de aplicación.

---

## Capítulo 2: The Physical Layer

### Idea Central
La capa física define las especificaciones mecánicas, eléctricas, funcionales y de temporización para la transmisión de flujos de bits puros sobre un medio físico. Su capacidad de transferencia está strictly delimitada por las leyes teóricas del electromagnetismo y la relación entre ancho de banda, ruido y distorsión de la señal.

### Conceptos Clave
* **Bandwidth (Ancho de banda)**: Rango de frecuencias que un medio de transmisión puede pasar sin atenuarse severamente, medido en Hertz (Hz); determina la capacidad de transporte del canal.
* **Nyquist's Theorem (Teorema de Nyquist)**: Establece que para un canal sin ruido de ancho de banda $B$, la tasa máxima de datos es $2B \log_2 V$ bits/seg, donde $V$ es el número de niveles discretos de la señal.
* **Shannon's Capacity Limit (Teorema de Shannon)**: Determina la tasa máxima teórica de un canal ruidoso con ancho de banda $B$ y relación señal/ruido $S/N$: $\text{Capacidad} = B \log_2 (1 + S/N)$ bps.
* **Guided vs. Unguided Media**: Medios guiados (*twisted pair*, cable coaxial, fibra óptica) dirigen las ondas electromagnéticas a lo largo de un camino físico; los medios no guiados (*radio*, microondas, infrarrojo, láser) transmiten ondas por el espacio libre.
* **Multiplexing (Multiplexación)**: Técnicas para combinar múltiples señales en un único medio: FDM (*Frequency Division Multiplexing*), TDM (*Time Division Multiplexing*) y WDM/DWDM (*Wavelength Division Multiplexing* en fibra óptica).
* **Modulación Digital (QPSK, QAM)**: Métodos para codificar datos digitales alterando la amplitud, frecuencia o fase de una onda portadora analógica; representados geométricamente mediante diagramas de constelación.

### Mecanismos y Procesos
* **Análisis de Fourier de Señales**: Toda señal periódica se reconstruye mediante una suma infinita de senos y cosenos; al transmitir una onda cuadrada digital por un canal de ancho de banda limitado, las armónicas de alta frecuencia se atenúan, distorsionando los pulsos y generando interferencia entre símbolos.
* **Transmisión por Fibra Óptica**: Modula pulsos de luz generados por diodos LED o láseres a través de un núcleo de vidrio ultra puro por reflexión interna total; los fotorreceptores convierten los fotones en pulsos eléctricos en el extremo receptor.
* **Operación de ADSL sobre Par Trenzado**: ADSL emplea modulación DMT (*Discrete MultiTone*), dividiendo el ancho de banda del bucle local de 1.1 MHz en 256 subcanales independientes de 4.3125 kHz para separar el tráfico telefónico tradicional (POTS), el flujo de subida (*upstream*) y el flujo de bajada (*downstream*).
* **Acceso Múltiple por División de Código (CDMA)**: Permite que múltiples emisores compartan simultáneamente la misma frecuencia asignando a cada estación una secuencia de chips ortogonal; el receptor realiza el producto escalar del vector recibido con el chip de la estación deseada para aislar la señal del ruido.

### Ejemplos e Ilustraciones
* **Paul Revere y la Comunicación Óptica**: Ejemplo histórico de transmisión óptica no guiada binaria utilizando faroles desde la iglesia Old North para enviar mensajes en código.
* **La analogía del idioma en CDMA**: CDMA equivale a varias parejas hablando simultáneamente en una misma habitación en diferentes idiomas; un oyente que habla francés puede concentrarse en la voz en francés e ignorar las demás transmisiones como ruido de fondo.
* **HFC (Hybrid Fiber Coax) en Televisión por Cable**: Redes de cable que combinan un backbone de fibra óptica con distribución final en cable coaxial compartido por vecindarios para ofrecer acceso a Internet a alta velocidad.

### Conexión Lógica y Relevancia
La capa física proporciona la base sobre la cual se transportan los bits raw entre sistemas. Dado que los canales físicos reales introducen distorsiones, atenuación y errores impredecibles, la capa física no ofrece garantías de entrega correcta, lo que obliga a crear la Capa de Enlace de Datos para detectar y corregir las fallas de transmisión.

---

## Capítulo 3: The Data Link Layer

### Idea Central
La capa de enlace de datos transforma una instalación de transmisión no confiable provista por la capa física en un enlace transparente, estructurado en tramas y libre de errores para la capa de red. Sus funciones principales incluyen el delimitado de tramas (*framing*), el control de errores (*error control*) y la gestión del flujo (*flow control*).

### Conceptos Clave
* **Framing (Enmarcado o Delimitación de Tramas)**: Proceso de fragmentar el flujo continuo de bits de la capa física en bloques discretos llamados tramas (*frames*), agregando cabeceras y tráileres de control.
* **Byte Stuffing / Bit Stuffing**: Mecanismos de transparencia de datos; *byte stuffing* inserta bytes de escape (`ESC`) antes de bytes de control aleatorios en la carga útil; *bit stuffing* inserta un bit `0` tras cinco unos consecutivos (`11111`) para evitar falsas coincidencias con la bandera de delimitación `01111110`.
* **Error-Correcting vs. Error-Detecting Codes**: Los códigos de corrección (como los códigos Hamming) añaden suficiente redundancia para reconstruir los datos originales en canales muy ruidosos (*Forward Error Correction*); los códigos de detección (como CRC) añaden poca redundancia para verificar la integridad y solicitar retransmisión en canales de bajo error.
* **Sliding Window Protocols (Protocolos de Ventana Deslizante)**: Algoritmos de control de flujo y error donde el emisor y el receptor mantienen rangos limitados de números de secuencia válidos para transmitir y recibir tramas en paralelo.
* **Piggybacking**: Técnica de acoplar temporalmente una confirmación de recepción (*ACK*) en el campo de control de una trama de datos saliente hacia la dirección opuesta.
* **Go-Back-N vs. Selective Repeat**: Go-Back-N descarta todas las tramas posteriores a una trama dañada y obliga a retransmitir desde el fallo (ventana del receptor de tamaño 1); Selective Repeat almacena en búfer las tramas correctas fuera de orden y solo solicita la retransmisión de la trama dañada (ventana del receptor mayor a 1).

### Mecanismos y Procesos
* **Algoritmo de Comprobación de Redundancia Cíclica (CRC)**: El emisor trata el mensaje como un polinomio de bits $M(x)$ y lo divide (usando aritmética módulo 2 con operaciones XOR) entre un polinomio generador $G(x)$; el residuo obtenido se añade como tráiler. El receptor divide la trama completa entre $G(x)$; un residuo distinto de cero indica un error de transmisión.
* **Protocolo PAR (Positive Acknowledgement with Retransmission / Stop-and-Wait)**: El emisor transmite una trama con un número de secuencia (0 o 1) e inicia un temporizador (*timer*). Si llega un ACK válido antes del tiempo de expiración (*timeout*), incrementa el número de secuencia y envía la siguiente trama; si expira el temporizador, retransmite la trama.
* **Gestión de Ventana en Selective Repeat (Protocolo 6)**: El emisor mantiene un búfer de tramas no confirmadas dentro del rango del tamaño de ventana. El receptor mantiene búferes para almacenar tramas válidas recibidas fuera de secuencia y envía un NAK (*Negative Acknowledgement*) al detectar un hueco en los números de secuencia para acelerar la retransmisión del bloque faltante.

### Ejemplos e Ilustraciones
* **El tubo de transporte ordenado**: Modelo del servicio orientado a conexión en el cual la capa de enlace funciona como un tubo donde los bits entran en un extremo y salen en el otro exactamente en el mismo orden.
* **Rayos en líneas telefónicas y colapso de secuencias**: Caso analizado en el texto donde la pérdida masiva de confirmaciones debido a descargas eléctricas demuestra por qué el tamaño de la ventana de recepción en Selective Repeat no debe exceder la mitad del espacio de números de secuencia $(2^n - 1)/2$ para evitar que tramas duplicadas sean aceptadas como nuevas.
* **HDLC (High-Level Data Link Control)**: Protocolo clásico orientado a bits que ilustra la estructura típica de trama con banderas de delimitación, campos de dirección, control de secuencia, carga útil y checksum CRC.

### Conexión Lógica y Relevancia
La capa de enlace de datos neutraliza las deficiencias de los medios físicos estudiados en el Capítulo 2, ofreciendo un canal virtual fiable y controlado a la Capa de Red (Capítulo 5). Asimismo, sus subcapas (como la subcapa MAC analizada en el Capítulo 4) gestionan el acceso cuando el medio físico es compartido por múltiples nodos en lugar de ser un enlace punto a punto.

---

## Capítulo 4: The Medium Access Control Sublayer

### Idea Central
La subcapa de control de acceso al medio (MAC), situada en la parte inferior de la capa de enlace de datos, resuelve el problema fundamental de asignar un único canal de transmisión de difusión entre múltiples estaciones en competencia. Controla la topología y operación de redes de área local cableadas (Ethernet) e inalámbricas (802.11, Bluetooth, 802.16), así como los mecanismos de conmutación a nivel de enlace mediante switches y puentes.

### Conceptos Clave
* **MAC Sublayer (Subcapa MAC)**: Subcapa inferior de la capa de enlace de datos encargada de arbitrar el acceso al canal compartido en redes de difusión.
* **Pure ALOHA vs. Slotted ALOHA**: Protocolos de acceso aleatorio. Pure ALOHA permite a las estaciones transmitir de inmediato, logrando un rendimiento máximo del 18.4%; Slotted ALOHA sincroniza el tiempo en ranuras discretas, duplicando la eficiencia teórica máxima a $1/e$ (36.8%).
* **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**: Protocolo base de Ethernet cableado donde las estaciones escuchan el medio antes de transmitir y abortan la transmisión inmediatamente si detectan una colisión durante la emisión.
* **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**: Protocolo de redes inalámbricas (IEEE 802.11) que combina detección física y virtual del medio para prevenir colisiones causadas por limitaciones de propagación radioeléctrica.
* **Hidden & Exposed Station Problems**: El problema de la estación oculta ocurre cuando una estación no puede detectar la transmisión de otra por estar fuera de su alcance radioeléctrico, colisionando en el receptor común; el problema de la estación expuesta ocurre cuando una estación se abstiene erróneamente de transmitir al escuchar a un vecino comunicarse con un tercero no interferente.
* **Switches vs. Bridges vs. Hubs**: Los hubs operan en la capa física repitiendo la señal a todos los puertos dentro de un mismo dominio de colisión; los puentes y switches operan en la subcapa MAC aislando los dominios de colisión y conmutando tramas según direcciones MAC aprendidas dinámicamente.

### Mecanismos y Procesos
* **Algoritmo de Retroceso Exponencial Binario (Binary Exponential Backoff)**: Tras detectar una colisión en CSMA/CD, el tiempo se divide en ranuras discretas de duración $2\tau$ (51.2 $\mu$s en Ethernet de 10 Mbps). Cada estación involucrada elige aleatoriamente un número de ranuras de espera en el intervalo $[0, 2^k - 1]$, donde $k = \min(\text{número de colisiones}, 10)$. Después de 16 colisiones consecutivas, se reporta un fallo permanente.
* **Intercambio RTS/CTS y Vector de Asignación de Red (NAV)**: En redes inalámbricas, el emisor transmite una trama de solicitud de envío (*Request to Send* - RTS) con la duración proyectada del intercambio; el receptor responde con un cuadro de libre para enviar (*Clear to Send* - CTS). Las estaciones adyacentes que escuchan el RTS o el CTS actualizan su temporizador interno NAV (*Network Allocation Vector*) y permanecen en silencio durante ese intervalo.
* **Aprendizaje Transparente y Algoritmo Spanning Tree en Switches**: Los switches construyen sus tablas de reenvío inspeccionando la dirección MAC de origen de cada trama entrante y asociándola al puerto de entrada. Para prevenir bucles infinitos de tramas en topologías redundantes, los switches ejecutan el algoritmo de árbol de expansión (*Spanning Tree Protocol* - STP) para desactivar lógicamente los enlaces que generen ciclos.

### Ejemplos e Ilustraciones
* **La analogía de la conferencia telefónica**: El problema del acceso al medio se compara con seis personas conectadas en una misma línea telefónica; si dos o más comienzan a hablar simultáneamente al detectar silencio, sus voces se solapan y deben pausar de forma independiente antes de reintentar.
* **Estructura Piconet/Scatternet en Bluetooth**: Organización maestro-esclavo en radiofrecuencia de corto alcance donde un nodo maestro asigna ranuras de tiempo de 625 $\mu$s a hasta siete esclavos activos; múltiples piconets interconectadas mediante nodos puente forman una red dispersa (*scatternet*).
* **El cartero frente al pregonero**: Los hubs actúan como pregoneros que gritan el mensaje a todas las casas de la calle; los switches funcionan como un servicio postal eficiente que lee la dirección escrita en el sobre y entrega la carta exclusivamente en el buzón del destinatario.

### Conexión Lógica y Relevancia
La subcapa MAC proporciona las técnicas de arbitraje necesarias para convertir medios físicos compartidos en canales de comunicación funcionales de punto a punto y conmutados. Al abstraer la transmisión local de tramas mediante direcciones físicas (MAC), establece la infraestructura requerida para que la Capa de Red (Capítulo 5) ejecute la interconexión global de paquetes entre distintas redes.

---

## Capítulo 5: The Network Layer

### Idea Central
La capa de red se encarga de transportar paquetes desde la máquina de origen hasta la de destino a través de múltiples saltos entre routers intermedios. Su diseño abarca la elección del modelo de conmutación de paquetes (datagramas frente a circuitos virtuales), la ejecución de algoritmos de enrutamiento estáticos y dinámicos, el control de la congestión, la garantía de calidad de servicio (QoS) y la interconexión de redes heterogéneas mediante el protocolo IP (IPv4 e IPv6).

### Conceptos Clave
* **Datagram Subnet vs. Virtual-Circuit Subnet**: En una subred de datagramas (sin conexión), cada paquete lleva la dirección completa de destino y se enruta de forma independiente; en una subred de circuitos virtuales (orientada a conexión), se establece una ruta previa y los paquetes solo transportan un identificador corto de circuito virtual (VC ID).
* **Routing vs. Forwarding**: El enrutamiento es el proceso global mediante el cual la red toma decisiones sobre las rutas a utilizar y llena las tablas internas de los routers; el reenvío (*forwarding*) es la acción local que ejecuta un router al recibir un paquete y pasarlo a la línea de salida correspondiente según su tabla.
* **Distance Vector vs. Link State Routing**: Distance Vector (algoritmo Bellman-Ford) intercambia vectores de distancia entre vecinos pero sufre del problema de conteo a infinito; Link State (algoritmo de Dijkstra) inunda la topología completa para que cada router calcule de forma independiente el camino más corto hacia todos los destinos.
* **CIDR (Classless Inter-Domain Routing)**: Asignación de direcciones IP sin clases mediante máscaras de subred de longitud variable (prefijos `/n`), permitiendo agrupar bloques de direcciones para mitigar el agotamiento del espacio IPv4 y reducir el tamaño de las tablas de enrutamiento.
* **Congestion Control & Traffic Shaping**: El control de congestión asegura que el tráfico ofrecido a la red no supere la capacidad de procesamiento y memoria de los routers (mediante *choke packets*, bits de advertencia o descarte RED); la conformación de tráfico (*traffic shaping*) regula la tasa y ráfaga de emisión del cliente (mediante algoritmos *Leaky Bucket* o *Token Bucket*).
* **IPv6 & Tunneling**: IPv6 sustituye el direccionamiento de 32 bits por 128 bits e introduce una cabecera fija simplificada de 40 bytes sin fragmentación intermedia; el tunelizado (*tunneling*) permite transmitir paquetes IPv6 encapsulándolos dentro de cargas útiles de redes IPv4 existentes.

### Mecanismos y Procesos
* **Funcionamiento del Enrutamiento por Estado de Enlace (Link State)**: Consta de cinco pasos: 1) Descubrir a los vecinos enviando paquetes `ECHO`; 2) Medir el retardo o costo hacia cada vecino; 3) Construir un paquete de estado de enlace (*Link State Packet* - LSP) con las mediciones; 4) Inundar de manera confiable el LSP a todos los demás routers usando números de secuencia y temporizadores de edad; 5) Aplicar el algoritmo de Dijkstra en cada router para obtener las rutas óptimas.
* **Mecanismos Leaky Bucket y Token Bucket**: *Leaky Bucket* almacena paquetes entrantes a tasa variable en una cola y los descarga a una tasa fija y constante, descartando el exceso si la cola se desborda. *Token Bucket* acumula fichas a una tasa constante; la transmisión de paquetes consume fichas, permitiendo emitir ráfagas a máxima velocidad siempre que existan fichas acumuladas en el contenedor.
* **Resolución de Direcciones con ARP (Address Resolution Protocol)**: Cuando un host conoce la dirección IP de destino pero desconoce su dirección MAC física, emite una solicitud ARP en difusión (*broadcast*) a la red local; la máquina que posee esa IP responde con una trama unicast que contiene su dirección MAC, la cual se almacena temporalmente en la tabla caché ARP del solicitante.

### Ejemplos e Ilustraciones
* **El tunelizado del automóvil en el tren**: Analogía donde un turista conduce un automóvil por Francia, lo carga en un vagón de tren para atravesar el Canal de la Mancha bajo el agua y lo descarga en Inglaterra para continuar conduciendo; ilustra cómo un paquete completo de una red se encapsula dentro del campo de datos de otra red de transporte para cruzar una infraestructura incompatible.
* **El embudo y la tubería de agua**: Representación gráfica de la congestión donde una tubería ancha vierte agua a gran velocidad sobre un embudo angosto; si la tasa de entrada supera la capacidad del cuello de botella, el embudo se desborda y la red pierde paquetes.
* **El código postal telefónico para enrutamiento jerárquico**: Comparación con la red telefónica internacional (código de país, código de área y número local), donde los routers internacionales solo almacenan prefijos jerárquicos en lugar de mantener rutas individuales hacia cada teléfono del mundo.

### Conexión Lógica y Relevancia
La capa de red unifica la diversidad de enlaces y redes locales estudiados en el Capítulo 4 en una interred coherente e interconectada a escala global. Sin embargo, el servicio básico ofrecido por IP es de "mejor esfuerzo" (*best-effort*), sin garantías de entrega, orden ni control de flujo extremo a extremo, dejando la responsabilidad de garantizar una comunicación confiable a la Capa de Transporte (Capítulo 6).

---

## Capítulo 6: The Transport Layer

### Idea Central
La capa de transporte proporciona servicios de comunicación lógicos y directos entre procesos de aplicación que se ejecutan en hosts independientes, actuando como la frontera definitiva entre el usuario y la subred de comunicación. Implementa protocolos no orientados a conexión y ligeros (UDP) y protocolos orientados a conexión, confiables, bidireccionales y adaptativos ante la congestión (TCP).

### Conceptos Clave
* **TSAP, Sockets y Puertos**: Los *Transport Service Access Points* son los puntos de acceso al servicio de transporte. En TCP/UDP se identifican mediante números de puerto de 16 bits que, combinados con la dirección IP (*NSAP*), forman un *socket* único.
* **Three-Way Handshake**: Protocolo de establecimiento de conexión en tres pasos (SYN, SYN+ACK, ACK) diseñado para negociar números de secuencia iniciales y evitar que duplicados antiguos retrasados en la red creen conexiones erróneas.
* **UDP (User Datagram Protocol)**: Protocolo no orientado a conexión que añade únicamente multiplexación por puertos y una verificación de suma (*checksum*) opcional sobre IP, orientado a aplicaciones de tiempo real o esquemas petición-respuesta rápidos.
* **TCP (Transmission Control Protocol)**: Protocolo orientado a conexión que ofrece un flujo de bytes estructurado, transparente y fiable (*stream socket*), garantizando la entrega ordenada mediante ventanas deslizantes, retransmisiones adaptativas y control de congestión.
* **Silly Window Syndrome (Síndrome de la Ventana Absurda)**: Estado de ineficiencia en TCP donde los datos se transmiten en segmentos de unos pocos bytes debido a que el emisor envía cada carácter de inmediato o el receptor anuncia incrementos mínimos de búfer; se resuelve mediante el algoritmo de Nagle (emisor) y la solución de Clark (receptor).
* **TCP Congestion Control (Slow Start, Congestion Avoidance, Fast Retransmit)**: Mecanismo dinámico donde el emisor ajusta el tamaño de su ventana de congestión (*cwnd*). Inicia con *Slow Start* (crecimiento exponencial) hasta alcanzar un umbral (*ssthresh*), y continúa con *Congestion Avoidance* (crecimiento lineal) hasta detectar pérdidas de paquetes.

### Mecanismos y Procesos
* **Gestión de Conexión en TCP**: Durante el inicio, el cliente envía un segmento con el bit `SYN=1` y un número de secuencia inicial $x$; el servidor responde con `SYN=1`, `ACK=1`, secuencia $y$ y confirmación $x+1$; el cliente finaliza enviando `ACK=1` con confirmación $y+1$. Durante la liberación simétrica, cada sentido se cierra de forma independiente enviando un segmento con el bit `FIN=1`, que debe ser confirmado por un `ACK`.
* **Desacoplamiento de Ventana y Ajuste de Flujo**: En TCP, las confirmaciones de recepción (*ACK*) y el permiso de envío están desacoplados. El receptor incluye en cada segmento devuelto un campo de ventana anunciada (*rwnd*). El emisor limita su volumen de datos no confirmados al valor $\min(rwnd, cwnd)$, evitando desbordar la memoria del receptor o la capacidad de la red.
* **Cálculo Dinámico del Temporizador de Retransmisión (Algoritmo de Jacobson)**: TCP mide continuamente el tiempo de ida y vuelta (*Round-Trip Time* - RTT) de los segmentos y calcula una media móvil suavizada (SRTT) junto con la desviación absoluta (DEV). El intervalo de retransmisión se ajusta dinámicamente mediante la fórmula $\text{RTO} = \text{SRTT} + 4 \times \text{DEV}$ para evitar retransmisiones innecesarias en redes inestables.

### Ejemplos e Ilustraciones
* **La paradoja de los dos ejércitos (Two-Armies Problem)**: Demostración matemática que prueba la imposibilidad de lograr un acuerdo perfecto de liberación de conexión sobre un canal no confiable; dos ejércitos aliados situados en colinas opuestas deben coordinar un ataque simultáneo enviando mensajeros que pueden ser capturados, requiriendo un número infinito de confirmaciones de confirmación.
* **La metáfora hidráulica de los dos cuellos de botella**: Ilustración del control de flujo y congestión mediante dos tuberías: una representa la capacidad de memoria del cubo del receptor y la otra el diámetro del tubo de transporte de la red; el emisor debe limitar su caudal al componente más estrecho para evitar derrames.
* **La analogía del archivo en UNIX**: La vista que tiene la aplicación de una conexión TCP es idéntica a la lectura/escritura de un archivo plano en UNIX: una secuencia continua de bytes donde el receptor no puede distinguir si los datos fueron escritos en bloque, byte a byte o mediante múltiples operaciones independientes.

### Conexión Lógica y Relevancia
La capa de transporte corona la infraestructura de red subyacente (física, enlace, MAC y red), convirtiendo el transporte no confiable y desordenado de datagramas IP en una comunicación de proceso a proceso transparente, segura y eficiente. Sobre esta abstracción sólida se construyen todos los servicios y protocolos de la Capa de Aplicación (Capítulo 7), como HTTP, DNS, SMTP y sistemas multimedia.

---

## Capítulo 7: The Application Layer

### Idea Central
La capa de aplicación define las reglas, protocolos e interfaces directamente empleados por los programas de usuario para ejecutar tareas funcionales a través de la red. Abarca desde la infraestructura de resolución de nombres jerárquicos (DNS) y los sistemas de mensajería (correo electrónico con SMTP, POP3 e IMAP) hasta la distribución de documentos hipertexto (HTTP en la World Wide Web) y la transmisión de medios continuos en tiempo real (RTP, SIP y VoIP).

### Conceptos Clave
* **DNS (Domain Name System)**: Base de datos jerárquica y distribuida encargada de traducir nombres de dominio legibles por humanos (ASCII) a direcciones IP numéricas mediante registros de recursos (*Resource Records* como A, MX, CNAME, NS y SOA).
* **HTTP (HyperText Transfer Protocol)**: Protocolo de solicitud-respuesta sin estado (*stateless*) en la capa de aplicación, que opera habitualmente sobre el puerto TCP 80 (o 443 para HTTPS) para transferir páginas Web, imágenes y objetos multimedia.
* **MIME (Multipurpose Internet Mail Extensions)**: Extensión del formato de correo electrónico tradicional de texto plano (RFC 822) que permite estructurar y codificar contenido no ASCII (imágenes, audio, archivos binarios y caracteres con acentos) utilizando esquemas como Base64.
* **POP3 vs. IMAP**: Protocolos para la recepción e inspección final de correo desde un servidor. POP3 descarga habitualmente los mensajes a la máquina local del cliente y los elimina del servidor; IMAP mantiene los mensajes guardados en el servidor, permitiendo búsquedas, organización en carpetas y acceso simultáneo desde múltiples dispositivos.
* **CDN (Content Delivery Network)**: Red distribuida geográficamente de servidores proxy que almacenan en caché copias de páginas y archivos multimedia para atender las solicitudes de los clientes desde el punto más cercano, reduciendo la latencia y la carga en los servidores de origen.

### Mecanismos y Procesos
* **Proceso de Resolución de Nombres en DNS**: Cuando una aplicación necesita resolver una dirección, llama a la biblioteca *resolver*. Esta envía una consulta UDP al servidor DNS local. Si la respuesta no está en su memoria caché ni en su zona de autoridad, el servidor local consulta iterativamente a la jerarquía de servidores (servidores raíz, servidores TLD del dominio de nivel superior como `.com` o `.edu`, y finalmente al servidor autoritativo del dominio) hasta obtener los registros de recursos e IP correspondientes.
* **Manejo de Estado en la Web mediante Cookies**: Debido a que HTTP es un protocolo sin estado, los servidores emplean la cabecera `Set-Cookie` para asignar un identificador único al cliente en su primera visita. En las peticiones subsecuentes, el navegador adjunta automáticamente la cabecera `Cookie` con el identificador asignado, permitiendo al servidor reconocer al usuario y reconstruir el contexto de la sesión (como carritos de compras o preferencias).
* **Transferencia de Mensajes de Correo con SMTP**: El cliente o servidor remitente inicia una conexión TCP hacia el puerto 25 del servidor de correo receptor. Se ejecuta un diálogo estructurado en comandos ASCII (`HELO` o `EHLO`, `MAIL FROM`, `RCPT TO` y `DATA`). El cuerpo del mensaje se transmite codificado en texto plano y se finaliza con una línea que contiene un único punto `.`.

### Ejemplos e Ilustraciones
* **La guía telefónica global de la red**: Comparación del DNS con las páginas blancas de la telefonía; sin DNS, los usuarios tendrían que memorizar direcciones IP cambiantes de 32 o 128 bits cada vez que un sitio cambia de servidor o proveedor.
* **La metáfora del guardarropa y las Cookies**: Las cookies funcionan de manera análoga al ticket de guardarropa en un teatro; el establecimiento no guarda a la persona, sino que le entrega una ficha numerada que el cliente presenta en cada interacción para recuperar sus pertenencias.
* **Smileys y Emoticonos**: Uso histórico de combinaciones de caracteres ASCII en correos electrónicos para transmitir tonos emocionales y lenguaje corporal en un medio puramente textual.

### Conexión Lógica y Relevancia
La capa de aplicación representa la cumbre de la pila de protocolos y la única capa visible para los usuarios e ingenieros de software. Depende directamente de la entrega ordenada y confiable provista por la Capa de Transporte (Capítulo 6) o del transporte ligero por datagramas para concretar los servicios de red finales.

---

## Capítulo 8: Network Security

### Idea Central
La seguridad en redes comprende el estudio de técnicas, algoritmos y protocolos diseñados para proteger la comunicación a través de infraestructuras no confiables. Abarca cuatro objetivos fundamentales: confidencialidad (*secrecy*), autenticación (*authentication*), no repudio (*nonrepudiation*) y control de integridad (*integrity*), fundamentados en los principios de redundancia y frescura de los mensajes.

### Conceptos Clave
* **Kerckhoffs's Principle (Principio de Kerckhoffs)**: Establece que la seguridad de un sistema criptográfico debe depender exclusivamente del secreto de la clave (*key*), y no del secreto del algoritmo (*cipher*), el cual debe asumirse conocido por el atacante.
* **Symmetric-Key Algorithms (DES, Triple-DES, AES/Rijndael)**: Algoritmos de cifrado simétrico que emplean la misma clave compartida para cifrar y descifrar el mensaje, aplicando múltiples rondas de sustituciones (S-boxes) y permutaciones (P-boxes) sobre bloques fijos de datos.
* **Public-Key Cryptography (RSA, Diffie-Hellman)**: Criptografía asimétrica basada en funciones de un solo sentido con trampa matemática. Cada usuario posee un par de claves: una clave pública para cifrar o verificar firmas, y una clave privada equivalente mantenida en secreto para descifrar o firmar.
* **Message Digests (MD5, SHA-1) y Firmas Digitales**: Funciones hash criptográficas unidireccionales que comprimen un mensaje de longitud variable en una huella digital de tamaño fijo. Al cifrar esta huella con la clave privada del emisor, se obtiene una firma digital que garantiza la autenticidad e integridad del documento.
* **PKI (Public Key Infrastructure) y Certificados X.509**: Estructura jerárquica de Autoridades de Certificación (CAs) que emiten y firman digitalmente certificados conforme al estándar X.509 para asociar de manera infalsificable la identidad de una entidad con su clave pública.
* **IPsec, SSL/TLS y Firewalls**: Mecanismos de protección en distintas capas; IPsec provee cifrado e integridad a nivel de red; SSL/TLS opera entre transporte y aplicación para conexiones seguras (HTTPS); los firewalls filtran paquetes o inspeccionan tráfico a nivel de aplicación para proteger el perímetro corporativo.

### Mecanismos y Procesos
* **Intercambio de Claves de Diffie-Hellman**: Algoritmo que permite a dos partes generar una clave secreta compartida a través de un canal inseguro sin haber intercambiado información secreta previa. Se seleccionan dos números públicos (un primo $n$ y una base $g$). Alice elige un valor secreto $x$ y envía $g^x \bmod n$; Bob elige un valor secreto $y$ y envía $g^y \bmod n$. Ambos elevan la cifra recibida a su propio exponente privado, obteniendo el valor idéntico $g^{xy} \bmod n$ como clave simétrica.
* **Cifrado en Bloque CBC (Cipher Block Chaining)**: Para evitar que bloques idénticos de texto plano generen bloques idénticos de texto cifrado, cada bloque de texto plano se somete a una operación XOR con el bloque de texto cifrado anterior antes de ser procesado por el algoritmo. El primer bloque se combina con un Vector de Inicialización (*Initialization Vector* - IV) aleatorio.
* **Autenticación con Kerberos**: Sistema de autenticación de terceros basado en Needham-Schroeder. El usuario se autentica ante un Servidor de Autenticación (AS) para obtener un Ticket de Concesión de Tickets (*Ticket-Granting Ticket* - TGT) cifrado. Posteriormente, presenta el TGT al Servidor de Concesión de Tickets (TGS) para solicitar tickets de servicio específicos que le permiten acceder a los servidores de recursos sin transmitir su contraseña por la red.

### Ejemplos e Ilustraciones
* **Ataque del Cumpleaños (Birthday Attack)**: Demostración matemática basada en la paradoja del cumpleaños (donde solo se necesitan 23 personas en una habitación para que la probabilidad de coincidencia de cumpleaños supere el 50%), aplicada a probar que para encontrar una colisión en una función hash de $m$ bits solo se requieren aproximadamente $2^{m/2}$ operaciones.
* **El puente levadizo del castillo (Firewall)**: Analogía medieval donde toda la estructura corporativa se rodea de un foso digital y se fuerza a que todo el tráfico entrante y saliente cruce por un único punto de inspección severamente controlado.
* **Man-in-the-Middle (Bucket Brigade Attack)**: Escenario donde un intruso (Trudy) se interpone de forma invisible entre Alice y Bob durante un intercambio de claves no autenticado, estableciendo sesiones criptográficas independientes con cada uno para descifrar, leer y modificar todo el tráfico de la conversación.

### Conexión Lógica y Relevancia
El Capítulo 8 actúa como el cierre transversal de la obra, demostrando que la seguridad no es una capa aislada, sino un requisito crítico que debe implementarse a lo largo de toda la arquitectura (desde el nivel físico y enlace, pasando por la capa de red con IPsec y transporte con TLS, hasta los protocolos de aplicación). Protege los recursos y flujos de datos analizados en todos los capítulos anteriores frente a ataques y suplantaciones en el entorno global de Internet.

---

## Capítulo 9: Reading List and Bibliography

### Idea Central
El capítulo final consolida la literatura científica y técnica de referencia que fundamenta el diseño de las redes de computadoras modernas. Proporciona una guía bibliográfica clasificada por capas del modelo de referencia y por temas especializados, permitiendo rastrear las fuentes originales y los estándares que dieron origen a la arquitectura de Internet.

### Conceptos Clave
* **Primary Literature (Literatura Primaria)**: Artículos científicos y publicaciones seminales donde se propusieron y formalizaron por primera vez los principios de redes (como ALOHA, Dijkstra, CSMA/CD, TCP/IP y RSA).
* **RFC (Request For Comments)**: Serie de documentos técnicos y memorandos de la IETF (*Internet Engineering Task Force*) que definen las especificaciones, protocolos y mejores prácticas oficiales de la arquitectura de Internet.
* **Standards Bodies (Organismos de Estandarización)**: Instituciones como IEEE, ITU-T, ISO e IETF encargadas de formalizar estándares internacionales para garantizar la interoperabilidad entre fabricantes.

### Mecanismos y Procesos
* **Estructuración y Consulta de la Bibliografía**: La literatura de referencia se organiza bajo dos esquemas complementarios: 1) Lecturas recomendadas con anotaciones analíticas organizadas por capítulo (Capa Física, Enlace, Subcapa MAC, Red, Transporte, Aplicación y Seguridad); 2) Índice alfabético detallado de citas bibliográficas para la verificación de demostraciones matemáticas, algoritmos y especificaciones formales.

### Ejemplos e Ilustraciones
* **El artículo de Arthur C. Clarke (1945)**: Cita histórica de *Wireless World* donde el autor de ciencia ficción calculó por primera vez la órbita de los satélites geoestacionarios décadas antes de que la tecnología de lanzamiento existiera.
* **RFC 1958 ("Architectural Principles of the Internet")**: Documento de referencia obligatoria citado para sintetizar los diez principios de diseño que guiaron la creación de la red global de paquetes (principio extremo a extremo, simplicidad y escalabilidad).

### Conexión Lógica y Relevancia
Este capítulo vincula el contenido académico de los Capítulos 1 al 8 con el cuerpo de investigación en constante evolución. Ofrece la ruta para profundizar en las especificaciones técnicas puras y los fundamentos matemáticos de cada sistema analizado en el cuaderno de notas.
