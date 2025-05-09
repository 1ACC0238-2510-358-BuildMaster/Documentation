## Capítulo V: Solution UI/UX Design
### 5.1. Product design

En esta sección se presenta el diseño del producto **BuildMaster** como una parte esencial de la arquitectura del sistema. El diseño ha sido cuidadosamente estructurado para alinear las funcionalidades clave del sistema con las necesidades detectadas en fases anteriores del análisis y modelado del dominio.

El producto está centrado en brindar a usuarios entusiastas de hardware y tecnología una plataforma intuitiva y poderosa para la creación, análisis y compartición de builds personalizados de PC. El diseño del sistema considera tanto la experiencia del usuario como la eficiencia del backend, asegurando una integración coherente entre sus diferentes componentes.

La arquitectura de BuildMaster contempla una aplicación móvil desarrollada en **Kotlin**, respaldada por un backend en **Spring Boot** y una base de datos relacional en **PostgreSQL**. Estas decisiones tecnológicas permiten escalabilidad, rapidez en el desarrollo y mantenibilidad a largo plazo.

#### 5.1.1. Style Guidelines
El objetivo de esta sección es establecer una guía clara y compartida por todo el equipo sobre el diseño visual de la aplicación. Contar con un set de reglas comunes sobre colores, tipografía, espaciados, iconografía y otros aspectos visuales asegura una experiencia de usuario coherente y profesional.

Todo el equipo trabaja sobre un repositorio central de **assets**, que incluye íconos, fuentes, paleta de colores, y componentes de UI reutilizables. Esto facilita la consistencia entre las pantallas, reduce ambigüedades en el diseño y mejora la colaboración entre desarrolladores y diseñadores.
##### 5.1.1.1. General Style Guidelines

**Paleta de colores principal**  
La estética visual de BuildMaster se basa en una paleta minimalista pero fuerte que refleja confianza, tecnología y modernidad:

| Color         | Hex       | Uso principal                                           |
|---------------|-----------|----------------------------------------------------------|
| Verde Tecla   | `#00B253` | Color primario en botones, íconos, acentos y el logo.    |
| Blanco        | `#FFFFFF` | Fondo principal en vistas limpias y legibilidad.         |
| Negro         | `#000000` | Tipografía principal, bordes y líneas.                   |
| Gris Claro    | `#F5F5F5` | Fondo neutro para secciones o tarjetas secundarias.      |
| Gris Oscuro   | `#333333` | Textos secundarios o subtítulos.                         |

**Tipografía**  
BuildMaster utiliza una fuente sans-serif moderna para garantizar claridad y consistencia:

- Fuente primaria: **Montserrat** o **Poppins**
- Pesos recomendados:
  - Títulos: Bold o Semi-Bold
  - Texto general: Regular
  - Botones: Medium

**Iconografía y botones**  
- Iconos minimalistas en negro o verde.
- Bordes ligeramente redondeados (`border-radius: 8px`).
- Botones primarios con fondo verde `#00B253` y texto blanco.
- En hover: verde más oscuro o borde verde con fondo blanco.

**Estilo visual**  
- Diseño limpio, con uso de espacio en blanco.
- Tarjetas para agrupar contenido (componentes, builds, guías).
- Sombra ligera (`box-shadow`) para destacar componentes interactivos.

**Usabilidad y accesibilidad**  
- Contraste suficiente entre texto y fondo.
- Botones navegables por teclado.
- Uso correcto de atributos `aria-*` para compatibilidad con lectores de pantalla.

#### 5.1.2. Information Architecture

Esta sección describe cómo se estructura la información dentro del sistema BuildMaster, tanto en su aplicación móvil como en su landing page. Se abordan aspectos como la organización visual, categorización, etiquetado, SEO/ASO y los mecanismos que facilitarán al usuario encontrar y recorrer los contenidos.

##### 5.1.2.1. Organization Systems

En **BuildMaster**, se aplican diferentes tipos de organización de la información, según el contexto y la funcionalidad:

- **Organización jerárquica**:
  - Aplicada en la navegación de componentes (Catálogo), donde los usuarios pueden explorar por categorías (CPU, GPU, RAM, etc.) y subcategorías.
  - También en la gestión de builds guardadas del usuario.

- **Organización secuencial**:
  - Utilizada en el proceso de creación de una build, el cual sigue una estructura paso a paso: seleccionar categoría → seleccionar componente → validar compatibilidad → guardar.

- **Organización matricial**:
  - Se aplica al comparar múltiples builds o especificaciones de componentes de forma tabular.

