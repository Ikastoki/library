# Operating Systems Three Easy Pieces

## Índice

- [Resumen Ejecutivo y Mapa Conceptual de las Capas de Abstracción](#resumen-ejecutivo-y-mapa-conceptual-de-las-capas-de-abstracción)
- [A Dialogue on the Book](#a-dialogue-on-the-book)
- [Introduction to Operating Systems](#introduction-to-operating-systems)
- [A Dialogue on Virtualization](#a-dialogue-on-virtualization)
- [The Abstraction: The Process](#the-abstraction-the-process)
- [Interlude: Process API](#interlude-process-api)
- [Mechanism: Limited Direct Execution](#mechanism-limited-direct-execution)
- [Scheduling: Introduction](#scheduling-introduction)
- [Scheduling: The Multi-Level Feedback Queue](#scheduling-the-multi-level-feedback-queue)
- [Scheduling: Proportional Share](#scheduling-proportional-share)
- [Multiprocessor Scheduling (Advanced)](#multiprocessor-scheduling-advanced)
- [The Abstraction: Address Spaces](#the-abstraction-address-spaces)
- [Interlude: Memory API](#interlude-memory-api)
- [Mechanism: Address Translation](#mechanism-address-translation)
- [Segmentation](#segmentation)
- [Free-Space Management](#free-space-management)
- [Paging: Introduction](#paging-introduction)
- [Paging: Faster Translations (TLBs)](#paging-faster-translations-tlbs)
- [Paging: Smaller Tables](#paging-smaller-tables)
- [Beyond Physical Memory: Mechanisms](#beyond-physical-memory-mechanisms)
- [Beyond Physical Memory: Policies](#beyond-physical-memory-policies)
- [Complete Virtual Memory Systems](#complete-virtual-memory-systems)
- [Concurrency: An Introduction](#concurrency-an-introduction)
- [Interlude: Thread API](#interlude-thread-api)
- [Locks](#locks)
- [Lock-based Concurrent Data Structures](#lock-based-concurrent-data-structures)
- [Condition Variables](#condition-variables)
- [Semaphores](#semaphores)
- [Common Concurrency Problems](#common-concurrency-problems)
- [Event-based Concurrency (Advanced)](#event-based-concurrency-advanced)
- [I/O Devices](#io-devices)
- [Hard Disk Drives](#hard-disk-drives)
- [Redundant Arrays of Inexpensive Disks (RAIDs)](#redundant-arrays-of-inexpensive-disks-raids)
- [Interlude: Files and Directories](#interlude-files-and-directories)
- [File System Implementation](#file-system-implementation)
- [Locality and The Fast File System](#locality-and-the-fast-file-system)
- [Crash Consistency: FSCK and Journaling](#crash-consistency-fsck-and-journaling)
- [Log-structured File Systems](#log-structured-file-systems)
- [Flash-based SSDs](#flash-based-ssds)
- [Data Integrity and Protection](#data-integrity-and-protection)
- [Distributed Systems](#distributed-systems)
- [Sun’s Network File System (NFS)](#suns-network-file-system-nfs)
- [The Andrew File System (AFS)](#the-andrew-file-system-afs)

## Resumen Ejecutivo y Mapa Conceptual de las Capas de Abstracción

### Resumen Ejecutivo

*Sistemas Operativos: Tres Piezas Fáciles* (*Operating Systems: Three Easy Pieces - OSTEP*), escrito por Remzi H. Arpaci-Dusseau y Andrea C. Arpaci-Dusseau, articula la arquitectura y el funcionamiento de los sistemas operativos modernos a través de tres pilares fundamentales: **virtualización** (*virtualization*), **concurrencia** (*concurrency*) y **persistencia** (*persistence*), extendiéndose en su bloque avanzado hacia los **sistemas distribuidos** (*distributed systems*).

La tesis central de la obra establece que el sistema operativo actúa como un transformador de recursos físicos ruidosos, complejos y limitados (procesadores, memoria RAM, dispositivos de E/S) en abstracciones virtuales limpias, de alto rendimiento, seguras y fáciles de utilizar. Para lograr esta ilusión sin comprometer la velocidad nativa del hardware, el sistema operativo implementa el principio de **Ejecución Directa Limitada** (*Limited Direct Execution - LDE*), combinando mecanismos de bajo nivel (como tablas de trampas, conmutaciones de contexto e interrupciones de reloj) con políticas de alto nivel (algoritmos de planificación y políticas de reemplazo de páginas).

- **Virtualización (*Virtualization*)**: El sistema operativo crea la ilusión de que cada proceso posee un procesador dedicado (*virtual CPU*) y un espacio de direcciones privado y contiguo (*virtual memory*). Mediante el reparto de tiempo (*time sharing*) y la traducción de direcciones por hardware (MMU, TLB, tablas de páginas multinivel), se logra la ejecución eficiente y el aislamiento absoluto entre aplicaciones y respecto al núcleo (*kernel*).
- **Concurrencia (*Concurrency*)**: Al compartir el espacio de direcciones entre múltiples hilos de ejecución (*threads*), surgen condiciones de carrera (*race conditions*) derivadas del entrelazado no determinista de instrucciones en la CPU. Para preservar la corrección, el sistema operativo y el hardware proveen primitivas de sincronización atómicas (cerrojos/*locks*, variables de condición y semáforos) que garantizan la exclusión mutua y la coordinación de estados.
- **Persistencia (*Persistence*)**: La memoria volátil requiere dispositivos de E/S no volátiles (discos duros mecánicos y SSDs) y un sistema de archivos (*file system*) que mantenga la integridad de los datos de forma duradera. Mediante abstracciones de inodos, directorios, estructuras en log (*LFS*) y protocolos de consistencia ante fallos (*journaling*, *copy-on-write*), el sistema de archivos garantiza la recuperación ordenada ante interrupciones de energía.
- **Distribución (*Distribution*)**: Amplía la persistencia y el cómputo a redes de máquinas independientes que fallan de manera parcial. Utilizando llamadas a procedimiento remoto (*RPC*), protocolos de almacenamiento apátridas (*NFS*) o sistemas con caché completa y *callbacks* (*AFS*), se construye la ilusión de un servicio unificado y escalable.

---

### Mapa Conceptual de las Capas de Abstracción

El sistema operativo se estructura mediante una jerarquía de capas interconectadas donde cada nivel oculta la complejidad del hardware inferior y expone una abstracción superior simplificada.

```
+-----------------------------------------------------------------------+
|                         APLICACIONES DE USUARIO                       |
|         (Nivel de usuario / User Mode - Instrucciones no privilegiadas)   |
+-----------------------------------------------------------------------+
                                    |
                    Interfaz de Llamadas al Sistema
                 (System Calls / Trap Instructions / LDE)
                                    |
+-----------------------------------------------------------------------+
|                    NÚCLEO DEL SISTEMA OPERATIVO                        |
|        (Modo Núcleo / Kernel Mode - Control Total de Recursos)        |
|                                                                       |
|  1. Virtualización de CPU y Memoria                                    |
|     - Proceso (PCB / Estados / Time Sharing)                          |
|     - Espacio de Direcciones Virtual (VPN -> PFN)                      |
|     - Algoritmos de Planificación (MLFQ, CFS, Stride)                 |
|     - Gestión de Memoria (Paginación Multinivel, TLB, Swap)           |
|                                                                       |
|  2. Concurrencia y Sincronización                                     |
|     - Hilos (Threads / TCB)                                           |
|     - Primitivas: Mutex, Variables de Condición, Semáforos            |
|     - Bucle de Eventos y E/S Asíncrona                               |
|                                                                       |
|  3. Persistencia y Gestión de Almacenamiento                          |
|     - Sistema de Archivos (Inodos, Directorios, Bitmaps)             |
|     - Consistencia: Journaling, Copy-on-Write (COW), FSCK              |
|     - Capa Genérica de Bloques y Controladores (Device Drivers)       |
|                                                                       |
|  4. Capa Distribuida y Redes                                          |
|     - RPC (Stubs, Marshaling, XDR)                                    |
|     - Sistemas de Archivos Distribuidos (NFS, AFS)                    |
+-----------------------------------------------------------------------+
                                    |
                    Interfaz de Hardware y Privilegios
               (Instrucciones Privilegiadas / MMU / DMA)
                                    |
+-----------------------------------------------------------------------+
|                           HARDWARE FÍSICO                             |
|  - CPU Física (Modos Usuario/Kernel, Tabla de Trampas, Reloj)         |
|  - Unidad de Manejo de Memoria (MMU, TLB)                             |
|  - Memoria RAM Física                                                 |
|  - Dispositivos I/O y Almacenamiento (HDD, SSD, Controladores, DMA)   |
+-----------------------------------------------------------------------+
```

---

## A Dialogue on the Book

### Idea Central
Esta sección introduce la estructura fundamental del libro como un homenaje a las célebres lecturas de física de Richard Feynman (*Six Easy Pieces*). Plantea que el estudio de los sistemas operativos se organiza en torno a tres grandes ejes temáticos: virtualización (*virtualization*), concurrencia (*concurrency*) y persistencia (*persistence*). Además, establece que la mejor metodología para dominar la materia combina la comprensión conceptual con la práctica directa escribiendo código real y ejecutando proyectos en lenguaje C.

### Conceptos Clave
- **Virtualización (*Virtualization*)**: Técnica mediante la cual el sistema operativo transforma un recurso físico en una versión virtual más general, flexible y fácil de usar.
- **Concurrencia (*Concurrency*)**: Conjunto de problemas y soluciones que surgen cuando el sistema o una aplicación maneja múltiples tareas que se ejecutan simultáneamente en el mismo espacio de memoria.
- **Persistencia (*Persistence*)**: Capacidad de almacenar datos de manera duradera en dispositivos no volátiles para evitar su pérdida al apagar o reiniciar el sistema.
- **Diálogo (*Dialogue*)**: Método didáctico utilizado a lo largo del texto entre un profesor y un estudiante para presentar y revisar conceptos desde una perspectiva accesible y crítica.

### Mecanismos y Procesos
El capítulo detalla el proceso pedagógico recomendado para aprender la materia. Este proceso requiere asistir a clase para recibir la introducción conceptual, releer las notas de forma periódica para consolidar las ideas y realizar proyectos prácticos escribiendo código real en C. La interacción dialéctica descompone problemas complejos en preguntas esenciales (*crux of the problem*) antes de abordar su implementación técnica.

### Ejemplos e Ilustraciones
El autor utiliza la analogía directa con la obra de Richard Feynman *Six Easy Pieces*, sugiriendo que los sistemas operativos son aproximadamente la mitad de difíciles que la física, justificando así el título de "Tres piezas fáciles" (*Three Easy Pieces*).

### Conexión Lógica y Relevancia
Este capítulo funciona como el mapa conceptual de toda la obra. Establece la hoja de ruta dividida en tres pilares interconectados e introduce la filosofía de diseño e investigación que guiará el estudio de la arquitectura de sistemas.

---

## Introduction to Operating Systems

### Idea Central
El sistema operativo es una capa de software que actúa como intermediario entre el hardware y las aplicaciones, transformando recursos físicos complejos en abstracciones virtuales fáciles de usar. Su función primordial es gestionar los recursos del sistema (*CPU*, memoria y almacenamiento) de forma eficiente, justa y segura mediante mecanismos y políticas. A través de la virtualización, la concurrencia y la persistencia, el sistema operativo crea la ilusión de recursos dedicados e ilimitados para cada programa.

### Conceptos Clave
- **Modelo de Von Neumann (*Von Neumann Model*)**: Arquitectura básica de cómputo donde el procesador busca (*fetch*), decodifica (*decode*) y ejecuta (*execute*) instrucciones secuencialmente desde la memoria.
- **Virtualización (*Virtualization*)**: Transformación de un recurso físico (procesador, memoria o disco) en una abstracción virtual administrada por el sistema operativo.
- **Llamada al Sistema (*System Call*)**: Interfaz de programación (API) que permite a las aplicaciones solicitar servicios protegidos al núcleo del sistema operativo.
- **Modo Usuario (*User Mode*) vs. Modo Núcleo (*Kernel Mode*)**: Niveles de privilegio de hardware; el modo usuario restringe las operaciones directas sobre el hardware, mientras que el modo núcleo otorga acceso total al sistema.
- **Instrucción de Trampa (*Trap Instruction*)**: Instrucción especial de hardware que eleva el nivel de privilegio a modo núcleo y transfiere el control a un manejador predefinido.
- **Mecanismos (*Mechanisms*) vs. Políticas (*Policies*)**: Los mecanismos responden a *cómo* se realiza una función (como el cambio de contexto), mientras que las políticas determinan *cuál* decisión tomar (como qué proceso ejecutar a continuación).
- **Espacio de Direcciones (*Address Space*)**: Abstracción de memoria privada que el sistema operativo asigna a cada proceso para aislar sus instrucciones y datos.

### Mecanismos y Procesos
- **Virtualización de la CPU**: Mediante el reparto de tiempo (*time sharing*), el sistema operativo ejecuta un proceso durante un breve intervalo, se detiene y conmuta a otro, creando la ilusión de que existen múltiples procesadores independientes.
- **Virtualización de Memoria**: Cada programa accede a direcciones virtuales privadas. El sistema operativo, en coordinación con el hardware, traduce estas direcciones virtuales a direcciones físicas reales, aislando la memoria de cada proceso.
- **Transición de Privilegio mediante Llamadas al Sistema**: Cuando un programa requiere una operación restringida (como acceso a disco), ejecuta una trampa (*trap*). El hardware eleva el nivel a modo núcleo y salta al manejador de trampas (*trap handler*) configurado durante el arranque. Al finalizar, la instrucción `return-from-trap` restaura el modo usuario y regresa la ejecución al programa.
- **Garantía de Persistencia**: Para guardar datos de forma permanente, el sistema de archivos coordina protocolos de escritura como el registro en diario (*journaling*) o la copia en escritura (*copy-on-write*) para garantizar la recuperación ante fallos del sistema o cortes de energía.

### Ejemplos e Ilustraciones
- **Ejemplo `cpu.c`**: Código que imprime un texto en un bucle con retardos de un segundo; al ejecutar cuatro instancias simultáneas en un solo procesador físico, todas parecen avanzar en paralelo gracias a la virtualización de la CPU.
- **Ejemplo `mem.c`**: Programa que asigna memoria con `malloc()`; al ejecutar dos instancias concurrentes, ambas imprimen la misma dirección de memoria virtual pero modifican valores independientes, ilustrando el aislamiento del espacio de direcciones.
- **Ejemplo `io.c`**: Demuestra la persistencia mediante las llamadas `open()`, `write()` y `close()` para crear un archivo en disco compartible entre distintos procesos como editores y compiladores.

### Conexión Lógica y Relevancia
Este capítulo sienta las bases teóricas e históricas de toda la asignatura. Al presentar la evolución desde bibliotecas simples en sistemas por lotes (*batch processing*) hasta la separación estricta de modos de privilegio y la multiprogramación, explica las razones fundamentales detrás de la arquitectura moderna de los sistemas operativos.

---

## A Dialogue on Virtualization

### Idea Central
Esta sección introduce formalmente el pilar de la virtualización de la CPU. A través de un diálogo didáctico, se establece el objetivo central: transformar un único procesador físico en una ilusión de múltiples procesadores virtuales dedicados para cada aplicación en ejecución.

### Conceptos Clave
- **Virtualización de la CPU (*CPU Virtualization*)**: Ilusión creada por el sistema operativo mediante la cual cada proceso asume que posee un procesador dedicado.
- **Ilusión del Sistema (*System Illusion*)**: Abstracción generada por software y hardware para ocultar las limitaciones del hardware físico subyacente.

### Mecanismos y Procesos
El mecanismo conceptual presentado es el reparto de tiempo (*time sharing*), en el cual el sistema operativo asigna el procesador físico de forma alternada a distintas aplicaciones. Este intercambio rápido ocurre sin que los programas noten la interrupción, manteniendo la transparencia.

### Ejemplos e Ilustraciones
El profesor plantea el caso de un sistema con un solo procesador físico que ejecuta múltiples programas de forma transparente, permitiendo visualizar la brecha entre la realidad física (un único núcleo) y la abstracción virtual (múltiples procesadores virtuales).

### Conexión Lógica y Relevancia
Sirve como puente entre la visión panorámica de la arquitectura del sistema presentada en el Capítulo 2 y los detalles mecánicos específicos del proceso, la conmutación de contexto y las políticas de planificación que se desarrollan en las secciones posteriores.

---

## The Abstraction: The Process

### Idea Central
Un proceso es la abstracción fundamental que proporciona el sistema operativo para representar un programa en ejecución. El sistema operativo transforma un ejecutable estático almacenado en disco en una entidad dinámica cargada en memoria con su propio espacio de direcciones, estado de registros y recursos. Esta abstracción permite simular la presencia de múltiples procesadores dedicados mediante el reparto de tiempo de la CPU física.

### Conceptos Clave
- **Proceso (*Process*)**: Programa en estado de ejecución que combina el código, los datos en memoria, el estado de los registros y los recursos del sistema.
- **Espacio de Direcciones (*Address Space*)**: Rango de memoria física virtualizada accesible por un proceso, integrado por el código, datos estáticos, la pila (*stack*) y el montón (*heap*).
- **Contador de Programa (*Program Counter - PC*)**: Registro de la CPU que apunta a la dirección de memoria de la siguiente instrucción a ejecutar por el proceso.
- **Bloque de Control de Proceso (*Process Control Block - PCB*)**: Estructura de datos interna del núcleo (también llamada *task_struct* o *process descriptor*) que registra el estado completo, el identificador y el contexto de un proceso.
- **Estados del Proceso (*Process States*)**: Fases operativas de un proceso: *Running* (ejecutando instrucciones en la CPU), *Ready* (listo para ejecutar pero a la espera de asignación de CPU) y *Blocked* (suspendido a la espera de un evento de E/S o sincronización).
- **Estado Zombie (*Zombie State*)**: Estado final donde un proceso ha concluido su ejecución pero su entrada en el PCB permanece retenida para permitir al proceso padre consultar su código de salida.

### Mecanismos y Procesos
El ciclo de vida y creación de un proceso involucra las siguientes fases mecánicas:
1. **Carga (*Loading*)**: El sistema operativo lee los bytes del ejecutable desde el almacenamiento persistente (disco o SSD) y los traslada al espacio de direcciones en memoria física.
2. **Asignación de Memoria**: Se reserva e inicializa la pila de ejecución (*stack*) asignando los argumentos de la línea de comandos (`argc` y `argv`), y se configura la memoria de asignación dinámica (*heap*).
3. **Inicialización de E/S**: Se abren tres descriptores de archivo predeterminados para la entrada estándar (`stdin`), salida estándar (`stdout`) y error estándar (`stderr`).
4. **Punto de Entrada**: El sistema operativo transfiere el control de la CPU saltando a la rutina `main()`, cambiando el proceso al estado *Running*.
5. **Transición de Estados**: El planificador (*scheduler*) conmuta procesos entre *Ready* y *Running*. Cuando un proceso solicita E/S, pasa a *Blocked*; al completarse la operación de E/S, el hardware genera una interrupción que devuelve el proceso a *Ready*.

### Ejemplos e Ilustraciones
- **Estructura `struct proc` en xv6**: Muestra la implementación real en C de un PCB en un núcleo didáctico, detallando campos para los registros guardados (`context`), la pila del núcleo (`kstack`), el estado de ejecución (`enum proc_state`) y la tabla de archivos abiertos.
- **Traza de ejecución concurrente**: Un diagrama de tiempo que ejemplifica cómo dos procesos comparten la CPU cuando uno realiza operaciones de E/S; mientras el primer proceso se bloquea esperando al disco, el segundo aprovecha los ciclos de CPU en estado *Running*.

### Conexión Lógica y Relevancia
Este capítulo define la entidad básica sobre la cual opera la virtualización de la CPU. Establece las estructuras de datos e interfaces conceptuales necesarias para abordar la API de gestión de procesos y las técnicas de ejecución segura desarrolladas en las secciones posteriores.

---

## Interlude: Process API

### Idea Central
La interfaz de programación de aplicaciones (API) para la gestión de procesos en sistemas UNIX se caracteriza por el desacoplamiento intencional entre la creación de un proceso y la ejecución de un nuevo programa. A través de la combinación de las llamadas al sistema `fork()`, `exec()` y `wait()`, el sistema operativo otorga una interfaz flexible que permite a la shell y a las aplicaciones manipular el entorno de ejecución antes de lanzar nuevo código.

### Conceptos Clave
- **`fork()`**: Llamada al sistema que crea un proceso hijo casi idéntico al proceso invocador, duplicando su espacio de direcciones y contexto de registros.
- **Identificador de Proceso (*PID - Process ID*)**: Entero único asignado por el núcleo para hacer referencia y controlar un proceso activo en el sistema.
- **`wait()` / `waitpid()`**: Llamada al sistema que suspende la ejecución del proceso padre hasta que alguno (o uno específico) de sus procesos hijos haya finalizado.
- **`exec()`**: Familia de llamadas al sistema que reemplaza el código, la pila, el *heap* y los datos del proceso actual con la imagen de un ejecutable distinto.
- **Redirección de E/S (*I/O Redirection*)**: Técnica permitida por la separación entre `fork()` y `exec()`, donde un proceso modifica sus descriptores de archivos (como la salida estándar) antes de llamar a `exec()`.
- **Señales (*Signals*)**: Mecanismo de notificación asíncrona mediante el cual el sistema operativo o un usuario pueden enviar comandos de control (como `SIGINT` o `SIGKILL`) a un proceso o grupo de procesos.

### Mecanismos y Procesos
- **Mecanismo de Duplicación Diferenciada (`fork`)**: Al invocar `fork()`, el núcleo duplica el proceso. Desde el punto de retorno de la llamada, existen dos procesos activos: para el padre, `fork()` retorna el PID del hijo recién creado; para el hijo, retorna `0`.
- **Mecanismo de Reemplazo de Imagen (`exec`)**: Al llamar a una variante de `exec()`, el sistema operativo lee el nuevo ejecutable desde el disco, sobreescribe los segmentos de código y datos del proceso llamante, reinicializa la pila y el *heap*, y salta al punto de entrada del nuevo programa. Si la llamada es exitosa, nunca retorna al código anterior.
- **Flujo de Ejecución de la Shell**: La shell lee una línea de comandos, ejecuta `fork()` para crear un hijo, modifica los descriptores de archivo en el hijo si se solicitó redirección (`>` o `|`), invoca `exec()` para cargar el comando escrito y ejecuta `wait()` en el padre para bloquear la shell hasta la conclusión del hijo.

### Ejemplos e Ilustraciones
- **Código de Redirección `p4.c`**: Muestra cómo el proceso hijo cierra la salida estándar (`STDOUT_FILENO`), abre un archivo en disco (asignándole el descriptor `1` por ser el entero libre más bajo) y luego ejecuta `execvp("wc", ...)`; el programa `wc` escribe su resultado directamente en el archivo sin saber que su salida estándar fue redirigida.
- **Uso de Tuberías (*Pipes*)**: El ejemplo de la línea de comandos `grep -o foo file | wc -l`, donde la salida de un proceso se conecta a la entrada de otro mediante el descriptor de archivo de una tubería en memoria gestionada por el núcleo.

### Conexión Lógica y Relevancia
Esta sección transforma la abstracción teórica del proceso en una herramienta práctica. Ilustra cómo la ortogonalidad de la API de UNIX permite construir flujos de trabajo complejos y herramientas avanzadas de sistema sin necesidad de agregar complejidad adicional dentro del núcleo.

---

## Mechanism: Limited Direct Execution

### Idea Central
La Ejecución Directa Limitada (*Limited Direct Execution - LDE*) es el mecanismo fundamental que permite virtualizar la CPU manteniendo alto rendimiento y control estricto. Consiste en ejecutar el código de las aplicaciones directamente sobre el hardware a velocidad nativa, mientras que el hardware y el sistema operativo colaboran mediante niveles de privilegio, interrupciones y trampas para evitar que los procesos no autorizados monopolicen la máquina o accedan a recursos protegidos.

### Conceptos Clave
- **Ejecución Directa Limitada (*Limited Direct Execution - LDE*)**: Protocolo de control donde los programas se ejecutan directamente en la CPU física pero bajo límites impuestos por la arquitectura de hardware y el núcleo.
- **Modo Usuario (*User Mode*) vs. Modo Núcleo (*Kernel Mode*)**: Modos de ejecución del procesador; el modo usuario prohíbe instrucciones privileged y acceso directo a dispositivos; el modo núcleo posee control absoluto sobre el hardware.
- **Instrucción de Trampa (*Trap Instruction*)**: Instrucción especial de hardware que eleva el nivel de privilegio a modo núcleo y transfiere el control a una dirección prefijada en el sistema operativo.
- **Tabla de Trampas (*Trap Table*)**: Estructura en memoria configurada por el núcleo durante el arranque donde se registran las direcciones de los manejadores de excepciones, llamadas al sistema e interrupciones.
- **Interrupción de Reloj (*Timer Interrupt*)**: Dispositivo de hardware programado para generar una interrupción periódica cada cierto número de milisegundos, devolviendo el control de la CPU al sistema operativo de forma no cooperativa.
- **Conmutación de Contexto (*Context Switch*)**: Operación de bajo nivel en ensamblador que guarda los registros de la CPU del proceso actual en su estructura del núcleo y carga los registros guardados del nuevo proceso objetivo.

### Mecanismos y Procesos
- **Fase de Inicialización (*Boot Time*)**: En modo núcleo, el sistema operativo configura la tabla de trampas e informa al hardware la ubicación de sus manejadores de interrupción (*trap handlers*). Posteriormente inicia el temporizador del reloj y conmuta a modo usuario mediante una instrucción `return-from-trap`.
- **Atención a Llamadas al Sistema**: Cuando un proceso requiere una operación restringida, ejecuta una instrucción `trap`. El hardware guarda los registros de usuario (PC, pila) en la pila del núcleo del proceso (*kernel stack*), cambia a modo núcleo y salta al manejador registrado. El SO procesa la solicitud y ejecuta `return-from-trap` para restaurar los registros y volver a modo usuario.
- **Recuperación del Control y Cambio de Contexto**: Para evitar que un proceso en bucle infinito bloquee el sistema (enfoque no cooperativo), la interrupción de reloj fuerza el salto al núcleo. Si el planificador decide conmutar del proceso A al proceso B:
  1. El hardware guarda los registros de modo usuario de A en su pila del núcleo.
  2. El SO ejecuta la rutina `swtch()`, guardando los registros de modo núcleo de A en su PCB y cargando los de B.
  3. El SO cambia el puntero de la pila física al de la pila del núcleo de B.
  4. La instrucción `return-from-trap` restaura los registros de modo usuario de B y reanuda su ejecución.

### Ejemplos e Ilustraciones
- **Analogía del "A prueba de bebés" (*Baby Proofing*)**: El autor compara la configuración del sistema operativo en el arranque con preparar una habitación para un niño pequeño: se aseguran los enchufes y gabinetes peligrosos (tabla de trampas y modos de privilegio) para luego dejar que el niño (el proceso) corra libremente sin riesgo de destruir el entorno.
- **Código Ensamblador `swtch` de xv6**: Muestra la rutina x86 exacta que extrae los punteros de las estructuras de contexto de ambos procesos, guarda los registros `%ebx`, `%ecx`, `%ebp`, etc., intercambia el puntero de la pila `%esp` y ejecuta `ret` para retornar en el contexto del nuevo proceso.

### Conexión Lógica y Relevancia
Este capítulo resuelve el problema de cómo ejecutar código a velocidad de hardware sin ceder el control de la máquina. La Ejecución Directa Limitada sirve como el cimiento operativo sobre el cual se construyen los algoritmos y políticas de planificación de CPU que se analizarán en los capítulos siguientes.

---

## Scheduling: Introduction

### Idea Central
Introduce los principios e hipótesis fundamentales para el diseño de políticas de planificación de la CPU mediante el análisis de métricas como el tiempo de retorno (*turnaround time*) y el tiempo de respuesta (*response time*). Evalúa algoritmos clásicos como FIFO, SJF, STCF y Round Robin, demostrando la tensión intrínseca entre la optimización del rendimiento global de los trabajos y la interactividad del sistema.

### Conceptos Clave
- **Carga de Trabajo (*Workload*)**: Conjunto de suposiciones sobre las características de los procesos que se ejecutan en el sistema, tales como tiempo de ejecución, momentos de llegada y operaciones de entrada/salida (E/S).
- **Métrica de Planificación (*Scheduling Metric*)**: Criterio cuantitativo utilizado para evaluar y comparar el desempeño de distintas políticas de planificación.
- **Tiempo de Retorno (*Turnaround Time*)**: Métrica de rendimiento definida como el tiempo en que un trabajo finaliza menos el tiempo en que llegó al sistema ($T_{	ext{turnaround}} = T_{	ext{completion}} - T_{	ext{arrival}}$).
- **Efecto Convoy (*Convoy Effect*)**: Fenómeno en el que múltiples procesos cortos o ligeros quedan bloqueados en la cola de espera detrás de un proceso extenso que monopoliza un recurso pesado.
- **Shortest Job First (SJF)**: Algoritmo de planificación no expulsivo (*non-preemptive*) que selecciona y ejecuta primero el trabajo que posee la menor duración estimada.
- **Shortest Time-to-Completion First (STCF)**: Algoritmo expulsivo (*preemptive*) que, ante la llegada de un nuevo trabajo, evalúa cuál de los procesos activos tiene el menor tiempo restante de ejecución y le asigna la CPU.
- **Tiempo de Respuesta (*Response Time*)**: Métrica de interactividad definida como el tiempo transcurrido desde la llegada del proceso hasta la primera vez que es atendido por la CPU ($T_{	ext{response}} = T_{	ext{firstrun}} - T_{	ext{arrival}}$).
- **Round Robin (RR)**: Algoritmo expulsivo que asigna la CPU a cada proceso por una fracción fija de tiempo llamada rodaja de tiempo (*time slice* o *quantum*), alternando cíclicamente entre los procesos en la cola de listos.
- **Amortización (*Amortization*)**: Técnica de ingeniería de sistemas que incrementa la duración del *time slice* para reducir el costo relativo del cambio de contexto y la limpieza de caché frente al tiempo de ejecución útil.

### Mecanismos y Procesos
- **Evolución de las Suposiciones de Carga**: Se parte de supuestos simplificados (duración idéntica y conocida, llegada simultánea, ejecución pura en CPU) y se relajan gradualmente para construir algoritmos realistas.
- **Manejo de E/S mediante Solapamiento (*Overlap*)**: Cuando un proceso inicia una solicitud de E/S, cambia al estado *Blocked*, liberando la CPU. El planificador trata cada ráfaga de CPU (*CPU burst*) como un subtrabajo independiente, permitiendo que otro proceso use la CPU mientras el dispositivo físico procesa la E/S, maximizando la utilización general del hardware.
- **Compromiso del *Time Slice* en RR**: Un *quantum* extremadamente corto mejora el tiempo de respuesta pero incrementa el costo overhead por conmutación de contexto; un *quantum* demasiado largo degrada la respuesta interactiva acercando el comportamiento a FIFO.

### Ejemplos e Ilustraciones
- **Analogía de la Fila del Supermercado**: El autor compara el algoritmo SJF con las cajas expresas de "10 artículos o menos" en una tienda, donde atender primero a clientes con pocos productos reduce el tiempo medio de espera de toda la fila en comparación con atender a clientes con carros llenos (efecto convoy).
- **Tratamiento de Ráfagas de E/S**: El trabajo A ejecuta ráfagas de 10 ms alternadas con operaciones de E/S de 10 ms, mientras que el trabajo B utiliza la CPU continuamente por 50 ms. Tratar a cada sub-ráfaga de A como un trabajo corto permite que A interrumpa a B, manteniendo la CPU y el disco ocupados simultáneamente de forma eficiente.

### Conexión Lógica y Relevancia
Conecta los mecanismos de bajo nivel (conmutación de contexto e interrupciones de reloj del Capítulo 6) con la toma de decisiones de alto nivel. Demuestra la imposibilidad teórica de lograr una planificación óptima de tiempo de retorno sin conocimiento previo del futuro, justificando la necesidad de algoritmos adaptativos.

---

## Scheduling: The Multi-Level Feedback Queue

### Idea Central
La Cola de Retroalimentación Multinivel (*Multi-Level Feedback Queue - MLFQ*) es un algoritmo de planificación adaptativo que utiliza el comportamiento histórico de los procesos para predecir su conducta futura. Su objetivo es optimizar simultáneamente el tiempo de retorno para trabajos extensos intensivos en CPU y el tiempo de respuesta para tareas interactivas, operando sin conocimiento *a priori* sobre la duración de los programas.

### Conceptos Clave
- **Cola de Retroalimentación Multinivel (*MLFQ*)**: Algoritmo estructurado en múltiples colas, cada una asignada con un nivel de prioridad distinto, que ajusta dinámicamente la posición de un proceso según sus ráfagas de ejecución y E/S.
- **Asignación de Tiempo (*Allotment*)**: Cantidad total de tiempo de CPU que un proceso puede consumir en un nivel de prioridad determinado antes de que el planificador reduzca su prioridad a una cola inferior.
- **Inanición (*Starvation*)**: Condición en la cual los procesos de baja prioridad son privados de tiempo de CPU de forma indefinida debido a la presencia constante de procesos en colas de mayor prioridad.
- **Engañar al Planificador (*Gaming the Scheduler*)**: Vulnerabilidad donde un programa diseñado maliciosamente cede voluntariamente la CPU justo antes de agotar su asignación de tiempo para mantener su prioridad alta artificialmente.
- **Impulso de Prioridad (*Priority Boost*)**: Mecanismo periódico que reubica todos los procesos del sistema en la cola de máxima prioridad para prevenir la inanición y reevaluar procesos cuya naturaleza haya cambiado.
- **Constante Voodoo (*Voo-doo Constant*)**: Parámetros de configuración del sistema (como el periodo de *boost* $S$) cuyos valores no derivan de fórmulas matemáticas directas y requieren ajuste empírico (*Ousterhout's Law*).

### Mecanismos y Procesos
- **Reglas Fundamentales de MLFQ**:
  - **Regla 1**: Si Prioridad(A) > Prioridad(B), A se ejecuta (B no).
  - **Regla 2**: Si Prioridad(A) = Prioridad(B), A y B se ejecutan en Round Robin usando el *time slice* de dicha cola.
  - **Regla 3**: Cuando un proceso entra al sistema, se ubica en la cola de mayor prioridad.
  - **Regla 4**: Una vez que un proceso consume su asignación de tiempo (*allotment*) en un nivel dado (sin importar cuántas veces haya cedido voluntariamente la CPU), su prioridad disminuye un nivel.
  - **Regla 5**: Transcurrido un intervalo de tiempo $S$, el sistema mueve todos los procesos a la cola superior (*priority boost*).
- **Adaptación y Aprendizaje Dinámico**: Un proceso nuevo inicia con la suposición de que es un trabajo corto. Si utiliza la CPU intensivamente, consume su asignación y desciende progresivamente hacia colas inferiores de menor prioridad pero con rodajas de tiempo (*quanta*) más largas. Si el proceso realiza E/S frecuente (interactivo), permanece en las colas superiores.

### Ejemplos e Ilustraciones
- **Ataque por Falsificación de E/S**: Ilustra cómo bajo reglas primitivas (que reiniciaban el contador de tiempo tras cualquier E/S), un programa que ejecuta el 99% de su *time slice* e emite una E/S ficticia permanece indefinidamente en la cola superior, monopolizando casi el 99% del procesador.
- **Configuración TS en Solaris**: Ejemplifica una implementación industrial con 60 colas de prioridad donde la cola de máxima prioridad usa un *time slice* de 20 ms y la de menor prioridad utiliza varios cientos de milisegundos, realizando impulsos de prioridad aproximadamente cada segundo.

### Conexión Lógica y Relevancia
Resuelve la limitación de los algoritmos teóricos introducidos en el Capítulo 7 al eliminar la necesidad de conocer la duración futura de los programas. MLFQ constituye la base de los planificadores reales en sistemas operativos como Solaris, BSD y versiones históricas de Windows y Linux.

---

## Scheduling: Proportional Share

### Idea Central
La planificación de reparto proporcional (*proportional-share* o *fair-share*) se enfoca en garantizar que cada proceso reciba un porcentaje determinado de los recursos de la CPU en lugar de optimizar únicamente el tiempo de respuesta o de retorno. Presenta modelos probabilísticos como la planificación por lotería (*lottery scheduling*), enfoques deterministas como la planificación por zancadas (*stride scheduling*), y la arquitectura eficiente del Completely Fair Scheduler (CFS) de Linux.

### Conceptos Clave
- **Tiquetes (*Tickets*)**: Mecanismo abstracto que representa la proporción o porcentaje relativo de un recurso del sistema al que tiene derecho un proceso o usuario.
- **Moneda de Tiquetes (*Ticket Currency*)**: Abstracción que permite a un usuario o grupo asignar tiquetes en unidades locales entre sus propios procesos, las cuales el sistema convierte automáticamente a la moneda global.
- **Transferencia e Inflación de Tiquetes (*Ticket Transfer / Inflation*)**: Mecanismos para ceder tiquetes temporalmente (como en una relación cliente-servidor) o alterar dinámicamente la cantidad de tiquetes propia en entornos de procesos de absoluta confianza.
- **Planificación por Zancada (*Stride Scheduling*)**: Algoritmo determinista de reparto proporcional donde cada proceso posee una zancada (*stride*) inversamente proporcional a sus tiquetes y un contador de pases (*pass value*) que rastrea su progreso global.
- **Completely Fair Scheduler (CFS)**: Planificador de Linux de alto rendimiento que divide la CPU de manera equitativa midiendo el tiempo de ejecución virtual de los procesos.
- **Tiempo de Ejecución Virtual (*vruntime*)**: Contador mantenido por CFS que registra el tiempo físico de CPU consumido por un proceso, escalado inversamente según el peso (*nice*) asignado al programa.
- **Árbol Rojo-Negro (*Red-Black Tree*)**: Estructura de datos equilibrada de búsqueda con complejidad $O(\log N)$ utilizada por CFS para seleccionar de forma eficiente el proceso con el menor *vruntime*.

### Mecanismos y Procesos
- **Mecanismo de Selección por Lotería**: En cada intervalo de planificación, el núcleo genera un número pseudoaleatorio entre 0 y el total de tiquetes del sistema. Se recorre la lista de procesos sumando sus tiquetes a un contador acumulativo; el primer proceso que hace que el contador supere el número ganador obtiene la CPU.
- **Algoritmo de Stride Scheduling**: La zancada se calcula dividiendo una constante grande entre el número de tiquetes del proceso. El planificador selecciona siempre el proceso con el *pass value* más bajo. Al finalizar su ejecución, se incrementa su *pass value* sumándole su *stride*.
- **Operación del Completely Fair Scheduler (CFS)**:
  1. CFS calcula dinámicamente el *time slice* dividiendo un intervalo objetivo (*sched latency*, ej. 48 ms) entre el número de procesos activos. Para evitar un exceso de conmutaciones de contexto con cargas elevadas, impone un límite inferior (*min granularity*, ej. 6 ms).
  2. Ajusta la proporción de CPU mediante valores `nice` (de -20 a +19), traduciéndolos a pesos (*weights*) que modifican la velocidad a la que acumulan *vruntime*.
  3. Cuando un proceso despierta tras dormir (E/S), su *vruntime* se ajusta al valor mínimo presente en el árbol rojo-negro para evitar que monopolice la CPU al intentar "recuperar" el tiempo perdido.

### Ejemplos e Ilustraciones
- **Estudio de Equidad Probabilística**: Demuestra mediante simulaciones que la equidad ($F = T_{	ext{completitud1}} / T_{	ext{completitud2}}$) de la lotería oscila ampliamente en ejecuciones cortas, alcanzando el reparto exacto ($F = 1.0$) únicamente a medida que el número de rodajas de tiempo crece de forma estadísticamente significativa.
- **Traza de Stride Scheduling**: Tres procesos A, B y C con 100, 50 y 250 tiquetes obtienen *strides* de 100, 200 y 40. Partiendo con *pass* igual a 0, C se ejecuta 5 veces, A 2 veces y B 1 vez, logrando proporciones exactas al cabo de cada ciclo determinista.

### Conexión Lógica y Relevancia
Concluye el análisis de políticas de planificación para un único procesador. Transiciona del paradigma de optimización por comportamiento (MLFQ) hacia la asignación garantizada de recursos por porcentajes, preparando los conceptos necesarios para abordar la planificación multiprocesador y la gestión de memoria virtual.

---

## Multiprocessor Scheduling (Advanced)

### Idea Central
La planificación multiprocesador expande las políticas de CPU a entornos con múltiples núcleos o procesadores físicos que comparten la memoria principal. El reto fundamental consiste en gestionar la coherencia de las cachés de hardware, preservar la afinidad de caché (*cache affinity*) y mitigar el desacoplamiento de rendimiento derivado de la sincronización y el desbalance de carga (*load imbalance*). Para solucionar esto, los sistemas emplean arquitecturas de cola única (SQMS) o múltiples colas (MQMS) junto con técnicas avanzadas como la migración de tareas y el robo de trabajo (*work stealing*).

### Conceptos Clave
- **Coherencia de Caché (*Cache Coherence*)**: Protocolo de hardware que garantiza que las escrituras en memoria realizadas por un procesador sean visibles para todos los demás núcleos, evitando que lean datos desactualizados (*stale data*).
- **Inspección de Bus (*Bus Snooping*)**: Técnica donde las cachés monitorean constantemente las transacciones del bus de memoria para invalidar o actualizar copias locales cuando un dato es modificado por otra CPU.
- **Afinidad de Caché (*Cache Affinity*)**: Tendencia y preferencia de planificar un proceso en la misma CPU donde se ejecutó anteriormente para aprovechar los datos y traducciones aún presentes en sus cachés locales.
- **SQMS (*Single-Queue Multiprocessor Scheduling*)**: Enfoque de planificación que utiliza una única cola global compartida de procesos para todos los procesadores del sistema.
- **MQMS (*Multi-Queue Multiprocessor Scheduling*)**: Enfoque de planificación que asigna una cola independiente de procesos a cada CPU o núcleo individual.
- **Desbalance de Carga (*Load Imbalance*)**: Situación en sistemas MQMS donde una CPU queda ociosa o con pocos procesos mientras otra se encuentra saturada de trabajo.
- **Robo de Trabajo (*Work Stealing*)**: Algoritmo de migración donde una cola con pocos o ningún proceso examina periódicamente las colas de otras CPUs para tomar tareas y equilibrar la carga del sistema.

### Mecanismos y Procesos
- **Mecanismo de SQMS**: Cada procesador libre toma el siguiente trabajo disponible de la cola global. Aunque simplifica la asignación, requiere bloqueos de sincronización (*locks*) severos que degradan la escalabilidad a medida que aumenta el número de CPUs, y destruye la afinidad de caché al mover los procesos continuamente entre núcleos.
- **Mecanismo de MQMS**: Los procesos se asignan a una cola específica al ingresar al sistema. Esto escala de manera eficiente y preserva intrínsecamente la afinidad de caché, pero exige mecanismos de migración activa.
- **Proceso de Migración y Trabajo Robado**: Cuando finalizan tareas y se produce un desbalance, el núcleo ejecuta rutinas de migración continua o *work stealing*. Una CPU ociosa consulta con una frecuencia regulada las colas vecinas; si la diferencia de carga supera un umbral, transfiere un proceso a su cola local.

### Ejemplos e Ilustraciones
- **Análisis de Schedulers en Linux**: El capítulo repasa las tres filosofías de planificadores históricos en Linux: el planificador $O(1)$ y CFS (*Completely Fair Scheduler*), que emplean esquemas de múltiples colas (MQMS), frente al planificador BFS (*Brain Fuck Scheduler*), que utiliza con éxito una única cola global (SQMS) basada en EEVDF para evitar la complejidad del balanceo de carga.
- **Analogía del Robo de Trabajo**: Un procesador actúa como un trabajador en una línea de ensamblaje que, al terminar sus tareas locales, toma piezas de la bandeja de su compañero saturado para mantener la línea operando a máxima capacidad.

### Conexión Lógica y Relevancia
Concluye el bloque dedicado a la virtualización de la CPU y la planificación. Establece el puente directo hacia la sección de concurrencia al demostrar cómo las limitaciones físicas del hardware multiprocesador exigen primitivas de sincronización estrictas (*locks*) tanto a nivel de hardware como de software.

---

## The Abstraction: Address Spaces

### Idea Central
El espacio de direcciones es la abstracción fundamental de la memoria física que el sistema operativo proporciona a cada proceso en ejecución. A través de la virtualización de memoria, el sistema crea la ilusión transparente de que cada programa posee un espacio privado, continuo y de gran tamaño, aislando completamente a los procesos entre sí y protegiendo el núcleo del sistema.

### Conceptos Clave
- **Espacio de Direcciones (*Address Space*)**: Abstracción que abarca todo el estado de memoria accesible por un programa en ejecución, compuesto tradicionalmente por código, *heap* y *stack*.
- **Transparencia (*Transparency*)**: Propiedad por la cual la aplicación no percibe que la memoria está siendo virtualizada, operando como si dispusiera de la memoria física real desde la dirección cero.
- **Aislamiento y Protección (*Protection and Isolation*)**: Garantía arquitectónica de que ningún proceso puede leer ni modificar la memoria privada de otro proceso o del núcleo del sistema operativo.
- **Fragmentación Interna (*Internal Fragmentation*)**: Desperdicio de espacio dentro de una unidad de memoria asignada que ha sido reservada pero no está siendo utilizada por la aplicación.
- **Dirección Virtual (*Virtual Address*)**: Dirección de memoria generada por el programa que el hardware y el sistema operativo traducen a una dirección física real.

### Mecanismos y Procesos
- **Estructura del Espacio de Direcciones**: El código del programa se ubica en la parte superior (direcciones bajas, estáticas). El *heap* se posiciona justo debajo del código y crece hacia abajo (direcciones más altas) al solicitar memoria dinámica. La pila (*stack*) se sitúa en el extremo inferior (direcciones virtuales más altas) y crece hacia arriba (direcciones menores) durante llamadas a funciones.
- **Proceso de Traducción e Interposición**: Cada instrucción enviada por la CPU que hace referencia a memoria pasa por la Unidad de Manejo de Memoria (*MMU*). La MMU interpone la dirección virtual y la convierte dinámicamente en una dirección física en el módulo de memoria RAM.

### Ejemplos e Ilustraciones
- **Demostración `va.c`**: Código en C que imprime las direcciones del puntero a `main()` (código), el retorno de `malloc()` (heap) y una variable local (`stack`), comprobando visualmente cómo el código y el *heap* residen en direcciones bajas mientras la pila se ubica cerca del límite superior del espacio virtual de 64 bits.
- **Evolución Histórica**: Se contrapone los primeros sistemas monousuario (donde el programa compartía memoria física directamente con el SO) con la multiprogramación moderna, donde múltiples programas residen simultáneamente en RAM y requieren fronteras de protección estrictas.

### Conexión Lógica y Relevancia
Representa la puerta de entrada oficial al segundo gran pilar del libro: la virtualización de la memoria. Sienta la necesidad conceptual de crear la ilusión de memoria privada antes de explorar los mecanismos de traducción de direcciones por hardware (módulos base/límite, segmentación y paginación).

---

## Interlude: Memory API

### Idea Central
Presenta la interfaz de programación de aplicaciones (API) de gestión de memoria en entornos UNIX y lenguaje C, enfocándose en las funciones `malloc()` y `free()`. Explica la diferencia entre la memoria automática administrada en la pila (*stack*) y la memoria dinámica explícita en el montón (*heap*), detallando los errores de programación más comunes y las llamadas al sistema subyacentes que sustentan estas librerías.

### Conceptos Clave
- **Memoria de Pila (*Stack / Automatic Memory*)**: Memoria reservada e hiper-eficiente gestionada implícitamente por el compilador para variables locales y marcos de llamadas a funciones.
- **Memoria de Montón (*Heap Memory*)**: Espacio de asignación dinámica cuya vida útil es controlada explícitamente por el programador mediante llamadas a funciones de librería.
- **`malloc()`**: Función de la librería estándar de C (`stdlib.h`) que reserva un bloque contiguo de bytes en el *heap* y devuelve un puntero de tipo `void*` (o `NULL` en caso de fallo).
- **`free()`**: Función que libera la memoria previamente reservada en el *heap*, tomando como único parámetro el puntero devuelto por `malloc()`.
- **Fuga de Memoria (*Memory Leak*)**: Error donde la memoria dinámica asignada no se libera tras dejar de utilizarse, provocando el agotamiento paulatino de los recursos del sistema.
- **Puntero Colgante (*Dangling Pointer*)**: Condición peligrosa que ocurre al acceder o liberar memoria que ya ha sido devuelta o reasignada.
- **`brk` / `sbrk`**: Llamadas al sistema de bajo nivel utilizadas por la librería de asignación de memoria para mover el límite (*break*) del *heap* dentro del espacio de direcciones.

### Mecanismos y Procesos
- **Asignación en `malloc`**: El usuario pasa la cantidad de bytes requerida (generalmente usando el operador `sizeof()`). La librería calcula el tamaño total incluyendo una cabecera (*header*) oculta que registra el tamaño de la asignación y metadatos de control.
- **Desasignación en `free`**: Cuando se invoca `free(ptr)`, la librería realiza aritmética de punteros retrocediendo el tamaño de la cabecera para determinar cuántos bytes debe incorporar de nuevo a la lista de espacio libre (*free list*).
- **Soporte del Sistema Operativo**: La librería `malloc` administra el espacio virtual dentro del proceso. Si el *heap* se queda sin espacio, invoca la llamada al sistema `sbrk` o utiliza `mmap()` para solicitar nuevas páginas anónimas al núcleo del sistema operativo.

### Ejemplos e Ilustraciones
- **Error del `strlen` + 1**: Muestra el fallo clásico al asignar memoria para cadenas de texto (`malloc(strlen(s))`), omitiendo el byte adicional necesario para el carácter nulo de terminación (`null`), lo que genera un desbordamiento de búfer (*buffer overflow*).
- **Cabecera Oculta (*Header Block*)**: Ilustra gráficamente cómo un bloque asignado de 20 bytes en realidad ocupa 28 bytes en memoria física, debido a los 8 bytes iniciales donde la librería guarda el entero con el tamaño y la marca mágica (*magic number*).

### Conexión Lógica y Relevancia
Conecta las abstracciones teóricas del espacio de direcciones con la práctica directa de desarrollo de software en C. Establece los cimientos sobre cómo las aplicaciones solicitan memoria antes de estudiar los algoritmos internos de gestión de espacio libre (*Free-Space Management*) y traducción de direcciones.

---

## Mechanism: Address Translation

### Idea Central
La traducción de direcciones mediante hardware (*hardware-based address translation*) es la técnica fundamental que permite virtualizar la memoria de forma eficiente y segura. El hardware transforma dinámicamente cada dirección virtual generada por el programa en una dirección física en la RAM en tiempo de ejecución. Esta interposición garantiza la transparencia para las aplicaciones y permite que el sistema operativo mantenga el control absoluto sobre qué regiones de memoria física puede acceder cada proceso.

### Conceptos Clave
- **Traducción de Direcciones (*Address Translation*)**: Proceso mediante el cual el hardware transforma una dirección virtual generada por una instrucción en una dirección física real en la memoria principal.
- **Relocalización Dinámica (*Dynamic Relocation / Base and Bounds*)**: Mecanismo basado en registros del procesador donde un registro base desplaza las direcciones virtuales y un registro límite (*bounds* o *limit*) verifica que las direcciones permanezcan dentro de los márgenes permitidos.
- **Registro Base (*Base Register*)**: Registro de hardware que almacena la dirección física de inicio donde se encuentra cargado el espacio de direcciones de un proceso.
- **Registro Límite (*Bounds / Limit Register*)**: Registro de hardware que almacena el tamaño del espacio de direcciones (o la dirección física final) para evitar accesos fuera de rango.
- **Unidad de Manejo de Memoria (*MMU - Memory Management Unit*)**: Componente del procesador encargado de realizar la traducción de direcciones e imponer los chequeos de límites por hardware.
- **Lista de Espacio Libre (*Free List*)**: Estructura de datos utilizada por el sistema operativo para rastrear qué zonas de la memoria física no están siendo utilizadas y pueden asignarse a nuevos procesos.
- **Fragmentación Interna (*Internal Fragmentation*)**: Desperdicio de memoria física que ocurre cuando se asigna a un proceso un bloque de tamaño fijo mayor que el espacio que realmente utiliza.

### Mecanismos y Procesos
- **Cálculo de la Dirección Física**: Para cada acceso a memoria (búsqueda de instrucción, carga o almacenamiento de datos), la MMU ejecuta la traducción mediante la fórmula: $	ext{Dirección Física} = 	ext{Dirección Virtual} + 	ext{Base}$.
- **Chequeo de Módulos Límite**: Antes de sumar la base, el hardware verifica que $0 \le 	ext{Dirección Virtual} < 	ext{Límite}$. Si la dirección virtual es negativa o mayor o igual al límite, la CPU genera una excepción por acceso ilegal (*out-of-bounds exception*).
- **Intervención del Sistema Operativo en Eventos Clave**:
  1. *Creación de procesos*: El SO busca un espacio libre en la *free list* y marca el bloque como ocupado.
  2. *Finalización de procesos*: El SO recupera la memoria del proceso y la devuelve a la *free list*.
  3. *Conmutación de contexto*: El SO guarda los valores de los registros base y límite del proceso actual en su PCB y carga los del nuevo proceso a ejecutar.
  4. *Manejo de excepciones*: El hardware cambia a modo núcleo y salta al manejador de excepciones del SO cuando ocurre un acceso fuera de límites, finalizando el proceso infractor.

### Ejemplos e Ilustraciones
- **Traza de Instrucción de Incremento**: Para un proceso cargado en la dirección física 32 KB con un límite de 16 KB, si ejecuta una instrucción en la dirección virtual 128 que lee una variable en la dirección virtual 15 KB:
  - Búsqueda de instrucción: $128 + 32	ext{ KB} = 32896$ en memoria física.
  - Carga de datos: $15	ext{ KB} + 32	ext{ KB} = 47	ext{ KB}$ en memoria física.
- **Ejemplo de Traducción**: Un espacio de direcciones de 4 KB cargado en la dirección física 16 KB traduce la dirección virtual `0` a `16 KB`, la `1024` a `17 KB`, y la `4400` causa un fallo (*fault*) por superar el límite de 4 KB.

### Conexión Lógica y Relevancia
Aplica el principio de Ejecución Directa Limitada (LDE) a la gestión de memoria. Constituye el mecanismo básico de virtualización de memoria, pero revela la ineficiencia de requerir bloques contiguos rígidos, lo que provoca desperdicio de espacio (*fragmentación interna*) y motiva la aparición de la segmentación.

---

## Segmentation

### Idea Central
La segmentación es una generalización del esquema de base y límites que divide el espacio de direcciones de un proceso en segmentos lógicos independientes (como código, *heap* y pila). Esto permite colocar cada segmento en ubicaciones separadas de la memoria física, evitando reservar espacio para el hueco no utilizado entre el *heap* y la pila (*sparse address space*). Sin embargo, al manejar segmentos de tamaño variable, surge el problema de la fragmentación externa en la memoria física.

### Conceptos Clave
- **Segmentación (*Segmentation*)**: Técnica de virtualización de memoria que asigna un par de registros base/límite independiente a cada segmento lógico del programa (código, *heap*, *stack*).
- **Segmento (*Segment*)**: Porción contigua del espacio de direcciones de una longitud determinada asociada a una función lógica específica.
- **Segmentación de Grano Grueso (*Coarse-grained Segmentation*)**: Enfoque que divide el espacio de direcciones en unos pocos segmentos grandes y predefinidos (código, *heap*, pila).
- **Segmentación de Grano Fino (*Fine-grained Segmentation*)**: Enfoque más flexible que soporta miles de pequeños segmentos mediante una tabla de segmentos en memoria.
- **Fragmentación Externa (*External Fragmentation*)**: Dispersión de la memoria física libre en pequeños huecos no contiguos que imposibilitan satisfacer solicitudes de asignación grandes, a pesar de haber suficiente memoria libre total.
- **Compactación de Memoria (*Memory Compaction*)**: Proceso mediante el cual el SO detiene la ejecución de procesos y copia sus segmentos para reagrupar la memoria libre en un único bloque contiguo.
- **Fallo de Segmentación (*Segmentation Fault / Violation*)**: Excepción lanzada por el hardware cuando un programa intenta acceder a una dirección fuera de los límites válidos de un segmento o violando sus permisos.

### Mecanismos y Procesos
- **Identificación de Segmento y Desplazamiento (*Offset*)**:
  - *Enfoque explícito*: Se reservan los bits superiores de la dirección virtual para identificar el segmento (ej. `00` para código, `01` para *heap*, `11` para pila) y los bits inferiores determinan el desplazamiento (*offset*).
  - *Enfoque implícito*: El hardware deduce el segmento según el origen de la dirección (si proviene del PC es código, si proviene del SP es pila, cualquier otro es *heap*).
- **Cálculo con Crecimiento Negativo (Pila)**: Como la pila crece hacia direcciones menores, el hardware utiliza un bit adicional para indicar la dirección de crecimiento. El desplazamiento negativo se obtiene restando el tamaño máximo del segmento al *offset* virtual ($	ext{Offset Negativo} = 	ext{Offset Virtual} - 	ext{Tamaño Máximo}$). La dirección física resultante es $	ext{Base} + 	ext{Offset Negativo}$.
- **Bits de Protección y Compartición**: Cada segmento incluye bits de permisos (Lectura/Escritura/Ejecución). Segmentos como el de código se marcan como *Read-Execute*, permitiendo que múltiples procesos compartan el mismo segmento físico de código de forma segura.

### Ejemplos e Ilustraciones
- **Traducción de Dirección en el Heap**: En un espacio de direcciones de 14 bits con páginas de 4 KB, la dirección virtual `4200` (`01 0000 0110 1000` en binario) usa los bits `01` para el *heap*. El *offset* es $4200 - 4096 = 104$. Sumando la base del *heap* (34 KB), la dirección física resultante es $34	ext{ KB} + 104 = 34920$.
- **Memoria No Compactada vs. Compactada**: Un sistema con 24 KB libres distribuidos en tres huecos no contiguos de 8 KB no puede satisfacer una solicitud de un segmento de 20 KB. Tras la compactación, los segmentos activos se mueven juntos dejando un único bloque contiguo de 24 KB.

### Conexión Lógica y Relevancia
Resuelve la ineficiencia de fragmentación interna del modelo base/límite único al acomodar espacios de direcciones dispersos (*sparse address spaces*). Sin embargo, introduce la fragmentación externa debido a los tamaños variables de los segmentos, preparando la transición lógica hacia la paginación (*paging*).

---

## Free-Space Management

### Idea Central
La gestión del espacio libre aborda cómo administrar regiones de memoria asignadas dinámicamente en unidades de tamaño variable, ya sea en las librerías de usuario (`malloc`/`free`) o en el sistema operativo al gestionar la memoria física con segmentación. El objetivo principal es construir un asignador rápido que minimice la fragmentación externa mediante estrategias de selección y mecanismos de división (*splitting*), coalescencia (*coalescing*) y cabeceras (*headers*).

### Conceptos Clave
- **Lista Libre (*Free List*)**: Estructura de datos integrada en el espacio gestionado que registra todos los bloques de memoria física o virtual actualmente no asignados.
- **División (*Splitting*)**: Proceso por el cual el asignador satisface una solicitud pequeña tomando un bloque libre más grande, dividiéndolo en dos partes: la requerida y el residuo libre restante.
- **Coalescencia / Fusión (*Coalescing*)**: Proceso de combinar bloques libres adyacentes en la memoria en un único bloque contiguo más grande al momento de liberar memoria.
- **Cabecera (*Header*)**: Bloque de metadatos ubicado inmediatamente antes de la región de memoria entregada al usuario que almacena el tamaño del bloque asignado y un número mágico para verificación.
- **Listas Segregadas (*Segregated Lists / Slab Allocator*)**: Técnica que mantiene listas independientes para tamaños de objetos populares o frecuentes, acelerando la asignación y evitando la fragmentación.
- **Asignador de Compañeros (*Binary Buddy Allocator*)**: Algoritmo de gestión donde el espacio se divide recursivamente a la mitad en potencias de 2, simplificando la coalescencia mediante aritmética de bits entre direcciones "compañeras".

### Mecanismos y Procesos
- **Estructura Interna del Asignador (`malloc` / `free`)**:
  - Al solicitar $N$ bytes con `malloc(N)`, el asignador busca un bloque libre de tamaño $N + 	ext{sizeof(header\_t)}$.
  - Modifica el puntero devuelto al usuario para que apunte justo después de la cabecera.
  - Al llamar a `free(ptr)`, el asignador resta el tamaño de la cabecera a `ptr` (`(header_t*)ptr - 1`), extrae el tamaño real asignado y reintegra todo el bloque a la *free list*, fusionando con vecinos si están libres.
- **Estrategias Básicas de Selección**:
  - **Best Fit**: Examina toda la lista y elige el bloque libre más pequeño que sea capaz de albergar la solicitud. Minimiza el espacio desperdiciado por bloque pero deja pequeños residuos y requiere búsqueda exhaustiva.
  - **Worst Fit**: Examina toda la lista y elige el bloque libre más grande. Pretende dejar residuos grandes aprovechables, pero muestra un rendimiento pobre en la práctica.
  - **First Fit**: Selecciona el primer bloque libre en la lista que sea lo suficientemente grande. Es rápido al evitar búsquedas completas, pero tiende a acumular pequeños residuos al principio de la lista.
  - **Next Fit**: Similar a First Fit, pero mantiene un puntero a la última posición consultada para distribuir las búsquedas de forma uniforme a lo largo de la lista.

### Ejemplos e Ilustraciones
- **Mapeo de Bloque con Cabecera**: Un usuario solicita 20 bytes mediante `ptr = malloc(20)`. Si la cabecera ocupa 8 bytes (tamaño + número mágico `1234567`), el asignador reserva 28 bytes físicos en total.
- **Árbol de Buddy Allocator**: Para una memoria total de 64 KB, al solicitar 7 KB, el espacio de 64 KB se divide sucesivamente en $32	ext{ KB} 	o 16	ext{ KB} 	o 8	ext{ KB}$. Se entrega un bloque de 8 KB. Al liberarse, la dirección del bloque difiere de su "compañero" en un solo bit, lo que permite combinarlos de inmediato.

### Conexión Lógica y Relevancia
Profundiza en la gestión interna de la memoria no uniforme que requiere la segmentación. Demuestra que no existe un algoritmo de asignación variable perfecto para evitar la fragmentación externa, lo que justifica la adopción de unidades de tamaño fijo en la paginación.

---

## Paging: Introduction

### Idea Central
La paginación aborda el problema de la gestión del espacio en la memoria virtual dividiendo el espacio de direcciones de un proceso en unidades de tamaño fijo llamadas páginas, las cuales se asignan a marcos de página equivalentes en la memoria física. Esta técnica elimina completamente la fragmentación externa y ofrece flexibilidad para soportar espacios de direcciones dispersos. Sin embargo, introduce dos ineficiencias fundamentales: el consumo masivo de memoria para almacenar las tablas de páginas y la degradación del rendimiento al requerir un acceso adicional a la RAM para traducir cada dirección.

### Conceptos Clave
- **Página Virtual (*Virtual Page - VP*)**: Bloque de tamaño fijo en el que se divide el espacio de direcciones virtuales de un proceso.
- **Marco de Página (*Page Frame / Physical Frame - PFN/PPN*)**: Ranura de tamaño fijo en la memoria física capaz de albergar una página virtual.
- **Número de Página Virtual (*Virtual Page Number - VPN*)**: Bits superiores de una dirección virtual utilizados para identificar e indexar la página requerida dentro de la tabla de páginas.
- **Desplazamiento (*Offset*)**: Bits inferiores de una dirección virtual que indican la posición exacta del byte deseado dentro de una página y que no sufren traducción.
- **Tabla de Páginas (*Page Table*)**: Estructura de datos mantenida por el sistema operativo (generalmente una por proceso) que registra la asignación entre páginas virtuales y marcos físicos.
- **Entrada de Tabla de Páginas (*Page Table Entry - PTE*)**: Registro individual en la tabla de páginas que contiene el número de marco físico y bits de control (*valid*, *protection*, *present*, *dirty*, *accessed*).
- **Bit de Validez (*Valid Bit*)**: Indicador en la PTE que señala si la página virtual correspondiente ha sido asignada y puede ser accedida legítimamente por el proceso, permitiendo representar espacios de direcciones dispersos.

### Mecanismos y Procesos
- **Descomposición de la Dirección Virtual**: La dirección virtual generada por la CPU se divide mediante operaciones de máscara y desplazamiento de bits en dos componentes: el VPN (bits de orden superior) y el *offset* (bits de orden inferior).
- **Algoritmo de Traducción con Tabla Lineal**:
  1. El hardware obtiene la dirección base de la tabla de páginas del proceso activo desde un registro del procesador (*Page Table Base Register - PTBR*).
  2. Calcula la dirección de la PTE correspondiente mediante la fórmula: $	ext{PTEAddr} = 	ext{PTBR} + (	ext{VPN} 	imes 	ext{sizeof(PTE)})$.
  3. Accede a la memoria RAM para leer la PTE.
  4. Verifica que el *valid bit* esté activo y que los permisos de lectura/escritura/ejecución sean respetados; de lo contrario, la CPU genera una trampa (*trap*) de fallo de protección o de segmentación.
  5. Extrae el PFN de la PTE, lo desplaza a la izquierda y realiza una operación OR lógica con el *offset* original para construir la dirección física final.
  6. Emite la solicitud de lectura o escritura a la memoria RAM.
- **Penalización de Rendimiento**: En una paginación lineal pura, cada referencia implícita o explícita a memoria (búsqueda de instrucción, carga o almacenamiento de datos) duplica los accesos a la RAM, reduciendo la velocidad de ejecución a la mitad.

### Ejemplos e Ilustraciones
- **Traducción en Espacio de 64 Bytes**: En un espacio de direcciones hipotético de 64 bytes con páginas de 16 bytes, la dirección requiere 6 bits (2 bits para el VPN y 4 bits para el *offset*). Para la instrucción de carga en la dirección virtual 21 (`010101` en binario):
  - VPN = `01` (página 1), Offset = `0101` (byte 5).
  - La tabla de páginas indica que el VPN 1 se ubica en el PFN 7 (`111` en binario).
  - La dirección física resultante es `1110101` (dirección 117 en RAM).
- **Traza de Memoria de `array.c`**: Un bucle en C que inicializa un arreglo de 1000 enteros realiza 10 accesos a memoria por iteración (4 búsquedas de instrucciones, 1 escritura explícita en datos y 5 accesos a la tabla de páginas para traducir cada una de las 5 operaciones anteriores).

### Conexión Lógica y Relevancia
Resuelve de forma definitiva la fragmentación externa y los problemas de asignación compleja inherentes a la segmentación del Capítulo 16. No obstante, expone con claridad los dos obstáculos críticos que deben resolverse para hacer viable la paginación en sistemas reales: el costo de tiempo (resuelto con el TLB en el Capítulo 19) y el costo de espacio (resuelto con tablas multinivel en el Capítulo 20).

---

## Paging: Faster Translations (TLBs)

### Idea Central
El *Translation-Lookaside Buffer* (TLB) es una caché de hardware de alta velocidad integrada en la Unidad de Manejo de Memoria (MMU) que almacena las traducciones más frecuentes de direcciones virtuales a físicas. Aprovechando los principios de localidad temporal y espacial de las aplicaciones, el TLB permite realizar la inmensa mayoría de las traducciones en un solo ciclo de reloj sin consultar la tabla de páginas en la RAM, haciendo posible que la paginación funcione a velocidad nativa.

### Conceptos Clave
- **Translation-Lookaside Buffer (*TLB*)**: Caché de hardware de direccionamiento asociativo integrada en la MMU que guarda mapeos recientes de VPN a PFN.
- **Acierto en TLB (*TLB Hit*)**: Condición en la cual la traducción para un VPN solicitado se encuentra presente en el TLB, permitiendo generar la dirección física de inmediato.
- **Fallo en TLB (*TLB Miss*)**: Condición en la cual la traducción no está en el TLB, requiriendo un acceso adicional a la tabla de páginas en memoria física para cargar la traducción.
- **TLB Gestionado por Hardware (*Hardware-Managed TLB*)**: Arquitectura (ej. x86) donde la MMU recorre automáticamente la tabla de páginas en memoria RAM (*page table walk*) ante un fallo de TLB sin intervención del software.
- **TLB Gestionado por Software (*Software-Managed TLB*)**: Arquitectura (ej. MIPS, SPARC) donde un fallo de TLB genera una excepción gestionada por un manejador de trampas del sistema operativo en modo núcleo.
- **Identificador de Espacio de Direcciones (*Address Space Identifier - ASID*)**: Campo en las entradas del TLB que identifica el proceso al que pertenece cada traducción, permitiendo que múltiples procesos compartan el TLB simultáneamente sin requerir un vaciado en cada cambio de contexto.
- **Ley de Culler (*Culler's Law*)**: Principio técnico que establece que la memoria RAM no ofrece un tiempo de acceso uniforme cuando las referencias aleatorias superan la cobertura del TLB (*TLB coverage*), provocando caídas severas de rendimiento.

### Mecanismos y Procesos
- **Flujo de Traducción con TLB**:
  1. La CPU genera una dirección virtual y la MMU extrae el VPN.
  2. La MMU busca en paralelo en todas las entradas del TLB.
  3. En caso de *TLB Hit*, recupera el PFN, verifica los permisos y construye la dirección física.
  4. En caso de *TLB Miss*:
     - *En TLB por Hardware*: La MMU consulta la tabla de páginas apuntada por el PTBR, inserta la traducción en el TLB y reejecuta la instrucción.
     - *En TLB por Software*: La CPU lanza la excepción `TLB_MISS`. El SO ejecuta el manejador, busca en su tabla de páginas, usa instrucciones privilegiadas (`TLBWI`/`TLBWR`) para escribir la entrada en el TLB y ejecuta un retorno de trampa especial que reinterpreta la instrucción que falló.
- **Gestión en Cambios de Contexto**: Al conmutar de proceso, si no existen ASIDs, el SO ejecuta un *TLB Flush* (reseteando a 0 todos los bits de validez del TLB) para evitar que el nuevo proceso acceda por error a la memoria del proceso anterior. Con ASIDs, el SO simplemente actualiza un registro privilegiado con el ASID del proceso entrante.

### Ejemplos e Ilustraciones
- **Acceso Sequencial a un Arreglo**: Para un arreglo de 10 enteros de 4 bytes ubicado en páginas de 16 bytes, el primer acceso (`a[0]`) sufre un fallo de TLB (*miss*). Como los elementos `a[1]` y `a[2]` residen en la misma página, sus accesos resultan en aciertos (*hits*). El patrón de accesos resulta en: *miss, hit, hit, miss, hit, hit, hit, miss, hit, hit* (70% de aciertos gracias a la localidad espacial).
- **Experimento de Saavedra-Barrera (`tlb.c`)**: Programa que mide el tiempo de acceso al incrementar el número de páginas consultadas. Demuestra saltos bruscos en el tiempo de acceso de 5 ns a 20 ns y luego a 70 ns cuando el número de páginas supera la capacidad de las cachés L1 y L2 del TLB.

### Conexión Lógica y Relevancia
Resuelve la penalización de rendimiento por dobles accesos a memoria identificada en el Capítulo 18. Al transformar la traducción de direcciones en una operación casi instantánea en el caso habitual, convierte a la paginación en un mecanismo altamente eficiente desde la perspectiva del tiempo de ejecución.

---

## Paging: Smaller Tables

### Idea Central
Las tablas de páginas lineales requieren cantidades prohibitivas de memoria física cuando se aplican a espacios de direcciones de 32 o 64 bits, ya que deben reservar entradas para regiones no utilizadas. Para solucionar este problema de espacio, las tablas de páginas multinivel convierten la tabla lineal en una estructura jerárquica en forma de árbol mediante la adición de un directorio de páginas. Esto permite asignar memoria únicamente para las porciones de la tabla de páginas que contienen traducciones válidas, soportando eficientemente espacios de direcciones dispersos (*sparse*).

### Conceptos Clave
- **Directorio de Páginas (*Page Directory*)**: Estructura de nivel superior que organiza la tabla de páginas en bloques del tamaño de una página y rastrea cuáles de estos bloques están asignados en memoria física.
- **Entrada de Directorio de Páginas (*Page Directory Entry - PDE*)**: Registro en el directorio de páginas que contiene un bit de validez y el PFN de la página física que almacena un fragmento de la tabla de páginas.
- **Tabla de Páginas Multinivel (*Multi-level Page Table*)**: Estructura jerárquica de traducción que añade uno o más niveles de indirección para evitar la asignación de memoria contigua para entradas inválidas.
- **Compromiso Tiempo-Espacio (*Time-Space Trade-off*)**: Intercambio de diseño donde se reduce drásticamente el consumo de memoria RAM sacrificando velocidad en los fallos de TLB, los cuales requieren múltiples lecturas a la jerarquía de tablas.
- **Tabla de Páginas Invertida (*Inverted Page Table*)**: Alternativa donde se mantiene una única tabla global para todo el sistema con tantas entradas como marcos de página físicos existan en la RAM, utilizando tablas *hash* para buscar qué proceso y página virtual ocupan cada marco.
- **Páginas Grandes / Superpáginas (*Huge Pages / Superpages*)**: Mecanismo que permite utilizar páginas de mayor tamaño (ej. 2 MB o 1 GB en x86) para reducir el número de niveles en la tabla de páginas y maximizar la cobertura del TLB en aplicaciones con gran consumo de memoria.

### Mecanismos y Procesos
- **Estructura y Traducción en Dos Niveles**:
  1. La dirección virtual se divide en tres campos: Índice de Directorio (`PDIndex`), Índice de Tabla (`PTIndex`) y Desplazamiento (`Offset`).
  2. La MMU consulta el registro base del directorio de páginas (*PDBR*) y busca el PDE en la posición `PDIndex`.
  3. Si el PDE no es válido (`Valid = 0`), se lanza una excepción de fallo de segmentación inmediatamente, evitando tener asignada esa zona de la tabla.
  4. Si el PDE es válido, recupera su PFN y accede a la página de la tabla de páginas en la posición `PTIndex` para leer la PTE.
  5. Si la PTE es válida, extrae el PFN del dato y le concatena el `Offset` para formar la dirección física.
- **Soporte para Más de Dos Niveles**: Cuando el propio directorio de páginas excede el tamaño de una página física debido a la amplitud del espacio de direcciones (común en 64 bits), se agrega un nivel adicional de directorio (PDIndex 0, PDIndex 1, etc.), creando árboles de 3, 4 o más niveles.

### Ejemplos e Ilustraciones
- **Ahorro de Memoria en Espacio Disperso**: En un espacio de direcciones de 16 KB con páginas de 64 bytes que solo utiliza código (páginas 0-1), *heap* (páginas 4-5) y *stack* (páginas 254-255):
  - Una tabla lineal requeriría asignar 16 páginas físicas contiguas para albergar las 256 PTEs.
  - Una tabla multinivel solo asigna 3 páginas físicas en total: 1 para el directorio de páginas, 1 para el fragmento de código/*heap* y 1 para el fragmento del *stack*, liberando las 13 páginas restantes para el sistema.
- **Analogía del Híbrido (*Reese's Peanut Butter Cup*)**: El autor compara la combinación de segmentación y paginación con mezclar chocolate y mantequilla de maní para intentar obtener lo mejor de ambos mundos, aunque advierte sobre los problemas de fragmentación externa que aún surgen al gestionar tablas de tamaño variable.

### Conexión Lógica y Relevancia
Resuelve la ineficiencia de espacio identificada en el Capítulo 18 sin perder la flexibilidad de la paginación ni reintroducir la fragmentación externa grave. Con esto concluye la arquitectura básica de mecanismos de memoria virtual en memoria RAM, sirviendo como fundamento previo para estudiar el almacenamiento secundario (*swap space*) y los algoritmos de reemplazo de páginas.

---

## Beyond Physical Memory: Mechanisms

### Idea Central
Esta sección extiende la virtualización de memoria más allá de los límites de la memoria RAM física mediante el uso de almacenamiento secundario como espacio de intercambio (*swap space*). Permite que el sistema operativo soporte un espacio de direcciones agregado que excede la capacidad de la memoria física disponible, gestionando la transferencia de páginas entre la RAM y el disco mediante el control de fallos de página (*page faults*).

### Conceptos Clave
- **Espacio de Intercambio (*Swap Space*)**: Región del disco secundario o SSD reservada por el sistema operativo para almacenar páginas de memoria que han sido evacuadas temporalmente de la memoria física.
- **Bit de Presencia (*Present Bit*)**: Indicador en cada entrada de la tabla de páginas (*PTE*) que señala si la página virtual reside actualmente en la memoria RAM (1) o en el espacio de intercambio (0).
- **Fallo de Página (*Page Fault*)**: Excepción de hardware producida cuando un proceso intenta acceder a una página virtual cuyo bit de presencia es 0, transfiriendo el control al manejador de fallos de página del núcleo.
- **Manejador de Fallos de Página (*Page Fault Handler*)**: Rutina del sistema operativo en modo núcleo encargada de localizar la página requerida en el disco, asignar un marco libre en RAM, ejecutar la lectura de E/S y actualizar la tabla de páginas.
- **Demonio de Páginas (*Page Daemon / Swap Daemon*)**: Proceso en segundo plano del sistema operativo que monitorea la memoria física libre y activa el desalojo de páginas cuando la RAM disponible cae por debajo de un umbral determinado.
- **Umbral Superior e Inferior (*High and Low Watermarks*)**: Límites de memoria física libre configurados en el sistema operativo para desencadenar (*low watermark*) y pausar (*high watermark*) la liberación preventiva de páginas.

### Mecanismos y Procesos
- **Flujo de Atención a la Memoria con Paginación a Disco**:
  1. La CPU genera una dirección virtual y la MMU extrae el VPN.
  2. Si ocurre un fallo en el TLB (*TLB miss*), la MMU o el manejador por software consulta la entrada de la tabla de páginas (*PTE*).
  3. Si la PTE está marcada como válida pero su bit de presencia es 0, el hardware genera una excepción por fallo de página (*page fault*).
  4. El manejador de fallos del SO intercepta la excepción, suspende el proceso solicitante (pasándolo al estado *Blocked*) y extrae la dirección de disco de la página desde la propia PTE.
  5. El SO emite la solicitud de lectura al almacenamiento secundario. Durante la operación de E/S, el planificador ejecuta otros procesos para mantener alta la utilización de la CPU.
  6. Al completarse la E/S de disco, el SO ubica la página en un marco físico (liberando otro marco mediante una política de reemplazo si la RAM está llena), actualiza la PTE con el nuevo PFN y cambia el bit de presencia a 1.
  7. El proceso regresa al estado *Ready*. Al reanudarse, reejecuta la instrucción que causó el fallo, logrando un acceso exitoso a la memoria RAM.
- **Estrategias de Reemplazo Asíncrono**: Para evitar retrasos durante el manejo de un fallo de página, el *page daemon* despierta de forma periódica cuando la memoria libre cae por debajo del *low watermark*. El demonio selecciona páginas para evacuar o liberar hasta recuperar el espacio libre indicado por el *high watermark*.

### Ejemplos e Ilustraciones
- **Estructura Ampliada de la PTE**: Cuando el bit de presencia se establece en 0, los bits destinados normalmente a almacenar el número de marco físico (PFN) son reutilizados por el sistema operativo para registrar la dirección exacta de bloque o sector dentro del espacio de intercambio.
- **Gestión de Latencia de E/S**: El autor destaca el impacto de la diferencia de velocidades entre dispositivos: acceder a la RAM requiere decenas de nanosegundos, mientras que leer del disco secundario toma milisegundos. Esta disparidad justifica suspender inmediatamente el proceso infractor para evitar el desperdicio de millones de ciclos de instrucción.

### Conexión Lógica y Relevancia
Resuelve la limitación de capacidad física de la memoria RAM, completando la ilusión de un espacio de direcciones virtual amplio e independiente del hardware instalado. Sienta la infraestructura mecánica necesaria para abordar el problema de decisión analizado en el capítulo posterior: qué páginas deben ser desalojadas a disco.

---

## Beyond Physical Memory: Policies

### Idea Central
Analiza las políticas de reemplazo de páginas (*page replacement policies*) empleadas por el sistema operativo para decidir qué página de la memoria RAM evacuar a disco cuando la memoria física se llena. Compara algoritmos teóricos con aproximaciones prácticas de bajo costo que aprovechan el bit de referencia de hardware para maximizar la tasa de aciertos (*hit rate*) y prevenir la degradación por hiperactividad de disco (*thrashing*).

### Conceptos Clave
- **Tasa de Acierto / Fallo (*Hit / Miss Rate*)**: Porcentaje de referencias a memoria virtual que se satisfacen directamente desde la RAM física frente a las que requieren accesos al espacio de intercambio en disco.
- **Política Óptima de Belady (*OPT / Optimal*)**: Algoritmo teórico perfecto que desaloja la página cuya próxima referencia se producirá más lejos en el futuro; se utiliza exclusivamente como punto de comparación o *benchmark*.
- **LRU (*Least Recently Used*)**: Política de reemplazo basada en la propiedad de localidad temporal que desaloja la página que no ha sido accedida durante el mayor intervalo de tiempo.
- **LFU (*Least Frequently Used*)**: Política de reemplazo que desaloja la página que acumula el menor número total de accesos.
- **Algoritmo del Reloj (*Clock Algorithm*)**: Aproximación de bajo costo a LRU que organiza los marcos de página en una lista circular y utiliza un bit de referencia (*use bit*) escaneado por un puntero rotativo.
- **Bit de Modificación (*Dirty / Modified Bit*)**: Bit de control que indica si una página ha sido escrita; las páginas "limpias" pueden descartarse sin acceso a disco, mientras que las páginas "sucias" requieren una escritura en el espacio de intercambio antes de ser reutilizadas.
- **Hiperactividad de Memoria (*Thrashing*)**: Estado crítico donde el conjunto de páginas activas (*working set*) de los procesos excede la memoria RAM disponible, provocando que el sistema operativo dedique casi la totalidad de su tiempo a intercambiar páginas con el disco.

### Mecanismos y Procesos
- **Evaluación de Políticas de Reemplazo**:
  - *FIFO*: Expulsa las páginas en el orden estricto de su llegada a la memoria RAM, ignorando su frecuencia o recesión de uso.
  - *Random*: Selecciona páginas al azar para desalojar; es simple de implementar pero carece de capacidad predictiva.
- **Operación del Algoritmo del Reloj**:
  1. Las páginas físicas se ordenan conceptualmente en una estructura circular con un puntero de escaneo.
  2. Al requerirse una página libre, el algoritmo examina la página apuntada:
     - Si su bit de referencia (*use bit*) es 1, se limpia a 0 y el puntero avanza a la siguiente posición.
     - Si su bit de referencia es 0, la página es seleccionada inmediatamente para su desalojo.
  3. Cada vez que un proceso lee o escribe en una página residente en RAM, el hardware establece su *use bit* en 1.
- **Optimizaciones de E/S (Pre-petición y Agrupamiento)**:
  - *Prefetching*: El sistema operativo analiza patrones de acceso secuencial para cargar páginas por adelantado en la RAM.
  - *Clustering / Grouping*: Al escribir páginas modificadas (*dirty pages*) en el disco, el sistema las agrupa en bloques contiguos para reducir las operaciones de posicionamiento (*seeks*) del cabezal de almacenamiento.

### Ejemplos e Ilustraciones
- **Traza de la Política de Belady**: Una secuencia de accesos `0, 1, 2, 0, 1, 3, 0, 3, 1, 2` ejecutada en 3 marcos de memoria ilustra cómo OPT logra la menor cantidad de fallos al expulsar la página 2 cuando se solicita la 3, debido a que la página 2 es la que se utilizará más tarde en el tiempo.
- **Anomalía de Belady en FIFO**: Demuestra cómo en la política FIFO, incrementar la cantidad de memoria RAM física asignada a un proceso puede paradójicamente aumentar el número total de fallos de página para secuencias específicas de acceso.

### Conexión Lógica y Relevancia
Aporta la capa de inteligencia y toma de decisiones a los mecanismos de fallos de página introducidos en el Capítulo 21. Evalúa el equilibrio práctico entre la precisión del rastreo exacto de acceso (LRU) y la eficiencia computacional de sus aproximaciones (Clock), cerrando el diseño conceptual de la gestión de memoria virtual.

---

## Complete Virtual Memory Systems

### Idea Central
Examina la arquitectura completa e integrada de la memoria virtual en sistemas operativos reales mediante el estudio de caso del sistema VAX/VMS. Demuestra cómo un diseño de software bien estructurado puede superar limitaciones severas de hardware (como páginas pequeñas de 512 bytes y ausencia de bits de referencia por hardware) utilizando técnicas como la paginación segmentada, la asignación perezosa (*lazy allocation*), la copia en escritura (*copy-on-write*) y el reemplazo FIFO segmentado por listas globales de páginas libres y modificadas.

### Conceptos Clave
- **VAX/VMS**: Sistema operativo desarrollado por Digital Equipment Corporation (DEC) para la arquitectura VAX-11, reconocido por su rigor de diseño en la gestión de memoria virtual.
- **Paginación Segmentada (*Segmented Paging*)**: División del espacio de direcciones virtual en regiones explícitas (P0 para proceso, P1 para pila del proceso, S para el núcleo) para reducir el tamaño de las tablas de páginas.
- **FIFO Segmentado (*Segmented FIFO / Second-chance Lists*)**: Política de reemplazo que asigna un límite de páginas a cada proceso mediante FIFO local, amortiguando los errores de desalojo mediante una lista global de páginas libres (*Free List*) y modificadas (*Modified List*) que actúan como caché de reasignación.
- **Asignación Perezosa (*Lazy Allocation*)**: Filosofía de diseño donde el sistema operativo pospone la asignación de memoria física o la lectura de almacenamiento hasta el momento en que la aplicación intenta acceder por primera vez a la dirección correspondiente.
- **Copia en Escritura (*Copy-on-Write - COW*)**: Técnica donde dos procesos comparten las mismas páginas físicas de memoria marcadas como de solo lectura; únicamente cuando uno de los procesos intenta modificar una página, el hardware genera una trampa y el SO realiza la duplicación física de dicha página.
- **Página de Ceros a Demanda (*Zero-on-Demand*)**: Mecanismo de seguridad donde las páginas de memoria reservadas para la pila o el *heap* no se inicializan con ceros ni se asignan en RAM hasta que son accedidas por la aplicación, evitando fugas de información de otros procesos.

### Mecanismos y Procesos
- **Mitigación de la Ausencia de Bit de Referencia en VAX/VMS**:
  - Al carecer de un bit de referencia por hardware, VMS implementa una política FIFO local combinada con dos listas globales de respaldo.
  - Cuando una página es expulsada del conjunto residente (*resident set*) de un proceso, no se descarta ni se escribe a disco inmediatamente, sino que se traslada a la *Free Page List* (si está limpia) o a la *Modified Page List* (si está sucia).
  - Si el proceso vuelve a solicitar esa página mientras esta permanece en alguna de las listas globales, la página se rescata (*reclaim*) e integra de nuevo al espacio del proceso con un costo de CPU mínimo sin acceder al disco.
- **Agrupamiento de Escrituras (*Write Clustering*)**: La *Modified Page List* acumula páginas sucias procedentes de diversos procesos y las escribe en el almacenamiento secundario en operaciones de bloques contiguos, optimizando el rendimiento de la E/S.
- **Mapeo del Espacio del Sistema (*System Space*)**: La mitad superior del espacio de direcciones de cada proceso (región S) contiene el código y las estructuras de datos del núcleo. Permanece mapeada de forma idéntica en la memoria física para todos los procesos pero protegida por niveles de privilegio, simplificando la transferencia de datos durante las llamadas al sistema.

### Ejemplos e Ilustraciones
- **Optimización de `fork()` mediante Copy-on-Write**: En lugar de duplicar inmediatamente la memoria física del proceso padre durante un `fork()`, el sistema operativo copia únicamente la tabla de páginas marcando todas las entradas como de solo lectura. Al ejecutar a continuación `exec()`, el proceso hijo reemplaza su imagen sin haber realizado copias innecesarias de memoria física.
- **Control de Inanición Global**: VMS impone límites de tamaño al conjunto residente (*resident set size - RSS*) para cada proceso individual, impidiendo que un programa con patrones de acceso erráticos desaloje las páginas del resto de los procesos activos en el sistema.

### Conexión Lógica y Relevancia
Sintetiza la totalidad de los conceptos de virtualización de memoria desarrollados desde el Capítulo 13 hasta el 22. Muestra la integración de los mecanismos teóricos en un sistema de producción real, concluyendo formalmente el bloque de virtualización de memoria y preparando la transición hacia el siguiente gran pilar del libro: la concurrencia.

---

## Concurrency: An Introduction

### Idea Central
La concurrencia expande la abstracción del proceso introduciendo el hilo de ejecución (*thread*), donde múltiples puntos de ejecución comparten un mismo espacio de direcciones en memoria. Esto permite acelerar cómputos mediante la paralelizacion en múltiples CPUs y evitar el bloqueo del programa durante operaciones lentas de entrada/salida. Sin embargo, el acceso no coordinado a variables compartidas mediante secuencias de instrucciones no atómicas genera condiciones de carrera (*race conditions*), haciendo necesaria la sincronización para recuperar el determinismo en el sistema.

### Conceptos Clave
- **Hilo de Ejecución (*Thread*)**: Abstracción que representa un punto independiente de ejecución dentro de un proceso; posee su propia pila (*stack*) y registros (incluyendo el contador de programa - PC), pero comparte el espacio de direcciones con los demás hilos del mismo proceso.
- **Bloque de Control de Hilo (*Thread Control Block - TCB*)**: Estructura de datos utilizada por el sistema operativo para almacenar el estado de los registros de un hilo durante una conmutación de contexto.
- **Condición de Carrera (*Race Condition / Data Race*)**: Situación en la que el resultado de la ejecución depende impredeciblemente del orden y la sincronización en que el planificador intercala las instrucciones de múltiples hilos.
- **Sección Crítica (*Critical Section*)**: Fragmento de código que accede a un recurso compartido (como una variable global) y que no debe ser ejecutado simultáneamente por más de un hilo a la vez.
- **Exclusión Mutua (*Mutual Exclusion*)**: Propiedad de garantía que asegura que solo un hilo a la vez pueda encontrarse dentro de una sección crítica determinada.
- **Atomicidad (*Atomicity*)**: Propiedad por la cual una secuencia de instrucciones se ejecuta como una unidad indivisible ("todo o nada"), sin posibilidad de ser interrumpida a medio camino.
- **Resultado Indeterminado (*Indeterminate Result*)**: Salida de un programa que varía entre ejecuciones debido a la intercalación no controlada de hilos.

### Mecanismos y Procesos
- **Conmutación de Contexto entre Hilos**: A diferencia de la conmutación entre procesos, no requiere cambiar la tabla de páginas ni invalidar cachés de traducción de memoria, ya que el espacio de direcciones se mantiene idéntico. Solo se guardan los registros del hilo saliente en su TCB y se restauran los del hilo entrante.
- **El Problema del Incremento Compartido**: Un incremento en lenguaje C (`counter++`) se traduce típicamente en tres instrucciones ensamblador: lectura de memoria a registro (`mov`), incremento del registro (`add`) y escritura del registro a memoria (`mov`). Si ocurre una interrupción de reloj entre la lectura y la escritura, un segundo hilo puede leer el valor antiguo antes de que el primero guarde el nuevo, provocando la pérdida de actualizaciones.

### Ejemplos e Ilustraciones
- **Código `threads.c` (`t1.c`)**: Muestra cómo dos hilos incrementan en un bucle una variable global `counter` 10 millones de veces cada uno. En lugar de obtener el resultado esperado de 20,000,000, la ejecución devuelve valores inconsistentes (como 19,345,221 o 19,221,041) debido a interrupciones inoportunas en la sección crítica.

### Conexión Lógica y Relevancia
Marca la transición formal de la virtualización (de CPU y memoria) a la concurrencia. Demuestra cómo las abstracciones creadas en los capítulos anteriores (como la conmutación de contexto y el reparto de tiempo) introducen problemas de corrección cuando los hilos comparten memoria, justificando la necesidad de primitivas de sincronización como cerrojos (*locks*) y variables de condición.

---

## Interlude: Thread API

### Idea Central
Examina las interfaces de programación estándar POSIX Threads (`pthreads`) utilizadas para la creación, control y sincronización de hilos en sistemas operativos tipo UNIX. Detalla las funciones fundamentales para iniciar e integrar hilos (`pthread_create`, `pthread_join`), el uso correcto de cerrojos (`pthread_mutex_t`) y la interacción mediada por variables de condición (`pthread_cond_t`), haciendo énfasis en los errores comunes de asignación en la pila y la necesidad de comprobar siempre los códigos de retorno.

### Conceptos Clave
- **`pthread_create()`**: Función utilizada para instanciar un nuevo hilo en ejecución dentro del mismo espacio de direcciones, especificando la rutina de entrada y sus argumentos mediante punteros genéricos `void*`.
- **`pthread_join()`**: Llamada que bloquea el hilo llamante hasta que el hilo especificado finaliza su ejecución, permitiendo recolectar su valor de retorno de forma limpia.
- **Mutex (*`pthread_mutex_t`*)**: Primitiva de exclusión mutua que garantiza que solo un hilo a la vez pueda ingresar a la sección crítica delimitada por `pthread_mutex_lock()` y `pthread_mutex_unlock()`.
- **Variable de Condición (*`pthread_cond_t`*)**: Cola explícita de señales que permite a un hilo ponerse a dormir (`pthread_cond_wait`) a la espera de un cambio de estado en el sistema provocado por otro hilo (`pthread_cond_signal`).
- **Semántica de Espera en Bucle (*while loop condition check*)**: Práctica imperativa de reevaluar la condición deseada dentro de un bucle `while` tras despertar de un `pthread_cond_wait()`, previniendo despertares espurios o cambios de estado concurrentes por parte de otros hilos.

### Mecanismos y Procesos
- **Paso de Argumentos y Retorno Libre**: Como `pthread_create` y `pthread_join` aceptan punteros `void*`, se empaquetan estructuras dinámicas (`struct`) asignadas en el montón (*heap*) para transferir múltiples argumentos o recuperar estructuras complejas de resultados.
- **Mecanismo de Liberación y Re-adquisición del Mutex en `wait()`**: Al llamar a `pthread_cond_wait(&cond, &mutex)`, el sistema libera el cerrojo de forma atómica y pone al hilo a dormir; al ser despertado por una señal, reacquiere automáticamente el cerrojo antes de retornar de la llamada.

### Ejemplos e Ilustraciones
- **Error del Puntero a la Pila Local**: Muestra el código defectuoso donde un hilo retorna la dirección de una estructura declarada en su propia pila local (`myret_t oops`); al salir de la función, el marco de pila se destruye, dejando un puntero desreferenciado peligroso (*dangling pointer*) que corrompe los datos al ser leído por el hilo padre.

### Conexión Lógica y Relevancia
Conecta los conceptos teóricos de la concurrencia del Capítulo 26 con la implementación práctica en código C. Ofrece las herramientas de API reales que se utilizarán para construir cerrojos eficientes y estructuras de datos concurrentes en los capítulos posteriores.

---

## Locks

### Idea Central
El cerrojo (*lock*) es la primitiva fundamental diseñada para proporcionar exclusión mutua en secciones críticas. Explora el desarrollo histórico y técnico de los cerrojos, desde intentos fallidos mediante variables de memoria ordinarias hasta soluciones basadas en instrucciones atómicas de hardware (como *Test-And-Set*, *Compare-And-Swap*, *Fetch-And-Add* y *Load-Linked/Store-Conditional*) y el soporte indispensable del sistema operativo (colas de espera, `park`/`unpark`, `futex`) para evitar el desperdicio de ciclos de CPU por giro inútil (*spin-waiting*).

### Conceptos Clave
- **Cerrojo de Giro (*Spin Lock*)**: Cerrojo basado en hardware que hace que el hilo que espera consuma ciclos de CPU repetidamente en un bucle hasta que la variable quede libre.
- **Test-And-Set (*Atomic Exchange*)**: Instrucción de hardware que lee el valor antiguo de una posición de memoria y escribe un valor nuevo de manera atómica, devolviendo el valor anterior.
- **Compare-And-Swap (*CAS*)**: Instrucción atómica que comprueba si el valor en memoria coincide con un valor esperado; de ser así, actualiza la dirección con el nuevo valor.
- **Fetch-And-Add**: Instrucción atómica que incrementa el valor de una variable en memoria y devuelve el valor previo, utilizada para construir cerrojos equitativos por tiquete (*Ticket Locks*).
- **Ticket Lock**: Cerrojo que asigna un número de turno a cada hilo mediante *Fetch-And-Add*, garantizando el orden de atención y evitando la inanición (*starvation*).
- **Rendición Voluntaria (`yield()`)**: Llamada al sistema que permite a un hilo en giro ceder voluntariamente la CPU, pasando del estado *Running* al *Ready*.
- **Cerrojo de Dos Fases (*Two-Phase Lock*)**: Algoritmo híbrido que primero gira durante un intervalo breve con la esperanza de obtener el cerrojo y, si no lo logra, recurre al sistema operativo para ponerse a dormir.
- **Futex (*Fast Userspace Mutex*)**: Primitiva de Linux que gestiona el caso sin contención en el espacio de usuario de manera ultrarrápida y delega al núcleo la cola de bloqueo únicamente cuando existe contención real.

### Mecanismos y Procesos
- **Inadecuación de la Desactivación de Interrupciones**: Desactivar interrupciones solo funciona en uniprocesadores y otorga privilegios peligrosos al código de usuario; en multiprocesadores no impide que hilos en otros núcleos accedan a la memoria compartida.
- **Mecanismo de Cola con `park()` y `unpark()` (Solaris)**: Para evitar girar en vano en un solo procesador, el cerrojo mantiene una cola de hilos esperados (`queue_t`). El hilo que no obtiene el cerrojo se añade a la cola y llama a `park()`. Al liberar el cerrojo, `unlock()` desencola el siguiente hilo y llama a `unpark(tid)`.
- **Carrera de Despertar (*Wakeup/Waiting Race*)**: Vulnerabilidad en la cual un hilo está a punto de llamar a `park()`, pero es interrumpido por otro hilo que libera el cerrojo e invoca `unpark()`; si el primer hilo ejecuta `park()` después, se dormirá indefinidamente. Se resuelve con llamadas en el núcleo como `setpark()`.

### Ejemplos e Ilustraciones
- **Inversión de Prioridad en Mars Pathfinder (*Priority Inversion*)**: Ejemplo histórico donde un hilo de alta prioridad quedó bloqueado indefinidamente girando sobre un cerrojo en posesión de un hilo de baja prioridad al que se le impidió ejecutar por la presencia de un hilo de prioridad media.

### Conexión Lógica y Relevancia
Proporciona la solución detallada al problema fundamental expuesto en los Capítulos 26 y 27. Sienta las bases de hardware y kernel necesarias para construir estructuras de datos concurrentes (Capítulo 29) y coordinar interacciones avanzadas de espera mediante variables de condición (Capítulo 30) y semáforos (Capítulo 31).

---

## Lock-based Concurrent Data Structures

### Idea Central
La adición de cerrojos a las estructuras de datos tradicionales las transforma en estructuras seguras para hilos (*thread-safe*), permitiendo su acceso dinámico y correcto en entornos multihilo. No obstante, el desafío fundamental de diseño radica en equilibrar la corrección con el rendimiento, transitando desde estrategias simples de cerrojo único hasta técnicas complejas de grano fino (como el cerrojo por contenedor en tablas hash o el contador aproximado) para evitar que la sincronización destruya la escalabilidad del sistema.

### Conceptos Clave
- **Estructura de Datos Segura para Hilos (*Thread-Safe Data Structure*)**: Estructura manipulada por múltiples hilos concurrentes que mantiene un comportamiento correcto y consistente mediante mecanismos de sincronización.
- **Cerrojo Único o de Grano Grueso (*Coarse-Grained Locking / Big Lock*)**: Enfoque donde un solo cerrojo protege la totalidad de la estructura de datos en cada operación, garantizando corrección a costa de limitar la concurrencia.
- **Contador Aproximado (*Sloppy / Approximate Counter*)**: Estructura de contador distribuido que utiliza contadores físicos locales por núcleo de CPU y un contador global, transfiriendo actualizaciones locales al contador global al alcanzar un umbral definido.
- **Umbral de Transferencia ($S$) (*Threshold $S$*)**: Parámetro que determina la frecuencia con la que los contadores locales actualizan el contador global, controlando el compromiso entre la precisión del conteo y la escalabilidad del rendimiento.
- **Cerrojo Mano Sobre Mano (*Hand-over-hand Locking / Lock Coupling*)**: Técnica de recorrido en listas enlazadas donde cada nodo posee su propio cerrojo; un hilo adquiere el cerrojo del siguiente nodo antes de liberar el del nodo actual.
- **Optimización Prematura (*Premature Optimization*)**: Ley de Knuth que establece que la sincronización de grano grueso debe utilizarse por defecto y solo refinarse hacia esquemas más complejos si las mediciones empíricas demuestran un cuello de botella de rendimiento real.

### Mecanismos y Procesos
- **Mapeo y Transferencia en el Contador Aproximado**:
  1. Cada hilo actualiza el contador local correspondiente a su núcleo de CPU actual bajo un cerrojo local, evitando contención con hilos en otros núcleos.
  2. Cuando el acumulado local alcanza el umbral $S$, el hilo adquiere el cerrojo global, suma el valor local al contador global y reinicia el contador local a cero.
  3. Las lecturas del valor global solo adquieren el cerrojo global, devolviendo un valor aproximado pero de acceso ultra-rápido.
- **Estructuración Segura de Control de Flujo**: En listas enlazadas concurridas, la asignación de memoria (`malloc`) se realiza fuera del cerrojo para reducir el tiempo dentro de la sección crítica. Asimismo, se unifican las rutas de salida para garantizar que el cerrojo se libere siempre antes de retornar, previniendo fugas de cerrojos en caminos de error.
- **Cola Concurrente de Michael y Scott**: Emplea dos cerrojos independientes: uno para la cabeza (`head_lock`) y otro para la cola (`tail_lock`). Mediante un nodo ficticio (*dummy node*) asignado al inicializar la cola, las operaciones de encolado (`enqueue`) y desencolado (`dequeue`) pueden ejecutarse de forma simultánea sin interferirse en el caso habitual.
- **Tabla Hash Concurrente por Contenedores**: Asigna un cerrojo independiente a cada lista enlazada o contenedor (*bucket*). Dado que las claves se distribuyen entre los contenedores mediante el operador módulo (`key % BUCKETS`), las operaciones sobre distintos contenedores ocurren en paralelo sin contención.

### Ejemplos e Ilustraciones
- **Degradación de Rendimiento en Contadores**: Experimentos con 4 CPUs demuestran que un contador de cerrojo único sufre un retraso masivo al pasar de 1 a 2 hilos (de 0.03 segundos a más de 5 segundos para 1 millón de operaciones por hilo), mientras que el contador aproximado mantiene un tiempo de ejecución plano e insensible al número de hilos.
- **El Big Kernel Lock (BKL) en Linux**: Caso histórico donde los sistemas operativos iniciales protegían todo el núcleo con un único cerrojo global; con la masificación de CPUs multinúcleo, Linux reemplazó progresivamente el BKL por cerrojos de grano fino, mientras que Sun diseñó Solaris desde cero para ser inherentemente concurrente.

### Conexión Lógica y Relevancia
Aplica las primitivas de exclusión mutua desarrolladas en el Capítulo 28 sobre las estructuras de datos esenciales de los sistemas informáticos. Demuestra que aumentar la concurrencia no siempre incrementa la velocidad si el costo de adquisición de cerrojos supera los beneficios del paralelismo.

---

## Condition Variables

### Idea Central
Las variables de condición son primitivas de sincronización explícitas que permiten a un hilo ponerse a dormir hasta que otro hilo modifique el estado del programa y le notifique que una condición específica se ha cumplido. Resuelven la ineficiencia del sondeo ininterrumpido (*spin-waiting*) en interacciones donde un hilo debe aguardar eventos o cambios de estado provocados por otro hilo, como en el problema del productor-consumidor.

### Conceptos Clave
- **Variable de Condición (*Condition Variable - CV*)**: Cola explícita de hilos en memoria administrada por el sistema operativo donde los hilos se suspenden a la espera de que cambie una condición de estado.
- **`pthread_cond_wait()`**: Operación que suspende atómicamente el hilo llamante y libera el mutex asociado; al ser despertado por una señal, reacquiere automáticamente el mutex antes de retornar.
- **`pthread_cond_signal()`**: Operación que despierta a uno de los hilos suspendidos en la variable de condición.
- **Semántica de Mesa (*Mesa Semantics*)**: Modelo estándar donde señalar a un hilo es solo una indicación (*hint*) de que el estado cambió; el hilo despertado no se ejecuta de inmediato y debe reevaluar la condición al reanudar la ejecución.
- **Semántica de Hoare (*Hoare Semantics*)**: Modelo teórico donde la señalización transfiere de forma inmediata el control de la CPU y el cerrojo al hilo despertado.
- **Despertar Espurio (*Spurious Wakeup*)**: Situación en la cual un hilo se despierta de una variable de condición sin que haya ocurrido una señal explícita o sin que la condición deseada se mantenga verdadera.
- **Condición Cobertora (*Covering Condition / Broadcast*)**: Uso de `pthread_cond_broadcast()` para despertar a todos los hilos en espera cuando una señal individual no puede determinar con certeza cuál hilo específico puede continuar.

### Mecanismos y Procesos
- **Protocolo Estándar de Espera y Señalización**:
  1. El hilo adquiere el mutex y evalúa la condición de estado dentro de un bucle `while`.
  2. Si la condición no se satisface, invoca `pthread_cond_wait(&cond, &mutex)`, liberando el mutex y durmiéndose de forma atómica.
  3. El hilo emisor adquiere el mismo mutex, modifica la variable de estado compartida, ejecuta `pthread_cond_signal(&cond)` y libera el mutex.
  4. El hilo en espera despierta, compite por re-adquirir el mutex, sale de `wait()` y vuelve a verificar la condición en el bucle `while`.
- **Solución al Problema del Búfer Acotado (*Bounded Buffer*)**:
  - Requiere **dos** variables de condición separadas: `empty` (para que los productores esperen si el búfer está lleno) y `fill` (para que los consumidores esperen si el búfer está vacío).
  - Los productores evalúan `while (count == MAX)` en `empty`, insertan el elemento (`put`) y señalan `fill`.
  - Los consumidores evalúan `while (count == 0)` en `fill`, extraen el elemento (`get`) y señalan `empty`.

### Ejemplos e Ilustraciones
- **Tuberías de UNIX (*UNIX Pipes*)**: La orden de la shell `grep foo file.txt | wc -l` conecta dos procesos mediante un búfer acotado en el núcleo, donde `grep` actúa como productor y `wc` como consumidor coordinados por variables de estado internas.
- **Manejo de Memoria Libre con Broadcast**: Un proceso solicita 100 bytes y se duerme por falta de espacio; un segundo proceso solicita 10 bytes y también se duerme. Cuando un tercer proceso libera 50 bytes, emitir `signal` podría despertar al proceso de 100 bytes (el cual volvería a dormirse al no alcanzarle el espacio), dejando bloqueado al de 10 bytes que sí podía continuar. Usar `broadcast` despierta a ambos, permitiendo que la tarea adecuada progrese.

### Conexión Lógica y Relevancia
Complementa la exclusión mutua de los cerrojos al proporcionar el mecanismo de coordinación de estado y suspensión eficiente de hilos. Sirve como el componente indispensable para resolver problemas complejos de sincronización orientados a eventos.

---

## Semaphores

### Idea Central
El semáforo es una primitiva de sincronización unificada introducida por Edsger Dijkstra que integra un valor entero manipulado atómicamente mediante dos rutinas: `sem_wait()` y `sem_post()`. Un semáforo puede operar tanto de cerrojo (semáforo binario) cuando se inicializa en 1, como de mecanismo de ordenamiento o condición cuando se inicializa en 0 o en $N$, ofreciendo un modelo abstracto y flexible para resolver múltiples patrones de concurrencia.

### Conceptos Clave
- **Semáforo (*Semaphore*)**: Objeto de sincronización con un estado entero interno inicializado mediante `sem_init()`.
- **`sem_wait()` / $P()$ / *Down***: Rutina que decrementa el valor del semáforo en 1; si el valor resultante es negativo, el hilo llamante se suspende en la cola de espera.
- **`sem_post()` / $V()$ / *Up***: Rutina que incrementa el valor del semáforo en 1 y, si existen hilos esperando, despierta a uno de ellos.
- **Semáforo Binario (*Binary Semaphore*)**: Semáforo con valor inicial 1 que actúa como un cerrojo (*lock*), restringiendo los estados válidos a 1 (disponible) y 0 (ocupado).
- **Cerrojo de Lectores y Escritores (*Reader-Writer Lock*)**: Primitiva que permite múltiples lecturas concurrentes pero exige exclusión mutua absoluta para cualquier operación de escritura.
- **Limitación de Hilos (*Thread Throttling / Admission Control*)**: Uso de un semáforo inicializado en $N$ para limitar el número máximo de hilos que pueden ingresar simultáneamente a una región de código intensiva en recursos (como asignación masiva de memoria).
- **Zemáforo (*Zemaphore*)**: Construcción conceptual que demuestra cómo implementar un semáforo utilizando únicamente cerrojos mutex y variables de condición.

### Mecanismos y Procesos
- **Sincronización de Ordenamiento (Patrón Join)**:
  - Se inicializa el semáforo en 0.
  - El hilo padre crea al hijo e invoca `sem_wait()`, decrementando el contador a -1 y durmiéndose de inmediato.
  - Al concluir su tarea, el hilo hijo ejecuta `sem_post()`, incrementando el contador a 0 y despertando al padre, garantizando que el padre nunca continúe antes que el hijo.
- **Solución Robusta al Productor-Consumidor**:
  - Utiliza tres semáforos: `empty` (inicializado en $MAX$), `full` (inicializado en 0) y `mutex` (inicializado en 1).
  - El productor ejecuta `sem_wait(&empty)`, luego `sem_wait(&mutex)`, inserta los datos, libera `sem_post(&mutex)` y señala `sem_post(&full)`.
  - Intercambiar el orden de colocación de los cerrojos (adquirir `mutex` antes que `empty` o `full`) provoca un interbloqueo (*deadlock*) cuando la cola se llena o vacía.
- **Solución al Problema de los Filósofos Comensales**:
  - 5 filósofos y 5 tenedores (semáforos en 1). Para comer, el filósofo $p$ adquiere el tenedor izquierdo $p$ y el derecho $(p+1)\%5$.
  - Para romper la dependencia circular que genera interbloqueos, se altera el orden de adquisición para el último filósofo (filósofo 4), haciendo que tome primero el tenedor derecho y luego el izquierdo.

### Ejemplos e Ilustraciones
- **Regla de Inicialización de Kivolowitz**: El valor inicial de un semáforo representa el número de unidades del recurso que el sistema está dispuesto a entregar de inmediato (1 para un cerrojo, 0 para un evento de espera, $N$ para permisos de almacenamiento).
- **Etimología de $P$ y $V$**: Dijkstra denominó a las funciones partiendo de las palabras en holandés *prolaag* (*probeer* + *verlaag*: probar y decrementar) para $P()$, y *verhoog* (incrementar) para $V()$.

### Conexión Lógica y Relevancia
Sintetiza la exclusión mutua y la señalización condicional en una única abstracción matemática. Concluye el estudio de las primitivas fundamentales de sincronización, preparando el terreno para analizar los errores comunes de concurrencia y el interbloqueo (*deadlock*) en los capítulos finales de la sección.

---

## Common Concurrency Problems

### Idea Central
Examina la naturaleza y taxonomía de los errores de concurrencia encontrados en aplicaciones de producción reales (como MySQL, Apache, Mozilla y OpenOffice) a partir de estudios empíricos. Divide los fallos en dos grandes categorías: errores sin interbloqueo (*non-deadlock bugs*, que representan la gran mayoría e incluyen violaciones de atomicidad y de orden) y errores de interbloqueo (*deadlock bugs*). Analiza las cuatro condiciones fundamentales de Coffman necesarias para que ocurra un interbloqueo y evalúa estrategias de prevención, evitación, detección y recuperación.

### Conceptos Clave
- **Violación de Atomicidad (*Atomicity-Violation Bug*)**: Error que ocurre cuando una secuencia de accesos a memoria concebida para ejecutarse de forma indivisible se ve interrumpida por la ejecución concurrente de otro hilo que modifica el estado compartido.
- **Violación de Orden (*Order-Violation Bug*)**: Error que surge cuando el orden de ejecución pretendido entre dos operaciones (por ejemplo, A debe ejecutarse antes que B) no se impone explícitamente, permitiendo que B se ejecute antes que A.
- **Interbloqueo (*Deadlock*)**: Estado de congelamiento en el que dos o más hilos quedan bloqueados indefinidamente porque cada uno posee un recurso que el otro requiere para continuar.
- **Condiciones de Coffman (*Coffman Conditions*)**: Las cuatro condiciones de hardware y software necesarias para que exista un interbloqueo: Exclusión Mutua (*Mutual Exclusion*), Retención y Espera (*Hold-and-Wait*), Sin Expropiación (*No Preemption*) y Espera Circular (*Circular Wait*).
- **Prevención de Interbloqueo (*Deadlock Prevention*)**: Estrategia de diseño que elimina la posibilidad de interbloqueo destruyendo al menos una de las cuatro condiciones de Coffman (por ejemplo, imponiendo un ordenamiento total de cerrojos para evitar la espera circular).
- **Livelock**: Condición en la cual dos o más hilos cambian constantemente de estado en respuesta a los demás (por ejemplo, liberando y reintentando adquirir cerrojos de forma repetida) sin lograr realizar trabajo útil.
- **Evitación de Interbloqueo (*Deadlock Avoidance*)**: Técnica de planificación dinámica que utiliza conocimiento previo sobre las demandas futuras de recursos de cada hilo para programar la ejecución evitando estados inseguros.

### Mecanismos y Procesos
- **Mitigación de Violaciones de Atomicidad y Orden**:
  - Para corregir violaciones de atomicidad, se envuelven las lecturas y escrituras de las variables compartidas dentro de bloques delimitados por un mismo cerrojo (`pthread_mutex_lock` y `pthread_mutex_unlock`).
  - Para corregir violaciones de orden, se emplean variables de condición (`pthread_cond_wait` / `signal`) o semáforos que fuerzan al hilo dependiente a esperar hasta que el hilo inicializador establezca una variable de estado.
- **Eliminación de la Espera Circular**: Se establece un ordenamiento estricto (total o parcial) en la adquisición de cerrojos. Si existen los cerrojos $L1$ y $L2$, todos los hilos del sistema deben adquirir siempre $L1$ antes de $L2$. En estructuras dinámicas con direcciones arbitrarias de memoria, se compara la dirección física de los cerrojos (ej. `if (m1 > m2)`) para decidir el orden de adquisición.
- **Eliminación de Retención y Espera**: Se adquieren todos los cerrojos requeridos de forma atómica envolviendo su llamada dentro de un cerrojo global de prevención (`prevention_lock`).
- **Uso de `pthread_mutex_trylock` (Evitar Sin Expropiación)**: Un hilo intenta adquirir un segundo cerrojo con `trylock()`; si este falla, libera inmediatamente el primer cerrojo que ya poseía y regresa al principio para reintentar el proceso completo, evitando quedar retenido.

### Ejemplos e Ilustraciones
- **Fallo de Atomicidad en MySQL**: Un hilo verifica `if (thd->proc_info)` e inmediatamente intenta imprimir con `fputs(thd->proc_info, ...)`. Un segundo hilo se intercala entre ambas líneas y ejecuta `thd->proc_info = NULL`, provocando un fallo de desreferencia de puntero nulo en el primer hilo al reanudarse.
- **Deadlock en Vectores de Java (`AddAll`)**: La llamada `v1.AddAll(v2)` adquiere primero el cerrojo interno del vector `v1` y luego el de `v2`. Si simultáneamente otro hilo ejecuta `v2.AddAll(v1)`, adquiere el cerrojo de `v2` y luego solicita el de `v1`, generando un interbloqueo por cruce de peticiones encadenadas.

### Conexión Lógica y Relevancia
Sintetiza la aplicación de las primitivas de exclusión mutua y sincronización estudiadas en los capítulos anteriores. Cierra el ciclo de diseño multihilo al proporcionar un catálogo práctico de patrones de fallos y las técnicas necesarias para construir software seguro ante condiciones de carrera y bloqueos.

---

## Event-based Concurrency (Advanced)

### Idea Central
La concurrencia basada en eventos ofrece un modelo alternativo al uso de hilos de ejecución para construir servidores de alto rendimiento (como Node.js, nginx o Flash). Reemplaza la ejecución multihilo por un bucle de eventos (*event loop*) monohilo que recibe e invoca manejadores para procesar notificaciones de E/S. Esta arquitectura elimina la necesidad de cerrojos y sus fallos asociados, otorga control directo sobre la planificación a nivel de aplicación, pero exige el uso estricto de llamadas de E/S asíncronas para evitar bloquear el servidor y requiere gestión manual de pila mediante continuaciones.

### Conceptos Clave
- **Bucle de Eventos (*Event Loop*)**: Estructura central en un servidor basado en eventos que espera continuamente notificaciones de E/S y las despacha a sus manejadores correspondientes de forma secuencial.
- **Manejador de Eventos (*Event Handler*)**: Función callback que procesa una tarea concreta asociada a un evento entrante sin ser interrumpida por otros hilos en el mismo procesador.
- **`select()` / `poll()`**: Llamadas al sistema de E/S multiplexada que permiten a un proceso monohilo monitorear múltiples descriptores de archivos (sockets, archivos) para determinar cuáles están listos para lectura o escritura sin bloquearse.
- **E/S Asíncrona (*Asynchronous / Non-blocking I/O*)**: Interfaz de E/S (como la API POSIX AIO `aio_read`) que inicia una solicitud a disco o red y devuelve el control de forma inmediata al programa antes de completar la transferencia.
- **Gestión Manual de Pila (*Manual Stack Management*)**: Tarea de empaquetar y almacenar explícitamente el estado de una operación en el montón (*heap*) cuando un manejador emite una E/S asíncrona, debido a la ausencia de una pila de llamadas por hilo.
- **Continuación (*Continuation*)**: Estructura de datos almacenada en memoria que guarda las variables y el contexto necesario para que un segundo manejador complete el procesamiento de una solicitud cuando la E/S asíncrona asociada finalice.

### Mecanismos y Procesos
- **Flujo del Bucle de Eventos**:
  1. El servidor inicializa un conjunto de descriptores de archivos (`fd_set`) y llama a `select()`.
  2. La llamada `select()` suspende el proceso en el núcleo hasta que al menos un descriptor esté listo para E/S.
  3. Al retornar `select()`, el bucle recorre los descriptores listos utilizando la macro `FD_ISSET()` e invoca el manejador correspondiente para cada evento.
  4. Dado que el servidor es monohilo, cada manejador se ejecuta hasta su conclusión sin requerir cerrojos de exclusión mutua.
- **Manejo de E/S a Disco con POSIX AIO (`aio_read`)**:
  1. El manejador configura un bloque de control AIO (`struct aiocb`) especificando el descriptor de archivo, el desplazamiento, la longitud y el búfer de destino.
  2. Llama a `aio_read(&aiocb)`; la función inicia la lectura en segundo plano y retorna de inmediato, permitiendo al bucle atender otros eventos.
  3. El servidor comprueba periódicamente el estado de la operación con `aio_error()` o configura un manejador de señales UNIX (`SIGIO`) para recibir una notificación cuando el dispositivo complete la transferencia.

### Ejemplos e Ilustraciones
- **Servidores Web Tipo Node.js o Flash**: Ejemplifican cómo gestionar miles de conexiones TCP concurrentes en un único hilo de CPU, reduciendo la sobrecarga de consumo de memoria por pilas de hilos y eliminando el costo de las conmutaciones de contexto del sistema operativo.
- **Continuación para la Cadena Lectura-Escritura**: Para leer datos de un archivo (`fd`) y enviarlos a un socket de red (`sd`), el servidor emite la lectura asíncrona de `fd` y guarda la relación entre `fd` y `sd` en una tabla hash (la continuación). Cuando la E/S de `fd` concluye, el evento busca en la tabla hash el socket `sd` correspondiente y ejecuta la escritura en la red.

### Conexión Lógica y Relevancia
Presenta un paradigma arquitectónico diametralmente opuesto al modelo multihilo analizado en los Capítulos 26 a 31. Demuestra cómo devolver el control de la planificación a la aplicación resuelve los problemas de rendimiento y sincronización de los cerrojos, preparando el terreno para estudiar el subsistema de E/S.

---

## I/O Devices

### Idea Central
Introduce la arquitectura de hardware y las capas de software necesarias para integrar dispositivos de entrada/salida (E/S) en un sistema de cómputo. Explica la estructura de buses jerárquicos (bus de memoria, PCIe, SATA/USB) y la interfaz canónica de un dispositivo (registros de estado, comando y datos). Detalla cómo el sistema operativo reduce la sobrecarga del procesador mediante el uso de interrupciones de hardware y motores de Acceso Directo a Memoria (DMA), y cómo la abstracción del controlador de dispositivo (*device driver*) permite mantener un núcleo neutral e independiente del hardware específico.

### Conceptos Clave
- **Dispositivo Canónico (*Canonical Device*)**: Modelo abstracto de un componente de hardware compuesto por una interfaz de registros accesibles por software (Status, Command, Data) y un controlador interno compuesto por circuitos o *firmware*.
- **Sondeo (*Polling / Busy-Waiting*)**: Técnica donde la CPU lee repetidamente el registro de estado de un dispositivo en un bucle cerrado a la espera de que quede libre, consumiendo ciclos de cómputo de manera ineficiente.
- **Interrupción de Hardware (*Hardware Interrupt*)**: Señal eléctrica enviada por un dispositivo a la CPU al concluir una operación, lo que permite al SO suspender el proceso en espera, ejecutar otras tareas y saltar a una rutina de atención a la interrupción (*ISR*) cuando el dispositivo responde.
- **Acceso Directo a Memoria (*Direct Memory Access - DMA*)**: Unidad de hardware especializada capaz de transferir bloques de datos entre los dispositivos de E/S y la memoria RAM principal sin requerir la intervención continua de la CPU.
- **E/S por Instrucciones (*Port-Mapped I/O*) vs. Mapeada en Memoria (*Memory-Mapped I/O*)**: La primera utiliza instrucciones especiales de CPU (como `in` y `out` en x86) enviadas a puertos de E/S específicos; la segunda mapea los registros del dispositivo en el espacio de direcciones de memoria física.
- **Controlador de Dispositivo (*Device Driver*)**: Módulo de software del sistema operativo que encapsula las operaciones de bajo nivel de un hardware específico, presentando una interfaz estándar (como la capa de bloques) a las capas superiores del núcleo.

### Mecanismos y Procesos
- **Protocolo de E/S Mediante Interrupciones y DMA**:
  1. El sistema operativo escribe la dirección de memoria de origen/destino y la cantidad de bytes en el controlador DMA.
  2. El SO escribe el comando de lectura o escritura en el registro de comandos del dispositivo.
  3. El SO cambia el estado del proceso solicitante a *Blocked* y conmuta la CPU para ejecutar otro proceso (*overlap*).
  4. El motor DMA transfiere directamente los datos entre el dispositivo y la memoria RAM.
  5. Al finalizar la transferencia, el controlador DMA genera una interrupción de hardware.
  6. La CPU salta al manejador de interrupciones (*ISR*), el cual marca el proceso original como *Ready* para ser reanudado por el planificador.
- **Abstracción en la Pila de Archivos**: Las aplicaciones emiten llamadas estándar POSIX (`read`/`write`). El sistema de archivos las convierte en peticiones de bloques lógicos enviadas a la capa genérica de bloques (*Generic Block Layer*). Esta capa enruta la solicitud al *device driver* específico (SCSI, SATA, NVMe), el cual traduce el comando a las instrucciones de hardware exactas del dispositivo.

### Ejemplos e Ilustraciones
- **Jerarquía de Buses del Sistema**: Muestra la distribución de rendimiento donde los dispositivos rápidos (como tarjetas gráficas y SSDs NVMe) se conectan cerca de la CPU mediante buses PCIe/DMI de alto costo, mientras que dispositivos más lentos (discos SATA, teclados y ratones USB) se ubican en buses periféricos alejados para optimizar el costo y permitir conectar múltiples dispositivos.
- **Driver IDE de xv6**: Código en C de un núcleo didáctico que ilustra cómo las funciones `ide_rw`, `ide_start_request` e `ide_intr` leen y escriben en los registros `0x1F0`-`0x1F7` del controlador de disco IDE mediante instrucciones `in` y `out` en ensamblador x86.

### Conexión Lógica y Relevancia
Representa el capítulo de apertura del tercer y último pilar del libro: la Persistencia (*Persistence*). Establece la infraestructura física y los mecanismos de bajo nivel sobre los cuales se construyen los discos duros, las matrices RAID y los sistemas de archivos en las secciones posteriores.

---

## Hard Disk Drives

### Idea Central
El disco duro mecánico es un dispositivo de almacenamiento persistente no volátil cuya interfaz abstrae la superficie física como un arreglo lineal de sectores de 512 bytes. Su rendimiento está dominado por restricciones mecánicas (movimiento del brazo de lectura/escritura y rotación de los platos), lo que crea una brecha masiva entre el acceso secuencial y el acceso aleatorio. Para reducir esta latencia, los discos y los sistemas operativos utilizan algoritmos de planificación que optimizan los tiempos de búsqueda (*seek*) y rotación (*rotational delay*).

### Conceptos Clave
- **Plato (*Platter*) y Superficie (*Surface*)**: Discos circulares recubiertos con una capa magnética donde se almacenan los datos de forma permanente.
- **Pista (*Track*) y Cilindro (*Cylinder*)**: Círculos concéntricos de sectores en la superficie de un plato; un cilindro agrupa las pistas ubicadas a la misma distancia del centro en todos los platos.
- **Tiempo de Búsqueda (*Seek Time*)**: Tiempo requerido para mover mecánicamente el brazo del disco y posicionar el cabezal sobre la pista deseada; incluye fases de aceleración, velocidad constante, desaceleración y asentamiento (*settling time*).
- **Retardo Rotacional (*Rotational Delay*)**: Tiempo que tarda el plato en girar hasta que el sector solicitado pasa directamente debajo del cabezal de lectura/escritura.
- **Tiempo de Transferencia (*Transfer Time*)**: Tiempo empleado en leer o escribir físicamente los bits a medida que la superficie pasa por el cabezal.
- **Desviación de Pista (*Track Skew*)**: Desfase intencional en la numeración de los sectores entre pistas adyacentes para permitir que lecturas secuenciales continúen sin perder una revolución completa al cambiar de pista.
- **Shortest Seek Time First (SSTF)**: Algoritmo de planificación de disco que atiende primero las solicitudes en las pistas más cercanas al cabezal, propenso a la inanición (*starvation*).
- **SCAN / C-SCAN (Elevador)**: Algoritmos de planificación que barren el disco en ambas direcciones (SCAN) o en un solo sentido circular (C-SCAN) para evitar la inanición.
- **Shortest Positioning Time First (SPTF / SATF)**: Algoritmo de planificación que evalúa simultáneamente el tiempo de búsqueda y el retardo rotacional para seleccionar la solicitud que minimice el tiempo total de posicionamiento.

### Mecanismos y Procesos
- **Cálculo del Tiempo Total de E/S**: El tiempo total para procesar una solicitud se define como $T_{	ext{I/O}} = T_{	ext{seek}} + T_{	ext{rotation}} + T_{	ext{transfer}}$. En accesos aleatorios pequeños (ej. 4 KB), $T_{	ext{seek}}$ y $T_{	ext{rotation}}$ dominan el tiempo total, reduciendo la transferencia efectiva a menos del 1% del ancho de banda máximo. En accesos secuenciales grandes, los costos mecánicos se amortizan sobre una transferencia extensa, alcanzando casi el 100% de la tasa máxima del disco.
- **Planificación Anticipatoria (*Anticipatory Scheduling*)**: Enfoque de planificación no conservador de trabajo (*non-work-conserving*) donde el planificador espera unos milisegundos antes de atender la siguiente solicitud distante, anticipando que el proceso actual emitirá de inmediato una nueva solicitud contigua, reduciendo búsquedas innecesarias.
- **Agrupamiento de E/S (*I/O Merging*)**: Técnica donde el sistema operativo o el controlador del disco combina solicitudes contiguas consecutivas (ej. bloques 33 y 34) en una sola operación física de mayor tamaño para reducir la sobrecarga de comandos.

### Ejemplos e Ilustraciones
- **Comparativa entre Disco SCSI (*Cheetah 15K*) y SATA (*Barracuda*)**: El autor compara un disco de alto rendimiento (15,000 RPM) contra uno de alta capacidad (7,200 RPM). En cargas aleatorias de 4 KB, el Cheetah alcanza apenas ~0.66 MB/s y el Barracuda ~0.31 MB/s; en cargas secuenciales de 100 MB, alcanzan 125 MB/s y 105 MB/s respectivamente, ilustrando la brecha de rendimiento de más de 200 veces entre patrones de acceso aleatorio y secuencial.
- **Demostración de SPTF frente a SSTF**: Si el cabezal está sobre el sector 30 de la pista interna y existen peticiones para el sector 21 (pista media) y el sector 8 (pista externa), SSTF elegirá el sector 21 por estar en una pista más cercana. Sin embargo, si el sector 21 acaba de pasar por el cabezal y requiere una rotación casi completa, SPTF elegirá el sector 8 en la pista externa si el tiempo de desplazamiento del brazo es menor que la espera rotacional del sector 21.

### Conexión Lógica y Relevancia
Sienta las bases físicas del rendimiento de almacenamiento persistente. Explica por qué el patrón de acceso a disco condiciona de manera crítica la arquitectura de los sistemas de archivos y las matrices de discos (RAID), motivando el diseño de estructuras orientadas a escrituras secuenciales en los capítulos posteriores.

---

## Redundant Arrays of Inexpensive Disks (RAIDs)

### Idea Central
RAID es una técnica de virtualización de almacenamiento que combina múltiples discos físicos independientes en una única entidad lógica de gran capacidad, alto rendimiento y alta disponibilidad. Operando de forma transparente para el sistema operativo y las aplicaciones, RAID utiliza técnicas de entrelazado (*striping*), duplicación (*mirroring*) y paridad (*parity*) para optimizar los compromisos entre capacidad útil, tolerancia a fallos y rendimiento en lecturas y escrituras.

### Conceptos Clave
- **Transparencia de Despliegue (*Deployment Transparency*)**: Propiedad por la cual una matriz RAID se presenta ante el sistema operativo como un único disco de bloques, sin requerir modificaciones en las aplicaciones ni en el núcleo.
- **Modelo de Fallo Fail-Stop (*Fail-Stop Fault Model*)**: Supuesto de diseño donde un disco físico solo puede estar en dos estados: completamente operativo o fallado de forma permanente y detectable de inmediato.
- **RAID 0 (Striping)**: Configuración que distribuye los bloques de datos alternadamente entre los discos (*chunk size*) sin almacenar redundancia; ofrece capacidad y rendimiento máximos pero cero tolerancia a fallos.
- **RAID 1 (Mirroring / Mirror de Franjas)**: Configuración que mantiene dos copias idénticas de cada bloque en discos separados, ofreciendo alta tolerancia a fallos y rendimiento en lecturas aleatorias a costa de sacrificar el 50% de la capacidad total.
- **RAID 4 (Paridad Dedicada)**: Configuración que utiliza un único disco dedicado para almacenar la paridad calculada mediante la función XOR sobre los bloques de datos correspondientes de la misma franja (*stripe*).
- **Problema de la Escritura Pequeña (*Small-Write Problem*)**: Cuello de botella en sistemas de paridad donde la reescritura de un único bloque de datos exige leer y escribir el disco de paridad, convirtiéndolo en un punto de contención secuencial.
- **Paridad Subtractiva (*Subtractive Parity*)**: Método para recomputar la paridad de un bloque modificado mediante la fórmula $P_{	ext{nuevo}} = (D_{	ext{viejo}} \oplus D_{	ext{nuevo}}) \oplus P_{	ext{viejo}}$, requiriendo 2 lecturas y 2 escrituras físicas por cada escritura lógica.
- **RAID 5 (Paridad Rotativa)**: Evolución de RAID 4 que distribuye en patrón rotativo los bloques de paridad entre todos los discos de la matriz, eliminando el cuello de botella del disco de paridad dedicado en escrituras aleatorias.

### Mecanismos y Procesos
- **Reconstrucción de Datos Mediante XOR**: La paridad mantiene el invariante de que la suma XOR de todos los bits de una fila (incluyendo el bit de paridad) debe dar como resultado un número par de unos (resultado 0). Si un disco falla, el contenido del bloque perdido se reconstruye aplicando la operación XOR entre los bloques de datos supervivientes de la misma franja y el bloque de paridad.
- **Escritura en Franja Completa (*Full-Stripe Write*)**: En RAID 4 y RAID 5, si una solicitud actualiza simultáneamente todos los bloques de datos de una franja, la paridad se calcula directamente aplicando XOR sobre todos los nuevos bloques de datos y se escribe en paralelo en una sola operación, evitando las lecturas previas de paridad reconstructiva.
- **Problema de la Actualización Consistente (*Consistent-Update Problem*)**: Si ocurre un corte de energía mientras se actualiza un bloque de datos y su correspondiente paridad/espejo, los discos quedan en un estado inconsistente. Las controladoras RAID resuelven esto utilizando registros en memoria RAM no volátil (*NVRAM*) respaldada por batería.

### Ejemplos e Ilustraciones
- **Evaluación de Rendimiento en RAID 5 vs. RAID 4**: En una matriz de $N$ discos con velocidad aleatoria $R$ por disco, RAID 4 satura su disco de paridad en escrituras aleatorias pequeñas, limitando el rendimiento global a $R/2$ MB/s independientemente de cuántos discos se añadan. RAID 5, al rotar la paridad entre todos los discos, distribuye las operaciones y permite alcanzar un rendimiento global de $(N \cdot R) / 4$ MB/s.
- **Matriz de Comparación Teórica**:
  - *RAID 0*: Capacidad $N \cdot B$, tolerancia 0 fallos, rendimiento secuencial $N \cdot S$.
  - *RAID 1*: Capacidad $(N \cdot B)/2$, tolerancia 1 fallo (hasta $N/2$ si son en parejas independientes), lectura aleatoria $N \cdot R$, escritura aleatoria $(N \cdot R)/2$.
  - *RAID 5*: Capacidad $(N - 1) \cdot B$, tolerancia 1 fallo, lectura aleatoria $N \cdot R$, escritura aleatoria $(N \cdot R)/4$.

### Conexión Lógica y Relevancia
Aplica la interposición y la abstracción para solucionar las tres limitaciones físicas clave del disco duro individual expuestas en el Capítulo 37: velocidad, capacidad y confiabilidad. Prepara el terreno para analizar la interfaz de software y la organización de archivos que utilizará estas matrices subyacentes.

---

## Interlude: Files and Directories

### Idea Central
Presenta la API y las abstracciones fundamentales que proporciona el sistema operativo para gestionar el almacenamiento persistente: el archivo y el directorio. Explica el funcionamiento de las llamadas al sistema POSIX para crear, leer, escribir, desplazar y eliminar archivos, destacando cómo el núcleo administra los descriptores de archivo, la tabla de archivos abiertos y los enlaces duros y simbólicos.

### Conceptos Clave
- **Archivo (*File*)**: Arreglo lineal de bytes direccionable de forma arbitraria, referenciado internamente por un identificador numérico único de bajo nivel llamado número de inodo (*i-number*).
- **Directorio (*Directory*)**: Tipo especial de archivo cuyos datos contienen una lista estructurada de parejas (*nombre legible por usuario*, *i-number*).
- **Descriptor de Archivo (*File Descriptor - fd*)**: Entero opaco gestionado por proceso que actúa como un manejador de acceso (*capability*) para realizar operaciones sobre un archivo abierto.
- **Tabla de Archivos Abiertos (*Open File Table*)**: Estructura de datos global en la memoria del sistema operativo que registra los archivos activos, sus contadores de referencias, permisos y el desplazamiento actual de lectura/escritura (*offset*).
- **`lseek()`**: Llamada al sistema que modifica la variable de desplazamiento de posición (*offset*) dentro de la tabla de archivos abiertos sin realizar operaciones de E/S sobre el disco físico.
- **`fsync()`**: Llamada al sistema que fuerza al sistema operativo a vaciar (*flush*) inmediatamente a disco todos los datos y metadatos modificados en el búfer de memoria de un archivo.
- **Opción Atómica `rename()`**: Operación de cambio de nombre que garantiza atomicidad ante fallos del sistema; el archivo conserva su nombre original o adquiere el nuevo sin estados intermedios.
- **Enlace Duro (*Hard Link*)**: Entrada adicional en un directorio que apunta directamente al mismo número de inodo existente, incrementando su contador de enlaces (*link count*).
- **Enlace Simbólico (*Symbolic / Soft Link*)**: Archivo especial independiente cuyo contenido es una cadena de texto que representa la ruta a otro archivo o directorio; puede apuntar a destinos inexistentes (*dangling references*).
- **`unlink()`**: Llamada al sistema que elimina un nombre de enlace en un directorio y decrementa el contador de enlaces del inodo; la memoria física del archivo se libera solo cuando el contador llega a cero y ningún proceso lo mantiene abierto.

### Mecanismos y Procesos
- **Compartición de Descriptores mediante `fork()` y `dup()`**:
  - Al ejecutar `fork()`, el proceso hijo duplica la tabla de descriptores del padre, pero los descriptores apuntan a las **mismas** entradas en la Tabla Global de Archivos Abiertos. Si el hijo modifica el *offset* mediante `lseek()`, el cambio se refleja inmediatamente en el padre.
  - La llamada `dup(fd)` asigna un nuevo descriptor en el mismo proceso que apunta a la misma entrada en la tabla global de archivos abiertos, técnica clave utilizada por las shells de UNIX para implementar la redirección de E/S (`>` y `|`).
- **Patrón de Actualización Atómica de Archivos en Editores**: Para evitar la corrupción de archivos si el sistema se apaga durante un guardado, un editor (como Emacs) escribe la nueva versión en un archivo temporal (`foo.txt.tmp`), ejecuta `fsync()` sobre el archivo temporal, cierra el archivo y finalmente invoca `rename("foo.txt.tmp", "foo.txt")`. El intercambio atómico de `rename` sustituye la versión antigua de golpe.
- **Desconexión y Eliminación de Archivos (`unlink`)**: Cuando se llama a `unlink()`, el sistema borra la entrada en el directorio y resta 1 al campo `st_nlink` del inodo. El sistema de archivos verifica dos condiciones para liberar los bloques de datos y el inodo: que `st_nlink` sea igual a 0 y que el contador de referencias de la tabla de archivos abiertos (`refcnt`) sea 0. Si un proceso mantiene el archivo abierto, la eliminación física se pospone hasta que el proceso ejecute `close()` o finalice.

### Ejemplos e Ilustraciones
- **Descriptores Predeterminados**: Todo proceso UNIX nace con tres descriptores abiertos por defecto en las posiciones de su arreglo: `0` para entrada estándar (`stdin`), `1` para salida estándar (`stdout`) y `2` para error estándar (`stderr`). Al abrir el primer archivo de usuario, la llamada `open()` asigna el entero más bajo libre, que casi siempre es `3`.
- **Diferencia Estructural entre Hard Link y Soft Link**:
  - `ln file file2` crea dos nombres (`file` y `file2`) apuntando al inodo 67158084. Eliminar `file` deja los datos accesibles mediante `file2`.
  - `ln -s file file2` crea un nuevo inodo con tipo `symbolic link` cuyos datos almacenan el texto `"file"`. Si se elimina `file`, `file2` permanece en el directorio pero intentar leerlo devuelve un error de "No tal archivo o directorio" (referencia colgante).

### Conexión Lógica y Relevancia
Conecta las características físicas del hardware (Capítulo 37) y las matrices de discos (Capítulo 38) con las primitivas del sistema operativo accesibles para los programadores. Establece la interfaz conceptual cuyas estructuras de datos e implementación interna se detallarán en los capítulos siguientes (*File System Implementation* y *FFS*).

---

## File System Implementation

### Idea Central
Muestra la implementación práctica de un sistema de archivos simplificado denominado *Very Simple File System* (VSFS) para ilustrar las estructuras en disco y los métodos de acceso esenciales. Explica cómo la organización en bloques, tablas de inodos y mapas de bits permite estructurar archivos y directorios, y cómo el uso de *caching* y *buffering* amortigua el alto costo de las operaciones de entrada/salida a disco.

### Conceptos Clave
- **VSFS (*Very Simple File System*)**: Sistema de archivos didáctico que organiza una partición de disco en bloques de tamaño fijo (por ejemplo, 4 KB) divididos en regiones para datos, inodos, mapas de bits y el superbloque.
- **Inodo (*Index Node - inode*)**: Estructura de datos persistente identificada implícitamente por un número de inodo (*i-number*) que almacena los metadatos de un archivo (tamaño, permisos, propietario, marca de tiempo y punteros a bloques de datos).
- **Índice Multinivel (*Multi-Level Index*)**: Esquema de organización de punteros dentro del inodo que combina punteros directos, indirectos simples, dobles y triples para dar soporte eficiente a archivos pequeños y de gran tamaño.
- **Superbloque (*Superblock*)**: Bloque reservado al inicio del sistema de archivos que contiene metadatos globales sobre la configuración (cantidad de inodos y bloques, ubicación de tablas y número mágico de identificación).
- **Mapa de Bits (*Bitmap*)**: Estructura de asignación donde cada bit representa el estado libre (0) u ocupado (1) de un inodo (*inode bitmap*) o bloque de datos (*data bitmap*).
- **Caché Unificado de Páginas (*Unified Page Cache*)**: Arquitectura en memoria RAM que integra las páginas de memoria virtual y las páginas de archivos para adaptar dinámicamente el uso de memoria según la carga del sistema.
- **Escritura Diferida (*Write Buffering*)**: Técnica que pospone la escritura inmediata a disco reteniendo las modificaciones en memoria durante un intervalo (de 5 a 30 segundos) para agrupar (*batch*), programar y evitar operaciones innecesarias.

### Mecanismos y Procesos
- **Cálculo de Ubicación Física de un Inodo**: Dado un *i-number*, el sistema calcula su dirección de sector físico mediante la fórmula $	ext{blk} = (i 	imes 	ext{sizeof(inode)}) / 	ext{blockSize}$, sumando el resultado a la dirección base del *inode table*.
- **Travesía de Rutas para Abrir Archivos (`open`)**: La búsqueda se inicia siempre en el inodo raíz (inodo 2). Se leen los bloques de datos del directorio raíz para localizar la entrada de la siguiente subcarpeta, recuperando su número de inodo y repitiendo el proceso de forma recursiva hasta hallar el inodo del archivo final e instanciar un descriptor en la tabla de archivos abiertos del proceso.
- **Flujo de Lectura (`read`)**: Consulta el desplazamiento (*offset*) en la tabla de archivos abiertos, lee el inodo para localizar la dirección del bloque de datos correspondiente, transfiere los datos a memoria y actualiza la marca de tiempo de último acceso y el desplazamiento.
- **Flujo de Escritura con Asignación de Bloque**: Genera 5 operaciones de E/S lógicas: lectura del *data bitmap*, escritura del *data bitmap* actualizado (marcando el bloque como ocupado), lectura del inodo, escritura del inodo actualizado (con el nuevo puntero y tamaño) y la escritura del bloque de datos real en disco.

### Ejemplos e Ilustraciones
- **Estructura de Disco de 64 Bloques**: División gráfica de un disco hipotético de 64 bloques de 4 KB donde el bloque 0 es el superbloque, el 1 el mapa de inodos, el 2 el mapa de datos, los bloques 3 al 7 la tabla de inodos (albergando 80 inodos de 256 bytes) y los bloques 8 al 63 la región de datos del usuario.
- **Traza de Creación de Archivos (`/foo/bar`)**: Muestra las 10 operaciones de E/S que provoca crear un archivo (lecturas y escrituras en el mapa de inodos, inodo del directorio padre, datos del directorio padre e inodo del nuevo archivo).

### Conexión Lógica y Relevancia
Conecta las API de archivos y directorios del Capítulo 39 con su representación física en disco y en memoria. Muestra el costo masivo de E/S que acarrean las operaciones simples sobre archivos, justificando la necesidad de optimizaciones de localización física como FFS (Capítulo 41) y mecanismos de consistencia frente a fallos (Capítulo 42).

---

## Locality and The Fast File System

### Idea Central
Introduce el Fast File System (FFS), desarrollado para superar el deficiente rendimiento y la fragmentación del sistema de archivos tradicional de UNIX. FFS incorpora la noción de "conciencia del disco" (*disk awareness*), organizando la superficie física en grupos de cilindros o bloques para posicionar los datos y metadatos relacionados cerca entre sí, maximizando la localidad espacial y el ancho de banda secuencial.

### Conceptos Clave
- **Fast File System (*FFS*)**: Sistema de archivos desarrollado en Berkeley que mantiene la API POSIX estándar pero reestructura la organización interna del disco para optimizar el rendimiento reconociendo las limitaciones mecánicas del hardware.
- **Grupo de Cilindros / Bloques (*Cylinder / Block Group*)**: Agrupación contigua de pistas y bloques en el disco que contiene su propia copia del superbloque, mapas de bits de inodos y datos, tabla de inodos y región de datos.
- **Localidad de Nombre (*Namespace Locality*)**: Principio de diseño basado en la observación empírica de que los archivos dentro de un mismo directorio tienden a accederse juntos, por lo que deben ubicarse dentro del mismo grupo de bloques.
- **Excepción de Archivos Grandes (*Large-File Exception*)**: Heurística que divide los archivos de gran tamaño en fragmentos (*chunks*) y los distribuye entre diferentes grupos de bloques para evitar saturar un solo grupo.
- **Amortización de Tiempos de Búsqueda (*Amortization*)**: Selección de un tamaño de fragmento lo suficientemente grande para que el tiempo dedicado a la transferencia secuencial supere con creces el tiempo de búsqueda (*seek*) entre fragmentos.
- **Sub-bloques (*Sub-blocks*)**: Divisiones pequeñas de bloques (por ejemplo, 512 bytes dentro de un bloque de 4 KB) introducidas en FFS para reducir la fragmentación interna causada por archivos pequeños.

### Mecanismos y Procesos
- **Políticas de Ubicación de Directorios y Archivos**:
  1. *Directorios*: Se selecciona un grupo de bloques que posea un número bajo de directorios asignados y un elevado número de inodos libres para equilibrar la carga a lo largo del disco.
  2. *Archivos*: Se asigna el inodo del archivo en el mismo grupo de bloques donde reside el directorio padre, y sus bloques de datos se ubican en el mismo grupo que su inodo.
- **Manejo de Archivos Grandes**: Los primeros 12 bloques directos se asignan en el mismo grupo que el inodo. Cada bloque indirecto posterior (y los 1024 bloques a los que apunta, sumando 4 MB) se asigna a un grupo de bloques diferente con baja utilización, amortizando la búsqueda entre grupos mediante transferencias continuas.

### Ejemplos e Ilustraciones
- **Estudio de Localidad de Rastros SEER**: Muestra datos empíricos donde cerca del 40% de los accesos a archivos ocurren dentro del mismo directorio o en el archivo accedido previamente, confirmando la validez de la heurística de FFS.
- **Ubicación Parámetrizada (*Parameterized Placement*)**: Ilustra cómo en discos antiguos se escalonaban los sectores asignados (saltando un sector entre bloques contiguos) para dar tiempo a la CPU de emitir la siguiente orden de lectura antes de que el sector deseado pasara de largo bajo el cabezal.

### Conexión Lógica y Relevancia
Resuelve las ineficiencias de rendimiento y fragmentación del modelo VSFS básico expuesto en el Capítulo 40. Al reorganizar el espacio en estructuras conscientes del hardware, establece el paradigma moderno de diseño para sistemas de archivos basados en bloques como Linux `ext2`, `ext3` y `ext4`.

---

## Crash Consistency: FSCK and Journaling

### Idea Central
Aborda el problema de la consistencia ante fallos (*crash-consistency problem*), que ocurre cuando un corte de energía o un fallo del sistema interrumpe una secuencia de escrituras en disco dejando las estructuras de datos en un estado inconsistente o corrupto. Evalúa la solución tradicional basada en verificadores tardíos (`fsck`) y la solución moderna basada en registro en diario (*journaling* o *write-ahead logging*), analizando sus variantes de datos y de metadatos.

### Conceptos Clave
- **Problema de Consistencia ante Fallos (*Crash-Consistency Problem*)**: Inconsistencia que surge cuando una operación lógica del sistema de archivos requiere actualizar múltiples bloques en disco pero el sistema se apaga tras completar solo una parte de dichas escrituras.
- **Verificador del Sistema de Archivos (*FSCK - File System Checker*)**: Herramienta tradicional que se ejecuta tras un reinicio inesperado para auditar todas las estructuras del disco, corregir discrepancias entre inodos y mapas de bits y restaurar la consistencia básica.
- **Registro en Diario (*Journaling / Write-Ahead Logging*)**: Técnica que escribe previamente una transacción en un área reservada del disco (*journal*) describiendo los cambios planificados antes de sobreescribir las estructuras en sus ubicaciones finales.
- **Punto de Control (*Checkpointing*)**: Fase del proceso de *journaling* en la que las modificaciones guardadas y comprometidas en el diario se escriben en sus ubicaciones definitivas en el sistema de archivos.
- **Registro en Diario Completo (*Data Journaling*)**: Modo de operación donde tanto los datos de usuario como los metadatos se escriben en el diario antes de ser guardados en el sistema de archivos, ofreciendo máxima seguridad a costa de duplicar el tráfico de E/S.
- **Registro en Diario de Metadatos / Ordenado (*Metadata / Ordered Journaling*)**: Modo de operación común donde solo los metadatos se escriben en el diario, imponiendo que los bloques de datos de usuario se escriban físicamente en el disco *antes* de comprometer la transacción de metadatos en el diario.
- **Barrera de Escritura (*Write Barrier*)**: Instrucción emitida al dispositivo de almacenamiento para asegurar que todas las escrituras previas se hayan grabado en la superficie física del disco antes de procesar las escrituras posteriores.
- **Registro de Revocación (*Revoke Record*)**: Registro especial utilizado en el diario para evitar que la reejecución (*replay*) de transacciones antiguas sobreescriba datos de bloques que han sido liberados y reasignados a nuevos archivos.

### Mecanismos y Procesos
- **Protocolo de Data Journaling (3 fases)**:
  1. *Journal Write*: Se escriben el bloque de inicio de transacción (`TxB`), los metadatos modificados y los bloques de datos en el diario.
  2. *Journal Commit*: Se escribe el bloque de fin de transacción (`TxE`) en el diario de forma atómica.
  3. *Checkpoint*: Se escriben los bloques en sus ubicaciones reales en el sistema de archivos y se marca la transacción como libre en el superbloque del diario.
- **Protocolo de Metadata Journaling (Ordered Mode)**:
  1. *Data Write*: Se escriben los datos de usuario en sus ubicaciones finales en disco y se espera la confirmación.
  2. *Journal Metadata Write*: Se escribe el `TxB` y los metadatos en el diario.
  3. *Journal Commit*: Se escribe el `TxE` en el diario.
  4. *Checkpoint Metadata*: Se escriben los metadatos en sus ubicaciones reales.
  5. *Free*: Se libera la transacción en el diario.
- **Recuperación tras Fallo (*Redo Logging*)**: Al reiniciar tras un apagón, el sistema escanea el diario circular. Ignora transacciones incompletas (sin `TxE` o con suma de comprobación errónea) y reejecuta secuencialmente todas las transacciones completamente comprometidas (`committed`), garantizando consistencia en segundos sin importar el tamaño del disco.

### Ejemplos e Ilustraciones
- **Anexado de un Bloque a un Archivo**: Detalla las tres escrituras requeridas (inodo actualizado $I[v2]$, mapa de datos actualizado $B[v2]$ y bloque de datos $D_b$) y muestra cómo un corte de luz entre cualquiera de ellas genera archivos corruptos, fuga de espacio o punteros a datos basura.
- **Analogía de las Llaves de FSCK**: El autor compara la ineficiencia de `fsck` con dejar caer las llaves en el dormitorio y proceder a buscar en toda la casa habitación por habitación desde el sótano; funciona, pero resulta inaceptablemente lento en discos de gran capacidad.

### Conexión Lógica y Relevancia
Resuelve el mayor riesgo de persistencia identificado en los Capítulos 40 y 41: la vulnerabilidad ante cortes de energía durante escrituras complejas. Sienta las bases de confiabilidad que utilizan sistemas de archivos modernos como Linux `ext3`, `ext4`, `NTFS` y `XFS`, preparando el camino para estudiar sistemas alternativos como Log-Structured File Systems (Capítulo 43).

---

## Log-structured File Systems

### Idea Central
El sistema de archivos estructurado en logs (LFS) replantea el almacenamiento en disco al convertir todas las escrituras (tanto de datos como de metadatos) en un flujo secuencial continuo dentro de un búfer en memoria llamado segmento, el cual se escribe en ubicaciones libres sin sobreescribir datos existentes. Esta técnica maximiza el rendimiento de escritura al aprovechar el ancho de banda secuencial del disco y evitar las búsquedas aleatorias de FFS, introduciendo a su vez el desafío de la recolección de basura (*garbage collection*) para limpiar versiones obsoletas de bloques.

### Conceptos Clave
- **LFS (*Log-structured File System*)**: Sistema de archivos que acumula todas las actualizaciones en un log secuencial en memoria antes de escribirlas de forma contigua en disco.
- **Segmento (*Segment*)**: Bloque grande de memoria (normalmente de varios megabytes) utilizado por LFS para agrupar escrituras en un único búfer antes de transferirlas secuencialmente al dispositivo físico.
- **Mapa de Inodos (*Inode Map - imap*)**: Estructura de indirección que toma un número de inodo y devuelve la ubicación física más reciente de dicho inodo en el disco, resolviendo la dispersión de inodos provocada por la falta de sobreescritura in situ.
- **Región de Control / Punto de Control (*Checkpoint Region - CR*)**: Ubicación fija en disco que almacena los punteros a los fragmentos del mapa de inodos y que se actualiza periódicamente (por ejemplo, cada 30 segundos).
- **Problema de la Actualización Recursiva (*Recursive Update Problem*)**: Dilema donde mover un inodo exigiría actualizar el directorio padre, y este a su vez a su directorio superior hasta la raíz; LFS lo evita al aislar los cambios de ubicación dentro del `imap`.
- **Limpieza de Segmentos (*Segment Cleaning / Garbage Collection*)**: Proceso en segundo plano que lee segmentos parcialmente obsoletos, identifica los bloques vivos, los reubica en un nuevo segmento y libera los segmentos antiguos.
- **Bloque Resumen de Segmento (*Segment Summary Block - SS*)**: Cabecera en cada segmento que registra la identidad (inodo y desplazamiento) de cada bloque de datos almacenado, permitiendo determinar si un bloque sigue vivo.

### Mecanismos y Procesos
- **Flujo de Escritura y Búfer**: LFS acumula en un segmento en RAM tanto los bloques de datos como los inodos actualizados y las porciones correspondientes del `imap`. Cuando el segmento se llena, se emite una única escritura secuencial masiva a una región libre del disco.
- **Búsqueda y Lectura de Archivos**:
  1. El sistema consulta la *Checkpoint Region* (CR) para localizar las partes del `imap`.
  2. Mediante el número de inodo, el `imap` devuelve la dirección de disco exacta del inodo más reciente.
  3. LFS lee el inodo y accede a sus punteros directos o indirectos para recuperar el bloque de datos del mismo modo que un sistema UNIX tradicional.
- **Mecanismo de Recolección de Basura (*Liveness Check*)**:
  1. El limpiador escanea el `Segment Summary Block` del segmento objetivo para obtener el número de inodo $N$ y el desplazamiento $T$ de un bloque ubicado en la dirección $A$.
  2. Consulta en el `imap` la ubicación del inodo $N$ y verifica si la entrada $T$ de dicho inodo apunta a $A$.
  3. Si apunta a $A$, el bloque está vivo y se copia al nuevo segmento; si apunta a otra dirección, es basura (*dead*) y se descarta.

### Ejemplos e Ilustraciones
- **Anexo en FFS vs. LFS**: Mientras que crear un archivo pequeño en FFS requiere múltiples escrituras dispersas (bitmap de inodos, inodo, bloque de directorio, bitmap de datos y bloque de datos), LFS agrupa todas esas estructuras en un único segmento contiguo y las escribe de una sola pasada.
- **Metáfora del Periódico / Diario**: LFS funciona como un diario donde las entradas nunca se borran ni se corrigen en la página original; en su lugar, se añade una nueva entrada al final indicando los cambios, requiriendo un proceso posterior de resumen para descartar borradores antiguos.

### Conexión Lógica y Relevancia
Conecta directamente con las limitaciones de FFS (Capítulo 41) y la técnica de *journaling* (Capítulo 42) al llevar el principio de registro secuencial al extremo: todo el sistema de archivos se convierte en un log. Constituye el pilar conceptual de la arquitectura de la copia en escritura (*Copy-on-Write / COW*) usada en sistemas como ZFS, Btrfs y la capa FTL de las unidades SSD.

---

## Flash-based SSDs

### Idea Central
Las unidades de estado sólido basadas en memoria Flash NAND (SSDs) reemplazan la mecánica de los discos duros por transistores de silicio no volátiles, ofreciendo accesos aleatorios de baja latencia. Su diseño está condicionado por la asimetría funcional entre operaciones (las lecturas y programaciones ocurren por páginas de pocos kilobytes, mientras que el borrado ocurre por bloques grandes de cientos de kilobytes o megabytes) y por el desgaste de las celdas (*wear out*), lo que obliga a emplear una Capa de Traducción de Flash (*FTL*) basada en logs para gestionar la redirección de bloques, la recolección de basura y el nivelado de desgaste.

### Conceptos Clave
- **Flash NAND**: Tecnología de semiconductores no volátil estructurada en celdas (SLC, MLC, TLC) que almacenan bits mediante cargas eléctricas atascadas en transistores.
- **Página Flash (*Flash Page*)**: Unidad básica de lectura y programación (escritura) de entre 2 KB y 8 KB.
- **Bloque de Borrado (*Erase Block*)**: Agrupación de múltiples páginas (entre 128 KB y 2 MB) que constituye la unidad mínima sobre la cual se puede ejecutar la operación de borrado.
- **Programación (*Program*)**: Operación de bajo nivel que cambia bits de 1 a 0 para escribir datos en una página previamente borrada.
- **Capa de Traducción de Flash (*FTL - Flash Translation Layer*)**: Software/firmware interno del controlador SSD que abstrae la memoria Flash presentando una interfaz estándar de bloques lógicos al sistema operativo.
- **Amplificación de Escritura (*Write Amplification*)**: Razón entre el total de bytes físicamente escritos en las celdas Flash por la FTL y los bytes solicitados por el cliente/sistema operativo.
- **Nivelado de Desgaste (*Wear Leveling*)**: Algoritmo de la FTL que distribuye uniformemente los ciclos de borrado/programación (P/E) entre todos los bloques físicos de la unidad para evitar el fallo prematuro de bloques populares.
- **Comando TRIM**: Notificación de la API de almacenamiento mediante la cual el sistema operativo informa al SSD que ciertas direcciones de bloques lógicos ya no contienen datos válidos, facilitando la recolección de basura.

### Mecanismos y Procesos
- **Ciclo de Vida de las Páginas**:
  1. *INVALID*: Estado inicial de una página desconfigurada o que contiene datos obsoletos.
  2. *ERASED*: Estado alcanzado tras borrar todo el bloque físico; establece todos los bits en 1 y habilita la página para ser programada.
  3. *VALID*: Estado adquirido al ejecutar el comando `Program`, donde los bits se ajustan para guardar datos útiles. No se puede reprogramar una página `VALID` sin borrar antes el bloque completo.
- **Organización de la FTL Híbrida (*Hybrid Mapping*)**:
  - Mantiene un conjunto pequeño de *log blocks* mapeados a nivel de **página** (*page-level mapping*) para recibir escrituras aleatorias rápidas.
  - La gran mayoría del SSD utiliza mapeo a nivel de **bloque** (*block-level mapping*) para ahorrar espacio en la RAM del FTL.
  - Cuando los *log blocks* se llenan, se consolidan con los bloques de datos mediante operaciones de fusión (*switch merge*, *partial merge* o *full merge*).
- **Recolección de Basura en la FTL**: La FTL selecciona bloques con páginas muertas (*garbage*), lee las páginas aún válidas hacia el búfer en RAM, las escribe en un nuevo bloque libre dentro del log y borra (*erase*) el bloque antiguo para retornar sus páginas al estado `ERASED`.

### Ejemplos e Ilustraciones
- **Desgaste P/E por Tipo de Celda**: Las celdas SLC (1 bit por celda) soportan hasta ~100,000 ciclos de borrado/programación, mientras que las MLC (2 bits) y TLC (3 bits) ofrecen ~10,000 y ~1,000-3,000 ciclos respectivamente debido a la degradación por acumulación de carga residual en los aislamientos del transistor.
- **Efecto de las Fusiones (*Merge Cases*)**: En una *switch merge*, un bloque de log escrito en orden secuencial sustituye directamente a un bloque de datos desactualizado con costo de E/S casi nulo. En una *full merge*, el SSD debe recopilar páginas dispersas de múltiples bloques para reconstruir un bloque contiguo, elevando drásticamente la amplificación de escritura.

### Conexión Lógica y Relevancia
Introduce el medio de almacenamiento persistente moderno que compite con los discos mecánicos del Capítulo 37. Demuestra cómo las técnicas de estructuración en log diseñadas originalmente para discos duros en LFS (Capítulo 43) resurgieron internamente dentro del controlador de hardware de los SSDs para mitigar los costos de borrado y prolongar la vida útil de las celdas.

---

## Data Integrity and Protection

### Idea Central
La integridad de datos abarca los mecanismos de software y hardware necesarios para detectar y corregir fallos parciales e indetectables de almacenamiento, como los errores de sector latente (LSEs) y la corrupción silenciosa de datos (*silent data corruption*). Mediante la adición de sumas de comprobación (*checksums*), identificadores físicos e inspección periódica de disco (*scrubbing*), el sistema operativo o el sistema de archivos garantiza que los datos leídos coincidan exactamente con los que fueron escritos originalmente.

### Conceptos Clave
- **Fallo Parcial (*Fail-Partial Model*)**: Modelo de fallos realista donde una unidad de almacenamiento parece funcionar normalmente pero sufre fallos localizados en bloques específicos.
- **Error de Sector Latente (*Latent Sector Error - LSE*)**: Error en el cual un sector de disco o celda no se puede leer debido a daño físico o fallo grave detectado directamente por el código de corrección de errores (ECC) del propio dispositivo.
- **Corrupción Silenciosa (*Silent Data Corruption*)**: Modificación inadvertida de los datos almacenados producida por *firmware* defectuoso, buses corruptos o fallos de lectura/escritura que el controlador del disco no detecta ni reporta.
- **Suma de Comprobación (*Checksum*)**: Función matemática (como XOR, adición, Fletcher o CRC) que calcula un resumen compacto de bytes (ej. 4 a 8 bytes) sobre un bloque de datos para verificar su integridad.
- **Escritura Misdirigida (*Misdirected Write*)**: Fallo donde el controlador del disco escribe un bloque válido de datos en una dirección física o disco equivocado.
- **Escritura Perdida (*Lost Write*)**: Fallo en el cual el dispositivo confirma la recepción y finalización de una escritura pero nunca persiste físicamente los datos en el medio magnético o flash.
- **Limpieza de Disco (*Disk Scrubbing*)**: Tarea en segundo plano realizada periódicamente por el sistema de archivos que lee todos los bloques del disco para verificar sus sumas de comprobación y reparar errores latentes antes de que causen pérdida irrecoverable.

### Mecanismos y Procesos
- **Verificación de Integridad con Checksum**:
  1. *Escritura*: El sistema calcula la suma de comprobación $C(D)$ sobre el bloque de datos $D$ y guarda ambos en disco.
  2. *Lectura*: El sistema lee el bloque $D$ y la suma almacenada $C_s(D)$.
  3. *Comprobación*: Calcula en tiempo real la suma sobre los datos leídos $C_c(D)$. Si $C_s(D) == C_c(D)$, los datos son válidos. Si discrepan, se detecta corrupción y se intenta recuperar el bloque usando copias redundantes (como en RAID o ZFS).
- **Protección contra Escrituras Misdirigidas**: Se incluye un identificador físico (número de disco y número de bloque) junto con la suma de comprobación. Al leer el bloque, si el identificador recuperado no coincide con la dirección que se pretendía leer, el sistema detecta la escritura misdirigida.
- **Protección contra Escrituras Perdidas**:
  - *Enfoque indirecto (ej. ZFS)*: Guarda la suma de comprobación del bloque de datos dentro del inodo padre o bloque indirecto en lugar de guardarla en el propio bloque de datos. Si se pierde la escritura del bloque de datos, la suma leída en el inodo no coincidirá con el bloque antiguo no actualizado.
  - *Read-after-write*: Lee el bloque inmediatamente después de escribirlo para verificar su presencia, aunque duplica las operaciones de E/S.

### Ejemplos e Ilustraciones
- **Colisión de Checksum**: Situación analógica donde dos bloques de datos totalmente distintos generan la misma suma de comprobación; algoritmos robustos como CRC-32 o hashes criptográficos reducen la probabilidad de colisiones a niveles prácticamente nulos frente a funciones simples de suma o XOR.
- **Doble Fallo en RAID-5 (LSE durante Reconstrucción)**: Si un disco falla en una matriz RAID-5 y durante el proceso de reconstrucción sobre un disco de repuesto (*hot spare*) se detecta un error LSE en uno de los discos supervivientes, la reconstrucción falla por completo. Esto motiva el desarrollo de arquitecturas como RAID-DP (doble paridad).

### Conexión Lógica y Relevancia
Concluye la sección de persistencia y la arquitectura general del sistema operativo. Expande el modelo simplificado de fallos *fail-stop* de RAID (Capítulo 38) hacia la realidad física del hardware (*fail-partial*), demostrando cómo los sistemas de archivos avanzados (como ZFS y Btrfs) combinan la arquitectura de copia en escritura, sumas de comprobación e indirección para garantizar la integridad completa de la información.

---

## Distributed Systems

### Idea Central
Introduce los conceptos fundamentales de los sistemas distribuidos, centrándose en el desafío principal: construir un servicio confiable a partir de componentes individuales (máquinas, redes, discos) que pueden fallar de manera independiente. Examina las capas de comunicación, la abstracción de la Llamada a Procedimiento Remoto (*Remote Procedure Call - RPC*) y los inconvenientes de modelos como la Memoria Compartida Distribuida (*Distributed Shared Memory - DSM*).

### Conceptos Clave
- **Sistema Distribuido (*Distributed System*)**: Conjunto de computadoras independientes interconectadas por red que colaboran para ofrecer un servicio unificado a los clientes.
- **Fallo Parcial e Independiente (*Partial / Independent Failure*)**: Propiedad clave de los sistemas distribuidos donde una máquina o enlace de red puede fallar sin que el resto del sistema deje de funcionar, complicando la detección y recuperación de errores.
- **Llamada a Procedimiento Remoto (*Remote Procedure Call - RPC*)**: Abstracción de lenguaje de programación que permite ejecutar un procedimiento en una máquina remota de forma tan transparente como si fuera una función local.
- **Generador de Talones (*Stub Generator / Protocol Compiler*)**: Herramienta de software que automatiza el empaquetado (*marshaling*) y desempaquetado (*unmarshaling*) de parámetros y resultados entre el cliente y el servidor.
- **Serialización / Embalaje (*Marshaling / Serialization*)**: Proceso de convertir variables y estructuras de datos de la memoria en un búfer contiguo de bytes listo para ser transmitido por la red.
- **Memoria Compartida Distribuida (*Distributed Shared Memory - DSM*)**: Enfoque donde la memoria virtual de múltiples máquinas se unifica mediante el manejador de fallos de página del sistema operativo; sufrió problemas graves de rendimiento y manejo de fallos que impidieron su adopción práctica.
- **Representación Externa de Datos (*XDR - External Data Representation*)**: Capa de abstracción en RPC que resuelve las diferencias de orden de bytes (*endianness*) entre distintas arquitecturas de hardware.

### Mecanismos y Procesos
- **Flujo de Ejecución de RPC**:
  1. El cliente llama a la función local en el *stub* del cliente.
  2. El *client stub* empaqueta (*marshaling*) la identificación de la función y sus argumentos en un búfer de bytes.
  3. La librería de tiempo de ejecución de RPC envía el mensaje mediante un protocolo de red (generalmente UDP con temporizadores de retransmisión y reconocimientos).
  4. El servidor recibe el paquete; el *server stub* desempaqueta (*unmarshaling*) los datos e invoca la función real del servidor (frecuentemente dentro de un conjunto de hilos o *thread pool* concurrente).
  5. El resultado se empaqueta y se transmite de vuelta al cliente, donde el *client stub* lo desempaqueta y retorna el control a la aplicación.
- **Mantenimiento de Confiabilidad sobre Capas No Confiables**: Dado que protocolos como UDP pueden perder paquetes, la capa de tiempo de ejecución de RPC implementa mecanismos de reintento por tiempo de espera (*timeout/retry*) y confirmaciones de recepción (*acknowledgments - ACKs*), asignando números de secuencia para descartar duplicados y garantizar semánticas de ejecución adecuadas.

### Ejemplos e Ilustraciones
- **El Argumento Fin a Fin (*End-to-End Argument*)**: Principio formulado por Saltzer, Reed y Clark que establece que ciertas funciones (como la transferencia confiable de un archivo) solo pueden ser implementadas de forma correcta y completa en los extremos de la aplicación, ya que garantizar confiabilidad en capas de red inferiores no previene la corrupción en la memoria o disco del emisor o receptor.
- **Infraestructuras Modernas de RPC**: El texto contrapone implementaciones clásicas como Sun RPC (`rpcgen`) con alternativas modernas como gRPC de Google y Apache Thrift.

### Conexión Lógica y Relevancia
Representa la apertura de la cuarta y última sección del libro: la Distribución (*Distribution*). Establece las bases de comunicación en red y manejo de fallos parciales sobre las que se construyen los sistemas de archivos distribuidos analizados en los capítulos posteriores.

---

## Sun’s Network File System (NFS)

### Idea Central
Analiza la arquitectura del sistema de archivos distribuido NFS (en su versión 2), cuyo objetivo primordial es ofrecer una recuperación rápida y sencilla ante fallos del servidor. Para lograrlo, NFS emplea un protocolo apátrida (*stateless protocol*) basado en identificadores opacos de archivo (*file handles*) y operaciones idempotentes, gestionando el rendimiento mediante almacenamiento en caché en el cliente y políticas de consistencia como la escritura al cerrar (*flush-on-close*).

### Conceptos Clave
- **Protocolo Apátrida (*Stateless Protocol*)**: Diseño donde el servidor no mantiene información de estado sobre los clientes (como archivos abiertos o posiciones de puntero), permitiendo que el servidor se reinicie tras un fallo sin requerir un protocolo complejo de recuperación.
- **Manejador de Archivo (*File Handle*)**: Identificador único y opaco de 32 bytes compuesto por un identificador de volumen (*volume ID*), número de inodo (*inode number*) y número de generación (*generation number*) para evitar accesos indebidos a inodos reutilizados.
- **Operación Idempotente (*Idempotent Operation*)**: Operación cuyo resultado o efecto final en el sistema es idéntico independientemente de si se ejecuta una única vez o múltiples veces de forma repetida.
- **Semántica Flush-on-Close / Close-to-Open**: Política de consistencia en el cliente NFS que fuerza el envío de todas las páginas de memoria modificadas al servidor en el momento exacto en que la aplicación cierra un archivo (`close()`).
- **Caché de Atributos (*Attribute Cache*)**: Caché local en el cliente que almacena los metadatos de los archivos (obtenidos mediante `GETATTR`) durante un breve intervalo para reducir el volumen de mensajes de validación enviados al servidor.
- **VFS / Vnode (*Virtual File System / Virtual Node*)**: Capa de abstracción introducida por Sun en el sistema operativo para permitir que múltiples sistemas de archivos (locales y distribuidos) coexistan bajo una misma interfaz de sistema de archivos en el núcleo.

### Mecanismos y Procesos
- **Manejo de Fallos mediante Reintentos e Idempotencia**:
  - Si un cliente no recibe respuesta a una solicitud de lectura, escritura o consulta (debido a pérdida de paquete o reinicio del servidor), retransmite la petición tras vencer un temporizador (*timeout*).
  - Dado que escrituras (`WRITE`), lecturas (`READ`) y búsquedas (`LOOKUP`) son idempotentes (especifican el *file handle* y el desplazamiento exacto `offset`), ejecutar la misma escritura dos veces no corrompe el archivo.
- **Validación de Caché en el Cliente**:
  - Antes de entregar datos leídos desde la caché local, el cliente consulta la hora de última modificación del archivo en el servidor (`GETATTR`). Si la fecha del servidor es más reciente que la versión en caché, el cliente invalida sus datos locales y descarga el archivo de nuevo.
- **Escrituras Obligatorias en el Servidor**:
  - El servidor NFSv2 no responde con éxito a un mensaje de escritura `WRITE` hasta que los datos hayan sido persistidos físicamente en el disco o en memoria RAM respaldada por batería (NVRAM).

### Ejemplos e Ilustraciones
- **Los Tres Tipos de Pérdida de Mensajes**: Un análisis de fallos muestra que la ausencia de respuesta puede deberse a 1) pérdida del mensaje de solicitud en la red, 2) servidor caído, o 3) pérdida del mensaje de respuesta del servidor. Gracias a la idempotencia, el cliente maneja los tres escenarios retransmitiendo la misma solicitud.
- **Fallo de Idempotencia en `MKDIR`**: La creación de directorios no es strictly idempotente; si la respuesta de éxito de un `MKDIR` se pierde y el cliente retransmite la petición, el servidor devuelve un error de "directorio existente", representando un caso particular dentro del diseño del protocolo.

### Conexión Lógica y Relevancia
Aplica los principios de RPC del Capítulo 48 para construir un sistema de archivos distribuido de amplia adopción industrial. Demuestra cómo las decisiones de diseño enfocadas en la recuperación simple ante fallos impelen compromisos en la consistencia de la caché y en el rendimiento de escritura en el servidor.

---

## The Andrew File System (AFS)

### Idea Central
Examina el sistema de archivos distribuido AFS (desarrollado en la Universidad Carnegie Mellon), diseñado con un enfoque prioritario en la escalabilidad (*scalability*) para soportar miles de clientes por servidor. AFS logra este objetivo mediante el almacenamiento en caché de archivos completos en el disco local del cliente y la introducción del mecanismo de *callbacks*, garantizando una semántica de consistencia clara y reduciendo al mínimo la interacción con el servidor.

### Conceptos Clave
- **Escalabilidad (*Scalability*)**: Capacidad de una arquitectura de sistema para mantener un rendimiento adecuado a medida que se incrementa masivamente el número de clientes o dispositivos conectados a un servidor central.
- **Caché de Archivo Completo (*Whole-File Caching*)**: Enfoque de AFS donde la totalidad de un archivo se descarga y almacena en el disco local del cliente durante la operación `open()`.
- **Callback**: Promesa o compromiso mantenido por el servidor AFS de notificar proactivamente al cliente cuando otro usuario modifique un archivo que el cliente tiene almacenado en su caché local.
- **Ruptura de Callback (*Callback Break*)**: Mensaje enviado por el servidor a todos los clientes que están almacenando una copia de un archivo para invalidar sus cachés locales cuando un cliente envía una nueva versión.
- **Identificador de Archivo (*FID - File Identifier*)**: Estructura de dirección en AFS (similar al *file handle* de NFS) compuesta por un identificador de volumen (*Volume ID*), identificador de archivo de vnode (*Vnode ID*) y un unificador (*Uniquifier*) para soportar reutilización de inodos.
- **Consistencia "El Último en Cerrar Gana" (*Last-Closer-Wins*)**: Modelo de consistencia donde si múltiples clientes modifican el mismo archivo simultáneamente, la versión completa guardada por el cliente que ejecuta la última llamada `close()` se convierte en la imagen definitiva en el servidor.

### Mecanismos y Procesos
- **Flujo de Trabajo con Callbacks (AFSv2)**:
  1. Un cliente ejecuta `open()` sobre un archivo. Si el archivo no está en la caché local, envía un mensaje `Fetch` al servidor especificando el FID.
  2. El servidor envía el archivo completo, guarda un *callback* asociando la dirección IP del cliente con dicho FID y retorna el control.
  3. Todas las lecturas (`read`) y escrituras (`write`) posteriores ocurren sobre la copia en el disco local a velocidad nativa sin mensajes de red.
  4. Al llamar a `close()`, si el archivo fue modificado, el cliente envía la nueva versión completa al servidor mediante un mensaje `Store`.
  5. Al recibir el `Store`, el servidor actualiza su disco y emite una ruptura de *callback* (*callback break*) a todos los demás clientes que tengan guardado dicho FID.
- **Recuperación tras Fallos en AFS**:
  - Dado que los *callbacks* se almacenan en la memoria RAM del servidor, si el servidor sufre un apagón o reinicio, pierde la lista de *callbacks*. Al reiniciar, notifica a los clientes mediante un mensaje de latido (*heartbeat*); los clientes deben marcar temporalmente todas sus entradas de caché como sospechosas y emitir un mensaje `TestAuth` antes del próximo uso para revalidarlas.

### Ejemplos e Ilustraciones
- **Comparativa Cualitativa entre AFS y NFS**: En lecturas repetidas de archivos grandes que exceden la memoria RAM del cliente, NFS debe descargar continuamente los bloques por la red, mientras que AFS lee directamente de su caché en el disco local. No obstante, en archivos enormes donde solo se modifica un byte (como en una base de datos), AFS sufre una penalización al tener que transferir el archivo completo en el `open` y el `close`.
- **Etimología de Vice y Venus**: La arquitectura de AFS denominaba *Vice* al conjunto de servicios del servidor central y *Venus* al proceso demonio cliente que corre en la máquina del usuario interceptando las llamadas al sistema.

### Conexión Lógica y Relevancia
Cierra el bloque de sistemas distribuidos y la totalidad de los capítulos de la obra. Contrasta con NFS al demostrar cómo añadir estado (*callbacks*) en el servidor permite escalar a miles de clientes, sirviendo como la base conceptual para el diseño de repositorios de código y sistemas de sincronización modernos.
