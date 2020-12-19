Fuente: **Antoni Simelio**, Ingeniero de Control de Sistemas.

Puestos ocupados:

 

| Centro                                         | Departamento                           | Puesto                          | Rol                                                          |
| ---------------------------------------------- | -------------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| **Centro Espacial Europeo (Guayana Francesa)** | Sistema de Control del Sector de Suelo | Ingeniero de Control            | A)   Soyuz: Diseño, Implementación e integración en el Control Central de los sistemas industriales de soporte de la base.<br/> B)    Ariane: Renovación y mantenimiento del Sistema de Control Central e Industriales de soporte. Ingeniero de Control en las Campañas de lanzamiento. |
| **ITER**                                       | Sistema de Control                     | Control System Support Engineer | Diseño e implementación de los sistemas industriales, Integración al sistema de Control central usando CODAC (EPICS). |
| **ESS**                                        | Sistema de Control Integrado           | Control System Engineer         | Diseño e implementación de los sistemas industriales, Integración al sistema de Control central usando E3 (EPICS)Gestión, desarrollo e instalación del Software del sistema de Control Central (E3 - EPICS). |

 

**Cuestión: En los proyectos como el ITER, o instalaciones como la ESS, deben de contar con recursos computacionales extraordinarios para explotar los datos que potencialmente producirán las investigaciones**.

