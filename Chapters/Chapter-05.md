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

A continuación el diseño realizado de la Landing Page del producto Build Master.

##### 5.1.3.1. Landing Page Wireframe

Los diseños de los wireframes para la landing page se desarrollaron con la plataforma de diseño en línea Figma. El enlace es el siguiente:
https://www.figma.com/design/FqAYzDC46kVQpv46HhYI8O/Landing-Page-Build-Master?node-id=51-81&t=WEg4UUejSRIh8MVj-1

Además, dichos modelos fueron trabajados bajo una estructura visual limpia y organizada, con un enfoque en la usabilidad y la jerarquía de la información. A continuación, se explican algunas de las decisiones de diseño y arquitectura de la información empleadas:

## 1. Encabezado con redirección al Home y Menú Hamburguesa

El encabezado incluye el nombre de la app ubicado en la parte izquierda, funcionando como enlace al Home. A la derecha, se encuentra un menú hamburguesa que, al hacer clic, despliega las opciones: **Inicio**, **Acerca de Nosotros**, **Ayuda (Preguntas Frecuentes)** y **Contáctanos**. Debajo del encabezado, se presenta nuevamente el nombre de la app junto a un mensaje de enganche a favor de la descarga de la App y un slider a la derecha con los íconos representativos de la aplicación.

## 2. Encabezado con Redirección al Home y Menú Hamburguesa

El diseño del encabezado implementa una estructura simplificada y funcional. A la izquierda, el nombre de la aplicación actúa como un enlace directo al Home, proporcionando una referencia constante para el usuario. A la derecha, se integra un menú hamburguesa que, al hacer clic, despliega opciones clave de navegación: **Inicio**, **Acerca de Nosotros**, **Ayuda (Preguntas Frecuentes)** y **Contáctanos**. Esta disposición compacta optimiza el espacio visual y mantiene una estética minimalista. Debajo del encabezado, se refuerza la identidad de la aplicación mediante la reiteración del nombre, acompañado de una breve descripción y un slider con íconos de la app, alineando visualmente los elementos y asegurando una estructura coherente.

## 3. Contenido Informativo Acerca de la Aplicación

La información está organizada en bloques que siguen un flujo lógico, lo que mejora la experiencia de usuario mediante una jerarquía visual clara. Se establecen secciones bien definidas para guiar al usuario a través del contenido:

- **Propiedades de la APP**: Se destacan las características más relevantes de la aplicación, resaltando los elementos diferenciadores que captan la atención del público objetivo y comunican su propuesta de valor.
  
- **Sección de Experiencia del Usuario (Build Master App)**: Enfocada en proporcionar recomendaciones que optimicen la interacción del usuario con la app. Se destaca la simplicidad del proceso, incorporando un llamado a la acción para calificar la aplicación.

## 4. Sección “Sobre Nosotros”

Esta sección profundiza en la identidad de la empresa, presentando de forma estructurada la misión, visión y valores. Asimismo, se define claramente el público objetivo y se contextualiza la aplicación dentro del marco empresarial, creando una conexión entre la marca y los usuarios.

## 5. Sección “Preguntas Frecuentes (FAQs)”

Diseñada estratégicamente para anticipar y resolver las inquietudes comunes de los usuarios durante sus primeras interacciones con la aplicación. Se incluye un botón **“Leer más”**, que redirige a una página dedicada a preguntas adicionales, ampliando el alcance del soporte informativo.

## 6. Sección “Contáctanos”

Funciona como un canal de comunicación directa entre los usuarios y el equipo de soporte. Esta sección no solo permite resolver dudas no cubiertas en las FAQs, sino que también refuerza la percepción de accesibilidad y cercanía con la empresa.

## 7. Footer con Enlaces Complementarios

El footer integra enlaces estratégicos hacia redes sociales, fomentando la interacción continua con los usuarios más allá de la landing page. Esta estrategia contribuye al fortalecimiento de la comunidad en torno a la aplicación y la marca.

## 8. Uso de Botones de Llamada a la Acción (CTA)

En puntos estratégicos del recorrido del usuario se incluyen botones CTA que motivan la interacción:

