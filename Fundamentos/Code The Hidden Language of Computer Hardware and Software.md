# Code – The Hidden Language of Computer Hardware and Software (2nd Edition)

## Índice

- [Resumen General del Libro](#resumen-general-del-libro)
- [Capítulo 1: Best Friends (Mejores amigos)](#capítulo-1-best-friends-mejores-amigos)
- [Capítulo 2: Codes and Combinations (Códigos y combinaciones)](#capítulo-2-codes-and-combinations-códigos-y-combinaciones)
- [Capítulo 3: Braille and Binary Codes (Braille y códigos binarios)](#capítulo-3-braille-and-binary-codes-braille-y-códigos-binarios)
- [Capítulo 4: Anatomy of a Flashlight (Anatomía de una linterna)](#capítulo-4-anatomy-of-a-flashlight-anatomía-de-una-linterna)
- [Capítulo 5: Communicating Around Corners (Comunicación a la vuelta de la esquina)](#capítulo-5-communicating-around-corners-comunicación-a-la-vuelta-de-la-esquina)
- [Capítulo 6: Logic with Switches (Lógica con interruptores)](#capítulo-6-logic-with-switches-lógica-con-interruptores)
- [Capítulo 7: Telegraphs and Relays (Telégrafos y relés)](#capítulo-7-telegraphs-and-relays-telégrafos-y-relés)
- [Capítulo 8: Relays and Gates (Relés y puertas lógicas)](#capítulo-8-relays-and-gates-relés-y-puertas-lógicas)
- [Capítulo 9: Our Ten Digits (Nuestros diez dígitos)](#capítulo-9-our-ten-digits-nuestros-diez-dígitos)
- [Capítulo 10: Alternative 10s (Dieces alternativos)](#capítulo-10-alternative-10s-dieces-alternativos)
- [Capítulo 11: Bit by Bit by Bit (Bit a bit por bit)](#capítulo-11-bit-by-bit-by-bit-bit-a-bit-por-bit)
- [Capítulo 12: Bytes and Hexadecimal (Bytes y hexadecimal)](#capítulo-12-bytes-and-hexadecimal-bytes-y-hexadecimal)
- [Capítulo 13: From ASCII to Unicode (De ASCII a Unicode)](#capítulo-13-from-ascii-to-unicode-de-ascii-a-unicode)
- [Capítulo 14: Adding with Logic Gates (Sumando con puertas lógicas)](#capítulo-14-adding-with-logic-gates-sumando-con-puertas-lógicas)
- [Capítulo 15: Is This for Real? (¿Es esto real?)](#capítulo-15-is-this-for-real-es-esto-real)
- [Capítulo 16: But What About Subtraction? (Pero ¿qué pasa con la resta?)](#capítulo-16-but-what-about-subtraction-pero-qué-pasa-con-la-resta)
- [Capítulo 17: Feedback and Flip-Flops (Retroalimentación y flip-flops)](#capítulo-17-feedback-and-flip-flops-retroalimentación-y-flip-flops)
- [Capítulo 18: Let's Build a Clock! (¡Construyamos un reloj!)](#capítulo-18-lets-build-a-clock-construyamos-un-reloj)
- [Capítulo 19: An Assemblage of Memory (Un ensamblaje de memoria)](#capítulo-19-an-assemblage-of-memory-un-ensamblaje-de-memoria)
- [Capítulo 20: An Automated Computer (Una computadora automatizada)](#capítulo-20-an-automated-computer-una-computadora-automatizada)
- [Capítulo 21: The Arithmetic Logic Unit (La Unidad Aritmético-Lógica)](#capítulo-21-the-arithmetic-logic-unit-la-unidad-aritmético-lógica)
- [Capítulo 22: Registers and Busses (Registros y buses)](#capítulo-22-registers-and-busses-registros-y-buses)
- [Capítulo 23: CPU Control Signals (Señales de control de la CPU)](#capítulo-23-cpu-control-signals-señales-de-control-de-la-cpu)
- [Capítulo 24: Loops, Jumps, and Calls (Bucles, saltos y llamadas)](#capítulo-24-loops-jumps-and-calls-bucles-saltos-y-llamadas)
- [Capítulo 25: Peripherals (Periféricos)](#capítulo-25-peripherals-periféricos)
- [Capítulo 26: The Operating System (El sistema operativo)](#capítulo-26-the-operating-system-el-sistema-operativo)
- [Capítulo 27: Coding (Programación y lenguajes de alto nivel)](#capítulo-27-coding-programación-y-lenguajes-de-alto-nivel)
- [Capítulo 28: The World Brain (El cerebro mundial)](#capítulo-28-the-world-brain-el-cerebro-mundial)
- [Diagrama de Capas de Abstracción](#diagrama-de-capas-de-abstracción)
- [Desglose por Niveles de Abstracción](#desglose-por-niveles-de-abstracción)

## Resumen General del Libro

El libro *Code: The Hidden Language of Computer Hardware and Software* demuestra cómo la complejidad de una computadora moderna se construye apilando niveles de abstracción simples sobre una base física y matemática unificada. Charles Petzold enseña que una computadora no es un dispositivo mágico incomprensible, sino la unión sistemática entre el álgebra booleana y la energía eléctrica.

## Capítulo 1: Best Friends (Mejores amigos)

### Idea Central
El primer capítulo utiliza la situación hipotética de dos amigos que necesitan comunicarse de noche entre sus ventanas para introducir la necesidad de crear códigos de comunicación a distancia. Muestra cómo los intentos de dibujar letras en el aire resultan ineficientes, demostrando que cualquier información puede transmitirse combinando únicamente dos estados discretos o elementos binarios.

### Conceptos Fundamentales
* **Código (Code)**: Sistema para transferir información entre personas, entre personas y computadoras, o dentro de las propias computadoras. Debe ser comprendido por ambas partes para ser efectivo.
* **Elemento binario (Binary element)**: Componente o señal que posee únicamente dos estados posibles (encendido/apagado, corto/largo, *dih*/*dah*). Dos estados son suficientes para representar cualquier tipo de información.
* **Código Morse (Morse code)**: Sistema que asigna a cada letra, número o signo de puntuación una secuencia de impulsos de luz o sonido cortos (*dots* o puntos) y largos (*dashes* o rayas).

### Mecanismos y Procesos
* **Mecanismo de transmisión visual**: La linterna se enciende brevemente para un punto y se mantiene encendida tres veces más tiempo para una raya.
* **Estructura temporal de las pausas**: Las pausas separan los impulsos. El espacio entre puntos y rayas dentro de una misma letra dura un punto; entre letras de una palabra equivale a una raya; y entre palabras completas equivale a dos rayas.
* **Optimización por frecuencia**: Las letras más comunes en inglés (como E y T) reciben las secuencias más cortas (un punto o una raya), mientras que letras poco frecuentes utilizan secuencias más largas.

### Ejemplos Clave
* **Dibujar letras en el aire con luz**: Intentar formar trazos en el aire fracasa porque la mente del receptor no puede ensamblar con precisión los trazos en movimiento en la oscuridad.
* **Conteo simple de parpadeos**: Asignar 1 parpadeo a la A hasta 26 a la Z requiere 131 parpadeos solo para emitir "How are you?", resultando sumamente lento.
* **Señal de socorro SOS y la Quinta Sinfonía de Beethoven**: SOS (tres puntos, tres rayas, tres puntos) es una secuencia elegida por su facilidad de recordación. El inicio de la Quinta Sinfonía de Beethoven (*dit-dit-dit-dah*) coincide con el código Morse de la letra V (Victoria).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Estructura alfabética básica del lenguaje escrito y funcionamiento de un interruptor.
* **Relación futura**: Establece la premisa central del libro: los sistemas binarios son el fundamento técnico del hardware y el software.

### Dudas y Aspectos a Verificar
* El código Morse original no diferencia entre mayúsculas y minúsculas.
* La flexibilidad de la duración relativa del punto exige sintonizar el ritmo entre emisor y receptor

## Capítulo 2: Codes and Combinations (Códigos y combinaciones)

### Idea Central
Este capítulo explica cómo calcular matemáticamente la cantidad de códigos únicos que se pueden generar agrupando elementos binarios mediante el uso de potencias de 2. Asimismo, muestra que la organización de los códigos en estructuras de árbol facilita la decodificación durante la recepción de un mensaje.

### Conceptos Fundamentales
* **Combinación binaria (Binary combination)**: El número total de patrones distintos que pueden formarse al agrupar objetos con exactamente dos estados posibles.
* **Potencias de 2 ($2^n$)**: Relación matemática donde el número total de códigos equivale a 2 elevado al número de impulsos o bits utilizados.
* **Código no definido (Undefined code)**: Secuencia binaria matemáticamente posible a la que no se le ha asignado un significado, útil para detectar errores en la transmisión.
* **Árbol de decodificación (Decoding tree)**: Diagrama ramificado que permite traducir secuencias de impulsos a letras siguiendo un camino de izquierda a derecha.

### Mecanismos y Procesos
* **Asimetría entre emisión y recepción**: Una lista ordenada alfabéticamente (Letra a Código) es óptima para enviar mensajes, pero ineficiente para recibir, ya que exige escanear toda la lista.
* **Crecimiento exponencial por nivel**: Cada vez que se añade un impulso adicional a la secuencia, el número de códigos disponibles se duplica exactamente (2, 4, 8, 16, 32, 64).
* **Fórmula general de combinación**: Número de códigos = $2^n$, donde $n$ representa la cantidad de elementos binarios.

### Ejemplos Clave
* **Estructura del árbol de decodificación**: Iniciando en la raíz, cada punto toma la rama superior y cada raya la inferior; por ejemplo, la secuencia punto-raya-punto conduce a la letra R.
* **Lanzamiento de monedas**: Al tener una moneda solo dos lados, lanzarla 10 veces seguidas genera $2^{10} = 1024$ secuencias posibles, ilustrando secuencias binarias de 10 posiciones.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Se basa en la distinción de dos impulsos (punto y raya) introducida en el Capítulo 1.
* **Relación futura**: Introduce las potencias de 2, fundamentales para comprender bits, bytes y memoria digital.

### Dudas y Aspectos a Verificar
* Al expandir el código Morse a secuencias de 6 elementos para acomodar signos de puntuación, quedan muchas combinaciones sin definir, lo que genera redundancia a cambio de detectar errores.

## Capítulo 3: Braille and Binary Codes (Braille y códigos binarios)

### Idea Central
El capítulo explora cómo Louis Braille adaptó el sistema táctil militar de escritura nocturna para crear un código de lectura binario basado en celdas de seis puntos en una matriz de 2x3. Demuestra cómo una matriz fija de elementos táctiles binarios (elevado o plano) genera exactamente 64 combinaciones únicas. Introduce los conceptos de códigos de cambio (*shift codes*) y escape (*escape codes*) para expandir la representación sin añadir más puntos a la matriz.

### Conceptos Fundamentales
* **Celda de Braille (Braille cell)**: Matriz táctil de 2 columnas por 3 filas, con puntos numerados del 1 al 6.
* **Carácter binario (Binary character)**: Cada punto de la celda es binario porque solo posee dos estados físicos posibles: elevado (*raised*) frente a plano (*flat*).
* **Código de cambio (Shift code)**: Código que altera la interpretación de todos los símbolos posteriores hasta que se restaura su estado.
* **Código de escape (Escape code)**: Código que modifica la interpretación únicamente del símbolo inmediatamente posterior.
* **Grade 2 Braille**: Versión expandida que utiliza contracciones para ahorrar papel y acelerar la lectura.

### Mecanismos y Procesos
* **Cálculo de combinaciones**: Dado que cada celda contiene 6 puntos binarios, la capacidad de representación total es de $2^6 = 64$ combinaciones posibles.
* **Estructura por filas del alfabeto**:
  - Las letras de la **a** a la **j** utilizan únicamente combinaciones de los cuatro puntos superiores (puntos 1, 2, 4 y 5).
  - Las letras de la **k** a la **t** duplican la primera fila agregando el punto 3 elevado.
  - Las letras de la **u** a la **z** duplican la primera fila agregando los puntos 3 y 6 elevados.
* **Mecanismo de cambio de modo**: El indicador numérico transforma las celdas **a** a **j** en los dígitos 1 al 9 y 0. Un indicador de letra restaura la interpretación alfabética. Un indicador de mayúscula (punto 6) actúa como código de escape para una sola letra.

### Ejemplos Clave
* **Origen militar**: Sistema diseñado por Charles Barbier en 1815 para que los soldados transmitieran notas silenciosas en la oscuridad perforando papel.
* **Lectura de números**: El indicador numérico seguido de las celdas **b**, **e** y **f** se interpreta como el número 256.
* **Escritura de "Louis Braille"**: Se codifica anteponiendo el indicador de mayúscula antes de la **l** inicial y de la **b** del apellido.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Conecta con el cálculo de potencias de 2 ($2^n$) del Capítulo 2.
* **Relación futura**: Prefigura el manejo de conjuntos limitados de símbolos (códigos ASCII) y caracteres de escape en informática.

### Dudas y Aspectos a Verificar
* Al reutilizar patrones táctiles mediante prefijos, el sistema introduce ambigüedad local si se analiza un símbolo aislado.
* La celda de 6 puntos impuso un límite de 64 símbolos, motivando la creación posterior del Braille de 8 puntos ($2^8 = 256$) en informática.

## Capítulo 4: Anatomy of a Flashlight (Anatomía de una linterna)

### Idea Central
El capítulo analiza el funcionamiento físico de una linterna para demostrar cómo los principios de la electricidad fundamentan los sistemas digitales. Describe el circuito cerrado donde las reacciones químicas de las baterías impulsan electrones a través de un conductor hacia la bombilla. Introduce la Ley de Ohm ($I = E / R$) y muestra que el interruptor actúa como un control binario directo.

### Conceptos Fundamentales
* **Circuito eléctrico (Electrical circuit)**: Trayectoria circular continua requerida para que los electrones fluyan desde la fuente y regresen al origen.
* **Voltaje / Fuerza electromotriz ($E$ / Voltage)**: Presión eléctrica que impulsa los electrones a moverse, medida en voltios.
* **Corriente ($I$ / Current)**: Cantidad de electrones que circulan por un punto del circuito por unidad de tiempo, medida en amperios.
* **Resistencia ($R$ / Resistance)**: Oposición natural de un material al paso libre de electrones, medida en ohmios.
* **Ley de Ohm**: Relación fundamental $I = E / R$.
* **Cortocircuito (Short circuit)**: Unión de los polos de una fuente eléctrica con resistencia casi nula, desatando un flujo de corriente masivo y peligroso.

### Mecanismos y Procesos
* **Flujo de electrones**: Las reacciones químicas acumulan electrones en el terminal negativo y los demandan en el positivo, haciendo circular electrones del polo negativo al positivo al cerrar el circuito.
* **Conexiones de baterías**:
  - En serie: Los voltajes se suman ($1.5	ext{V} + 1.5	ext{V} = 3.0	ext{V}$), aumentando la intensidad luminosa.
  - En paralelo: El voltaje permanece en $1.5	ext{V}$, pero la capacidad química se duplica, extendiendo la duración.
* **Acción del interruptor binario**: Al abrirse, la resistencia del aire se vuelve extremadamente alta, reduciendo la corriente a cero. Al cerrarse, se restablece el camino metálico continuo.

### Ejemplos Clave
* **Linterna sin adornos**: Disposición experimental que conecta directamente dos baterías, una bombilla e hilos de cobre pelados.
* **Analogía del agua y las tuberías**: Corriente como caudal, voltaje como presión y resistencia como estrechez de la tubería.
* **Cálculo de corriente**: Dos baterías en serie de 1.5V ($E = 3	ext{V}$) y una bombilla ($R = 4\Omega$) producen $I = 3 / 4 = 0.75	ext{ amperios}$, lo que equivale a más de 4.5 quintillones de electrones por segundo.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Nociones atómicas elementales sobre electrones.
* **Relación futura**: Fundamenta la transición de la representación abstracta de bits a la implementación física mediante voltajes e interruptores.

### Dudas y Aspectos a Verificar
* En física los electrones fluyen de negativo a positivo, pero la convención tradicional de ingeniería marca el flujo de positivo a negativo. El autor utiliza el flujo real de electrones.
* La analogía del agua tiene límites: el agua puede salir de una tubería abierta, mientras que la carga eléctrica requiere un circuito cerrado.

## Capítulo 5: Communicating Around Corners (Comunicación a la vuelta de la esquina)

### Idea Central
El capítulo explica cómo extender la comunicación binaria por código Morse más allá de la línea de visión directa mediante cables eléctricos, baterías e interruptores. Muestra cómo interconectar ubicaciones distantes y optimizar la infraestructura reduciendo el número de cables al utilizar una línea común y la propia masa de la Tierra como conductor de retorno.

### Conceptos Fundamentales
* **Telégrafo de hilo (Wired telegraph)**: Sistema de comunicación a distancia que transmite impulsos eléctricos por conductores metálicos.
* **Línea común (Common line)**: Técnica de cableado que comparte un solo conductor de retorno entre dos circuitos independientes.
* **Tierra / Masa (Ground / Earth)**: Uso del suelo o la masa del planeta como conductor de retorno para cerrar un circuito sin un segundo cable físico.
* **Resistencia por longitud**: La oposición al paso de la corriente aumenta con la longitud del cable, debilitando la señal a largas distancias.

### Mecanismos y Procesos
* **Reducción de 4 a 3 cables**: Uniendo el polo negativo de dos baterías a una línea común de retorno se elimina un cable en un sistema bidireccional.
* **Reducción a 2 cables (Conexión a Tierra)**: Enterrando varillas de cobre o conectando a tuberías metálicas de agua en ambos extremos, la Tierra asume el retorno, necesitando solo 2 cables suspendidos.
* **Atenuación por distancia**: Un cable muy largo acumula suficiente resistencia para reducir el flujo de electrones, provocando que la bombilla receptora brille de forma tenue o no encienda.

### Ejemplos Clave
* **Ventanas contiguas sin visión directa**: Amigos cuyas habitaciones están en casas adosadas orientadas al mismo lado no pueden usar linternas directas, motivando instalar cables alrededor de la esquina.
* **Tuberías de agua fría**: Dispositivos cotidianos utilizados para lograr una conexión eléctrica efectiva con la masa de la Tierra.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Código Morse (Capítulo 1), circuito cerrado y Ley de Ohm (Capítulo 4).
* **Relación futura**: Plantea el problema técnico del Capítulo 7: cómo superar el límite de distancia impuesto por la resistencia mediante relés.

### Dudas y Aspectos a Verificar
* La conexión a Tierra requiere un voltaje adecuado y buena humedad en el suelo para ofrecer baja resistencia.
* En diagramas modernos, el símbolo *Ground* representa un punto de referencia común de cero voltios, no siempre una conexión al planeta.

## Capítulo 6: Logic with Switches (Lógica con interruptores)

### Idea Central
El capítulo demuestra cómo el álgebra booleana desarrollada por George Boole para formalizar el razonamiento lógico puede implementarse físicamente mediante combinaciones de interruptores eléctricos. Muestra que la conexión de interruptores en serie realiza la operación lógica AND, mientras que la conexión en paralelo realiza la operación lógica OR.

### Conceptos Fundamentales
* **Álgebra Booleana (Boolean algebra)**: Sistema matemático donde las variables solo adoptan uno de dos valores: Verdadero (1) o Falso (0).
* **Silogismo (Syllogism)**: Estructura de razonamiento deductivo de la filosofía aristotélica que obtiene una conclusión a partir de dos premisas.
* **Operación AND**: Operación lógica cuyo resultado es 1 únicamente si todas las entradas son 1.
* **Operación OR**: Operación lógica cuyo resultado es 1 si al menos una de las entradas es 1.
* **Operación NOT**: Inversión lógica que cambia 1 a 0 y 0 a 1.
* **Tabla de verdad (Truth table)**: Tabla que enumera todas las combinaciones posibles de entradas y sus resultados lógicos.

### Mecanismos y Procesos
* **Interruptores en serie (Operador AND)**: Al colocar dos interruptores en el mismo cable, la corriente solo fluye si el primer interruptor Y el segundo están cerrados.
* **Interruptores en paralelo (Operador OR)**: Al colocar dos interruptores en caminos ramificados, la corriente fluye si el primer interruptor O el segundo (o ambos) están cerrados.
* **Traducción algebraica**: Las condiciones verbales se simplifican usando multiplicación para AND, suma para OR e inversión para NOT.
* **Simplificación de redes**: Reducir una expresión booleana mediante leyes algebraicas permite diseñar un circuito equivalente con menos interruptores físicos.

### Ejemplos Clave
* **Silogismo de Sócrates**: "Todos los hombres son mortales; Sócrates es hombre; por lo tanto, Sócrates es mortal", ilustrando estructuras de lenguaje lógico.
* **El problema de la tienda de mascotas**: La búsqueda de un gato con criterios complejos convertida en la ecuación algebraíca $(M 	imes N 	imes (W + T)) + (F 	imes N 	imes (1 - W)) + B$ e implementada en una red de interruptores.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Interruptor eléctrico binario (Capítulo 4) y matemática binaria (Capítulo 2).
* **Relación futura**: Prefigura la creación de puertas lógicas (Capítulo 8), donde los relés reemplazan a los interruptores manuales.

### Dudas y Aspectos a Verificar
* En lógica booleana, el operador OR es incluyente por defecto (es 1 si ambas entradas son 1), a diferencia de ciertos usos cotidianos donde sugiere elegir solo una opción.

## Capítulo 7: Telegraphs and Relays (Telégrafos y relés)

### Idea Central
El capítulo describe la invención del telégrafo eléctrico y la introducción del electroimán para convertir impulsos eléctricos lejanos en movimiento físico o sonido. Para resolver la pérdida de señal causada por la resistencia en cables largos, introduce el relé o repetidor, un dispositivo que utiliza una señal eléctrica débil para accionar un interruptor que envía una señal fuerte renovada.

### Conceptos Fundamentales
* **Electroimán (Electromagnet)**: Núcleo de hierro envuelto en una bobina de cable que se magnetiza al pasar corriente, atrayendo objetos metálicos.
* **Llave telegráfica (Telegraph key)**: Interruptor accionado manualmente para emitir puntos y rayas de código Morse.
* **Resonador o emisor de sonido (Sounder)**: Receptor mecánico que emite un golpe seco al ser atraído (*click*) y otro al liberarse (*clack*), permitiendo escuchar el código.
* **Relé o repetidor (Relay / Repeater)**: Dispositivo electromecánico donde la corriente entrante activa un electroimán que abre o cierra los contactos de un circuito saliente independiente.

### Mecanismos y Procesos
* **Conversión de electricidad en movimiento**: La corriente en la bobina magnetiza el hierro y tira de la palanca del resonador. Al cortar la corriente, un muelle devuelve la palanca a reposo.
* **Evolución a la recepción auditiva**: El sistema de Morse dibujaba marcas en papel, pero los operadores descubrieron que podían interpretar los patrones escuchando el ritmo de los chasquidos mecánicos.
* **Amplificación mediante relé**: A mitad de camino, la corriente atenuada activa un electroimán sensible en el relé. Su palanca actúa como interruptor de alta precisión conectado a una batería local fresca, retransmitiendo la señal con voltaje completo.

### Ejemplos Clave
* **Semáforos ópticos previos**: Torres en colinas con brazos mecánicos que dependían de la luz del día y del clima.
* **La analogía del operador intermedio**: Imaginar a un trabajador en una caseta intermedia escuchando un resonador y pulsando al instante una nueva llave. El relé automatiza esta función.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Resistencia eléctrica y atenuación (Capítulo 5), código Morse (Capítulo 1).
* **Relación futura**: Transforma el relé en un interruptor controlado eléctricamente, clave para construir las puertas lógicas del Capítulo 8.

### Dudas y Aspectos a Verificar
* El relé no crea energía; requiere una fuente de alimentación local (batería) en la estación intermedia.
* La velocidad de conmutación del relé está limitada por la masa física de su palanca metálica y la tensión del muelle.

## Capítulo 8: Relays and Gates (Relés y puertas lógicas)

### Idea Central
Este capítulo une el álgebra booleana con la electrónica física al reemplazar interruptores manuales por relés electromagnéticos para construir puertas lógicas (*logic gates*). Al estar controlados por electricidad, las salidas de unos relés pueden activar las entradas de otros, permitiendo interconectar bloques lógicos simples (AND, OR, NOT, NOR, NAND) para ejecutar operaciones analíticas complejas.

### Conceptos Fundamentales
* **Puerta lógica (Logic gate)**: Circuito digital básico que evalúa entradas de voltaje para producir una sola salida lógica (1 o 0).
* **Relé de doble tiro (Double-throw relay)**: Relé con dos contactos de salida alternativos: normalmente cerrado (en reposo) y normalmente abierto (al activarse).
* **Inversor / Puerta NOT**: Circuito que invierte el valor de entrada (transforma 1 en 0 y 0 en 1).
* **Puerta NOR**: Operación OR seguida de una inversión NOT. Su salida es 1 únicamente si todas sus entradas son 0.
* **Puerta NAND**: Operación AND seguida de una inversión NOT. Su salida es 0 únicamente si todas sus entradas son 1.

### Mecanismos y Procesos
* **Implementación con relés**:
  - **AND**: Dos relés en serie. La corriente pasa si ambos están activos.
  - **OR**: Dos relés en paralelo. La corriente pasa si cualquiera está activo.
  - **NOT (Inversor)**: Utiliza la terminal normalmente cerrada. Cuando la entrada es 0, deja pasar voltaje (1). Cuando la entrada es 1, el electroimán atrae la palanca y corta el voltaje (0).
* **Cascada de puertas**: La salida de un relé es un voltaje adecuado para alimentar el electroimán de otro relé, permitiendo encadenar puertas sin intervención manual.

### Ejemplos Clave
* **El descubrimiento de Claude Shannon y Akira Nakashima**: Shannon en su tesis de 1938 en el MIT y Nakashima en 1936 demostraron que los relés de telefonía podían resolver cualquier ecuación del álgebra de George Boole.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Álgebra booleana (Capítulo 6), relé electromagnético (Capítulo 7).
* **Relación futura**: Bloques para sumadores binarios (Capítulo 14), memorias y flip-flops (Capítulo 17) y la ALU.

### Dudas y Aspectos a Verificar
* Regla estricta de conexión: Se pueden conectar salidas a múltiples entradas, pero nunca unir las salidas de dos puertas entre sí para evitar cortocircuitos.

## Capítulo 9: Our Ten Digits (Nuestros diez dígitos)

### Idea Central
El capítulo examina el origen y la estructura del sistema numérico decimal (base 10) para demostrar que los números son códigos abstractos basados en la anatomía humana de diez dedos. Explica la elegancia de la notación posicional posibilitada por el cero y muestra cómo las reglas de la aritmética se descomponen en operaciones estructuradas de un solo dígito.

### Conceptos Fundamentales
* **Sistema decimal / Base 10**: Sistema posicional organizado en torno al diez, derivado del conteo con los diez dedos.
* **Notación posicional**: Sistema donde el valor de un dígito depende de su símbolo y de la posición relativa que ocupa, correspondiendo cada posición a una potencia de la base.
* **El Cero (Zero)**: Símbolo fundamental que indica la ausencia de cantidad en una posición específica, permitiendo diferenciar 25, 205 o 250 sin crear nuevos símbolos.

### Mecanismos y Procesos
* **Estructura jerárquica**: En la cifra 4825, cada posición representa una potencia ascendente de diez ($10^0, 10^1, 10^2, 10^3$):
  $$4825 = 4 	imes 10^3 + 8 	imes 10^2 + 2 	imes 10^1 + 5 	imes 10^0$$
* **Potencias negativas**: Las cifras a la derecha del punto decimal representan divisiones entre potencias de diez ($10^{-1}, 10^{-2}, 10^{-3}$).
* **Descomposición algorítmica**: La notación posicional reduce cálculos complejos a secuencias de pasos basados en tablas memorizadas de suma y multiplicación entre pares de dígitos.

### Ejemplos Clave
* **Números romanos**: Sistema no posicional donde calcular operaciones aritméticas como multiplicar resulta sumamente complejo e ineficiente.
* **Personajes de dibujos animados**: Tienen cuatro dedos en cada mano (ocho en total), sugiriendo que la base 10 no es la única base posible.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Código como representación arbitraria de símbolos (Capítulo 1).
* **Relación futura**: Base conceptual para sistemas alternativos (Capítulo 10) y circuitos sumadores eléctricos (Capítulo 14).

### Dudas y Aspectos a Verificar
* La familiaridad con la base 10 lleva a confundir la cantidad abstracta con el símbolo arbitrario usado para representarla.
* Existen excepciones históricas como el sistema sexagesimal (base 60) babilonio, presente hoy en la medición del tiempo.

## Capítulo 10: Alternative 10s (Dieces alternativos)

### Idea Central
Este capítulo explica cómo construir sistemas de numeración con bases distintas a diez (octal/base 8, cuaternario/base 4 y binario/base 2), demostrando que las reglas posicionales son idénticas independientemente de la base. Concluye revelando que el sistema binario es la base más simple para unir la aritmética con circuitos eléctricos.

### Conceptos Fundamentales
* **Base octal (Base 8)**: Sistema posicional que utiliza únicamente los dígitos del 0 al 7.
* **Base cuaternaria (Base 4)**: Sistema posicional que utiliza los dígitos 0, 1, 2 y 3.
* **Sistema binario (Base 2)**: El sistema posicional más simple posible, basado en el dos, que utiliza únicamente los dígitos 0 y 1.
* **El numeral "10" en bases no decimales**: En cualquier base $B$, la combinación de caracteres "10" representa la cantidad exacta equivalente a la base $B$ (8 en octal, 4 en cuaternario, 2 en binario).
* **Decodificador de 3 a 8**: Circuito digital que convierte una entrada binaria de 3 bits en una única salida activa entre 8 líneas posibles.

### Mecanismos y Procesos
* **Conteo en bases no decimales**: Al alcanzar el dígito máximo (7 en octal, 3 en cuaternario, 1 en binario), la siguiente cantidad reinicia la posición a 0 e incrementa la posición izquierda a 1, produciendo "10".
* **Descomposición en potencias**: El octal 14 equivale a $1 	imes 8^1 + 4 	imes 8^0 = 12$ en decimal. El binario 1001 equivale a $1 	imes 2^3 + 0 	imes 2^2 + 0 	imes 2^1 + 1 	imes 2^0 = 9$ en decimal.

### Ejemplos Clave
* **El sistema de las langostas (Base 4)**: Sistema cuaternario adaptado a animales con dos pinzas frontales, donde se cuenta 0, 1, 2, 3 y "10".
* **El delfín contando con sus aletas (Base 2)**: Al tener dos aletas, el delfín cuenta 0, 1 y pasa a "10", ilustrando la rapidez con que se agotan los dígitos individuales en binario.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Notación posicional (Capítulo 9) y serie de potencias de 2 (Capítulos 2 y 3).
* **Relación futura**: Lenguaje numérico indispensable para circuitos sumadores (Capítulo 14) y representación en bytes/hexadecimal (Capítulo 12).

### Dudas y Aspectos a Verificar
* Pronunciar "diez" al leer "10" en bases no decimales genera confusión; se recomienda decir "uno cero" (o "uno cero en base ocho").

## Capítulo 11: Bit by Bit by Bit (Bit a bit por bit)

### Idea Central
El capítulo introduce el término "bit" (*binary digit*) como la cantidad mínima e indivisible de información. Demuestra cómo cualquier mensaje puede reducirse a elecciones binarias y analiza la presencia visible de los bits en la vida cotidiana a través de códigos de barras UPC y códigos QR.

### Conceptos Fundamentales
* **Bit (Binary Digit)**: Término acuñado por John Tukey en 1947 para definir la unidad básica de información, representando una elección entre dos posibilidades (0 o 1).
* **Paridad (Parity)**: Método de control de errores que evalúa si la suma de unos en un grupo de bits es par (*even parity*) o impar (*odd parity*).
* **Código de barras UPC**: Sistema de identificación de productos de 95 bits visualizados como barras negras y espacios blancos.
* **Patrones de guardia (Guard patterns)**: Secuencias de bits fijas (101 a los extremos, 01010 al centro) que permiten al escáner calibrar el ancho y leer en cualquier dirección.
* **Código QR**: Matriz bidimensional de módulos cuadrados capaz de almacenar alta densidad de datos mediante corrección de errores y patrones de máscara.

### Mecanismos y Procesos
* **Estructura del UPC de 12 dígitos**:
  - Patrón de guardia izquierdo (101).
  - Seis dígitos a la izquierda en 7 bits con paridad impar.
  - Patrón de guardia central (01010).
  - Seis dígitos a la derecha en 7 bits con paridad par y valores invertidos.
  - Patrón de guardia derecho (101).
* **Cálculo del dígito de comprobación**: Se realiza una fórmula aritmética con las posiciones impares y pares. Si el escáner no obtiene el mismo valor, rechaza la lectura.

### Ejemplos Clave
* **Votación de Siskel y Ebert**: Pulgares arriba (1) o abajo (0) de dos críticos combinan 2 bits para generar 4 veredictos posibles: 00, 01, 10 o 11.
* **Paracaídas del rover Perseverance**: Trama de 320 franjas naranjas y blancas en círculos concéntricos que codifica en binario "Dare Mighty Things" y las coordenadas geográficas del laboratorio JPL de la NASA.
* **Lata de sopa Campbell**: Código `0 51000 01251 7`, donde `51000` es el fabricante y `01251` el producto. El código no contiene el precio.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Combinaciones binarias y potencias de 2 (Capítulos 2 y 10).
* **Relación futura**: Base para la agrupación de 8 bits (byte, Capítulo 12) y codificación de texto (Capítulo 13).

### Dudas y Aspectos a Verificar
* Un bit por sí solo no posee significado intrínseco; el valor '1' depende del contexto acordado entre emisor y receptor.

## Capítulo 12: Bytes and Hexadecimal (Bytes y hexadecimal)

### Idea Central
Este capítulo explica por qué la industria informática estandarizó la agrupación de bits en conjuntos de 8 unidades llamados bytes. Presenta el sistema hexadecimal (base 16) como una herramienta indispensable para representar el valor de cualquier byte mediante solo dos caracteres.

### Conceptos Fundamentales
* **Byte**: Secuencia de 8 bits continuos que puede adoptar 256 valores distintos (desde 00000000 hasta 11111111, equivalente a 0 hasta 255 en decimal, o $2^8$).
* **Nibble (Medio byte)**: Grupo de 4 bits. Un byte se compone de dos *nibbles*.
* **Sistema Hexadecimal (Base 16)**: Sistema posicional que utiliza 16 símbolos: los dígitos del 0 al 9 y las letras A, B, C, D, E y F (para los valores del 10 al 15).
* **Palabra (Word)**: Medida arquitectónica de una CPU que define el tamaño estándar de los grupos de bits con los que trabaja (ej. 16, 32 o 64 bits).

### Mecanismos y Procesos
* **Alineación de 4 bits a 1 dígito hexadecimal**: Un *nibble* de 4 bits ($2^4 = 16$) se traduce a un único carácter hexadecimal (0000 = 0, 1111 = F). Un byte de 8 bits se representa siempre con dos caracteres hexadecimales.
* **Incompatibilidad del octal con el byte**: El octal utiliza 3 bits por dígito, por lo que 8 bits no se dividen exactamente entre 3. El hexadecimal mantiene una relación exacta de dos dígitos por byte.
* **Conversión de decimal a hexadecimal**: Se divide el número entre 16; el cociente representa el primer dígito y el residuo el segundo.

### Ejemplos Clave
* **Origen del término byte en IBM**: Creado en 1956 durante el desarrollo de la supercomputadora Stretch. Se escribió con 'y' (*b-y-t-e*) para evitar confusiones accidentales con *bit*.
* **Colores RGB en HTML**: Cada píxel se forma mediante la mezcla de tres colores (Rojo, Verde, Azul), requiriendo 1 byte por color (3 bytes por píxel). `#E74536` representa `E7h` de rojo (231), `45h` de verde (69) y `36h` de azul (54).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Sistemas numéricos alternativos (Capítulo 10) y bits (Capítulo 11).
* **Relación futura**: Base para ASCII y Unicode (Capítulo 13), memoria RAM (Capítulo 19) e instrucciones de CPU (Capítulos 21 en adelante).

### Dudas y Aspectos a Verificar
* Las computadoras operan exclusivamente con voltajes binarios (0 y 1); la notación hexadecimal es una convención para facilitar la lectura humana.

## Capítulo 13: From ASCII to Unicode (De ASCII a Unicode)

### Idea Central
El capítulo explica la evolución técnica para representar caracteres de texto mediante códigos binarios: desde los códigos mecánicos de 5 bits (Baudot) y el estándar estadounidense de 7 bits (ASCII), pasando por extensiones de 8 bits y páginas de código incompatibles, hasta la creación de Unicode y el formato UTF-8.

### Conceptos Fundamentales
* **Código Baudot**: Sistema de 5 bits (32 combinaciones) de la década de 1870 que utilizaba códigos de cambio (*Letter Shift* y *Figure Shift*) para alternar entre letras y números.
* **ASCII**: Estándar de 7 bits (128 combinaciones) formalizado en 1967. Asigna un valor único a cada letra, dígito y signo de puntuación en inglés sin códigos de cambio, e incluye 33 caracteres de control.
* **Caracteres de control**: Códigos ASCII (00h al 1Fh) que representan instrucciones de formato e interacción mecánica (ej. *Carriage Return*, *Line Feed*, *Tab*).
* **ASCII extendido y Páginas de código**: Uso del octavo bit del byte (códigos 80h a FFh, alcanzando 256 valores) para incluir letras acentuadas regionales, generando variantes incompatibles entre sí.
* **Unicode**: Estándar universal desarrollado desde 1988 para codificar todos los caracteres del mundo (hasta U+10FFFF, permitiendo más de 1 millón de caracteres).
* **UTF-8**: Formato de codificación de longitud variable para Unicode que utiliza entre 1 y 4 bytes por carácter, 100% compatible hacia atrás con ASCII.

### Mecanismos y Procesos
* **Estructura de la tabla ASCII**:
  - Las letras mayúsculas (41h a 5Ah) y minúsculas (61h a 7Ah) difieren únicamente en el sexto bit (diferencia de 20h o 32 decimal), permitiendo convertir entre mayúsculas y minúsculas cambiando un solo bit.
  - Los dígitos '0' a '9' se ubican entre 30h y 39h, facilitando obtener su valor matemático restando 30h.
* **Codificación dinámica en UTF-8**:
  - Caracteres ASCII (U+0000 a U+007F): 1 byte con formato `0xxxxxxx`.
  - Caracteres acentuados/europeos (U+0080 a U+07FF): 2 bytes con formato `110xxxxx 10xxxxxx`.
  - Ideogramas (U+0800 a U+FFFF): 3 bytes con formato `1110xxxx 10xxxxxx 10xxxxxx`.
  - Emojis (U+10000 a U+10FFFF): 4 bytes con formato `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx`.

### Ejemplos Clave
* **El error Mojibake**: Ocurre cuando texto en UTF-8 (como la comilla `’` representada por `E2h 80h 99h`) se interpreta erróneamente mediante una página de 8 bits como Windows-1252, mostrando `â€™`.
* **EBCDIC en IBM**: Código de 8 bits derivado de tarjetas perforadas con huecos discontinuos en la secuencia de letras que complicaban la ordenación alfabética.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Byte de 8 bits y hexadecimal (Capítulo 12), Braille como código binario (Capítulo 3).
* **Relación futura**: Representación de texto en RAM antes de ser procesado por la CPU (Capítulos 19 y 21).

### Dudas y Aspectos a Verificar
* La diferencia entre *Big-Endian* y *Little-Endian* al almacenar valores de 16 bits exigió introducir la marca de orden de bytes (BOM: `U+FEFF`).
* Almacenar el número 12 como texto (códigos 31h y 32h) ocupa 2 bytes y no equivale al valor numérico binario `0Ch` (12 decimal).

## Capítulo 14: Adding with Logic Gates (Sumando con puertas lógicas)

### Idea Central
El capítulo detalla la construcción paso a paso de un circuito sumador aritmético de 8 bits (1 byte) utilizando únicamente puertas lógicas basadas en relés. Explica cómo la simplicidad de la suma binaria permite separar el cálculo del bit de suma (*Sum*) y del bit de acarreo (*Carry*), combinando semisumadores (*Half Adders*) y sumadores completos (*Full Adders*).

### Conceptos Fundamentales
* **Sumador de 1 bit**: Circuito básico que procesa dos entradas binarias y genera dos salidas: suma (*Sum*) y acarreo (*Carry*).
* **Puerta XOR (OR Excluyente)**: Puerta lógica cuyo resultado es 1 únicamente si las entradas son distintas. Coincide exactamente con la tabla de verdad del bit de suma.
* **Semisumador (Half Adder)**: Circuito compuesto por una puerta XOR (suma) y una puerta AND (acarreo). Suma dos bits pero no acepta acarreo previo.
* **Sumador Completo (Full Adder)**: Circuito formado por dos semisumadores y una puerta OR. Acepta tres entradas (A, B y Acarreo de Entrada / *Carry In*) y produce dos salidas (Suma y Acarreo de Salida / *Carry Out*).
* **Acarreo en cascada (Ripple Carry)**: Conexión donde la salida *Carry Out* de cada bit se conecta a la entrada *Carry In* del bit superior.

### Mecanismos y Procesos
* **Descomposición de la suma binaria**:
  - $0 + 0 = 00$
  - $0 + 1 = 01$
  - $1 + 0 = 01$
  - $1 + 1 = 10$ (suma 0, acarreo 1).
  - La columna de suma coincide con la función XOR; la de acarreo coincide con la función AND.
* **Construcción del Sumador de 8 Bits**:
  - Se interconectan 8 sumadores completos en serie (144 relés en total).
  - El *Carry In* del primer bit (Bit 0) se conecta a masa (0).
  - El *Carry Out* del octavo sumador (Bit 7) alimenta un noveno indicador luminoso para marcar el desbordamiento (sumas superiores a 255).

### Ejemplos Clave
* **Suma de dos bytes**: La suma binaria de `01100101` (101 decimal) y `10110110` (182 decimal) produce `100011011` (283 decimal), demostrando la propagación de acarreos.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Puertas lógicas (Capítulo 8), aritmética binaria (Capítulo 10) y circuito cerrado (Capítulo 4).
* **Relación futura**: Base de la Unidad Aritmético-Lógica (ALU, Capítulo 21) y restas por complemento a dos (Capítulo 16).

### Dudas y Aspectos a Verificar
* **Retardo de propagación (*Ripple carry delay*)**: El pulso de acarreo debe viajar secuencialmente a través de los 8 sumadores, introduciendo un retraso que en computadoras de alta velocidad se resuelve con generadores de acarreo anticipado.

## Capítulo 15: Is This for Real? (¿Es esto real?)

### Idea Central
Este capítulo responde a si las computadoras reales se construyen utilizando la misma lógica de circuitos vista anteriormente. Explica la evolución física desde relés y tubos de vacío hasta transistores de silicio y circuitos integrados, demostrando que aunque la velocidad y escala han cambiado, las reglas lógicas permanecen idénticas.

### Conceptos Fundamentales
* **Tubo de vacío (Vacuum tube)**: Dispositivo electrónico que conmuta corriente sin partes mecánicas móviles mediante calor en el vacío, aumentando la velocidad respecto al relé.
* **Transistor**: Dispositivo semiconductor de estado sólido que actúa como interruptor o amplificador, eliminando el desgaste mecánico y el exceso de calor.
* **Circuito Integrado / Chip**: Componente de silicio que empaqueta múltiples transistores, resistencias y conexiones en una sola pastilla diminuta.
* **Lógica Transistor-Transistor (TTL)**: Familia estándar de circuitos integrados (como la serie 7400) que integran puertas lógicas y sumadores en un solo encapsulado comercial.

### Mecanismos y Procesos
* **Evolución de la tecnología de conmutación**: Del relé físico (lento, desgaste mecánico) al tubo de vacío (rápido pero frágil y caliente), al transistor individual (pequeño, rápido y duradero) y al circuito integrado (millones de transistores fabricados simultáneamente sobre silicio).
* **Encapsulado comercial (Serie 7400 TTL)**: Los ingenieros usan chips estandarizados (como el 7408 para cuatro puertas AND o el 7483 para un sumador completo de 4 bits) en lugar de montar transistores individuales a mano.

### Ejemplos Clave
* **El manual TTL Data Book**: Catálogo de referencia usado por ingenieros con los esquemas de pines de chips reales.
* **Computadoras históricas**: Máquinas como la Complex Number Computer (relés) o ENIAC (tubos) demostraron la validez práctica de estos circuitos antes del silicio.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Sumador de 8 bits (Capítulo 14) y conmutación (Capítulos 7 y 8).
* **Relación futura**: Marco físico para la memoria RAM (Capítulo 19) y la ALU/CPU (Capítulos 21 y 22).

### Dudas y Aspectos a Verificar
* Aunque la lógica es idéntica, los problemas físicos han cambiado: de desgaste mecánico en relés a disipación térmica y límites cuánticos en transistores nanométricos.

## Capítulo 16: But What About Subtraction? (Pero ¿qué pasa con la resta?)

### Idea Central
El capítulo explica cómo realizar operaciones de resta utilizando exclusivamente circuitos de adición, eliminando la necesidad de implementar mecanismos complejos de préstamo (*borrow*). Muestra el uso de complementos matemáticos (complemento a 1 y a 2 en binario) y demuestra cómo la notación en complemento a dos permite representar enteros positivos y negativos.

### Conceptos Fundamentales
* **Préstamo (*Borrow*)**: Proceso mecánico tradicional de la resta donde una columna toma prestada una unidad de la columna izquierda, complejo de implementar en lógica digital.
* **Complemento a uno (Ones' complement)**: En binario, inversión completa de todos los bits de un número (cambiar 0 por 1 y 1 por 0), equivalente a pasar la señal por puertas NOT.
* **Complemento a dos (Two's complement)**: Estándar informático para representar números con signo. Se obtiene invirtiendo todos los bits (complemento a uno) y sumando 1 al resultado.
* **Bit de signo (Sign bit)**: El bit en la posición más significativa (extremo izquierdo); vale 0 para números positivos y 1 para negativos.
* **Desbordamiento de signo (*Overflow*)**: Condición errónea que ocurre cuando operar dos números positivos genera un bit de signo negativo (o viceversa), superando la capacidad de bits.

### Mecanismos y Procesos
* **Resta binaria con complemento a dos**:
  - Para restar B a A ($A - B$), se invierten los bits de B (complemento a 1).
  - Se introduce esa señal invertida en las entradas B del sumador.
  - Se activa el acarreo de entrada (*Carry In*) del primer bit a 1 (completando el complemento a 2).
  - El sumador realiza una suma convencional produciendo el resultado correcto de la resta.
* **Circuito sumador/restador de 8 bits**: Una línea de control *Subtract* se conecta a puertas XOR en la entrada B. Si *Subtract* = 0, el circuito realiza una suma directa. Si *Subtract* = 1, invierte los bits de B y pone *Carry In* = 1 para restar.

### Ejemplos Clave
* **Resta binaria real de 8 bits**: Restar 253 (`11111101`) menos 176 (`10110000`). El complemento a 1 de 176 es `01001111`. Sumar `11111101 + 01001111 + 1` produce `101001101`; descartar el noveno bit de acarreo deja `01001101` (77 decimal).
* **Rango de 8 bits con signo**: Desde `10000000` (-128) hasta `01111111` (+127).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Sumador de 8 bits (Capítulo 14) y propiedad de inversión de la puerta XOR (Capítulos 8 y 14).
* **Relación futura**: Mecanismo aritmético para instrucciones de resta, comparación y banderas de signo en la ALU (Capítulo 21).

### Dudas y Aspectos a Verificar
* La secuencia de bits `10110110` en memoria no indica por sí misma si es un número negativo (-74) o positivo (182); depende del contexto de interpretación de la CPU.

## Capítulo 17: Feedback and Flip-Flops (Retroalimentación y flip-flops)

### Idea Central
El capítulo introduce el concepto de retroalimentación (*feedback*), conectando la salida de un circuito a su propia entrada. Muestra cómo un inversor retroalimentado genera un oscilador (un reloj que cambia de estado automáticamente) y cómo la retroalimentación entre puertas NOR crea el *flip-flop* o cerrojo (*latch*), el primer circuito capaz de memorizar 1 bit de información.

### Conceptos Fundamentales
* **Retroalimentación (Feedback)**: Redirección de la señal de salida de un circuito hacia su origen como una de las entradas.
* **Oscilador (Oscillator / Clock)**: Circuito digital cuya salida alterna automáticamente entre 0 y 1 a un ritmo constante medido en hertzios (Hz).
* **Flip-Flop / Latch (Cerrojo)**: Circuito lógico con dos estados estables capaz de conservar 1 bit de información según el último impulso recibido.
* **Flip-Flop R-S (Reset-Set)**: El flip-flop elemental con dos puertas NOR cruzadas, con entradas *Set* (poner Q a 1) y *Reset* (poner Q a 0).
* **Flip-Flop D activado por flanco positivo (Positive edge-triggered D flip-flop)**: Circuito que captura el estado de la entrada *Data* exclusivamente en el instante exacto en que el reloj cambia de 0 a 1 (flanco de subida).
* **Divisor de frecuencia**: Configuración donde la salida Q negada de un flip-flop D se conecta a su entrada *Data*, reduciendo la frecuencia del reloj a la mitad.

### Mecanismos y Procesos
* **Oscilación por inversor**: Al conectar la salida de una puerta NOT a su entrada, la señal entra en bucle continuo entre 0 y 1 a una velocidad que depende del tiempo de propagación físico del componente.
* **Solución mediante disparo por flanco (*Edge-triggering*)**: En un cerrojo por nivel, si el reloj permanece en 1, cualquier cambio en los datos se propaga instantáneamente creando bucles no deseados. El disparo por flanco aísla la entrada para congelar el dato solo en la transición rápida de 0 a 1.
* **Contador binario**: Al encadenar $n$ flip-flops divisores de frecuencia, cada etapa divide la frecuencia por 2. Leyendo las salidas Q de derecha a izquierda, se genera una secuencia de conteo binario.

### Ejemplos Clave
* **El balancín o sube y baja**: Analogía física de las dos posiciones estables de un flip-flop, donde el sistema permanece en un extremo hasta que una fuerza externa lo empuja al otro.
* **El chip TTL 7474**: Circuito integrado estándar que empaqueta dos flip-flops tipo D activados por flanco positivo.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Puertas lógicas NOR, AND y NOT (Capítulo 8) y conteo binario (Capítulos 2 y 10).
* **Relación futura**: Componente celular para la memoria RAM (Capítulo 19), relojes digitales (Capítulo 18) y el contador de programa de la CPU.

### Dudas y Aspectos a Verificar
* Los relés mecánicos resultan demasiado lentos para usarse como osciladores de alta frecuencia; las computadoras reales emplean cristales de cuarzo.

## Capítulo 18: Let's Build a Clock! (¡Construyamos un reloj!)

### Idea Central
El capítulo aplica osciladores, flip-flops, contadores y puertas lógicas para diseñar un reloj digital funcional. Muestra cómo dividir frecuencias para obtener pulsos exactos de 1 segundo, cómo implementar contadores decimales codificados en binario (BCD) que se reinician al llegar a 9 o 59 y cómo adaptar el circuito al formato de 12 horas.

### Conceptos Fundamentales
* **Decimal Codificado en Binario (BCD - Binary-Coded Decimal)**: Esquema donde cada dígito decimal (0 al 9) se codifica independientemente mediante un grupo de 4 bits.
* **Oscilador de cristal de cuarzo**: Componente de alta precisión que vibra a frecuencias fijas (frecuentemente 32,768 Hz, equivalente a $2^{15}	ext{ Hz}$).
* **Contador Decimal / Década**: Circuito de 4 flip-flops modificado para reiniciar su conteo a 0000 al alcanzar el valor decimal 10 (1010 binario).
* **Decodificador BCD**: Red de puertas lógicas que convierte una cifra BCD de 4 bits en una salida individual activa entre 10 líneas para pantallas numéricas.

### Mecanismos y Procesos
* **División de frecuencia de 32,768 Hz a 1 Hz**: Encadenando 15 flip-flops divisores de frecuencia ($32,768 / 2^{15} = 1$), la frecuencia del cristal se reduce de forma exacta a un pulso de 1 segundo.
* **Estructura de conteo BCD**:
  - El dígito bajo de segundos usa 4 flip-flops. Una puerta AND detecta el valor 10 (1010 binario) y activa la entrada *Clear* para reiniciarlo a 0000, enviando un pulso al dígito alto.
  - El dígito alto de segundos usa 3 flip-flops para contar del 0 al 5, reiniciándose al alcanzar 6 (110 binario).
* **Lógica de 12 horas**: Reinicia las horas al alcanzar el valor 12 y utiliza una puerta NOR para forzar a que las pantallas muestren visualmente el número 12 cuando el contador indica 00:00:00.

### Ejemplos Clave
* **Estructura de las 6 cifras BCD**: Segundos bajos (0-9), segundos altos (0-5), minutos bajos (0-9), minutos altos (0-5), horas bajas (0-9), horas altas (0-1).
* **Pantallas de tubo Nixie**: Válvulas de cristal llenas de gas neón con filamentos metálicos en forma de números que se iluminan al recibir corriente.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Divisores de frecuencia y contadores (Capítulo 17), numeración BCD y decodificadores (Capítulo 10), propiedad de inversión XOR (Capítulo 14).
* **Relación futura**: Señales de sincronización (*clocks* de bus), decodificación de direcciones RAM (Capítulo 19) y temporización en la CPU (Capítulo 23).

### Dudas y Aspectos a Verificar
* Reiniciar flip-flops forzando las entradas *Clear* cuando se detecta el estado 1010 mediante puertas AND puede generar impulsos parásitos muy breves (*glitches*).

## Capítulo 19: An Assemblage of Memory (Un ensamblaje de memoria)

### Idea Central
El capítulo explica cómo combinar múltiples celdas de almacenamiento de 1 bit (basadas en latches) para construir arreglos de memoria de acceso aleatorio (RAM) direccionables. Muestra cómo decodificadores y selectores permiten leer y escribir bytes individuales en ubicaciones específicas, escalando desde celdas unitarias hasta bloques de 64 Kilobytes (64 KB).

### Conceptos Fundamentales
* **RAM (Random-Access Memory)**: Memoria de lectura/escritura donde se accede a cualquier dirección directamente en el mismo tiempo, sin recorrer las ubicaciones secuencialmente.
* **Dirección de Memoria (Memory Address)**: Número binario único asignado a cada celda o byte para especificar la posición a leer o escribir.
* **Decodificador de dirección**: Circuito digital que toma el bus de dirección y activa únicamente la línea correspondiente a esa posición específica.
* **Amortiguador Tri-Estado (Tri-State Buffer)**: Componente que adopta tres estados: nivel alto (1), nivel bajo (0) y alta impedancia (desconectado), permitiendo conectar múltiples salidas al mismo bus sin cortocircuitos.
* **SRAM frente a DRAM**: La RAM estática (SRAM) utiliza flip-flops que conservan el dato mientras reciban energía. La RAM dinámica (DRAM) usa un transistor y un condensador por celda, requiriendo refrescar la carga miles de veces por segundo.
* **Kilobyte (KB en informática)**: Unidad equivalente a 1,024 bytes ($2^{10}$ bytes) debido a la escala de potencias en base 2.

### Mecanismos y Procesos
* **Escalado de arreglos**:
  - Una celda de 1 bit combina entradas de datos (*Data In*), escritura (*Write*) y salida (*Data Out*).
  - Un arreglo de $8 	imes 1$ usa un decodificador de 3 a 8 para direccionar 8 bits mediante 3 bits de dirección.
  - Agrupando ocho arreglos de $8 	imes 1$ en paralelo se forma un arreglo de $8 	imes 8$ (8 bytes). Escalando con 16 bits de dirección se alcanzan $2^{16} = 65,536$ bytes (64 KB).
* **Control mediante conmutador Takeover**: Desconecta las líneas internas y conmuta el bus de dirección y datos a los interruptores manuales del operador para escribir instrucciones o examinar resultados.

### Ejemplos Clave
* **Analogía de los casilleros de correo**: Una RAM de 256 bytes equivale a una oficina postal con 256 casilleros numerados del 00h al FFh, donde cada casillero guarda un byte.
* **Equivalencia de $2^{16} = 65,536$ bytes a 64 KB**: Estándar habitual de las microcomputadoras de los años 80.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Latches y flip-flops tipo D (Capítulo 17), decodificadores de 3 a 8 (Capítulo 10) y potencias de 2 (Capítulo 2).
* **Relación futura**: Espacio físico donde se almacena el código del programa y datos que la CPU leerá secuencialmente mediante el contador de programa (Capítulos 20 a 22).

### Dudas y Aspectos a Verificar
* La distinción entre prefijos métricos (kilo = 1,000) y binarios (kilo = 1,024) generó la estandarización del término *kibibyte* (KiB).

## Capítulo 20: An Automated Computer (Una computadora automatizada)

### Idea Central
El capítulo muestra la transición desde una calculadora manual a una computadora automatizada capaz de ejecutar secuencias de instrucciones almacenadas en la memoria RAM. Explica cómo reemplazar la intervención humana conectando un contador de 16 bits que incrementa las direcciones de memoria secuencialmente, permitiendo que la máquina lea códigos de operación (*opcodes*) y datos para operar de forma autónoma.

### Conceptos Fundamentales
* **Acumulador (Accumulator)**: Registro de memoria intermedia donde se guarda el resultado temporal de una operación, sirviendo simultáneamente como entrada para la siguiente operación.
* **Código de operación / Opcode**: Valor numérico binario almacenado en memoria que indica a la máquina qué comando ejecutar (ej. sumar, restar, guardar o detenerse).
* **Código frente a Datos**: Los códigos (*opcodes*) son las instrucciones que controlan los circuitos; los datos son los valores numéricos sobre los que operan dichas instrucciones.
* **Contador de Dirección**: Circuito contador binario que suministra las direcciones secuenciales a la memoria RAM para avanzar a través del programa.

### Mecanismos y Procesos
* **Automatización del sumador**: Los números se guardan previamente en posiciones continuas de RAM. Un contador de 16 bits genera automáticamente las direcciones 0000h, 0001h, 0002h..., alimentando el sumador y guardando la suma en el acumulador.
* **Acumulador de tres bytes**:
  - Para operar con números de 3 bytes (-8,388,608 a +8,388,607), cada registro se descompone en 3 latches (*High*, *Mid*, *Low*).
  - Un decodificador 2 a 4 evalúa los 2 bits menos significativos de la dirección de memoria (A0 y A1) para identificar si la posición corresponde a un código de instrucción (00), byte bajo (01), medio (10) o alto (11).
* **Ciclo de opcodes**:
  - `02h` (*Add*): Suma el byte al acumulador.
  - `03h` (*Subtract*): Invierte la entrada mediante puertas XOR y pone a 1 el *Carry In* para restar por complemento a 2.
  - `04h` (*Write*): Habilita los búferes tri-estado del acumulador y envía la señal de escritura a RAM.
  - `08h` (*Halt*): Desactiva la puerta AND del oscilador para detener el reloj principal.

### Ejemplos Clave
* **Procesamiento contable en RAM**: Un programa que procesa depósitos y retiros en dólares almacenando opcodes seguidos de valores de 3 bytes: `02h 00h AFh C8h` (sumar \$450.00), `03h 00h 88h B8h` (restar \$350.00), `04h` (guardar saldo) y `08h` (detener).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Sumador de 8 bits (Capítulo 14), complemento a dos (Capítulo 16), flip-flops y contadores (Capítulo 17) y direccionamiento de RAM (Capítulo 19).
* **Relación futura**: Arquitectura directa para la CPU basada en el Intel 8080 desarrollada en los Capítulos 21 a 24.

### Dudas y Aspectos a Verificar
* Almacenar primero el byte menos significativo (*low byte*) seguido del más significativo (*high byte*) se conoce como formato *Little-Endian*.

## Capítulo 21: The Arithmetic Logic Unit (La Unidad Aritmético-Lógica)

### Idea Central
El capítulo explica el diseño y funcionamiento de la Unidad Aritmético-Lógica (ALU), el componente del procesador encargado de realizar operaciones matemáticas y lógicas sobre los datos. Muestra cómo extender un sumador para ejecutar sumas y restas con o sin acarreo/préstamo (*Carry/Borrow*), operaciones lógicas bit a bit (AND, OR, XOR) y comparaciones, guardando el estado mediante banderas (*flags*).

### Conceptos Fundamentales
* **Unidad Aritmético-Lógica (ALU)**: Componente principal de cálculo dentro de la CPU que ejecuta operaciones aritméticas y lógicas sobre bytes.
* **Operaciones bit a bit (Bitwise operations)**: Operaciones lógicas (AND, OR, XOR) aplicadas de manera independiente a cada par de bits homólogos en dos bytes.
* **Operación de comparación (Compare - CMP)**: Resta internamente un valor de otro para ajustar las banderas de la ALU sin modificar el contenido del acumulador.
* **Banderas de estado (Flags)**: Registros de 1 bit que preservan el resultado de la última operación: *Carry* (CY, acarreo/préstamo), *Zero* (Z, resultado cero) y *Sign* (S, bit más significativo en 1 que indica negativo).
* **Instrucciones inmediatas**: Instrucciones en código máquina donde el dato a operar sigue inmediatamente al código de operación en la RAM (ej. `ADI data`).

### Mecanismos y Procesos
* **Estructura funcional de la ALU (3 bits de control: F2, F1, F0)**:
  - 000 (Add), 001 (Add with Carry), 010 (Subtract), 011 (Subtract with Borrow), 100 (Bitwise AND), 101 (Bitwise XOR), 110 (Bitwise OR), 111 (Compare).
* **Operaciones bit a bit en ASCII**:
  - *Bitwise OR con 20h*: Fuerza el sexto bit a 1, convirtiendo letras mayúsculas ASCII en minúsculas.
  - *Bitwise AND con DFh*: Fuerza el sexto bit a 0, convirtiendo letras minúsculas ASCII en mayúsculas.
* **Generación de banderas**:
  - *Zero (Z)*: Una puerta NOR de 8 entradas evalúa los 8 bits de salida; produce un 1 si todos son 0.
  - *Sign (S)*: Copia el valor del bit más significativo (Bit 7).
  - *Carry (CY)*: Captura el acarreo producido por el sumador/restador.

### Ejemplos Clave
* **Conversión de texto mediante máscaras**: Aplicar `OR 20h` a la 'T' (54h) produce 't' (74h); aplicar `AND DFh` a 't' (74h) produce 'T' (54h).
* **Evaluación mediante AND**: Ejecutar `AND 20h` sobre un carácter ASCII para verificar si es minúscula (resultado 20h) o mayúscula (resultado 00h).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Sumador binario (Capítulo 14), complemento a dos (Capítulo 16), lógica booleana (Capítulos 6 y 8) y código ASCII (Capítulo 13).
* **Relación futura**: Bloque funcional de cálculo para combinarse con el arreglo de registros (Capítulo 22) y el decodificador de control de la CPU (Capítulo 23).

### Dudas y Aspectos a Verificar
* La ALU de 8 bits no realiza multiplicaciones ni divisiones directamente en hardware; deben implementarse mediante software por sumas, restas y desplazamientos repetidos.

## Capítulo 22: Registers and Busses (Registros y buses)

### Idea Central
El capítulo explica cómo se organizan y conectan los datos dentro del procesador mediante el uso de registros internos y buses compartidos. Muestra la arquitectura del arreglo de siete registros (A, B, C, D, E, H, L) del Intel 8080 y detalla cómo el bus de datos de 8 bits y el bus de direcciones de 16 bits mueven información de forma coordinada.

### Conceptos Fundamentales
* **Registro (Register)**: Latch interno de alta velocidad dentro de la CPU que guarda un byte temporalmente durante la ejecución.
* **Acumulador (Registro A)**: Registro principal de 8 bits de la CPU, entrada obligatoria para la ALU y destino automático de sus resultados.
* **Par de registros H y L (HL)**: Pareja de registros de 8 bits (H = *High byte*, L = *Low byte*) que pueden combinarse para formar una dirección de memoria de 16 bits ([HL] o M).
* **Direccionamiento indirecto**: Técnica donde una instrucción no incluye explícitamente la dirección de memoria, sino que consulta la dirección almacenada previamente en el par HL.
* **Bus de datos**: Vía de comunicación compartida de 8 bits por donde circulan bytes entre registros, ALU, RAM y latches de instrucción.
* **Bus de direcciones**: Vía compartida de 16 bits que transmite la dirección de memoria deseada desde el contador de programa o el par HL hacia la RAM.

### Mecanismos y Procesos
* **Selección de registros mediante códigos de 3 bits (DDD y SSS)**:
  - Códigos: 000 (B), 001 (C), 010 (D), 011 (E), 100 (H), 101 (L), 110 (Memoria [HL] o M), 111 (A).
  - En instrucciones `MOV destino, origen` (patrón `01 DDD SSS`), DDD activa la escritura en el registro destino y SSS activa la lectura en el origen.
* **Ciclo de latches de instrucción**:
  - *Instruction Latch 1*: Guarda el opcode.
  - *Instruction Latch 2*: Guarda datos inmediatos o el byte bajo de dirección.
  - *Instruction Latch 3*: Guarda el byte alto de dirección de 16 bits.

### Ejemplos Clave
* **Instrucción `MOV L, C` (`69h`)**: Copia el byte almacenado en C al registro L (patrón `01 101 001`). El valor de C permanece inalterado.
* **Carga/almacenamiento indirecto `MOV A, M` (`7Eh`) y `MOV M, A` (`77h`)**: Utilizan los valores guardados en H y L para leer de RAM o escribir en ella.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: RAM y direccionamiento (Capítulo 19), automatización mediante contadores (Capítulo 20), ALU (Capítulo 21) y búferes tri-estado (Capítulo 19).
* **Relación futura**: Estructura física orquestada por las señales de control de la CPU (Capítulos 23 y 24).

### Dudas y Aspectos a Verificar
* En la sintaxis `MOV destino, origen`, el registro que recibe la información se escribe a la izquierda y el origen a la derecha (`MOV L, C` copia C en L).

## Capítulo 23: CPU Control Signals (Señales de control de la CPU)

### Idea Central
El capítulo explica cómo las señales de control sincronizan los componentes de la CPU (ALU, banco de registros, contador de programa e incrementador) con la memoria RAM. Muestra cómo la CPU descompone la ejecución de cada código de operación en ciclos de máquina divididos entre etapas de lectura (*instruction fetch*), incremento de dirección y ejecución (*execute*).

### Conceptos Fundamentales
* **Señales de control**: Líneas eléctricas encargadas de abrir búferes tri-estado (poner valores en un bus) o activar entradas de reloj en latches (capturar valores desde un bus).
* **Búsqueda de instrucción (*Instruction fetch*)**: Fase inicial donde el contador de programa coloca su dirección en el bus de direcciones para leer el opcode desde RAM hacia el latch de instrucción.
* **Ciclo de máquina (*Machine cycle*)**: Impulsos de reloj discretos requeridos para recuperar e incrementar una instrucción o ejecutar una operación.
* **Decodificador de opcodes**: Red de decodificadores lógicos que interpreta el código de operación almacenado y genera las señales activas específicas para esa instrucción.

### Mecanismos y Procesos
* **Ejecución de una instrucción inmediata (`MVI A, 27h`)**:
  1. *Fetch 1*: El contador de programa (PC) coloca `0000h` en el bus de direcciones. La RAM entrega `3Eh` en el bus de datos, guardándose en el latch 1 y en el incrementador.
  2. *PC Increment*: El incrementador devuelve `0001h` al bus de direcciones y actualiza el PC.
  3. *Fetch 2*: Se lee el byte de dato `27h` desde RAM hacia el latch 2.
  4. *PC Increment*: Se actualiza el PC al valor `0002h`.
  5. *Execute*: Se habilita el latch 2 hacia el bus de datos y se activa el reloj del acumulador para guardar el dato.
* **Control de parada y reinicio (*Halt & Reset*)**: La señal *Reset* inicializa el PC a `0000h`. Al ejecutarse la instrucción `HLT`, un flip-flop de parada bloquea el oscilador principal, congelando el procesador.

### Ejemplos Clave
* **Programa de muestra de seis instrucciones**: `MVI A, 27h` $	o$ `MOV B, A` $	o$ `ADI 61h` $	o$ `ADD B` $	o$ `STA 000Ah` $	o$ `HLT`, ilustrando el intercambio coordinado de voltajes en los buses.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Arreglo de registros (Capítulo 22), ALU (Capítulo 21), búferes tri-estado y RAM (Capítulo 19) y tablas de verdad (Capítulos 8 y 10).
* **Relación futura**: Mecanismo físico necesario para modificar dinámicamente el contador de programa en las instrucciones de salto y subrutinas (Capítulo 24).

### Dudas y Aspectos a Verificar
* La arquitectura simplificada limita las instrucciones a un máximo de 3 bytes y 2 ciclos de ejecución. Procesadores comerciales reales implementan estados de espera (*Wait states*) o múltiples ciclos de acceso a memoria.

## Capítulo 24: Loops, Jumps, and Calls (Bucles, saltos y llamadas)

### Idea Central
El capítulo explica cómo alterar el flujo secuencial del contador de programa mediante instrucciones de salto (*Jump*), saltos condicionales y llamadas a subrutinas (*Call* y *Return*). Muestra cómo los saltos condicionales basados en las banderas de la ALU permiten construir bucles y estructuras de decisión (Turing completitud). Introduce la pila (*stack*) y el puntero de pila (*stack pointer*) para gestionar direcciones de retorno en subrutinas.

### Conceptos Fundamentales
* **Salto incondicional (`JMP`)**: Instrucción de 3 bytes que reemplaza directamente el valor del contador de programa (PC) por la dirección de 16 bits especificada en sus datos.
* **Salto condicional (`JZ`, `JNZ`, `JC`, `JNC`, `JP`, `JM`)**: Evalúa las banderas de la ALU (Zero, Carry, Sign) y modifica el PC únicamente si se cumple la condición.
* **Turing completitud**: Propiedad de un procesador o lenguaje que garantiza la capacidad de resolver cualquier problema de cálculo mediante operaciones aritméticas/lógicas y saltos condicionales.
* **Subrutina / Función**: Bloque de código independiente ejecutable desde diferentes puntos que devuelve el control al origen tras completar su tarea.
* **Llamada y Retorno (`CALL` y `RET`)**: `CALL` guarda la dirección de la siguiente instrucción en la pila y salta a la subrutina; `RET` recupera la dirección guardada en la pila y la carga en el PC.
* **Pila (*Stack*) y Puntero de Pila (*Stack Pointer - SP*)**: Área de RAM organizada como LIFO (*Last-In, First-Out*) administrada por un registro de 16 bits (SP) que decrece al guardar datos (*Push*) e incrementa al recuperarlos (*Pop*).

### Mecanismos y Procesos
* **Control de un bucle condicional**:
  - Se inicializan registros (ej. par HL con la dirección inicial y registro C con el número de iteraciones).
  - Tras procesar cada elemento, el contador C se decrementa (`SUI 1`).
  - La instrucción `JNZ Label` examina la bandera de Cero (*Zero flag*): si el resultado no es cero, fuerza al PC a volver al inicio del bucle; si es cero, continúa secuencialmente.
* **Gestión de la pila durante `CALL` y `RET`**:
  - Al ejecutar `CALL Subrutina` desde `0625h` (estando la siguiente instrucción en `0628h`):
    1. SP decrece a `FFFFh` y guarda el byte alto de retorno (`06h`).
    2. SP decrece a `FFFEh` y guarda el byte bajo de retorno (`28h`).
    3. El PC se actualiza con la dirección de la subrutina.
  - Al ejecutar `RET`:
    1. Se lee el byte bajo (`28h`) desde `FFFEh` y SP pasa a `FFFFh`.
    2. Se lee el byte alto (`06h`) desde `FFFFh` y SP pasa a `0000h`.
    3. Ambos bytes se cargan en el PC, reanudando la ejecución en `0628h`.

### Ejemplos Clave
* **La subrutina `ToAscii` y `Digit`**: Programa que toma un byte en el acumulador (ej. `5Bh`) y lo descompone en dos dígitos hexadecimales individuales, utilizando operaciones `ANI 0Fh`, rotaciones y comparaciones (`CPI 0Ah`) para convertirlos en caracteres ASCII (`'5'` = `35h` y `'B'` = `42h`).
* **Multiplicación por desplazamiento frente a fuerza bruta**: Demuestra cómo multiplicar dos bytes evaluando cada bit del multiplicador mediante máscaras `ANA E` y duplicando valores, reduciendo la operación de cientos de iteraciones a solo 8 pasos.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Banderas de estado de la ALU (Capítulo 21), contador de programa y registros de 16 bits (Capítulo 22) y ciclo de decodificación de instrucciones (Capítulo 23).
* **Relación futura**: Interrupciones de hardware por periféricos (Capítulo 25), sistemas operativos (Capítulo 26) y lenguajes de alto nivel (Capítulo 27).

### Dudas y Aspectos a Verificar
* Por simplicidad esquemática, el autor no implementa físicamente las instrucciones `CALL`, `RET`, `PUSH` y `POP` en el hardware dibujado en el libro, pero están totalmente operativas en el emulador en línea.

## Capítulo 25: Peripherals (Periféricos)

### Idea Central
El capítulo explica cómo la CPU interactúa con el mundo exterior mediante dispositivos periféricos de entrada y salida (I/O) como teclados, pantallas y almacenamiento. Muestra la diferencia entre entrada/salida mapeada en memoria (*memory-mapped I/O*) y por puertos (*port I/O*), y detalla cómo las interrupciones de hardware (*interrupts*) permiten a los periféricos solicitar atención inmediata a la CPU sin obligarla a realizar una espera activa (*polling*).

### Conceptos Fundamentales
* **Periféricos de Entrada/Salida**: Dispositivos externos a la CPU y memoria principal (teclados, monitores, discos) que introducen datos o muestran y almacenan resultados.
* **Entrada/Salida mapeada en memoria**: Técnica donde los registros de control y datos de un periférico se asignan a direcciones del espacio de memoria RAM.
* **Entrada/Salida por puertos**: Sistema que utiliza instrucciones especiales del procesador (como `IN` y `OUT`) y un espacio de direcciones separado para comunicarse con los periféricos sin ocupar memoria RAM.
* **Espera activa (*Polling*)**: Método donde la CPU ejecuta un bucle continuo consultando repetidamente el estado de un periférico hasta que está listo.
* **Interrupción de hardware (IRQ)**: Señal eléctrica enviada por un periférico a la CPU a través de una línea dedicada para pausar temporalmente el programa en ejecución y atender una tarea prioritaria.
* **Rutina de servicio de interrupción (ISR)**: Subrutina en memoria que la CPU ejecuta automáticamente al recibir una interrupción para procesar el evento del periférico y devolver el control al programa principal.
* **Memoria de video (Video RAM / Framebuffer)**: Bloque de RAM dedicado donde cada byte representa un carácter ASCII que una memoria ROM generadora de caracteres convierte en píxeles para el monitor.

### Mecanismos y Procesos
* **Procesamiento de una interrupción de hardware**:
  1. El periférico activa la línea física *Interrupt Request* (IRQ).
  2. La CPU completa la instrucción actual y guarda el contador de programa (PC) y las banderas en la pila (*Stack*).
  3. La CPU lee el número de vector de interrupción para obtener la dirección de inicio de la ISR.
  4. El PC salta a la ISR, la cual lee o escribe los datos del periférico.
  5. La ISR finaliza con la instrucción de retorno de interrupción, restaurando el PC desde la pila y reanudando la ejecución exactamente donde fue pausado.

### Ejemplos Clave
* **El teletipo (Teletype / TTY)**: Dispositivo electromecánico derivado de la telegrafía que combinaba un teclado mecánico y una impresora de papel continuo, utilizado como la primera interfaz de usuario.
* **El timbre de puerta frente a mirar por la ventana**: Analogía para comparar interrupciones con espera activa (*polling*). Mirar fijamente por la ventana es *polling* (consume todo el tiempo de la CPU); escuchar sonar el timbre mientras se lee un libro es una interrupción (permite hacer otro trabajo hasta que llega la señal).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Código ASCII (Capítulo 13), direccionamiento de RAM (Capítulo 19), instrucciones `CALL`/`RET` y la pila (Capítulo 24), señales de control de bus (Capítulo 23).
* **Relación futura**: Base de hardware necesaria para que el sistema operativo (Capítulo 26) gestione los controladores de dispositivos (*device drivers*).

### Dudas y Aspectos a Verificar
* La E/S mapeada en memoria reduce el espacio de direcciones RAM disponible para datos y programas; la E/S por puertos requiere instrucciones de arquitectura específicas (`IN` y `OUT`).

## Capítulo 26: The Operating System (El sistema operativo)

### Idea Central
El capítulo examina el papel del sistema operativo como la capa de software que abstrae la complejidad del hardware y administra los recursos de la computadora. Explica el proceso de arranque (*bootstrapping*), la gestión de archivos en almacenamiento secundario, las llamadas al sistema (*system calls*) y la transición desde sistemas monousuario como CP/M y MS-DOS hasta sistemas multitarea con protección de memoria.

### Conceptos Fundamentales
* **Sistema Operativo (OS)**: Software de control principal que actúa como intermediario entre las aplicaciones y el hardware, ofreciendo servicios de gestión de memoria, archivos y dispositivos.
* **Proceso de arranque (*Bootstrapping*)**: Secuencia en la que un programa en memoria ROM (BIOS) lee un sector de arranque desde el disco para cargar el sistema operativo en RAM.
* **Sistema de Archivos (File System)**: Estructura lógica (como FAT - *File Allocation Table*) que organiza y realiza el seguimiento de cómo se almacenan, nombran y recuperan archivos.
* **Tabla de asignación de archivos (FAT)**: Tabla indexada que mapea los sectores y clústeres físicos de un disco con los nombres de archivo, registrando las cadenas de bloques que componen cada archivo.
* **Llamada al sistema (System Call / API)**: Mecanismo por el cual una aplicación solicita al sistema operativo realizar una operación de hardware restringida (ej. leer un archivo o imprimir).
* **Protección de memoria (Kernel mode vs. User mode)**: Mecanismo que impide que las aplicaciones de usuario accedan directamente al hardware o modifiquen la memoria asignada a otros programas o al núcleo (*kernel*).

### Mecanismos y Procesos
* **El proceso de carga e inicio (*Booting*)**:
  1. Al encender la máquina, el contador de programa (PC) se inicializa en una dirección fija de memoria ROM donde reside el programa BIOS.
  2. El BIOS ejecuta la prueba de autodiagnóstico (*POST*) para verificar la RAM y los periféricos.
  3. El BIOS lee el primer sector del disco (Sector de arranque) y lo carga en RAM.
  4. El control se transfiere al sector de arranque, el cual localiza y carga en memoria los archivos principales del núcleo del sistema operativo.
* **Funcionamiento de la asignación de archivos en FAT**:
  - El disco se divide en bloques o clústeres numerados. El directorio almacena el nombre del archivo y el número del primer clúster.
  - La tabla FAT contiene una entrada para cada clúster que indica el número del siguiente clúster de la cadena o una marca de fin de archivo (*EOF*).

### Ejemplos Clave
* **CP/M (Control Program for Microcomputers)**: Sistema operativo pionero creado por Gary Kildall en 1974 para procesadores Intel 8080. Introdujo la separación entre el sistema de archivos (BDOS), la entrada/salida (BIOS) y las letras de unidad (`A:`, `B:`).
* **MS-DOS**: Sistema operativo para la IBM PC (1981), derivado de QDOS, que popularizó la estructura jerárquica de directorios (`C:\NOTAS\GITHUB`).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Interrupciones de hardware y periféricos (Capítulo 25), la pila y subrutinas (Capítulo 24) y memoria RAM de acceso directo (Capítulo 19).
* **Relación futura**: Plataforma sobre la cual se ejecutan lenguajes de programación de alto nivel, compiladores e intérpretes (Capítulos 27 y 28).

### Dudas y Aspectos a Verificar
* En MS-DOS, las aplicaciones podían eludir las llamadas al sistema operativo y escribir directamente en la memoria de video. En sistemas modernos, la protección de memoria prohíbe este acceso directo por razones de seguridad.

## Capítulo 27: Coding (Programación y lenguajes de alto nivel)

### Idea Central
El capítulo aborda la evolución del software desde la escritura manual de código máquina y lenguaje ensamblador hacia los lenguajes de programación de alto nivel (FORTRAN, COBOL, C y JavaScript) y el uso de compiladores e intérpretes. Detalla la estructura de JavaScript en el entorno web y analiza el estándar IEEE 754 para la aritmética de coma flotante.

### Conceptos Fundamentales
* **Lenguaje Ensamblador**: Lenguaje de programación de bajo nivel que sustituye los valores numéricos de las instrucciones por nemónicos legibles (`MOV`, `ADD`, `JMP`), manteniendo correspondencia de uno a uno con el código máquina.
* **Ensamblador y Parseo (*Assembler & Parsing*)**: El ensamblador es un programa que analiza (*parsing*) el código fuente en texto plano para traducirlo a ejecutable binario.
* **Lenguaje de alto nivel y Portabilidad**: Lenguajes que abstraen la arquitectura interna del procesador mediante expresiones algebraicas. Son portables porque el mismo código fuente puede compilarse para diferentes CPUs.
* **Compilador frente a Intérprete**: Un compilador traduce todo el código fuente de una vez produciendo un ejecutable independiente; un intérprete lee, analiza y ejecuta las instrucciones línea por línea en tiempo real.
* **Coma Flotante (*IEEE 754*)**: Estándar universal para almacenar números reales con decimales mediante notación científica binaria. Divide los bits en tres campos: bit de signo, exponente con sesgo (*bias*) y fracción de significando o mantisa.

### Mecanismos y Procesos
* **Estructura en Coma Flotante de Doble Precisión (64 bits, IEEE 754)**:
  - 1 bit para el signo (0 para positivo, 1 para negativo).
  - 11 bits para el exponente con un sesgo (*bias*) de 1023.
  - 52 bits para la fracción del significando (al asumir que el primer bit antes del punto binario siempre es 1, se logra una precisión efectiva de 53 bits, equivalente a unas 16 cifras decimales).
* **Causa de imprecisiones decimales**: Números decimales simples como 0.1 o 0.2 se convierten en fracciones binarias periódicas infinitas. Al ser almacenadas en un número finito de bits (53 bits), se produce un leve redondeo que ocasiona que operaciones como `55.2 * 27.8` devuelvan `1534.5600000000002`.

### Ejemplos Clave
* **El programa en ensamblador de CP/M**: Código que utiliza `LXI DE, Text`, prepara la llamada al sistema mediante `MVI C, 9` y ejecuta `CALL 5` para imprimir la cadena "Hello!$" en pantalla.
* **Criba de Eratóstenes en JavaScript**: Ejemplo práctico que utiliza un arreglo (*array*) de 10,000 valores booleanos y bucles anidados (`for`) para calcular y mostrar todos los números primos menores a 10,000.

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Opcodes y registros del Intel 8080 (Capítulos 21 a 24), código ASCII (Capítulo 13) y notación posicional binaria (Capítulos 9 y 10).
* **Relación futura**: Infraestructura de código que ejecuta la World Wide Web y motores de renderizado (Capítulo 28).

### Dudas y Aspectos a Verificar
* A pesar de que los compiladores optimizan el código, el problema de parada (*Halting problem*) demostrado por Alan Turing establece que es matemáticamente imposible escribir un programa general que verifique si otro programa funcionará de forma correcta sin errores.

## Capítulo 28: The World Brain (El cerebro mundial)

### Idea Central
El capítulo final recorre la evolución histórica de las ideas sobre la interconexión global de la información: desde el "Cerebro Mundial" de H. G. Wells y el "Memex" de Vannevar Bush hasta la invención del hipertexto por Ted Nelson y la creación de la World Wide Web por Tim Berners-Lee. Describe la infraestructura técnica de la red (protocolos HTTP/HTTPS, URLs, routers y paquetes TCP/IP) y demuestra cómo la combinación de hardware, sistemas operativos, navegadores y computación en la nube hace realidad el intercambio universal de conocimiento.

### Conceptos Fundamentales
* **Memex y Cerebro Mundial**: Visiones teóricas de mediados del siglo XX sobre dispositivos mecanizados capaces de almacenar libros y registros para consultarlos y vincularlos mediante asociaciones lógicas.
* **Hipertexto (*Hypertext*)**: Término acuñado por Ted Nelson en 1965 para definir bloques de texto e imágenes interconectados mediante enlaces dinámicos no lineales.
* **URL (Uniform Resource Locator)**: Cadena de texto estandarizada que identifica la ubicación única de un recurso en la red, compuesta por protocolo, nombre de dominio, directorio y archivo.
* **Protocolo HTTP / HTTPS**: Conjunto de reglas clientela/servidor que rigen el envío de solicitudes (*requests*) y la recepción de respuestas (*responses*) de documentos e imágenes web.
* **Enrutamiento de paquetes (*Packet switching & Routers*)**: Técnica donde la información digital se fragmenta en pequeños paquetes etiquetados con direcciones IP origen y destino, enviándose de forma independiente a través de nodos de red (*routers*).
* **Computación en la nube (*The Cloud*)**: Modelo donde el procesamiento y almacenamiento se desplazan hacia redes distribuidas de servidores de alta capacidad.

### Mecanismos y Procesos
* **Ciclo de carga e interacción de una página web**:
  1. El usuario introduce una URL en el navegador (cliente).
  2. El sistema resuelve el nombre de dominio en una dirección IP mediante servidores DNS.
  3. El cliente emite una solicitud HTTP *GET* a través de routers de red.
  4. El servidor procesa la petición y devuelve un paquete con la respuesta (código 200 OK y el archivo HTML, o código 404 si no existe).
  5. El motor del navegador parsea el HTML, descarga las hojas de estilo (CSS) e imágenes y ejecuta los scripts de JavaScript mediante compilación en tiempo real (JIT).
* **Renderizado y uso de memoria caché (*Caching*)**: El navegador almacena copias locales de recursos estáticos en memoria o disco del dispositivo, evitando descargarlos nuevamente en visitas posteriores.

### Ejemplos Clave
* **El Memex de Vannevar Bush (1945)**: Dispositivo concebido como un escritorio con pantallas translúcidas y botones capaz de proyectar microfilmes enlazados mediante un índice asociativo.
* **Anatomía de una URL**: La estructura del protocolo seguro (`https`), dominio (`www.CodeHiddenLanguage.com`), directorio (`Chapter27`) y archivo (`index.html`).

### Relaciones y Conocimientos Previos
* **Conocimientos previos**: Integra la totalidad de los temas del libro: bit binario (Capítulo 11), código ASCII/Unicode (Capítulo 13), arquitectura de la CPU (Capítulos 21 a 24), interrupciones y periféricos (Capítulo 25), sistema operativo (Capítulo 26) y programación en JavaScript (Capítulo 27).
* **Cierre conceptual**: Demuestra cómo todas las capas de abstracción (relés, puertas lógicas, suma binaria, memoria RAM, código máquina, compiladores y protocolos) se acoplan perfectamente para hacer funcionar la informática mundial contemporánea.

### Dudas y Aspectos a Verificar
* Diferencia conceptual entre Internet y la World Wide Web: Internet es la infraestructura física global de redes; la Web es uno de los servicios que se ejecutan sobre Internet utilizando documentos de hipertexto y HTTP.

## Diagrama de Capas de Abstracción
```text
[ Red Global e Hipertexto ]          --> WWW, HTTP, URLs, Routers (Capítulo 28)
              |
[ Software de Alto Nivel ]           --> JavaScript, C, Compiladores, IEEE 754 (Capítulo 27)
              |
[ Sistema Operativo y E/S ]          --> BIOS, Drivers, Interrupciones, FAT (Capítulos 25-26)
              |
[ Arquitectura de la CPU ]           --> Registros, ALU, Bus de Datos/Direcciones (Capítulos 21-24)
              |
[ Automatización y Memoria RAM ]     --> Memoria SRAM/DRAM, Contador de Programa (Capítulos 19-20)
              |
[ Aritmética y Flip-Flops ]          --> Sumadores, Complemento a 2, Latches (Capítulos 14, 16-18)
              |
[ Lógica y Conmutación ]             --> Puertas Lógicas (AND, OR, NOT, XOR), Relés (Capítulos 6-8, 15)
              |
[ Fundamentos Físicos ]              --> Circuitos, Ley de Ohm, Código Binario (Capítulos 1-5, 9-13)
```

## Desglose por Niveles de Abstracción

* **Nivel 1 — Fundamentos Físicos y Representación Binaria**: La información se transmite y codifica mediante estados discretos binarios. Conceptos clave: Código Morse, Braille, circuito cerrado, Ley de Ohm, potencias de 2, notación posicional, código ASCII, UTF-8 y notación Hexadecimal.
* **Nivel 2 — Conmutación Eléctrica y Lógica Booleana**: Las leyes del razonamiento lógico se implementan abriendo y cerrando caminos conductores. Conceptos clave: Álgebra booleana, puertas lógicas (AND, OR, NOT, NAND, NOR, XOR), tablas de verdad, relés electromagnéticos, tubos de vacío y transistores.
* **Nivel 3 — Aritmética Binaria y Memoria Elemental**: Las operaciones matemáticas y el almacenamiento surgen al combinar puertas lógicas y retroalimentación de señales. Conceptos clave: Semisumadores, sumadores completos, resta por complemento a dos, cerrojos, flip-flops tipo D, osciladores de reloj, contadores BCD.
* **Nivel 4 — Almacenamiento Estructurado y Automatización**: La ejecución se vuelve autónoma al guardar instrucciones y datos de forma conjunta en una memoria común direccionable. Conceptos clave: Direccionamiento de memoria RAM (SRAM/DRAM), decodificadores de dirección, búferes tri-estado, acumulador, contador de direcciones secuencial.
* **Nivel 5 — Unidad Central de Procesamiento (CPU)**: Un procesador orquesta el cómputo leyendo secuencialmente códigos de operación y ejecutándolos sobre registros. Conceptos clave: Unidad Aritmético-Lógica (ALU), banderas de estado (Zero, Carry, Sign), arreglo de registros (A, B, C, D, E, H, L), contador de programa (PC), puntero de pila (SP), saltos condicionales y llamadas a subrutinas (CALL/RET).
* **Nivel 6 — Periféricos y Gestión del Sistema**: La CPU se conecta con dispositivos externos y gestiona recursos mediante capas de software de control. Conceptos clave: E/S mapeada en memoria y por puertos, interrupciones de hardware (IRQ), memoria de video (VRAM), secuencia de arranque (Bootstrapping), tabla de asignación de archivos (FAT), llamadas al sistema (System Calls), protección de memoria.
* **Nivel 7 — Lenguajes de Programación de Alto Nivel**: La programación se independiza del hardware específico mediante lenguajes legibles por humanos traducidos automáticamente. Conceptos clave: Lenguaje ensamblador, compiladores, intérpretes, estructuras de control (if/while/for), formato de coma flotante (IEEE 754).
* **Nivel 8 — Redes Globales e Hipertexto**: La información se descentraliza e interconecta a través de una red mundial de comunicación en tiempo real. Conceptos clave: Direcciones IP, enrutamiento de paquetes (routers), URLs, protocolo HTTP/HTTPS, documentos HTML/CSS/JS, computación en la nube.