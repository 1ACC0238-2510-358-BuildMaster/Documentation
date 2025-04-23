## Capítulo IV: Product Software Design 

### 4.1. Strategic-Level Domain-Driven Design
#### 4.1.1. EventStorming

Con el objetivo de realizar un modelado colaborativo y estratégico del dominio de *BuildMaster*, se llevó a cabo una sesión de **EventStorming**, una técnica visual centrada en eventos del dominio que permite identificar flujos de negocio, entidades relevantes, actores y límites naturales del sistema.

El foco de esta sesión fue descomponer el dominio de una aplicación móvil que permite a usuarios configurar PCs según su presupuesto y necesidades, revisar precios y disponibilidad de componentes, y compartir builds con la comunidad. 

###### Herramientas utilizadas

- Herramienta visual: **Figma**
- Herramienta para la reunión virtual: **Discord**
- Participantes: 3 miembros del equipo
- Duración: 1 hora y 30 minutos

---
###### Actividades realizadas

Durante la sesión se siguieron los siguientes pasos:

1. **Identificación de Dominio Principal**  
   - Dominio central: *Armado de PC personalizado*
   - Subdominios auxiliares: *Gestión de usuarios*, *Catálogo de componentes*, *Comunidad y feedback*

2. **Registro de Eventos del Dominio (Orange Sticky Notes)**  
   - “Usuario solicita sugerencia de build”  
   - “Sistema analiza compatibilidad entre componentes”  
   - “Usuario guarda build”  
   - “Usuario publica build en comunidad”  
   - “Usuario califica build de otro usuario”  
   - “Usuario registra una nueva cuenta”  
   - “Sistema consulta precios en tienda externa”

3. **Identificación de Comandos (Blue Notes)**  
   - “Solicitar análisis de compatibilidad”  
   - “Guardar build favorita”  
   - “Publicar build”  
   - “Enviar comentario”

4. **Agregados/Entidades Clave (Yellow Notes)**  
   - `Usuario`  
   - `Build`  
   - `Componente`  
   - `Comentario`  
   - `Tienda`

5. **Descubrimiento de problemas y mejoras**  
   - Se detectaron decisiones clave de negocio como las reglas de validación técnica para compatibilidad.  
   - Se propuso separar el análisis técnico como un contexto independiente.

---

###### Evidencias del EventStorming