**Esquemas de categorización**:

- **Alfabética**: listado de fabricantes o builds ordenados por nombre.
- **Por tópicos**: guías técnicas agrupadas por tema (Overclocking, Ensamblaje, Mantenimiento, etc.).
- **Por audiencia**: contenido educativo clasificado para principiantes, intermedios o expertos.

##### 5.1.2.2. Labelling Systems

Para garantizar la claridad y facilidad de uso, los datos y acciones estarán etiquetados con palabras breves, claras y coherentes.

**Ejemplos de etiquetas principales**:

- **Botones**: `Agregar`, `Guardar Build`, `Comparar`, `Eliminar`, `Filtrar`, `Ver Detalles`.
- **Secciones**:
  - Catálogo → `Componentes`
  - Builds → `Mis Builds`, `Builds Populares`
  - Comunidad → `Comentarios`, `Votaciones`
  - Guías → `Tips`, `Tutoriales`, `Guías Técnicas`
- **Filtros de búsqueda**: `Nombre`, `Tipo`, `Fabricante`, `Compatibilidad`, `Categoría`.

Las asociaciones visuales estarán apoyadas por iconografía intuitiva, colores y agrupamiento por tarjetas.

##### 5.1.2.3. SEO Tags and Meta Tags

Se definirán metadatos específicos para mejorar la visibilidad en motores de búsqueda (SEO) y en tiendas de aplicaciones (ASO).

**Landing Page - SEO Tags**:

- `Title`: BuildMaster - Crea y Comparte Builds de PC
- `Meta Description`: Plataforma para armar builds de PC personalizados, comparar componentes y recibir sugerencias de compatibilidad.
- `Keywords`: build pc, armar pc, componentes pc, catálogo hardware, builds personalizadas
- `Author`: Equipo BuildMaster

**Web App / Mobile App - ASO Tags**:

- `App Title`: BuildMaster
- `App Subtitle`: Creador de Builds de PC con validación automática
- `App Description`: Con BuildMaster puedes crear builds de PC personalizados, analizar compatibilidad de componentes, guardar tus configuraciones y compartirlas con la comunidad.
- `App Keywords`: build pc, compatibilidad, hardware, armar computadora, piezas pc

##### 5.1.2.4. Searching Systems

Se definirán metadatos específicos para mejorar la visibilidad en motores de búsqueda (SEO) y en tiendas de aplicaciones (ASO).

**Landing Page - SEO Tags**:

- `Title`: BuildMaster - Crea y Comparte Builds de PC
- `Meta Description`: Plataforma para armar builds de PC personalizados, comparar componentes y recibir sugerencias de compatibilidad.
- `Keywords`: build pc, armar pc, componentes pc, catálogo hardware, builds personalizadas
- `Author`: Equipo BuildMaster

**Web App / Mobile App - ASO Tags**:

- `App Title`: BuildMaster
- `App Subtitle`: Creador de Builds de PC con validación automática
- `App Description`: Con BuildMaster puedes crear builds de PC personalizados, analizar compatibilidad de componentes, guardar tus configuraciones y compartirlas con la comunidad.
- `App Keywords`: build pc, compatibilidad, hardware, armar computadora, piezas pc

##### 5.1.2.5. Navigation Systems

Para asegurar una experiencia fluida, BuildMaster cuenta con sistemas de navegación estructurados tanto en la landing como en la aplicación móvil:

**Landing Page**:
- Menú superior con scroll y anclas: `Inicio`, `Sobre Nosotros`, `Contacto`, `FAQ`.
- Botones destacados de llamada a la acción: `Explorar Builds`, `Comenzar Build`.

**Aplicación Móvil**:
- Barra de navegación inferior con íconos: `Catálogo`, `Mis Builds`, `Crear`, `Comunidad`, `Perfil`.
- Botones contextuales flotantes (FAB) para crear o guardar rápidamente.
- Breadcrumbs internos y etiquetas de paso en la creación de builds para mantener al usuario orientado.

#### 5.1.3. Landing Page UI Design
##### 5.1.3.1. Landing Page Wireframe
##### 5.1.3.2. Landing Page Mock-up
#### 5.1.4. Mobile Applications UX/UI Design
##### 5.1.4.1. Mobile Applications Wireframes
##### 5.1.4.2. Mobile Applications Wireflow Diagrams
##### 5.1.4.3. Mobile Applications Mock-ups
##### 5.1.4.4. Mobile Applications User Flow Diagrams
##### 5.1.4.5. Mobile Applications Prototyping