**Respuesta:** *En los dos casos* [*ITER*](https://www.iter.org/) *y la* [*ESS*](https://europeanspallationsource.se/) *tienen un espacio exclusivamente dedicado a salvaguardar los datos y transmitirlos a todos los científicos que pueden estar interesados en ellos. Estos datos son de acceso público para las entidades que se dedican a la investigación científico, aunque esto es más bien almacenamiento de datos y servidores de información. El centro de datos consta de varios clusters de ordenadores con gran capacidad de almacenamiento, procesamiento de datos, y altísimo ancho de banda. Básicamente estos data centers son la puerta de entrada del mundo a todos los datos científicos que genera el experimento.*

**Nota del autor:** Si estás más interesado en conocer el proyecto ITER puedes ver a continuación el post del Youtuber, divulgador científico, y PhD en Física, Javier Santaolalla.

[ITER: Así será el mayor reactor nuclear del planeta - YouTube](https://www.youtube.com/watch?v=eA-xuOjyU5I&t=139s)](Pinchar aquí para vídeo)

![Captura](Foro física_files/image001.jpg)

 

**Cuestión:** **¿Qué tipo de arquitectura se utiliza en esas instituciones?**

 

**Respuesta:** *Tanto ITER como ESS, utilizan una arquitectura similar. Ambos están compuestos por un System Control dividido en:*

 

- *2 estratos horizontales: Plant Systems, o los sistemas ubicados en planta, y Central System, los accesibles desde cualquier punto.*
- *Estos dos estratos están subdivididos a su vez en tres sistemas de control denominados: Control Convencional, Protection Maquina (Interlock), Protection Personals (Safety)*
- *La explotación de datos se produce al más alto nivel de la jerarquía, el denominado ‘CODAC Services’ a través del cual permite el acceso a el ‘resto del mundo’.*

 

*Plant System* *. Los denominados Plant System, son los sistemas de control individuales (hay unos 60) que se dedican a controlar cada uno de los sistemas industriales que funcionan en todo el ‘site’ de forma coordinada, reportando información al sistema de central y también ejecutando las comandas que vienen de ahí. Aunque tienen un alto grado de independencia y también se pueden operar en local si es requerido.*

*El Plan System, está a su vez dividido en estratos. Los tres sistemas de control (convencional, máquina y persona) tienen una configuración similar, así que solo detallaré el control convencional.*

- *Signal Interface: Interfaz del mundo físico al mundo digital.*
- *Remote IO:  Tarjetas de entrada/salidas remotas de un controlador ([plc](https://es.wikipedia.org/wiki/Controlador_lógico_programable)).*
- *Fast Controller: Controlador rápido, alta potencia de cálculo, para datos con frecuencia de cambio superior a 10ms (es decir, 1Mhz y para arriba)*
- *Slow Controller: Controlador lento, baja potencia de cálculo, para datos con frecuencia de cambio inferior a 10ms (es decir, 1hz a 10hz aprox.).*
- *Plant System Host: Donde corren los programas que ‘reportan al sistema central’ los datos del plant system y transfieren al plant system las comandas del sistema central. Es importante recordar que este ordenador transforma los datos al mundo EPICS y viceversa.*

*Ejemplo practico*

 

*El reactor de fusión de ITER, va a funcionar de forma pulsada, dicho de otra manera, se va a inicializar y va a fusionar gas durante digamos media hora. El objetivo es que genere más energía que la que consume. Durante esta media hora se van a generar millones de datos de todos los sensores que el reactor tiene, los datos de estos sensores son recogidos por controladores. Algunos son rápidos (Fast Controllers) otros lentos ([PLCs](https://es.wikipedia.org/wiki/Controlador_lógico_programable) ). Finalmente, y gracias al sistema* [*EPICS*](https://epics-controls.org/)*, son archivados.*

 

*Una vez estos datos son recogidos, se almacenan, procesan, y distribuyen en el DATA CENTER.*

 

**Cuestión: ¿Qué recursos computacionales se utilizan en ese tipo de instalaciones?**

**Respuesta:** *No se utiliza cloud computing. El procesado de datos se realiza en el DATA CENTER. Se utilizan técnicas de procesamiento en paralelo.*

**Cuestión: Para los proyectos de ITER y ESS, ¿se utilizan recursos computacionales de serie, o se han diseñado “ad hoc” para los mismos?**

**Respuesta:** *En ITER y en ESS recomienda fuertemente utilizar recursos computacionales de serie, los diseños específicos están altamente desaconsejados. Dicho esto, en la ESS se han realizado diseños de un controlador rápido específico para ser utilizado en el acelerador, habiéndose llegado a la conclusión de que no es viablemente económico.*

**Cuestión: ¿qué tipo de software se utiliza para el cálculo científico?**

**Respuesta:** *Se utiliza* [*EPICS*](https://epics-controls.org/)*, que es el principal software utilizado en grandes proyectos.*

**Cuestión: ¿Es software corporativo, o existe un equipo que diseña el software requerido para ajustarlo a las instalaciones?**

**Respuesta:** *Este software no es corporativo. Se trata de software de código abierto. Básicamente ajustar el Software EPICS a la instalación es uno de mis cometidos. Cada gran proyecto tiene como su ‘sabor’ de EPICS, eso quiere decir, se coge la base EPICS y se adapta, un poco como las diferentes versiones de LINUX. En ESS el “sabor” de EPICS se llama E3, y en ITER se llama CODAC. En este tipo de instituciones, ITER, ESS, CERN…, se tiende a utilizar código abierto.*

*EPICS es un intento de software libre que ha tenido muchísimo éxito, aunque este software no es el utilizado para cálculos científicos, sino que se utiliza más bien como base para la implementación de los sistemas del organismo en cuestión.*

*EPICS es un paquete con todas las herramientas necesarias para diseñar tu sistema de control, lo tiene todo, miles de drivers para conectar a equipos, software para generar las pantallas, software para generar alarmas, también para archivar datos, para hacer gráficas y muchos otros usos. A pesar de ello, este software no es el utilizado en el Data Center para el tratamiento de los datos, pero sin duda es el software más importante del sistema de control. El software que del que estoy hablando software de alto nivel; el software de los Controladores suele ser de la compañía SIEMENS y se tiene que interfasar con el EPICS Central Control System usando los drivers que EPICS proporciona.*

**Cuestión: ¿Podrías facilitar las especificaciones de los equipos utilizados?**

**Respuesta:** *A continuación, te detallo las especificaciones técnicas de los recursos de hardware utilizado para la gestión de datos en ESS.*

 

| **Recurso**                                                  | **Descripción**                                              | **Usuario**                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **HPC clúster**                                              | A 1464 core cluster interconnected using Infiniband          | DMSC employees, ESS Science directorate, ESS Target division, In-kind partners working on instruments in collaboration with ESS Science Directorate |
| **Storage**                                                  | 80TB ZFS (backed up), 320TB ZFS (not backed up) and 66TB of Lustre | Users of the HPC cluster and virtualized services.           |
| **Virtualization system**                                    | Software development environments                            | DMSC Data analysis group, DMSC DST group and ESS Instruments groups. |
| **Services such as wikis mail servers web servers and the like** |                                                              |                                                              |

**HPC clusters**

*Cada clúster está compuesto de los siguientes componentes:*

- *42 compute nodes, each consisting of 2 processors with 6 cores each.*
- *24 compute nodes, each consisting of 2 processors with 8 cores each.*
- *4 compute nodes, each consisting of 2 processors with 8 cores each.*
- *24 compute nodes, each consisting of 2 processors with 14 cores each.*
- *60TB of fast Lustre scratch storage storage.*
- *80TB of slow* [*ZFS*](https://en.wikipedia.org/wiki/ZFS) *home storage system.*
- *320TB of slow ZFS project storage system.*
- *A management network, used for maintainance.*
- *A* [*InifiniBand*](https://es.wikipedia.org/wiki/InfiniBand) *network, implementing the interconnect between nodes, and between the nodes and the Lustre storage system.*
- *A batch-system for handling jobs.*

**Nodos**

*Cada uno de los 42 nodos de computación corren bajo equipos DELL PowerEdge 410 con las siguientes especificaciones:*

- *Processor: 2x Intel Xeon 2.66Ghz with six cores.*
- *Memory: 48GB (6x8GB dual rank modules).*
- *System disk: 2x 300GB SAS 6GBPS.*
- *Ethernet: Gigabit Ethernet controller, used for management.*
- *InifiniBand: QLogic HPA InfiniBand controller, used for production interconnect.*

*Cada uno de los 24 nodos de computación corren bajo equipos DELL C8220 con las siguientes especificaciones:*

- *Processor: 2x Intel Xeon 2.0Ghz with eight cores.*
- *Memory: 64GB.*
- *System disk: 2x 300GB SAS 6GBPS.*
- *Ethernet: Gigabit Ethernet controller, used for management.*
- *InifiniBand: QLogic HPA InfiniBand controller, used for production interconnect.*

*Cada uno de los 4 nodos de computación corren bajo equipos Lenovo M3550 M5 con las siguientes especificaciones:*

- *Processor: 2x Intel Xeon 2.40Ghz with eight cores each.*
- *Memory: 128GB.*
- *System disk: 280GB SSD.*
- *Ethernet: Gigabit Ethernet controller, used for management.*
- *InifiniBand: Mellanox MT27500 Family ConnectX-3 InfiniBand controller, used for production interconnect.*

*Cada uno de los 24 nodos de computación corren bajo equipos DELL FC430 con las siguientes especificaciones:*

- *Processor: 2x Intel Xeon 2.40Ghz with 14 cores each.*
- *Memory: 132GB.*
- *System disk: 186GB SSD.*
- *Ethernet: Gigabit Ethernet controller, used for management.*
- *InifiniBand: Mellanox MT27500 Family ConnectX-3 InfiniBand controller, used for production interconnect.*

**Almacenamiento**

*Cada uno de los sistemas de clústeres proporciona 60 TB de almacenamiento, accesible a través del sistema de archivos distribuido Lustre. Los servidores de almacenamiento están conectados a la red InfiniBand y el sistema de archivos está montado en todos los nodos informáticos. El sistema de almacenamiento consta de dos estantes de discos, dos servidores de almacenamiento y dos servidores de metadatos. Los directorios de inicio se sirven en el sistema de archivos ZFS, que proporciona 80 TB de almacenamiento totalmente redundante con copia de seguridad (remota). Los directorios para grupos y usuarios que necesitan almacenar una gran cantidad de datos reproducibles están disponibles en un sistema de disco basado en ZFS de 320 TB. Este sistema no está respaldado.*

**Red**

*El clúster está equipado con dos redes físicas. Un Gigabit Ethernet, que se utiliza para la administración y la conexión a Internet, y una red InfiniBand, que se utiliza como interconexión interna entre los nodos informáticos y entre los nodos informáticos y el sistema de almacenamiento distribuido* [*Lustre*](https://es.wikipedia.org/wiki/Lustre_(sistema_de_archivos)).

**Software development environment**

*DMSC (Data Management System Control) aloja y proporciona recursos para respaldar los entornos de desarrollo de software utilizados por otros empleados y usuarios de DMSC. Los recursos que proporciona DMSC son:*

- **Creación de servidores** [*oVirt*](https://www.ovirt.org/) *utilizado para la creación de entornos virtuales, incluyendo varias distribuciones Linux, Windows, y Mac OSX.*
- **Repositorios** *Mercurial y Git para alojar varios proyectoss.* [*Rhodecode*](https://rhodecode.com/) *y* [*GitLab*](https://about.gitlab.com/) *son las interfaces por defecto para los repositorios.*
- **Integración continua.** *DMSC aloja* [*Jenkins*](https://www.jenkins.io/) *para una integración continua.*

*Se espera que DMSC albergue aún más recursos de este tipo, así como otros recursos de desarrollo por venir.*

**Build Servers**

*El entorno de virtualización Ovirt consiste en tres equipos host.* *La máquinas son prácticamente iguales y consisten en:*

- *Marca/modelo: Two DELL Poweredge R620 and one DELL Power Edge R63.0*
- *Procesador: 2 x 8 core Intel Xeon E5-2650 2.60Ghz.*
- *Memoria: 264GB.*
- *Network interfaces: 2 x 4 1GB nics por máquina.*
- *Almacenamiento externo: 1 DELL MD1220 por máquina, cada una con discos de 24 x 1TB 2.5". Esto es usado para el almacenamiento de la VM. Las máquinas R630 no tienen disco de almacenamiento interno.*

UNIR (Universidad Internacional de La Rioja).

Asignatura: Fundamentos de Física

Alumno: Aitor Sánchez Garzón

18 de Diciembre de 2020

 

 