[![evidencia-reunion.png](https://i.postimg.cc/3w86Wpqs/evidencia-reunion.png)](https://postimg.cc/YvP8s4MR)

---

###### Principales aprendizajes

- Identificamos múltiples flujos principales del usuario desde una perspectiva centrada en eventos.
- Se diferenciaron claramente los contextos de **usuario**, **configuración técnica** y **comunidad**, lo que facilita la división futura del sistema en microservicios o módulos separados.

##### 4.1.1.1. Candidate Context Discovery

Luego de la sesión de EventStorming, se llevó a cabo una sesión de **Candidate Context Discovery**, con el fin de identificar **Bounded Contexts** naturales dentro del dominio de la aplicación móvil *BuildMaster*. Esta actividad permite separar el dominio en subconjuntos lógicos con responsabilidades bien delimitadas y coherencia interna, lo que facilita el diseño modular y distribuido del sistema.

La sesión tuvo una duración aproximada de **1 hora y 45 minutos** y se utilizó la herramienta **Miro** para mapear los cambios de contexto sobre el canvas inicial del EventStorming.


###### Técnica Aplicada: Start-With-Value

El equipo optó por el enfoque **Start-With-Value**, priorizando las partes del dominio que generan **mayor valor directo al usuario** final, como el asistente de configuración técnica y la validación de builds. Esto nos permitió identificar claramente qué partes del sistema debían ser consideradas como contextos centrales, y cuáles eran contextos de soporte.

---

###### Proceso realizado

A partir de la organización de eventos, comandos y entidades del EventStorming, se siguieron estos pasos:

1. **Identificación del flujo principal (Core Flow)**  
   - Inicio desde “Usuario solicita sugerencia de build”  
   - Finaliza con “Usuario guarda la build” o “Usuario publica la build”  
   - Se delimitó el flujo en pasos: entrada → análisis → resultado → persistencia

2. **Agrupación de eventos y acciones por cambio de estado**  
   - Se identificaron eventos pivote como:  
     - “Sistema analiza compatibilidad”  
     - “Usuario publica build”  
     - “Sistema consulta tienda externa”

3. **Delimitación de áreas de responsabilidad**  
   - Se trazaron límites lógicos sobre el canvas de EventStorming original, agrupando entidades, eventos y comandos por dominio coherente.

---

###### Candidate Bounded Contexts Identificados

| Bounded Context | Descripción breve | Tipo |
|-----------------|-------------------|------|
| **Configuración Técnica** | Donde ocurre el análisis de compatibilidad, sugerencias de componentes y detección de cuellos de botella. | Core |
| **Gestión de Usuario** | Autenticación, gestión de perfil y builds guardadas. | Supporting |
| **Catálogo de Componentes** | Almacén de componentes, filtros, búsqueda y visualización de specs. | Core |
| **Comunidad** | Publicación de builds, comentarios y votaciones. | Generic |
| **Proveedor / Tienda Externa** | Obtención de precios y disponibilidad por región. | Supporting |
| **Guías y Glosario** | Acceso a información educativa sobre componentes y tips. | Generic |

---

######  Reflexiones del equipo

- La separación por valor nos ayudó a distinguir claramente el **dominio técnico central** (donde se diferencia BuildMaster) del resto del sistema.
- Varios eventos de negocio sirvieron como puntos de transición natural entre contextos.
- Este ejercicio también ayudó a visualizar qué áreas podrán escalar como **microservicios independientes** más adelante.

##### 4.1.1.2. Domain Message Flows Modeling

Con la finalidad de visualizar la **colaboración entre los Bounded Contexts identificados**, el equipo llevó a cabo una sesión de modelado utilizando la técnica de **Domain Storytelling**. Esta técnica permite ilustrar, de manera narrativa y visual, cómo distintos contextos y actores interactúan mediante mensajes, para satisfacer los flujos principales del negocio.

Se eligieron dos **casos de uso principales** para modelar:

1. El armado y validación de una PC personalizada.  
2. La publicación de una build en la comunidad.

---

###### Enfoque y herramientas

- **Técnica aplicada**: Domain Storytelling (Level 2: Domain Message Flows)  
- Herramienta visual: **Figma**
- Herramienta para la reunión virtual: **Discord**
- **Duración de la sesión**: 1 hora  
- **Participantes**: 3 miembros del equipo

---

##### Caso 1: Armado y validación de una PC personalizada
###### Descripción narrativa

> El **usuario** abre el asistente de configuración. Selecciona el tipo de uso y presupuesto. El **contexto de configuración técnica** recibe los datos, consulta el **catálogo de componentes**, genera una sugerencia y verifica la **compatibilidad** y los **cuellos de botella**. Finalmente, se genera una build, que puede ser guardada por el usuario en su **perfil personal**.

###### Bounded Contexts involucrados

- Configuración Técnica  
- Catálogo de Componentes  
- Gestión de Usuario

###### Diagrama

[![Caso1.png](https://i.postimg.cc/W4CPPSvR/Caso1.png)](https://postimg.cc/5HBrBByp)

---

##### Caso 2: Publicación y valoración de una build en la comunidad

###### Descripción narrativa

> El **usuario** accede a su build guardada. Decide publicarla en la **comunidad**. El sistema transfiere los datos de la build al **contexto de comunidad**, donde otros usuarios pueden acceder a la publicación, dejar comentarios y valorarla. Cada calificación y comentario se registra dentro del mismo contexto.

###### Bounded Contexts involucrados

- Gestión de Usuario  
- Comunidad

###### Diagrama

[![Caso2.png](https://i.postimg.cc/J0h3c3sn/Caso2.png)](https://postimg.cc/R6jnvHQ5)

---

##### Conclusiones

- Los diagramas de **Domain Storytelling** ayudaron a visualizar claramente la colaboración entre contextos sin perder la perspectiva del usuario.
- Permitieron identificar puntos de integración técnica futuros como APIs REST entre servicios.
- También facilitaron el análisis de límites transaccionales y responsabilidades por cada módulo del sistema.

##### 4.1.1.3. Bounded Context Canvases

En esta sección se presentan los diseños de los Candidate Bounded Contexts identificados durante el proceso de EventStorming y Candidate Context Discovery. Para cada contexto, se detalla su estructura y propósito siguiendo el formato del **Bounded Context Canvas**, de forma iterativa y por orden de importancia. A continuación, se presentan los pasos aplicados para cada contexto:

###### Pasos seguidos para cada Bounded Context:

1. **Context Overview Definition**: Se define brevemente el propósito y alcance del contexto, así como su rol en el dominio general.
2. **Business Rules Distillation & Ubiquitous Language Capture**: Se identifican las reglas de negocio propias del contexto, así como términos clave que deben ser consistentes en la comunicación con otros contextos.
3. **Capability Analysis**: Se describen las funcionalidades que el contexto debe soportar y ofrecer.
4. **Capability Layering (si aplica)**: Se organiza la funcionalidad en capas si es necesario (por ejemplo, Application Layer, Domain Layer, Infrastructure Layer).
5. **Dependencies Capture**: Se identifican las dependencias externas que el contexto tiene con otros contextos, servicios, o APIs.
6. **Design Critique**: Se realiza un análisis crítico para validar que el diseño del contexto es coherente y eficiente con respecto al dominio y la arquitectura general.

---

###### Bounded Context 1: Gestión de Builds

- **Context Overview**: Encargado de la creación, guardado, modificación y visualización de configuraciones de PC personalizadas por los usuarios.
- **Business Rules**:
  - Un build debe tener un nombre único por usuario.
  - No se puede guardar un build sin seleccionar todos los componentes mínimos requeridos.
- **Ubiquitous Language**: build, componente, guardar, comparar, favorito.
- **Capabilities**:
  - Crear/editar builds.
  - Ver builds guardados.
  - Marcar builds como favoritos.
- **Dependencies**: Bounded Context de Usuario, Compatibilidad.
- **Design Critique**: Diseño claro y enfocado en la experiencia de usuario, dependencias controladas.

---

###### Bounded Context 2: Compatibilidad

- **Context Overview**: Responsable de evaluar y mostrar qué tan compatibles son los componentes seleccionados dentro de un build.
- **Business Rules**:
  - Si hay un cuello de botella evidente (por ejemplo, CPU/GPU), se debe notificar al usuario.
  - Mostrar alertas si hay incompatibilidades directas.
- **Ubiquitous Language**: compatibilidad, cuello de botella, rendimiento, evaluación.
- **Capabilities**:
  - Analizar compatibilidad entre componentes.
  - Mostrar alertas de incompatibilidad o limitaciones.
- **Dependencies**: Builds, Catálogo de Componentes.
- **Design Critique**: Aporta valor técnico al usuario, requiere constante actualización de reglas técnicas.

---

###### Bounded Context 3: Gestión de Usuario

- **Context Overview**: Maneja la autenticación, roles, y datos personales de los usuarios.
- **Business Rules**:
  - Un usuario debe estar autenticado para crear builds.
  - Las credenciales deben estar cifradas.
- **Ubiquitous Language**: login, registro, usuario, perfil, sesión.
- **Capabilities**:
  - Registro e inicio de sesión.
  - Edición de perfil.
- **Dependencies**: Builds, Seguridad.
- **Design Critique**: Contexto clásico pero esencial, bien separado del dominio funcional.

---

###### Bounded Context 4: Catálogo de Componentes

- **Context Overview**: Encargado de almacenar y mantener actualizado el listado de componentes disponibles.
- **Business Rules**:
  - Cada componente debe tener especificaciones completas.
  - Solo se muestran componentes activos en el catálogo.
- **Ubiquitous Language**: componente, categoría, especificación, stock, catálogo.
- **Capabilities**:
  - Visualizar y filtrar componentes.
  - Actualizar base de datos de componentes.
- **Dependencies**: Compatibilidad.
- **Design Critique**: Base para todo el dominio técnico, requiere buen rendimiento en búsquedas.

---

###### Bounded Context 5: Guías Técnicas

- **Context Overview**: Proporciona guías técnicas y definiciones útiles para usuarios que no están familiarizados con los componentes.
- **Business Rules**:
  - Las guías deben mantenerse actualizadas.
  - Debe haber términos destacados con definiciones.
- **Ubiquitous Language**: guía, glosario, componente, definición.
- **Capabilities**:
  - Mostrar guías organizadas por categoría.
  - Acceder a glosario interactivo.
- **Dependencies**: Catálogo de Componentes.
- **Design Critique**: Aporta valor educativo y diferencial, ayuda a retener usuarios nuevos.

---

###### Bounded Context 6: Comunidad y Comentarios

- **Context Overview**: Permite a los usuarios comentar builds y responder a otros usuarios.
- **Business Rules**:
  - Los comentarios deben moderarse para evitar spam.
  - Solo usuarios registrados pueden comentar.
- **Ubiquitous Language**: comentario, respuesta, build, comunidad.
- **Capabilities**:
  - Publicar y responder comentarios.
  - Reportar contenido inapropiado.
- **Dependencies**: Builds, Gestión de Usuario.
- **Design Critique**: Fortalece el componente social de la app, interacción moderada y positiva.

---

#### 4.1.2. Context Mapping


Luego de definir los Bounded Contexts y modelar sus colaboraciones, se realizó una sesión de **Context Mapping** con el fin de visualizar las relaciones estructurales entre los contextos del dominio de *BuildMaster*. Este proceso permite identificar acoplamientos, dependencias y oportunidades de modularización para mejorar la escalabilidad y mantenibilidad del sistema.

El equipo trabajó sobre el conjunto de Bounded Contexts definidos previamente, evaluando para cada uno:

- Su nivel de criticidad (Core, Supporting, Generic)
- Las funcionalidades clave (Capabilities)
- Las dependencias cruzadas con otros contextos
- Las oportunidades de aislamiento o colaboración
- Posibles reorganizaciones para mejorar el diseño estratégico

---

 Preguntas clave consideradas

Durante la sesión se exploraron diversas hipótesis para llegar a una mejor organización:

- ¿Qué pasaría si movemos la validación de compatibilidad al catálogo de componentes?
- ¿Qué pasaría si descomponemos “comunidad” en comentarios por un lado y puntuaciones por otro?
- ¿Qué pasaría si creamos un servicio compartido para los perfiles de usuario y builds favoritas?
- ¿Qué pasaría si duplicamos parte del glosario dentro del contexto de catálogo para evitar dependencias?
- ¿Qué pasaría si los datos de precios y disponibilidad se encapsulan en un nuevo contexto externo “Proveedores”?

---

###### Alternativa 1: Fusionar Comunidad + Builds

- **Pros**: Reduce comunicación entre contextos
- **Contras**: Rompe el principio de separación de intereses

**Decisión**: Rechazada. La comunidad debe poder operar sin alterar builds privadas.

###### Alternativa 2: Extraer Proveedor como contexto separado

- **Pros**: Aísla la lógica de scraping/API con tiendas externas
- **Contras**: Agrega complejidad inicial

**Decisión**: Aprobada. Se crea el contexto **Proveedores y Precios**.

###### Alternativa 3: Duplicar parte del glosario en Catálogo

- **Pros**: Mejora experiencia del usuario
- **Contras**: Riesgo de inconsistencias si no se sincroniza

**Decisión**: Rechazada. Se mantiene dependencia con ACL (Anti-Corruption Layer).

###### Alternativa 4: Separar “Comentarios” como contexto propio

- **Pros**: Facilita moderación, escalabilidad y métricas sociales
- **Contras**: Aumenta complejidad de diseño

**Decisión**: Rechazada por ahora. Se mantiene dentro de Comunidad para MVP.

---

###### Relaciones entre Bounded Contexts

| Source Context             | Target Context          | Tipo de Relación           |
|----------------------------|--------------------------|-----------------------------|
| Configuración Técnica      | Catálogo de Componentes  | Conformist                  |
| Configuración Técnica      | Proveedores y Precios    | Anti-Corruption Layer       |
| Gestión de Usuario         | Builds                   | Shared Kernel               |
| Comunidad                  | Builds                   | Customer/Supplier           |
| Comunidad                  | Gestión de Usuario       | Conformist                  |
| Catálogo de Componentes    | Guías Técnicas           | Customer/Supplier           |
| Gestión de Usuario         | Glosario                 | Conformist                  |

---

###### Visualización del Context Map

*(Aquí se debe insertar el diagrama del mapa de contextos, con líneas etiquetadas por tipo de relación. Se recomienda usar líneas sólidas para Customer/Supplier, punteadas para Conformist, flechas con sombreado para ACL, y doble borde para Shared Kernel).*

---

###### Reflexión final

El proceso de Context Mapping permitió:

- Visualizar riesgos de acoplamientos innecesarios
- Proponer estrategias de aislamiento y colaboración eficientes
- Identificar qué partes del sistema podrían evolucionar hacia microservicios
- Diseñar relaciones saludables entre contextos, usando patrones reconocidos de Domain-Driven Design

#### 4.1.3. Software Architecture
##### 4.1.3.1. Software Architecture Context Level Diagrams

En esta sección se presenta el **Context Level Diagram** del sistema **BuildMaster**, el cual representa una vista de alto nivel de su arquitectura. El propósito de este diagrama es identificar el sistema como una caja negra, mostrando los actores externos y sistemas con los que se comunica, así como el tipo de interacción que ocurre.

Este nivel de abstracción permite visualizar el alcance del sistema, sus límites y sus principales entradas y salidas de información, siendo útil tanto para equipos técnicos como para stakeholders no técnicos.

###### Explicación del diagrama

El sistema **BuildMaster** está ubicado en el centro del diagrama, rodeado por los siguientes elementos externos:

###### Actores humanos
- **Usuario Registrado**: Interactúa con la aplicación para crear, guardar y compartir builds personalizadas. Consulta componentes, valida compatibilidad y participa en la comunidad.
- **Usuario Visitante**: Puede navegar por la landing page, ver builds públicas y explorar el catálogo, sin crear una cuenta.

###### Sistemas externos
- **Proveedor de precios (API externa)**: Sistema de terceros (como Amazon, MercadoLibre, etc.) del que BuildMaster consulta precios actualizados y disponibilidad de componentes.
- **Sistema de autenticación de terceros (opcional)**: Si se usa un sistema como Firebase Auth o Auth0 para gestionar usuarios.
- **Servicio de base de datos**: Backend que almacena información de builds, usuarios, componentes, comentarios, etc.

Cada flecha entre elementos representa una interacción relevante, como la creación de builds, consultas de catálogo, recuperación de precios o publicación de comentarios.

[![structurizr-101461-System-Context-001.png](https://i.postimg.cc/WbhWxqP4/structurizr-101461-System-Context-001.png)](https://postimg.cc/KRhDMzjX)

##### 4.1.3.2. Software Architecture Container Level Diagrams

El **Container Level Diagram** muestra los elementos de alto nivel de la arquitectura del software de **BuildMaster** y cómo se distribuyen las responsabilidades entre los diferentes contenedores. Este diagrama proporciona una vista más detallada de los componentes de la arquitectura y cómo interactúan entre sí. Además, presenta las decisiones tecnológicas clave y las tecnologías utilizadas en la implementación de cada contenedor.

###### Descripción de los contenedores

- **Aplicación Movil (Frontend)**: 
  - **Responsabilidad**: Interfaz de usuario donde los usuarios registrados y visitantes pueden interactuar con el sistema. Permite la creación de builds, la visualización de componentes y la consulta de precios.
  - **Tecnología**: Flutter.
  - **Comunicación**: Se comunica con el backend a través de APIs RESTful.

- **API Backend (Backend)**:
  - **Responsabilidad**: Gestiona las peticiones de la aplicación movil, incluyendo la creación, actualización y consulta de builds. También maneja la integración con sistemas de terceros (API de precios y autenticación).
  - **Tecnología**: Node.js con Express (para las API RESTful).
  - **Comunicación**: Se comunica con el frontend y con los sistemas externos (API de precios y sistema de autenticación) a través de llamadas HTTP.

- **Base de Datos (DB)**:
  - **Responsabilidad**: Almacena los datos persistentes del sistema, como los builds, los usuarios, los componentes, los precios y las sesiones.
  - **Tecnología**: MySQL o PostgreSQL.
  - **Comunicación**: Se comunica con el backend para almacenar y recuperar datos.

- **Sistema de Precios (Proveedor de Precios)**:
  - **Responsabilidad**: API externa que proporciona información sobre precios y disponibilidad de componentes.
  - **Tecnología**: Servicio de terceros (por ejemplo, Amazon API, MercadoLibre API).
  - **Comunicación**: El backend consulta esta API para obtener datos sobre componentes.

- **Sistema de Autenticación (Auth)**:
  - **Responsabilidad**: Gestiona el registro e inicio de sesión de usuarios, manteniendo sesiones activas.
  - **Tecnología**: Firebase Auth, Auth0, o implementación propia de JWT.
  - **Comunicación**: El backend interactúa con este sistema para autenticar a los usuarios.

###### Flujo de Comunicación Entre Contenedores

1. **Frontend (Aplicación Movil)**:
   - Los usuarios registrados y visitantes interactúan con el frontend a través de su celular.
   - El frontend realiza peticiones al **Backend API** para obtener información sobre builds y componentes, y para registrar o autenticar usuarios.
   
2. **Backend API**:
   - El **Backend API** se comunica con la **Base de Datos** para guardar y recuperar información relacionada con builds, usuarios, y componentes.
   - Realiza peticiones a la **API de Precios** para obtener la información actualizada de precios de componentes.
   - Se comunica con el **Sistema de Autenticación** para validar la identidad de los usuarios y gestionar sesiones.

3. **Base de Datos**:
   - La base de datos almacena la información de builds, usuarios, y otros datos persistentes del sistema.
   
4. **Sistema de Precios**:
   - El backend realiza consultas a la API externa para obtener información sobre la disponibilidad y los precios de los componentes.

5. **Sistema de Autenticación**:
   - El backend interactúa con el sistema de autenticación para validar a los usuarios al inicio de sesión y registrar nuevos usuarios.

[![structurizr-101463-Container-001.png](https://i.postimg.cc/13K26hhB/structurizr-101463-Container-001.png)](https://postimg.cc/YvhdKPSL)

##### 4.1.3.3. Software Architecture Deployment Diagrams

El **Deployment Diagram** muestra la distribución física del sistema **BuildMaster**, destacando cómo los componentes del software se despliegan sobre el hardware y otros entornos. Este diagrama visualiza las máquinas, servidores, redes y otros dispositivos físicos que alojan el software, así como las relaciones y dependencias entre los distintos nodos. Su objetivo es describir cómo se implementa el sistema en la infraestructura de hardware.

###### Descripción del Diagrama de Despliegue

El diagrama de despliegue representa la infraestructura física sobre la que se ejecuta el sistema **BuildMaster** y cómo se distribuyen los contenedores de software sobre el hardware. Este diagrama está diseñado para ser comprendido tanto por el equipo de desarrollo como por los equipos de infraestructura y operaciones.

###### Elementos del Diagrama

- **Dispositivo del Usuario (Smartphone):**

  - **Responsabilidad:** Ejecutar la aplicación móvil (frontend nativo) instalada desde la tienda.

  - **Tecnología:** Flutter (Android/iOS)

  - **Comunicación:** Se conecta al backend a través de   internet mediante HTTP/HTTPS.

- **Servidor de Aplicaciones (Backend)**:
  - **Responsabilidad**: Alojamiento de la API backend que maneja la lógica del sistema y las comunicaciones con la base de datos y otros servicios externos.
  - **Tecnología**: Node.js, Express.
  - **Comunicación**: Se comunica con el servidor web a través de HTTP/HTTPS y con la base de datos y otros servicios mediante APIs internas.

- **Base de Datos**:
  - **Responsabilidad**: Alojamiento de la base de datos que almacena la información persistente del sistema.
  - **Tecnología**: MySQL o PostgreSQL.
  - **Comunicación**: Se comunica con el servidor de aplicaciones para almacenar y recuperar datos.

- **API Externa (Proveedor de Precios)**:
  - **Responsabilidad**: Sistema de terceros que proporciona datos sobre precios y disponibilidad de componentes. Se puede alojar en una infraestructura de nube o en un servidor externo.
  - **Tecnología**: API RESTful, Amazon API, MercadoLibre API.
  - **Comunicación**: El servidor de aplicaciones realiza peticiones HTTP/HTTPS a esta API.

- **Sistema de Autenticación (Auth)**:
  - **Responsabilidad**: Alojamiento del sistema que gestiona el registro e inicio de sesión de usuarios.
  - **Tecnología**: Firebase Auth, Auth0.
  - **Comunicación**: El servidor de aplicaciones realiza peticiones HTTP/HTTPS a esta API para autenticar usuarios.

###### Flujo de Despliegue

1. El **usuario** instala y ejecuta la **aplicación móvil** en su celular (Flutter).
2. Las **peticiones del frontend** se envían al **Backend (servidor de aplicaciones)** para ser procesadas.
3. El **Backend** se comunica con la **Base de Datos** para almacenar o recuperar información relacionada con builds, usuarios y componentes.
4. El **Backend** también interactúa con el **Proveedor de Precios** para obtener información sobre precios de componentes.
5. El **Backend** consulta el **Sistema de Autenticación** para autenticar a los usuarios y gestionar sesiones.

[![structurizr-101464-Container-001.png](https://i.postimg.cc/W30H2Qn0/structurizr-101464-Container-001.png)](https://postimg.cc/phXZCc3d)

### 4.2. Tactical-Level Domain-Driven Design
### 4.2.1. Bounded Context: Configuración Técnica

En esta sección, se detallan las clases y componentes identificados en el bounded context de **Configuración Técnica**, que abarca el análisis de compatibilidad entre componentes, recomendaciones, y detección de cuellos de botella.

---

#### 4.2.1.1. Domain Layer

Esta capa representa el núcleo del sistema y las reglas de negocio del dominio.

| Clase                    | Tipo               | Propósito                                                             | Atributos / Métodos                                  |
|--------------------------|--------------------|-----------------------------------------------------------------------|------------------------------------------------------|
| `Build`                  | Entity             | Representa una configuración completa de componentes.                 | `componentes: Componente[]`, `validarCompatibilidad()` |
| `Componente`             | Value Object       | Componente individual con atributos técnicos.                         | `tipo`, `modelo`, `socket`, `consumoEnergia`         |
| `BuildFactory`           | Factory            | Encargada de crear builds válidas.                                    | `crearBuild(componentes: Componente[]): Build`       |
| `CompatibilidadService` | Domain Service     | Valida compatibilidad entre componentes.                              | `validarCPU_RAM()`, `validarMotherboardGPU()`        |
| `BuildRepository`        | Repository Interface | Abstracción para el acceso a datos de builds.                        | `guardar(Build)`, `obtenerPorId(id)`                |

---

#### 4.2.1.2. Interface Layer

Encargada de exponer funcionalidades al usuario o consumidores externos.

| Clase              | Tipo       | Propósito                                                             | Métodos                             |
|--------------------|------------|-----------------------------------------------------------------------|-------------------------------------|
| `BuildController`  | Controller | Gestiona las peticiones relacionadas con builds.                      | `postNuevaBuild()`, `getBuildPorId()` |
| `BuildAPIConsumer` | Consumer   | Interfaz para APIs externas que devuelvan sugerencias de configuración. | `obtenerSugerencias(componentes)`   |

---

#### 4.2.1.3. Application Layer

Define los flujos de negocio mediante comandos y eventos.

| Clase                     | Tipo            | Propósito                                                  | Métodos                                |
|---------------------------|-----------------|------------------------------------------------------------|----------------------------------------|
| `CrearBuildCommandHandler`| Command Handler | Ejecuta la lógica para crear una nueva build.              | `handle(command: CrearBuildCommand)`   |
| `BuildCreadaEventHandler` | Event Handler   | Gestiona acciones posteriores a la creación de una build.  | `handle(event: BuildCreada)`           |

---

#### 4.2.1.4. Infrastructure Layer

Provee la implementación concreta de servicios como base de datos, brokers, etc.

| Clase                    | Tipo          | Propósito                                                                 | Tecnologías  |
|--------------------------|---------------|---------------------------------------------------------------------------|--------------|
| `BuildRepositoryImpl`    | Repository    | Implementación de `BuildRepository` con acceso a base de datos.           | PostgreSQL      |
| `CompatibilidadExternalAPI` | External Service | Llama a API externa para validaciones.                             | REST API     |
| `BuildMessageBroker`     | Message Broker| Publica eventos de builds para otros contextos.                          | RabbitMQ     |

##### 4.2.1.5. Bounded Context Software Architecture Component Level Diagrams

- Este Component Diagram descompone el container Configuración Técnica API (el backend del bounded context) en:

- Controller: punto de entrada HTTP.

- Command Handler: maneja la lógica principal.

- Domain Service y Factory: lógica de dominio para crear y validar builds.

- Repository: persistencia de datos en PostgreSQL.

- External API: cliente para validaciones externas.

[![structurizr-101490-Component-001.png](https://i.postimg.cc/GtzhXNvF/structurizr-101490-Component-001.png)](https://postimg.cc/1VnQtvCX)

##### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams

A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de **Configuración Técnica**. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.

###### 4.2.1.6.1. Bounded Context Domain Layer Class Diagrams

| Clase                  | Tipo               | Descripción                                           |
|------------------------|--------------------|-------------------------------------------------------|
| Build                  | Entity             | Representa un ensamble completo de PC                 |
| Componente             | Value Object       | Describe un componente individual                     |
| BuildFactory           | Factory            | Se encarga de construir una Build válida              |
| CompatibilidadService  | Domain Service     | Valida que una Build no tenga cuellos de botella      |
| BuildRepository        | Repository (interface) | Abstracción para almacenar y recuperar builds     |



[![Domain-Layer-Configuraci-n-T-cnica.png](https://i.postimg.cc/Ls6nDHPb/Domain-Layer-Configuraci-n-T-cnica.png)](https://postimg.cc/yDt1YCvm)

###### 4.2.1.6.2. Bounded Context Database Design Diagram

Este diagrama representa el modelo relacional que da soporte a la persistencia de datos del bounded context **Configuración Técnica**.

El diseño se alinea con el dominio previamente modelado en las secciones anteriores, asegurando que cada build pueda ser construida, validada y recuperada eficientemente con sus respectivos componentes.

Se utilizaron las siguientes decisiones de modelado:

- Se modela la entidad `builds` como una tabla principal, la cual contiene un identificador único (`id`), el `nombre` de la configuración y el `usuario_id` que la creó (relacionado desde otro contexto).
- La entidad `components` representa cada parte de hardware (CPU, GPU, RAM, etc.) con atributos como `tipo`, `modelo`, `socket` y `consumo_w`.
- La tabla `build_components` implementa la relación **muchos a muchos** entre `builds` y `components`, permitiendo reutilización de componentes y manteniendo trazabilidad.
- Se incluye un atributo `orden` para indicar la posición o relevancia del componente dentro del ensamble.

**Relaciones clave:**
- Una build puede tener múltiples componentes asociados.
- Un mismo componente puede formar parte de múltiples builds.
- Cada build pertenece a un usuario (modelado en otro bounded context).

**Tecnología objetivo:**  
La base de datos utilizada será **PostgreSQL**, por su robustez y compatibilidad con UUIDs y relaciones complejas. Las claves primarias y foráneas están correctamente tipadas y normalizadas para mantener integridad referencial.

[![Database-Design-Diagram-Configuracion-tecnica.png](https://i.postimg.cc/bNyxWj11/Database-Design-Diagram-Configuracion-tecnica.png)](https://postimg.cc/vDKxxkqm)

#### 4.2.2. Bounded Context: Gestión de usuario

En esta sección, se detallan las clases y componentes identificados en el bounded context de Gestión de Usuario, que abarca la configuración y personalización de la cuenta del usuario en nuestra plataforma.  

---

##### 4.2.2.1. Domain Layer

Esta capa representa el núcleo del sistema y las reglas de negocio del dominio.

| Clase | Tipo | Propósito | Atributos/Métodos |
| :---- | :---- | :---- | :---- |
| Usuario | Entidad | Representar al usuario del sistema y gestionar su ciclo de vida. | id, nombre, email, contraseña, perfil, buildsFavoritas registrar(), login(), editarPerfil(), eliminarCuenta() |
| Perfil | Value Object | Contener la información editable del usuario. | nombreCompleto, imagenPerfil, biografia, redesSociales actualizarInfo() |
| Credenciales | Value Object | Validar el acceso del usuario con email y contraseña. | email, contraseña validar() |
| Build | Entidad | Representar una build que puede ser marcada como favorita. | id, titulo, descripcion, elementos, autor |
| Favorito | Entidad | Relacionar a un usuario con sus builds favoritas. | usuarioId, buildId agregarFavorito(), removerFavorito() |
| MensajeSistema | Value Object | Proveer feedback al usuario después de acciones (éxito, error, confirmación). | tipo, contenido |

---

##### 4.2.2.2. Interface Layer

Encargada de exponer funcionalidades al usuario o consumidores externos.

| Clase | Tipo | Propósito | Atributos/Métodos |
| :---- | :---- | :---- | :---- |
| UsuarioController | Controller | Controlar todas las interacciones del usuario con la aplicación: registro, login, perfil y favoritos.	 | mostrarFormularioRegistro() registrarUsuario(datosFormulario) mostrarFormularioLogin() iniciarSesion(email, contraseña) mostrarPerfil() editarPerfil(datosActualizados) mostrarBuildsFavoritas(usuarioId) confirmarEliminacion() cancelarEliminacion() eliminarUsuario(usuarioId) mostrarMensajeSistema(tipo, texto) |
| UsuarioDTO | DTO (Data Transfer Object) | Transferir los datos del usuario entre UI y casos de uso. | nombre, email, imagenPerfil, biografia, redesSociales, buildsFavoritas |
| UsuarioView | View | Mostrar pantallas e interfaces relacionadas al usuario. | renderFormularioRegistro() renderFormularioLogin() renderPerfil(usuarioDTO) renderEdicionPerfil() renderBuildsFavoritas(listaBuilds) mostrarMensaje(tipo, texto) mostrarModalConfirmacion() |

---

##### 4.2.2.3. Application Layer

Define los flujos de negocio mediante comandos y eventos.

| Clase | Tipo | Propósito | Atributos/Métodos |
| :---- | :---- | :---- | :---- |
| RegistrarUsuarioCommand | Comand Handler | Solicitar el registro de un nuevo usuario. | nombre, email, contraseña execute() |
| UsuarioRegistradoEvent | Event Handler | Notificar que un usuario fue registrado exitosamente. | usuarioId, timestamp |
| IniciarSesionCommand | Comand Handler | Solicitar el inicio de sesión con credenciales. | email, contraseña execute() |
| SesionIniciadaEvent | Event Handler | Confirmar que el usuario inició sesión con éxito. | usuarioId, timestamp |
| EditarPerfilCommand | Comand Handler | Solicitar actualización de datos del perfil. | usuarioId, datosActualizados execute() |
| PerfilActualizadoEvent | Event Handler | Confirmar que los datos del usuario fueron actualizados correctamente. | usuarioId, timestamp |
| VerBuildsFavoritasCommand | Comand Handler | Solicitar las builds favoritas del usuario. | usuarioId execute() |
| BuildsFavoritasMostradasEvent | Event Handler | Indicar que se han cargado correctamente las builds favoritas. | usuarioId, listaBuilds |
| EliminarUsuarioCommand | Comand Handler | Solicitar la eliminación de una cuenta de usuario. | usuarioId execute() |
| UsuarioEliminadoEvent | Event Handler | Confirmar que la cuenta fue eliminada del sistema. | usuarioId, timestamp |
| CancelarEliminacionCommand | Comand Handler | Solicitar la cancelación del proceso de eliminación de cuenta. | usuarioId execute() |
| EliminacionCanceladaEvent | Event Handler | Indicar que se canceló el proceso de eliminación de cuenta. | usuarioId, timestamp |

---

##### 4.2.2.4. Infrastructure Layer

Provee la implementación concreta de servicios como base de datos, brokers, etc.

| Clase | Tipo | Propósito | Tecnologías (Jetpack Compose stack) |
| :---- | :---- | :---- | :---- |
| FirebaseAuthService | Service | Gestionar autenticación de usuarios (registro, login, logout). | Firebase Authentication, Google Play Services |
| FirebaseFirestoreUserRepository | Repository | Persistir y recuperar información del usuario. | PostgreSQL |
| FirebaseBuildRepository | Repository | Gestionar las builds y builds favoritas del usuario. | PostgreSQL |
| LocalUserPreferences | Storage | Manejar almacenamiento local de sesión, tema, idioma, etc. | Jetpack DataStore (o SharedPreferences) |
| FirebaseMessagingService | Message Broker | Enviar y recibir notificaciones push relacionadas a eventos de usuario. | RabbitMQ |
| CloudFunctionsClient | External Service | Ejecutar lógica backend adicional como verificación de datos o auditoría. | Retrofit (API REST) |
| EventLogger | Observer / Logger | Registrar eventos importantes del sistema (ej. errores, sesiones, cambios). | Firebase Analytics, Crashlytics, Logcat, Timber |

###### 4.2.2.5. Bounded Context Software Architecture Component Level Diagrams

* Este Component Diagram descompone el container Gestión de Usuario API (el backend del bounded context) en:  
* Controller: punto de entrada HTTP.  
* Command Handler: maneja la lógica principal.  
* Domain Service y Factory: lógica de dominio para crear y validar builds.  
* Repository: persistencia de datos en PostgreSQL.  
* External API: cliente para validaciones externas.


[![image.png](https://i.postimg.cc/G3Ftk0WT/image.png)](https://postimg.cc/Z0qJSQKJ)
[![structurizr-Component-001.png](https://i.postimg.cc/9M6HyfZp/structurizr-Component-001.png)](https://postimg.cc/hz1YBcCz)


###### 4.2.2.6. Bounded Context Software Architecture Code Level Diagrams

A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de Gestión de Usuario. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.

####### 4.2.2.6.1. Bounded Context Domain Layer Class Diagrams

| Clase | Tipo | Descripción |
| :---- | :---- | :---- |
| Usuario | Entidad | Representa al usuario del sistema, con su identidad, perfil y builds favoritas. Contiene comportamiento relevante para su ciclo de vida. |
| Perfil | Value Object | Información editable del usuario, como nombre, biografía o foto. Se encarga de encapsular y validar esa información. |
| Credenciales | Value Object | Correo y contraseña del usuario, usado para autenticación. Puede incluir reglas de validación o hashing. |
| Favorito | Entidad | Representa una relación entre un usuario y una build marcada como favorita. Contiene información como fecha de marcado o metadatos de la build. |

[![Captura-de-pantalla-2025-04-22-173559.png](https://i.postimg.cc/SKYQVZV3/Captura-de-pantalla-2025-04-22-173559.png)](https://postimg.cc/B8sGnBrB)

####### 4.2.2.6.2. Bounded Context Database Design Diagram

Este diagrama representa el modelo relacional que da soporte a la persistencia de datos del bounded context Gestión de Usuario.  
El diseño se alinea con el dominio previamente modelado en las secciones anteriores, asegurando que cada build pueda ser construida, validada y recuperada eficientemente con sus respectivos componentes.  
Se utilizaron las siguientes decisiones de modelado:

* Se modela la entidad usuarios como una tabla principal, la cual contiene un identificador único (id), el nombre del usuario, su biografía, su foto, email y contraseña para validar.  
* La entidad favoritos tiene el usuario\_id , el build\_id que es favorito y la fecha\_marcado de la fecha que se marcó la build como favorito.  
* Adicionalmente, se muestran las relaciones que usuario tiene con las clases Perfil y Credensiales


Relaciones clave:

* Usuarios tiene una relación 1:N con favoritos.  
* Credenciales y perfil están embebidos dentro de usuarios como atributos directos (no se separan en tablas, por simplicidad y performance).

[![Captura-de-pantalla-2025-04-22-173944.png](https://i.postimg.cc/050ktKdk/Captura-de-pantalla-2025-04-22-173944.png)](https://postimg.cc/G99nt25V)

Tecnología objetivo:  
La base de datos utilizada será PostgreSQL, por su robustez y compatibilidad con UUIDs y relaciones complejas. Las claves primarias y foráneas están correctamente tipadas y normalizadas para mantener integridad referencial.  

#### 4.2.4. Bounded Context: Comunidad

En esta sección, se detallan las clases y componentes identificados en el bounded de comunidad encargada de generar un ambien coloborativo entre los usuarios sus opiniones o recomendaciones

##### 4.2.4.1. Domain Layer
Esta capa representa el sistema central y las reglas comerciales del dominio de la comunidad.

| Class               | Type             | Purpose                                                                 | Attributes / Methods                     |
|---------------------|------------------|-------------------------------------------------------------------------|------------------------------------------|
| Post                | Entity           | Represents a user post in the community                                | title, content, authorId, likes, comments, addComment(), like() |
| Comment             | Value Object     | A comment on a post                                                    | content, authorId, timestamp             |
| Rating              | Entity           | User rating for hardware components                                    | componentId, userId, score, review       |
| CommunityFactory    | Factory          | Creates valid community interactions                                   | createPost(), createComment(), createRating() |
| ValidationService   | Domain Service   | Validates community content                                            | validatePostContent(), filterProfanity() |
| PostRepository      | Repository Interface | Abstraction for post data access                                      | save(Post), findById(id), findByAuthor(userId) |
##### 4.2.4.2. Interface Layer

Responsable de exponer la funcionalidad a los usuarios o consumidores externos.

| Class               | Type       | Purpose                                                                 | Methods                                  |
|---------------------|------------|-------------------------------------------------------------------------|------------------------------------------|
| CommunityController | Controller | Manages community-related requests                                     | createPost(), getPosts(), addComment()   |
| RatingController    | Controller | Handles hardware component ratings                                     | submitRating(), getComponentRatings()    |
| ExternalModerationAPI | Consumer  | Interface for external content moderation services                     | checkContentSafety(content)              |


##### 4.2.4.3. Application Layer

Define flujos de trabajo mediante comandos y eventos.

| Class                     | Type             | Purpose                                                                 | Methods                                  |
|---------------------------|------------------|-------------------------------------------------------------------------|------------------------------------------|
| CreatePostCommandHandler  | Command Handler  | Executes logic for creating a new post                                 | handle(command: CreatePostCommand)       |
| PostCreatedEventHandler   | Event Handler    | Manages actions after post creation (notifications, etc.)              | handle(event: PostCreated)               |
| RateComponentCommandHandler | Command Handler | Handles component rating submissions                                  | handle(command: RateComponentCommand)    |

##### 4.2.4.4. Infrastructure Layer

Proporciona la implementación concreta de servicios como bases de datos, intermediarios, etc.

| Class                   | Type              | Purpose                                                                 | Technologies                             |
|-------------------------|-------------------|-------------------------------------------------------------------------|------------------------------------------|
| PostRepositoryImpl      | Repository        | MySQL implementation of PostRepository                            | PostgreSQL                               |
| ModerationServiceImpl   | External Service  | Calls external content moderation API                                  | REST API                                 |
| CommunityEventBroker    | Message Broker    | Publishes community events for other contexts                          | RabbitMQ                                 |
| CacheService            | Infrastructure    | Caches popular posts and ratings                                       | Redis                                    |

##### 4.2.4.5. Bounded Context Software Architecture Component Level Diagrams
En esta seccion explicaramos el bounded context comunidad 

1. __App Móvil Comunidad__

Tipo : Container (Flutter)
Función : Aplicación móvil usada por los usuarios para interactuar con la API.
Interacción : Realiza llamadas HTTP a la API.

2. ComunidadController
Tipo : REST Controller
Función : Recibe peticiones HTTP/JSON del frontend (App Móvil Comunidad).
Interacción :
Invoca comandos (CrearPost, ComentarPost) a los handlers correspondientes.

3. CrearPostCommandHandler
Tipo : Application Service
Función : Orquesta la creación de un nuevo post.
Interacción :
Valida el contenido del post mediante ModeracionService.
Construye una instancia válida de Post usando PostFactory.
Guarda el post en la base de datos mediante PostRepository.
Envía notificaciones a seguidores mediante NotificacionService.

4. ModeracionService
Tipo : Domain Service
Función : Valida el contenido de los posts.
Interacción : Recibe solicitudes de validación desde CrearPostCommandHandler.

5. PostRepository
Tipo : Repository
Función : Guarda y recupera posts en la base de datos.
Interacción : Recibe solicitudes de guardar posts desde CrearPostCommandHandler.

6. PostFactory
Tipo : Domain Factory
Función : Construye una instancia válida de Post.
Interacción : Recibe solicitudes de construcción desde CrearPostCommandHandler.

7. NotificacionService
Tipo : Infrastructure Service
Función : Envía notificaciones a seguidores.
Interacción : Recibe solicitudes de envío de notificaciones desde CrearPostCommandHandler.

8. ComentarPostCommandHandler
Tipo : Application Service
Función : Orquesta la creación de un comentario.
Interacción :
Valida el contenido del comentario mediante ModeracionComentariosService.
Construye una instancia válida de Comentario usando ComentarioFactory.
Guarda el comentario en la base de datos mediante ComentarioRepository.

9. ModeracionComentariosService
Tipo : Domain Service
Función : Valida el contenido de los comentarios.
Interacción : Recibe solicitudes de validación desde ComentarPostCommandHandler.

10. ComentarioRepository
Tipo : Repository
Función : Guarda y recupera comentarios en la base de datos.
Interacción : Recibe solicitudes de guardar comentarios desde ComentarPostCommandHandler.

11. ComentarioFactory
Tipo : Domain Factory
Función : Construye una instancia válida de Comentario.
Interacción : Recibe solicitudes de construcción desde ComentarPostCommandHandler.


[![structurizr-101532-Component-001-002.png](https://i.postimg.cc/Gt5kmcc3/structurizr-101532-Component-001-002.png)](https://postimg.cc/H8bJS1cF)
##### 4.2.4.6. Bounded Context Software Architecture Code Level Diagrams
A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de Configuración Técnica. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.
###### 4.2.4.6.1. Bounded Context Domain Layer Class Diagrams

Capa de Dominio : Contiene las entidades (Post, Valuation) y objetos de valor (PostPayload).

Capa de Repositorio : Maneja la persistencia de datos (PostRepository, ValuationRepository).

Capa de Servicio : Coordina las operaciones de negocio (PostServiceInterface).

Capa de Comandos : Encapsula acciones específicas (CreatePostCommand, RateBuildCommand).
[![Diagrama-en-blanco-2.png](https://i.postimg.cc/fy9PcW8y/Diagrama-en-blanco-2.png)](https://postimg.cc/64BzwKJx)
###### 4.2.4.6.2. Bounded Context Database Design Diagram

Users :
Almacena usuarios (UserId, Username, Email).

Publicaciones :
Publicaciones de usuarios (PublicacionId, UserId, Titulo, Contenido, LikeCount).
Relacionada con Users, Comentarios, y Valoraciones.

Comentarios :
Comentarios en publicaciones (ComentarioId, PublicacionId, UserId, Contenido).
Relacionada con Publicaciones y Users.

Valoraciones :
Puntuaciones a publicaciones (ValoracionId, PublicacionId, UserId, Score).
Relacionada con Publicaciones y Users.

Notificaciones :
Notificaciones para usuarios (NotificacionId, UserId, Tipo, Mensaje, IsRead).

Temas :
Categorías o temas (Temaid, Nombre, IsTrending).

Builds :
Registra builds o versiones (BuildId, UserId, CreationDate).


[![Diagrama-en-blanco-3.png](https://i.postimg.cc/BQdSftrY/Diagrama-en-blanco-3.png)](https://postimg.cc/8jmQhkPM)

#### 4.2.5. Bounded Context: Catalogo de Componentes

En esta seccion ira todo lo relacioano con el bounded context catalago.

##### 4.2.5.1. Domain Layer

| Class                 | Type             | Purpose                                                                 | Attributes / Methods                     |
|-----------------------|------------------|-------------------------------------------------------------------------|------------------------------------------|
| Component             | Entity           | Represents a hardware component                                        | id, name, type, specs, price, compatibilityList |
| Category              | Entity           | Component classification hierarchy                                     | name, parentCategory, childrenCategories |
| Manufacturer          | Entity           | Hardware component manufacturer                                        | name, website, supportContacts           |
| ComponentSpecs        | Value Object     | Technical specifications of a component                                | socket, tdp, dimensions, interface       |
| ComponentFactory      | Factory          | Creates validated component instances                                  | createComponent(), validateSpecs()       |
| CompatibilityService  | Domain Service   | Manages component compatibility rules                                  | checkCompatibility(), updateCompatibilityMatrix() |
| ComponentRepository   | Repository Interface | Component persistence operations                                     | save(), findByType(), search()           |


##### 4.2.5.2. Interface Layer

| Class                 | Type       | Purpose                                                                 | Methods                                  |
|-----------------------|------------|-------------------------------------------------------------------------|------------------------------------------|
| CatalogController     | Controller | Handles component search and details                                   | searchComponents(), getComponentDetails() |
| AdminController       | Controller | Manages component administration                                      | addComponent(), updatePrices(), importBatch() |
| ComponentAPI          | Consumer   | Integrates with external component databases                           | fetchExternalSpecs(), syncInventory()    |

##### 4.2.5.3. Application Layer

| Class                       | Type             | Purpose                                                                 | Methods                                  |
|-----------------------------|------------------|-------------------------------------------------------------------------|------------------------------------------|
| AddComponentCommandHandler  | Command Handler  | Handles new component additions                                        | handle(command: AddComponentCommand)     |
| PriceUpdateCommandHandler   | Command Handler  | Manages component price updates                                        | handle(command: PriceUpdateCommand)      |
| ComponentUpdatedEventHandler| Event Handler    | Notifies about component changes                                       | handle(event: ComponentUpdated)          |


##### 4.2.5.4. Infrastructure Layer


| Class                     | Type              | Purpose                                                                 | Technologies                             |
|---------------------------|-------------------|-------------------------------------------------------------------------|------------------------------------------|
| ComponentRepositoryImpl   | Repository        | MySQL implementation for components                                 | MySQL                                  |
| CategoryRepositoryImpl    | Repository        | MySQL implementation for categories                              | MySQL                              |
| ExternalComponentService  | External Service  | Integrates with manufacturer APIs                                     | GraphQL                                  |
| SearchService             | Infrastructure    | Full-text component search                                            | Elasticsearch                            |
| CatalogCache              | Infrastructure    | Caches frequent component queries                                      | Redis                                    |
| CatalogMessageBroker      | Message Broker    | Publishes catalog updates                                             | Kafka                                    |

##### 4.2.5.5. Bounded Context Software Architecture Component Level Diagrams

Estructura del Diagrama

Consulta de Componentes :
App Móvil → CatalogController → SearchService → ComponentRepositoryImpl.

Administración de Componentes :
App Móvil → AdminController → AddComponentCommandHandler PriceUpdateCommandHandler → Repositorios.

Sincronización de Datos Externos :
ExternalComponentService → ComponentAPI → Repositorios.

Notificaciones de Cambios :
Comandos → CatalogMessageBroker → Suscriptores (ComponentUpdatedEventHandler).

[![structurizr-101532-Component-001.png](https://i.postimg.cc/PqdMXW92/structurizr-101532-Component-001.png)](https://postimg.cc/VJHt4CYC)

##### 4.2.5.6. Bounded Context Software Architecture Code Level Diagrams

A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de Configuración Técnica. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.
###### 4.2.5.6.1.  Bounded Context Domain Layer Class Diagrams

Component :
Representa un componente con atributos como id, name, type, price, compatibility, Category y Manufacturer.

ComponentFactory :
Crea y valida componentes.

DomainService :
Verifica compatibilidad entre componentes.

Category :
Clasifica componentes en jerarquías (padre-hijo).

SpecificationsComponent :
Almacena detalles técnicos del componente.

Manufacturer :
Información del fabricante y contactos de soporte.

Contact :
Detalles de contacto (teléfono, email).

ComponentRepository :
Guarda y recupera componentes.

[![Diagrama-en-blanco-4.png](https://i.postimg.cc/FHw7GNgc/Diagrama-en-blanco-4.png)](https://postimg.cc/3kC8xMqJ)
###### 4.2.5.6.2. Bounded Context Database Design Diagram

COMPONENTS :
Almacena componentes (id, name, type, specs, price).
Relacionada con CATEGORIES y MANUFACTURERS.

COMPONENT_COMPATIBILITY :
Registra pares de componentes compatibles.
CATEGORIES :
Clasifica componentes en jerarquías (id, name, parent_id).

MANUFACTURERS :
Almacena fabricantes y contactos de soporte.

Relaciones:
Componentes → Categorías y Fabricantes.
Categorías → Jerarquía (padre-hijo).
Compatibilidad → Pares de componentes.

[![Diagrama-en-blanco-5.png](https://i.postimg.cc/W4JSfpRP/Diagrama-en-blanco-5.png)](https://postimg.cc/jWtzDbd8)

#### 4.2.5. Bounded Context: Proveedor / Tienda

En esta sección, se detallan las clases y componentes identificados en el bounded context de Proveedor/Tienda, que abarca lo que es la obtención de los datos de los componentes para PC  
---

###### 4.2.5.1. Domain Layer

Esta capa representa el núcleo del sistema y las reglas de negocio del dominio.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| ComponenteProveedor | Entidad | Representa un componente que un proveedor ofrece, incluyendo precio, detalles y enlace de compra. | \- id: String \- proveedor: Proveedor \- detalle: DetalleComponente \- precio: Precio \- stock: Stock? \- urlCompra: String \+ esDisponible(): boolean |
| Proveedor | Entidad | Representa una tienda externa o proveedor asociado a un componente. | \- id: String \- nombre: String \- sitioWeb: String |
| Precio | Value Object | Encapsula el valor monetario en una divisa específica. | \- monto: Double \- moneda: String (e.g. "USD", "PEN") |
| DetalleComponente | Value Object | Describe las características técnicas de un componente de PC. | \- modelo: String \- marca: String \- velocidad: String \- capacidad: String? \- imagenUrl: String |
| Stock | Value Object | Representa la cantidad disponible estimada. Opcional. | \- cantidad: Int \+ hayStock(): boolean |

---

###### 4.2.5.2. Interface Layer

Encargada de exponer funcionalidades al usuario o consumidores externos.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| ProveedorTiendaController | Controller | Maneja las peticiones relacionadas con componentes disponibles en tiendas externas, incluyendo precios y redirección. | \+ obtenerPrecioComponente(id: String): ComponenteProveedorDTO \+ redirigirAProveedor(id: String): void |
| ProveedorTiendaView | View | Vista unificada que presenta los precios estimados y botón para redirigir al proveedor externo. | \- componenteId: String \- nombre: String \- precio: String \- moneda: String \- urlCompra: String \- imagenUrl: String \+ mostrarInformacion() \+ mostrarBotonComprar() |

---

#### 4.2.5.3. Application Layer

Define los flujos de negocio mediante comandos y eventos.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| ConsultarPrecioComponenteCommand | Command | Solicita la información de precio y detalles del componente desde una fuente externa o base de datos. | \- componenteId: String |
| RedirigirAProveedorCommand | Command | Dispara el flujo de redirección hacia el proveedor externo asociado al componente. | \- componenteId: String |
| PrecioConsultadoEvent | Event | Evento lanzado cuando se ha consultado exitosamente el precio del componente. | \- componenteId: String \- precio: Double \- moneda: String |
| ProveedorRedireccionadoEvent | Event | Evento lanzado cuando un usuario ha sido redirigido correctamente al sitio del proveedor. | \- componenteId: String \- urlProveedor: String |
| ProveedorTiendaService | Application Service | Orquesta los casos de uso principales: consulta de precio y redirección. | \+ manejar(cmd: ConsultarPrecioComponenteCommand): PrecioConsultadoEvent \+ manejar(cmd: RedirigirAProveedorCommand): ProveedorRedireccionadoEvent |

---

##### 4.2.5.4. Infrastructure Layer

Provee la implementación concreta de servicios como base de datos, brokers, etc.

| Clase | Tipo | Propósito | Tecnologías |
| :---- | :---- | :---- | :---- |
| ComponenteProveedorRepositoryImpl | Repository Implementation | Implementación concreta para acceder a los datos de componentes ofrecidos por tiendas/proveedores. | Room (Jetpack Compose), PostgreSQL |
| ProveedorExternalRedirector | External Service | Servicio responsable de generar la redirección del usuario al sitio del proveedor. | Intents (Android), URL Schemes |
| ProveedorApiAdapter | External API Adapter | Adaptador para consumir APIs externas de tiendas (scraping o REST) y obtener detalles como precios, stock o imágenes. | Retrofit  |
| ProveedorEventPublisher | Event Publisher | Publica eventos relacionados con interacciones de tienda (consulta de precios, redirección). | Kotlin Coroutines / EventBus (opcional) |
| ProveedorDTOMapper | Mapper | Convierte entre entidades de dominio y DTOs usados en la capa Interface. | Kotlin, Manual Mapping o MapStruct (si Java interop) |

###### 4.2.5.5. Bounded Context Software Architecture Component Level Diagrams

* Este Component Diagram descompone el container Configuración Técnica API (el backend del bounded context) en:  
* Controller: punto de entrada HTTP.  
* Command Handler: maneja la lógica principal.  
* Domain Service y Factory: lógica de dominio para obtener información de los componentes.  
* Repository: persistencia de datos en PostgreSQL.  
* External API: cliente para validaciones externas.

[![image.png](https://i.postimg.cc/L6mjgR55/image.png)](https://postimg.cc/HjPrFqQ1)
[![image.png](https://i.postimg.cc/tgsc0FGK/image.png)](https://postimg.cc/06qnDMQn)

##### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams

A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de Proveedor/Tienda. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.

###### *4.2.1.6.1. Bounded Context Domain Layer Class Diagrams*

| Clase | Tipo | Descripción |
| :---- | :---- | :---- |
| ComponenteProveedor | Entidad | Representa un componente que un proveedor ofrece, incluyendo información sobre el precio, detalles técnicos y el enlace para comprar el componente. |
| Proveedor | Entidad | Representa una tienda o proveedor asociado a un componente. |
| Precio | Value Object | Encapsula el valor monetario en una divisa específica, utilizado para el precio de los componentes. |
| DetalleComponente | Value Object | Describe las características técnicas de un componente de PC (modelo, marca, velocidad, capacidad, etc.). |
| Stock | Value Object | Representa la cantidad disponible estimada de un componente. Opcional, puede no estar presente para algunos componentes. |

[![image.png](https://i.postimg.cc/BvsnvZMQ/image.png)](https://postimg.cc/9D8h8h6v)

###### *4.2.1.6.2. Bounded Context Database Design Diagram*

Este diagrama representa el modelo relacional que da soporte a la persistencia de datos del bounded context Proveedor/Tienda.  
El diseño se alinea con el dominio previamente modelado en las secciones anteriores, asegurando que se obtengan los datos requeridos para poder ser utilizados en comparativa.  
Se utilizaron las siguientes decisiones de modelado:

* Tabla Proveedor:

  * Contiene información sobre el proveedor de los componentes.

  * Atributos: id, nombre, sitioWeb.

* Tabla ComponenteProveedor:

  * Representa la información de los componentes que los proveedores ofrecen. Incluye atributos como el urlCompra y hace referencia a las tablas Proveedor, Precio, DetalleComponente y Stock (este último es opcional).

  * Atributos: id, proveedor\_id (relacionado con Proveedor), detalle\_id (relacionado con DetalleComponente), precio\_id (relacionado con Precio), stock\_id (relacionado con Stock), urlCompra.

* Tabla Precio:

  * Contiene la información del precio de un componente con su monto y moneda.

  * Atributos: id, monto, moneda.

* Tabla DetalleComponente:

  * Describe las características técnicas de cada componente (modelo, marca, velocidad, etc.).

  * Atributos: id, modelo, marca, velocidad, capacidad, imagenUrl.

* Tabla Stock:

  * Representa la cantidad disponible de un componente en stock. Es opcional en caso de que no se maneje stock.

  * Atributos: id, cantidad.

Relaciones claves:

* Un **ComponenteProveedor** pertenece a un **Proveedor**.

* Un **ComponenteProveedor** tiene un **Precio**, un **DetalleComponente** y opcionalmente un **Stock**.

* Las claves primarias son representadas por `PK(id)` y las claves foráneas son representadas por `FK`.  


[![image.png](https://i.postimg.cc/fb277P3X/image.png)](https://postimg.cc/McBjqdmK)

Tecnología objetivo:  
La base de datos utilizada será PostgreSQL, por su robustez y compatibilidad con UUIDs y relaciones complejas. Las claves primarias y foráneas están correctamente tipadas y normalizadas para mantener integridad referencial.  

#### 4.2.6. Bounded Context: Glosario
En esta sección, se detallan las clases y componentes identificados en el bounded context de Glosario, que abarca lo que son terminos, consejos para cada componente e información adicional para utilizar la aplicación  
---

##### 4.2.6.1. Domain Layer

Esta capa representa el núcleo del sistema y las reglas de negocio del dominio.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| TerminoGlosario | Entidad | Representa un término técnico con definición y ejemplos. | \- id: String \- termino: String \- definicion: String \- ejemplos: List\<String\> |
| GuiaTecnica | Entidad | Representa una guía agrupada por tipo de componente. | \- id: String \- categoria: String (ej. CPU, GPU) \- contenido: String |
| TipContextual | Value Object | Representa un consejo breve mostrado en el flujo de armado. | \- paso: String (ej. "CPU") \- mensaje: String \- linkGuia: String? \- linkGlosario: String? |
| CategoriaComponente | Value Object | Representa una categoría válida de componentes para organizar guías. | \- nombre: String |

---

##### 4.2.6.2. Interface Layer

Encargada de exponer funcionalidades al usuario o consumidores externos.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| GlosarioController | Controller | Maneja peticiones para obtener términos, guías o tips contextualizados. | \+ obtenerTermino(id: String): TerminoGlosarioDTO \+ buscarTermino(texto: String): TerminoGlosarioDTO? \+ obtenerGuiaPorCategoria(categoria: String): GuiaTecnicaDTO \+ obtenerTipContextual(paso: String): TipContextualDTO |
| GlosarioView | View | Vista que muestra el glosario, las guías por categoría o los tips contextuales. | \- termino: String \- definicion: String \- ejemplos: List\<String\> \- categoria: String \- contenido: String \- tip: String \+ mostrarTermino() \+ mostrarGuia() \+ mostrarTip() |

---

##### 4.2.6.3. Application Layer

Define los flujos de negocio mediante comandos y eventos.

| Clase | Tipo | Propósito | Atributos / Métodos |
| :---- | :---- | :---- | :---- |
| ConsultarTerminoCommand | Command | Solicita información de un término técnico. | \- terminoId: String |
| BuscarTerminoCommand | Command | Permite buscar un término por texto ingresado. | \- texto: String |
| ConsultarGuiaPorCategoriaCommand | Command | Recupera una guía por tipo de componente. | \- categoria: String |
| ObtenerTipContextualCommand | Command | Solicita un tip según el paso del flujo de armado. | \- paso: String |
| TerminoConsultadoEvent | Event | Evento emitido al consultar un término con éxito. | \- terminoId: String |
| GuiaConsultadaEvent | Event | Evento emitido al visualizar una guía. | \- categoria: String |
| TipMostradoEvent | Event | Evento emitido al mostrar un tip contextual. | \- paso: String |
| GlosarioService | ApplicationService | Servicio que maneja los casos de uso del glosario. | \+ manejar(cmd: ConsultarTerminoCommand): TerminoConsultadoEvent \+ manejar(cmd: BuscarTerminoCommand): TerminoConsultadoEvent? \+ manejar(cmd: ConsultarGuiaPorCategoriaCommand): GuiaConsultadaEvent \+ manejar(cmd: ObtenerTipContextualCommand): TipMostradoEvent |

---

##### 4.2.6.4. Infrastructure Layer

Provee la implementación concreta de servicios como base de datos, brokers, etc.

| Clase | Tipo (en inglés) | Propósito | Tecnologías |
| :---- | :---- | :---- | :---- |
| TerminoGlosarioRepositoryImpl | Repository Implementation | Accede a la base de datos para términos del glosario. | Room / SQLite / Firestore |
| GuiaTecnicaRepositoryImpl | Repository Implementation | Accede a la base de datos o archivos estáticos de guías. | Firestore / Assets |
| TipContextualProvider | External Service | Proveedor de tips para pasos del armado. | Local DB / Embedded Logic |
| GlosarioEventPublisher | Event Publisher | Publica eventos cuando se visualiza contenido del glosario. | EventBus / Kotlin Coroutines |
| GlosarioDTOMapper | Mapper | Convierte entidades del dominio a DTOs para la vista. | Manual Mapping / Kotlin |
| Clase | Tipo (en inglés) | Propósito | Tecnologías |
| TerminoGlosarioRepositoryImpl | Repository Implementation | Accede a la base de datos para términos del glosario. | Room / SQLite / Firestore |
| GuiaTecnicaRepositoryImpl | Repository Implementation | Accede a la base de datos o archivos estáticos de guías. | Firestore / Assets |

##### 4.2.6.5. Bounded Context Software Architecture Component Level Diagrams

* Este Component Diagram descompone el container Configuración Técnica API (el backend del bounded context) en:  
* Controller: punto de entrada HTTP.  
* Command Handler: maneja la lógica principal.  
* Domain Service y Factory: lógica de dominio para dar información de los componentes.  
* Repository: persistencia de datos en PostgreSQL.  
* External API: cliente para validaciones externas.

[![structurizr-Component-001-1.png](https://i.postimg.cc/MH2gvFJ3/structurizr-Component-001-1.png)](https://postimg.cc/BLpmzN62)

##### 4.2.6.6. Bounded Context Software Architecture Code Level Diagrams

A continuación, se detallan los diagramas de arquitectura de código que brindan mayor profundidad sobre la implementación interna del bounded context de Glosario. Esta vista se enfoca en clases, métodos, atributos y relaciones a nivel de código fuente.

###### *4.2.6.6.1. Bounded Context Domain Layer Class Diagrams*

| Clase | Tipo | Descripción |
| :---- | :---- | :---- |
| TerminoGlosario | Entidad | Representa un término técnico con su definición y ejemplos. |
| GuiaTecnica | Entidad | Representa una guía técnica asociada a una categoría de componente. |
| TipContextual | Value Object | Representa un consejo o recomendación mostrado en un paso del flujo. |
| CategoriaComponente | Value Object | Representa las categorías válidas de componentes (CPU, GPU, etc.). |

[![image.png](https://i.postimg.cc/cHYbyBtR/image.png)](https://postimg.cc/LY9TjfT5)

###### *4.2.6.6.2. Bounded Context Database Design Diagram*

Este diagrama representa el modelo relacional que da soporte a la persistencia de datos del Bounded Context Glosario.  
El diseño se alinea con el dominio previamente modelado, asegurando que los usuarios puedan acceder a definiciones, guías y tips relevantes durante la construcción de sus builds.

Se utilizaron las siguientes decisiones de modelado:

Tabla TerminoGlosario:

* Contiene los términos técnicos con su definición y ejemplos.

* Atributos: id, termino, definicion, ejemplos.

Tabla GuiaTecnica:

* Representa guías detalladas por categoría de componente.

* Atributos: id, titulo, contenido, categoria.

Tabla TipContextual:

* Almacena tips o consejos contextuales mostrados durante el armado de builds.

* Atributos: id, mensaje, linkRelacionado.

Relaciones clave:

* Cada TipContextual puede estar relacionado a una categoría de componente, pero no es obligatorio.

* Las categorías están predefinidas como enum o dominio controlado.

Tecnología objetivo:  
Se utilizará PostgreSQL por su robustez, manejo de tipos como UUID, y capacidades para relaciones complejas.  
Las claves primarias (PK) y foráneas (FK) están correctamente normalizadas para garantizar la integridad referencial.
  
[![image.png](https://i.postimg.cc/9Fx1knN3/image.png)](https://postimg.cc/tYxhZ2jD)

## Conclusiones
Conclusiones y recomendaciones.
Video About-the-team


## Bibliografía

- TechTarget. (s.f.). How to choose the right PC for business. SearchEnterpriseDesktop. Recuperado el 20 de abril de 2025, de https://www.techtarget.com/searchenterprisedesktop/tip/How-to-choose-the-right-PC-for-business

- ZDNet. (s.f.). How to choose the right PC: Everything you need to know about picking the right computer for work. Recuperado el 20 de abril de 2025, de https://www.zdnet.com/article/how-to-chose-the-right-pc-everything-you-need-to-know-about-picking-the-right-computer-for-work/

- Shapiro, J. (s.f.). Top 7 things to consider when buying a new computer to avoid disappointment. LinkedIn. Recuperado el 20 de abril de 2025, de https://www.linkedin.com/pulse/top-7-things-consider-when-buying-new-computer-avoid-

- Kingston Technology. (s.f.). Top 10 PC build mistakes beginners make. Recuperado el 20 de abril de 2025, de https://www.kingston.com/en/blog/gaming/top-10-pc-build-mistakes-beginners-make

- Justice IT Consulting. (s.f.). Justice IT Consulting. Recuperado el 20 de abril de 2025, de http://www.justiceitc.com/?trk=article-ssr-frontend-pulse_little-text-block

## Anexos

- To-be Scenario Mapping: https://miro.com/app/board/uXjVIE_P0Bw=/?share_link_id=102963333287 