- **Sección Build Master App**: CTA para descargar la app, alineado con el objetivo de conversión.
- **Sección Preguntas Frecuentes**: CTA **“Leer más”** para profundizar en las respuestas a preguntas comunes.

## 9. Diseño Adaptativo y Accesible

La disposición de los bloques y elementos visuales sigue una estructura alineada y coherente, garantizando una experiencia responsive que se ajusta a diferentes tamaños de pantalla sin comprometer la legibilidad ni la navegabilidad.

---

## Conclusión del Diseño

El diseño se enfoca en priorizar la claridad y simplicidad de la navegación mediante un encabezado compacto y una estructura organizada por secciones. La disposición estratégica de los botones de llamada a la acción guía al usuario hacia puntos clave de interacción, fomentando la conversión y mejorando la experiencia general. Además, el diseño visual facilita la navegación intuitiva y asegura una experiencia de usuario fluida, manteniendo la coherencia gráfica en todas las pantallas. Esta combinación de elementos no solo refuerza la identidad de la aplicación, sino que también optimiza la accesibilidad, garantizando que los usuarios puedan interactuar de forma efectiva con el contenido desde cualquier dispositivo.

# Desktop Web Browser: Interfaz para Dispositivos de Escritorio

La interfaz está diseñada para proporcionar una experiencia de usuario óptima en navegadores web de escritorio, garantizando una navegación fluida y una disposición visual coherente. A continuación, se detallan las principales secciones:

## Home: Punto de Entrada y Presentación del Producto

