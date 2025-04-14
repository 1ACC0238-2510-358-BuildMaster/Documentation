## Capítulo IV: Product Software Design 

### 4.1. Strategic-Level Domain-Driven Design
#### 4.1.1. EventStorming

Con el objetivo de realizar un modelado colaborativo y estratégico del dominio de *BuildMaster*, se llevó a cabo una sesión de **EventStorming**, una técnica visual centrada en eventos del dominio que permite identificar flujos de negocio, entidades relevantes, actores y límites naturales del sistema.

El foco de esta sesión fue descomponer el dominio de una aplicación móvil que permite a usuarios configurar PCs según su presupuesto y necesidades, revisar precios y disponibilidad de componentes, y compartir builds con la comunidad. 

###### Herramientas utilizadas

- Herramienta visual: **Miro**
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

//////

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

###### Evidencias visuales

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
- **Herramienta visual**: Miro (puede ser también Lucidchart, Figma o DomainStoryTelling.org)  
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
#### 4.1.3. Software Architecture
##### 4.1.3.1. Software Architecture Context Level Diagrams
##### 4.1.3.2. Software Architecture Container Level Diagrams
##### 4.1.3.3. Software Architecture Deployment Diagrams
///////////////
### 4.2. Tactical-Level Domain-Driven Design
#### 4.2.X. Bounded Context: <Bounded Context Name>
##### 4.2.X.1. Domain Layer
##### 4.2.X.2. Interface Layer
##### 4.2.X.3. Application Layer
##### 4.2.X.4. Infrastructure Layer
##### 4.2.X.5. Bounded Context Software Architecture Component Level Diagrams
##### 4.2.X.6. Bounded Context Software Architecture Code Level Diagrams
###### 4.2.X.6.1. Bounded Context Domain Layer Class Diagrams
###### 2.6.x.6.2. Bounded Context Database Design Diagram

//Como solo avanzaremos hasta este capitulo esto quedará aquí y luego lo pasaremos al capitulo 5 en su rama respectiva

## Conclusiones
Conclusiones y recomendaciones.
Video About-the-team


## Bibliografía
https://www.techtarget.com/searchenterprisedesktop/tip/How-to-choose-the-right-PC-for-business

https://www.zdnet.com/article/how-to-chose-the-right-pc-everything-you-need-to-know-about-picking-the-right-computer-for-work/

https://www.linkedin.com/pulse/top-7-things-consider-when-buying-new-computer-avoid-


https://www.kingston.com/en/blog/gaming/top-10-pc-build-mistakes-beginners-make


http://www.justiceitc.com/?trk=article-ssr-frontend-pulse_little-text-block 
## Anexos