![Home](https://i.postimg.cc/zfyhGtmq/W-Home.png)

La sección **Home** establece el punto de inicio de la experiencia del usuario, integrando elementos clave para captar su atención y facilitar la navegación:

- **Encabezado Funcional**:
  - A la izquierda, se ubica el nombre de la Startup, que actúa simultáneamente como enlace al Home, manteniendo la estructura de navegación accesible en todo momento.
  - A la derecha, se implementa un menú hamburguesa, diseñado para optimizar el espacio visual. Al hacer clic, el menú despliega opciones clave del landing page: **Inicio**, **Sobre Nosotros**, **Preguntas Frecuentes** y **Contáctanos**.
  
- **Hero Section**:
  - Debajo del encabezado, se presenta el nombre del producto acompañado de una frase enérgica que refuerza su propuesta de valor, por ejemplo, *“Construye tu PC”*.
  - A la derecha, un slider interactivo muestra imágenes representativas del producto y logotipos de la Startup, consolidando la identidad visual del proyecto.

- **Sección Informativa del Producto**:
  - A continuación, se incluye un bloque informativo que destaca las funcionalidades más relevantes de la aplicación, incentivando al usuario a explorar sus características y beneficios.

## About Us (Sobre Nosotros): Identidad y Propósito de la Startup

![About Us](https://i.postimg.cc/4N1VLHbR/W-About-us.png)

Esta sección tiene como objetivo establecer una conexión con el usuario a través de un relato claro y estructurado sobre la empresa:

- **Descripción Breve**: Se presenta una introducción concisa sobre la Startup, destacando los pilares fundamentales: misión, visión y valores.
- **Perfil del Usuario Objetivo**: Se define claramente a quién está dirigida la aplicación, abarcando tanto a usuarios individuales como a empresas de diferentes tamaños.
- **Reforzamiento Visual**: La sección incluye una imagen de fondo que muestra un ejemplo del producto, contextualizando la información y creando una experiencia más inmersiva para el usuario.

## Preguntas Frecuentes (FAQs): Resolución de Dudas Comunes

![FAQs](https://i.postimg.cc/y8Y9w6vg/W-Help-FAQs.png)

Esta sección está diseñada para anticipar y resolver las dudas más comunes de los usuarios que interactúan por primera vez con la aplicación:

- **Listado de Preguntas Frecuentes**: Se organiza un conjunto de consultas frecuentes que cubren las funcionalidades esenciales del producto, proporcionando respuestas claras y directas.
- **Botón “Leer Más”**: Si el usuario accede a esta sección desde el Home, se presenta un botón **“Leer Más”** que redirige a una página completa de FAQs, donde se detallan más preguntas y respuestas, asegurando un acceso rápido a información ampliada.

## Contacto: Canal de Comunicación Directa con el Equipo

![Contacto](https://i.postimg.cc/tCbFNN6z/W-Contact.png)

La sección de contacto está enfocada en facilitar la interacción directa entre los usuarios y el equipo de soporte de la Startup:

- **Formulario de Contacto**:
  - Se solicita al usuario completar un formulario con información básica: nombre completo, número de celular y correo electrónico, permitiendo un seguimiento efectivo de sus consultas.

- **Relación Cercana con el Cliente**:
  - Esta sección refuerza el compromiso de la Startup con sus usuarios, fomentando un trato cercano y personalizado, lo que contribuye a mejorar la percepción del producto y la experiencia general del usuario.

  ## Mobile Web Browser

La interfaz del navegador web para dispositivos móviles ha sido diseñada para garantizar una experiencia de usuario óptima, organizada en múltiples divisiones que estructuran de manera coherente el contenido. A continuación, se detallan cada una de las secciones:

### Home – División 1
![Home División 1](https://i.postimg.cc/QMNg7vt5/1.jpg)

Esta sección constituye la primera visualización del Home en dispositivos móviles. Incluye los siguientes elementos:
- **Encabezado:** Nombre de la Startup alineado a la izquierda y menú hamburguesa a la derecha.
- **Presentación del Producto:** Nombre del producto, acompañado de un eslogan representativo.
- **Call to Action (CTA):** Botón de descarga de la aplicación.
- **Identidad Visual:** Logo de la aplicación ubicado debajo del botón de descarga.

### Home – División 2
![Home División 2](https://i.postimg.cc/CKvGsJB2/2.png)

En esta sección se destacan las funcionalidades más relevantes de la aplicación de forma ordenada y visualmente atractiva. Cada característica está presentada de manera que facilite su comprensión rápida por parte del usuario.

### Home – División 3
![Home División 3](https://i.postimg.cc/nV94q4Hd/3si.jpg)

Esta división está destinada a proporcionar al usuario recomendaciones sobre cómo optimizar la experiencia de uso de la aplicación. Los elementos visuales están centrados y el botón de descarga se mantiene al final del bloque para motivar la acción inmediata.

### Home – División 4
![Home División 4](https://i.postimg.cc/KzRnqLt8/4.jpg)

La cuarta división aborda la sección “Sobre Nosotros”, donde se presentan los aspectos esenciales de la identidad corporativa:
- **Resumen Corporativo:** Breve descripción de la Startup, destacando su propuesta de valor.
- **Misión, Visión y Valores:** Exposición concisa que refuerza los principios y objetivos de la empresa.
- **Público Objetivo:** Definición clara del usuario objetivo, abarcando tanto usuarios individuales como empresas.

### Home – División 5
![Home División 5](https://i.postimg.cc/jdzyFRnP/5.jpg)

La sección “Preguntas Frecuentes” (FAQs) organiza de forma clara las dudas comunes que podrían surgir durante el uso de la aplicación. Incluye:
- Un listado de preguntas frecuentes estructuradas.
- Botón **Leer más** que redirige a una página completa con respuestas detalladas.

### Home – División 6
![Home División 6](https://i.postimg.cc/V6pX36FB/6.jpg)

En esta división se encuentra la sección “Contáctanos”, un formulario de contacto que permite al usuario comunicarse directamente con el equipo de soporte. Los campos solicitados son:
- Nombre
- Número de teléfono
- Correo electrónico
- Mensaje
- Logo de la aplicación ubicado al final de la sección.

### Home – División 7
![Home División 7](https://i.postimg.cc/4NCzPYyX/7.jpg)

La última división corresponde al Footer. Aquí se integran los enlaces a las redes sociales de la Startup y los créditos a los autores del desarrollo del Landing Page.

### Sobre Nosotros
![Sobre Nosotros Mobile](https://i.postimg.cc/zBSdNTVS/W-About-Us-Mobile.png)

En la versión móvil de la sección “Sobre Nosotros”, los textos se reorganizan para optimizar la visibilidad. La disposición incluye:
- **Misión, Visión y Valores:** Ubicados junto a “Nuestros clientes”, permitiendo una visualización compacta y accesible.
- **Imagen de Fondo:** Adaptada al tamaño de pantalla móvil, asegurando una experiencia visual consistente sin comprometer la legibilidad.

### Preguntas Frecuentes (FAQs)
![FAQs Mobile](https://i.postimg.cc/XJ02ts7Y/W-FAQs-Mobile.png)

La versión móvil de la sección “Preguntas Frecuentes” reorganiza los elementos para mantener la estructura vertical, facilitando la navegación y lectura en pantallas reducidas.

### Contáctanos
![Contáctanos Mobile](https://i.postimg.cc/nLmRdyxW/W-Contact-Mobile.png)

El formulario de contacto en su versión móvil conserva los campos de la versión Desktop, pero adaptados a un diseño compacto y simplificado. Los campos solicitados son:
- Nombre
- Número de teléfono
- Correo electrónico
- Mensaje

### Menú
![Menú Mobile](https://i.postimg.cc/cCFXgZ7v/W-Menu-Mobile.png)

En la versión móvil, el menú se despliega al tocar el ícono de menú hamburguesa, presentando las opciones principales de navegación de manera accesible y ordenada.

##### 5.1.3.2. Landing Page Mock-up

Los diseños de los mock-ups se encuentran disponibles en el siguiente enlace: [Landing Page Build Master - Figma](https://www.figma.com/design/FqAYzDC46kVQpv46HhYI8O/Landing-Page-Build-Master?node-id=9-841&t=EXHAb2Ez3ZlvzPh0-1).

Los mock-ups mantienen la coherencia con los wireframes, asegurando la continuidad en la estructura de información y diseño. Se aplicaron lineamientos de color y tipografía consistentes con la identidad visual de la marca, generando un contraste efectivo y mejorando la legibilidad.

### Desktop Web Browser

#### Home (index.html)
![Home Desktop](https://i.postimg.cc/L8BCVshJ/Home.png)

Visualización de la sección **Home** en la versión de escritorio del navegador web.

#### Sobre Nosotros (about-us.html)
![About Us Desktop](https://i.postimg.cc/XY01F5NM/About-us.png)

Visualización de la sección **Sobre Nosotros** desde un navegador web de escritorio.

#### Preguntas Frecuentes (help-center.html)
![FAQs Desktop](https://i.postimg.cc/SQ3vS5wx/Help-FAQs.png)

Sección **Preguntas Frecuentes (FAQs)** en su versión para escritorio, organizada para facilitar el acceso a información clave.

#### Contáctanos (contact.html)
![Contact Desktop](https://i.postimg.cc/WzkFsQgZ/Contact.png)

Formulario de contacto diseñado para la versión de escritorio, con campos para nombre, teléfono, correo electrónico y mensaje.

#### Menú
![Menú Desktop](https://i.postimg.cc/SN9tJdh7/Men.png)

Vista del menú hamburguesa desplegado en su versión para escritorio, presentando las opciones principales de navegación.

### Mobile Web Browser

La estructura del navegador web móvil está organizada en divisiones para optimizar la experiencia del usuario en dispositivos móviles. A continuación, se describen las secciones correspondientes:

### División 1 de Index.html
![División 1](https://i.postimg.cc/CxpCJzvj/1.png)
En esta división se presenta el encabezado que incluye:
- **Nombre de la Startup:** Posicionado en la parte superior izquierda.
- **Menú hamburguesa:** Ubicado a la derecha, con acceso a las opciones principales.
- **Banner principal:** Sección visual destacada para captar la atención del usuario.

### División 2 de Index.html
![División 2](https://i.postimg.cc/FHby6Nqw/2.png)
Esta división está centrada en la presentación de las características principales del producto, organizadas de forma que el usuario pueda comprender rápidamente los beneficios clave de la aplicación.

### División 3 de Index.html
![División 3](https://i.postimg.cc/zvRWFrKt/3.png)
En esta sección se proporciona una guía para optimizar la experiencia de usuario, presentando recomendaciones claras y un diseño enfocado en la usabilidad.

### División 4 de Index.html
![División 4](https://i.postimg.cc/d0q2Pgc3/4.png)
Esta división contiene la sección "Sobre Nosotros", donde se destacan los elementos esenciales de la empresa, incluyendo misión, visión, valores y público objetivo.

### División 5 de Index.html
![División 5](https://i.postimg.cc/KYJnZQmN/5.png)
En esta sección se presentan las **Preguntas Frecuentes (FAQs)**, organizadas de forma que los usuarios puedan acceder rápidamente a respuestas a las dudas más comunes.

### División 6 de Index.html
![División 6](https://i.postimg.cc/3RN2WpRH/6.png)
La sección de "Contáctanos" incluye un formulario sencillo que permite a los usuarios comunicarse con el equipo de soporte. Los campos solicitados son:
- Nombre
- Número de teléfono
- Correo electrónico
- Mensaje

### División 7 de Index.html
![División 7](https://i.postimg.cc/ZRQpNRBv/7.png)
En la última división se presenta el footer, que incluye enlaces a las redes sociales de la Startup y los créditos correspondientes a los desarrolladores del proyecto.

### About-us.html
![About Us](https://i.postimg.cc/prC1fKvX/M-About-Us-Mobile.png)
Esta sección presenta el apartado "Sobre Nosotros" adaptado a la visualización en dispositivos móviles, manteniendo la estructura informativa sobre misión, visión, valores y público objetivo.

### Help-center.html
![FAQs](https://i.postimg.cc/mDQnr069/M-FAQs-Mobile.png)
En esta sección se reordenan las preguntas frecuentes para adaptarse al formato móvil, garantizando una lectura clara y accesible.

### Contact.html
![Contact](https://i.postimg.cc/PxGcTtKh/M-Contact-Mobile.png)
Esta sección muestra el formulario de contacto en su versión móvil, manteniendo los mismos campos que en la versión desktop pero optimizados para pantallas reducidas.

### Menú
![Menu](https://i.postimg.cc/y6y5CCR4/M-Menu-Mobile.png)
En esta sección se observa el menú desplegable en su versión móvil, manteniendo la estructura de navegación compacta y accesible para el usuario.

#### 5.1.4. Mobile Applications UX/UI Design

Em esta sección se expresa el diseño para nuestra Mobile App utilizando wireframes y mock-ups en la herramienta de Figma.

##### 5.1.4.1. Mobile Applications Wireframes

Los wireframes fueron desarrollados en el siguiente enlace:  
[Ver wireframes en Figma](https://www.figma.com/design/FqAYzDC46kVQpv46HhYI8O/Landing-Page-Build-Master?node-id=97-2&t=62SAfUKM9sGyv2vu-1)  

---

## Inicio  
![Home](https://i.postimg.cc/vB80r1cX/Home.png)  

En esta imagen podemos observar la página de inicio, que tendrá:  
- El logo y el nombre de la aplicación en el **header**.  
- El menú y nuestro usuario.  
- Una pequeña descripción de la APP.  
- Un video introductorio.  
- Un botón de **llamado a la acción** para comenzar a configurar.  

---

## Inicio de Sesión  
![Login](https://i.postimg.cc/C1vmmF80/Login.png)  

En esta imagen podemos observar el inicio de sesión que contará con un botón de acción para dirigirse a la aplicación.  

---

## Registro de Usuario  
![Sign Up](https://i.postimg.cc/bNS39fwX/Sing-Up.png)  

En esta imagen podemos observar el registro de usuario, el cual permite crear una cuenta para ingresar a la aplicación.  

---

## PC Config  
![PC Config](https://i.postimg.cc/QCwSZ0Sn/PC-Config.png)  

En esta imagen podemos observar un listado con:  
- Nombres de los productos.  
- Categoría del producto.  
- Fabricante.  
- Botones para **editar** el producto, **eliminarlo** y **añadir un producto**.  

---

## Community  
![Community](https://i.postimg.cc/kGBwHkNb/Community.png)  

En esta imagen podemos observar un listado con los comentarios de la comunidad, incluyendo:  
- Nombre del usuario.  
- Fecha del comentario.  
- Comentario principal.  
- Respuestas con fecha al comentario principal.  
- Cantidad de **likes, dislikes, comentarios y veces compartido**.  

---

## Prices  
![Prices](https://i.postimg.cc/sfNTWgy9/Prices.png)  

En esta imagen podemos observar un listado comparativo de precios, mostrando:  
- Imagen del producto.  
- Nombre del producto.  
- Precio promedio.  
- Rango de precios.  
- Fecha de la última actualización.  
- Botón para **actualizar la información**.  

##### 5.1.4.2. Mobile Applications Wireflow Diagrams

---

### User Task 1  
![User Task 1](https://i.postimg.cc/4xnz6rbC/1.png)  

- **Acción del Usuario:** El usuario accede a una cuenta previamente creada.  
- **Elementos visibles:**  
  - Título.  
  - Imagen de logo de usuario.  
  - Cuadros para introducir usuario y contraseña.  
  - Botón para **Iniciar Sesión**.  

---

### User Task 2  
![User Task 2](https://i.postimg.cc/vBwfdDRM/2.png)  

- **Acción del Usuario:** El usuario debe crear una cuenta para usar la aplicación.  
- **Elementos visibles:**  
  - Título.  
  - Imagen de logo de usuario.  
  - Cuadros para introducir nuevo usuario, contraseña y confirmación de contraseña.  
  - Botón para **Registrarse**.  

---

### User Task 3  
![User Task 3](https://i.postimg.cc/4xMpBBBY/3.png)  

- **Acción del Usuario:** El usuario interactúa con el **Home** de la aplicación, puede reproducir el video y comenzar con la configuración haciendo clic en el botón.  
- **Elementos visibles:**  
  - Logo de la app.  
  - Nombre de la app.  
  - Descripción.  
  - Video introductorio.  
  - Botón para **Empezar la Configuración**.  
  - Menú con más secciones de la aplicación.  

---

### User Task 4  
![User Task 4](https://i.postimg.cc/hGdTwT5p/4.png)  

- **Acción del Usuario:** El usuario interactúa con la sección **Comunidad** donde puede dar **like, dislike, comentar y compartir**.  
- **Elementos visibles:**  
  - Comentarios listados uno por uno.  
  - Nombre del usuario.  
  - Foto de perfil.  
  - Fecha del comentario.  
  - Comentario principal.  
  - Respuestas al comentario.  
  - Botones para **interactuar** (like, dislike, comentar, compartir).  

---

### User Task 5  
![User Task 5](https://i.postimg.cc/XJKFN335/5.png)  

- **Acción del Usuario:** El usuario interactúa con la sección **PC Config** donde puede **editar, eliminar y agregar productos**.  
- **Elementos visibles:**  
  - Productos listados uno por uno.  
  - Botones para **editar, eliminar** y **añadir producto nuevo**.  

---

### User Task 6  
![User Task 6](https://i.postimg.cc/Wz2ZhKbH/6.png)  

- **Acción del Usuario:** El usuario interactúa con la sección **Prices** donde puede ver los precios, su rango y la hora de actualización. Puede actualizar el precio de los productos con el botón **Actualizar**.  
- **Elementos visibles:**  
  - Productos listados uno por uno.  
  - Precio del producto.  
  - Rango de precios.  
  - Hora de la última actualización.  
  - Botón para **actualizar la información del producto**.

##### 5.1.4.3. Mobile Applications Mock-ups  

Los mock-ups fueron desarrollados en el siguiente enlace:  
[Ver mock-ups en Figma](https://www.figma.com/design/FqAYzDC46kVQpv46HhYI8O/Landing-Page-Build-Master?node-id=98-81&t=62SAfUKM9sGyv2vu-1)  

---

## Inicio  
![Home](https://i.postimg.cc/RZnyhnHH/Home.png)  

En este mockup podemos ver:  
- El **logo de la app** junto a su nombre.  
- El **logo de perfil del usuario**.  
- El **menú hamburguesa** en el header.  
- Una presentación de la aplicación.  
- Un video acerca del **proceso de ensamblado de un PC y sus costos**.  
- Un botón para comenzar la configuración de nuestra propia PC.  
- Secciones de la app: Home, PC Config, Chat, Store y Prices.  

---

## Login  
![Login](https://i.postimg.cc/tJSwZ3kh/Login.png)  

En este mockup se muestra la pantalla de inicio de sesión, donde se ingresa:  
- **Usuario y contraseña**.  
- Botón **Log in** para acceder a la app.  

---

## Sign Up  
![Sign Up](https://i.postimg.cc/mrYnNfVZ/Sing-Up.png)  

En esta pantalla se solicita al usuario completar:  
- Nombre de usuario.  
- Contraseña.  
- Confirmación de contraseña.  
- Botón **Sign Up** para registrarse.  

---

## PC Config  
![PC Config](https://i.postimg.cc/c1XVbWWr/Pc-Config.png)  

En este mockup se muestra una lista con:  
- Nombre del producto.  
- Categoría del producto.  
- Fabricante.  
- Íconos para **editar** y **eliminar** el producto.  
- Botón para **añadir otro producto**.  

---

## Community  
![Community](https://i.postimg.cc/65qDsP6z/Community.png)  

En este mockup se muestra la sección de comunidad, donde se puede ver:  
- **Nombre del usuario**.  
- Foto de perfil.  
- Fecha del comentario.  
- Comentario principal.  
- Respuestas con fechas.  
- **Likes, dislikes, cantidad de comentarios y veces compartido**.  

---

## Prices  
![Prices](https://i.postimg.cc/QMGPTxQn/Prices.png)  

En este mockup se muestra el comparador de precios, que incluye:  
- Nombre del producto.  
- Imagen del producto.  
- Precio promedio.  
- Rango de precios.  
- Fecha de la última actualización.  
- Botón para **actualizar la información del producto**.

##### 5.1.4.4. Mobile Applications User Flow Diagrams  

Desarrollado en Figma. Ingresar al siguiente enlace:  
[Ver User Flow Diagrams en Figma](https://www.figma.com/design/FqAYzDC46kVQpv46HhYI8O/Landing-Page-Build-Master?node-id=111-1633&t=62SAfUKM9sGyv2vu-1)  

---

### Inicio de sesión  
![Inicio de sesión](https://i.postimg.cc/XJ3SmM8q/1.png)  

- **Acción del Usuario:** El usuario introduce sus credenciales y presiona **Log In**, lo que lo redirige al **Home**.  

---

### Crear Usuario  
![Crear Usuario](https://i.postimg.cc/XqYMNwt0/2.png)  

- **Acción del Usuario:** Desde el **Login**, el usuario presiona en **Create User** para registrarse y usar la aplicación.  

---

### Creación del Usuario  
![Creación del Usuario](https://i.postimg.cc/d1BPKWHB/3.png)  

- **Acción del Usuario:** Después de registrarse correctamente, el usuario es redirigido al **Login** para introducir sus credenciales y acceder al **Home**.  

---

### Acceder a Chat (Community)  
![Acceder a Chat (Community)](https://i.postimg.cc/qqbPNNd6/4.png)  

- **Acción del Usuario:** El usuario accede a la sección **Community** para interactuar con otros usuarios de la aplicación.  

---

### Acceder a PC Config  
![Acceder a PC Config](https://i.postimg.cc/PfSs3R8f/5.png)  

- **Acción del Usuario:** El usuario accede a **PC Config** para **agregar, editar o eliminar productos**.  

---

### Acceder a Prices  
![Acceder a Prices](https://i.postimg.cc/02rgL0pY/6.png)  

- **Acción del Usuario:** El usuario accede a **Prices** para ver los **precios actualizados** y sus **rango de precios**.  

##### 5.1.4.5. Mobile Applications Prototyping  

![Prototype](https://i.postimg.cc/7hLDWMZR/proto.png)  

En el siguiente video se muestran los **flujos o caminos que tomará el usuario** al usar la aplicación:  
https://upcedupe-my.sharepoint.com/:v:/g/personal/u202513698_upc_edu_pe/EXTE-vqTQhVNo8BayLhvX_kBrjdWvlN7uLvm9v6ZP8VmPQ?e=CDDjTc&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D
