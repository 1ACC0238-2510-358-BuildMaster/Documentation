## Capítulo VI: Product Implementation, Validation & Deployment
### 6.1. Software Configuration Management

En esta sección se detallan las decisiones, convenciones y configuraciones adoptadas para mantener la consistencia del desarrollo de software durante todo el ciclo de vida del proyecto. Las subsecciones cubren la configuración del entorno de desarrollo, el control de versiones del código fuente, las convenciones de codificación y la configuración de despliegue de los productos digitales.


#### 6.1.1. Software Development Environment Configuration.
| Herramienta / Producto | Propósito | Tipo | Enlace de Referencia |
|------------------------|----------|------|----------------------|
| GitHub | Gestión del código fuente | SaaS | [https://github.com/](https://github.com/) |
| IntelliJ IDEA Ultimate | Backend (Web Services con Spring Boot) | Local | [https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/) |
| Android Studio | Desarrollo de Aplicación Móvil (Frontend) | Local | [https://developer.android.com/studio](https://developer.android.com/studio) |
| PostgreSQL + PgAdmin | Base de datos relacional | Local | [https://www.pgadmin.org/](https://www.pgadmin.org/) |
| Visual Studio Code |Editor de código para documentación y landing page |Local (o SaaS con extensión GitHub Codespaces)|[https://code.visualstudio.com/](https://code.visualstudio.com/)|
| Figma | Diseño UX/UI de la solución | SaaS | [https://www.figma.com/](https://www.figma.com/) |
| Trello | Gestión del proyecto y backlog | SaaS | [https://trello.com/](https://trello.com/) |
| Postman | Pruebas de endpoints de la API | Local | [https://www.postman.com/](https://www.postman.com/) |
| Swagger UI | Documentación y prueba de API REST | Local | [https://swagger.io/](https://swagger.io/) |

**Repositorios GitHub:**
- Web Services (Backend):https://github.com/1ACC0238-2510-358-BuildMaster/Backend
- Mobile App (Frontend):https://github.com/1ACC0238-2510-358-BuildMaster/BuildMasterApp

**GitFlow Strategy Adoptada:**
- `main`: Rama principal de producción.
- `develop`: Rama de integración para desarrollo.
- `feature/*`: Ramas por cada nueva funcionalidad. Ejemplo: `feature/component-creation`.
- `release/*`: Ramas para preparación de releases. Ejemplo: `release/v1.0.0`.
- `hotfix/*`: Ramas para solucionar errores en producción. Ejemplo: `hotfix/login-crash`.

**Semantic Versioning:**
- Se utilizará el formato `MAJOR.MINOR.PATCH`. Ejemplo: `v1.0.0`, `v1.1.0`, `v1.1.1`.

**Conventional Commits:**
- `feat:` para nuevas funcionalidades.
- `fix:` para correcciones de bugs.
- `docs:` para documentación.
- `style:` para cambios de estilo (espacios, formatos, etc.).
- `refactor:` para cambios internos que no modifican funcionalidad.
- `test:` para agregar o actualizar pruebas.
- `chore:` para mantenimiento general.

#### 6.1.2. Source Code Management.

- Todos los miembros deben usar Git con GitHub como repositorio remoto.
- Cada tarea del backlog se realiza en una rama `feature/`, vinculada a su User Story.
- Las ramas se integran a `develop` mediante Pull Requests, luego de una revisión de código.
- Las versiones finales se fusionan de `develop` a `main` al completar una release.
- Se usarán etiquetas (`tags`) para identificar cada versión estable.

#### 6.1.3. Source Code Style Guide & Conventions.

| Lenguaje / Framework | Convención Adoptada |
|----------------------|----------------------|
| Java / Spring Boot | [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) |
| Kotlin | [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html) |
| HTML / CSS | [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html) |
| TypeScript | [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html) |
| Gherkin | [Gherkin Syntax](https://cucumber.io/docs/gherkin/reference/) |

**Buenas Prácticas:**
- Todo el código debe estar comentado en inglés.
- Se deben usar nombres claros, semánticos y consistentes para variables y métodos.
- Seguir arquitectura limpia en backend y separación de capas en frontend.
- Usar linters y formateadores en ambos entornos.

#### 6.1.4. Software Deployment Configuration.

**Backend (Spring Boot):**
- Construcción con Gradle Kotlin DSL.
- Base de datos PostgreSQL, configurada en `application.properties`.
- Ejecutar con `./gradlew bootRun`.

**Aplicación Móvil (Android):**
- Proyecto Android con Kotlin + Jetpack Compose.
- API base: `http://10.0.2.2:8090/api/v1/` (para emulador Android Studio).

##### Despliegue Local

**Pasos:**
1. Iniciar PostgreSQL local con una base de datos llamada `buildmaster`.
2. Ejecutar el backend con `./gradlew bootRun`.
3. Probar la API REST desde Swagger UI (`http://localhost:8090/swagger-ui/index.html`) o Postman.
4. Ejecutar la aplicación móvil en un emulador desde Android Studio.

---

##### Despliegue para Sprint 1 (Remoto)

| Producto | Plataforma | URL | Comentarios |
|----------|------------|-----|-------------|
| **Landing Page** | GitHub Pages | https://1acc0238-2510-358-buildmaster.github.io/buildmaster-landing/` | Página estática generada con HTML/CSS |
| **Backend (API REST)** | Firebase Hosting + Cloud Functions (Temporal) | `https://buildmaster-backend.firebaseapp.com/` | Adaptado para ejecutarse como función en Firebase |
| **Frontend Móvil** | Firebase Hosting (APK o WebView) | `https://buildmaster-app.firebaseapp.com/` | Para fines de validación rápida, podría usarse web móvil o APK descargable desde Firebase Hosting |

**Consideraciones:**
- La Landing Page se encuentra en un repositorio independiente y usa GitHub Pages para despliegue automático desde la rama `main`.
- El Backend fue empaquetado como un proyecto de función y adaptado para ser desplegado en Firebase Functions con endpoints compatibles REST.
- El Frontend móvil fue compilado y exportado para alojarse temporalmente como APK o WebApp en Firebase Hosting, lo que permite validaciones sin necesidad de publicar en Play Store.

Diagrama de despliegue para versión final: 

[![structurizr-101464-Container-001.png](https://i.postimg.cc/W30H2Qn0/structurizr-101464-Container-001.png)](https://postimg.cc/phXZCc3d)

### 6.2. Landing Page, Services & Applications Implementation.
#### 6.2.1. Sprint 1
#### 6.2.1.1. Sprint Planning 1.

| **Aspecto**                      | **Detalles**                                                                                                           |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **Sprint Planning Background**   |                                                                                                                        |
| **Date**                         | 8/05/2025                                                                                                             |
| **Time**                         | 4:00 pm                                                                                                                |
| **Location**                     | La reunión se realizó de forma virtual por la plataforma Discord                                                        |
| **Prepared By**                  | NovaPeak                                                                                                              |
| **Attendees (to planning meeting)** | Casaverde De La Cruz, Ernesto David / Cantoral Sedamano, Alexander Alberto / Romero Qwistgaard, Russell Stephen / Machuca García, Celso Eduardo |
| **Sprint n – 1 Review Summary**  | Antes de este sprint se lograron avances significativos en la creación de la estructura de la Landing Page y mobile app, incluyendo la definición de los elementos visuales clave y la arquitectura del sitio. Se identificaron mejoras que serán implementadas en futuros sprints                           |
| **Sprint n – 1 Retrospective Summary** | En el sprint anterior, los miembros del equipo destacaron la importancia de mantener una comunicación clara y efectiva. Se resaltó el buen flujo de trabajo, pero se sugirió dedicar más tiempo a la revisión de cada módulo antes de integrarlo para evitar posibles problemas en la fase de desarrollo posterior. |
| **Sprint Goal & User Stories**   |         **Our focus is on** *completar el desarrollo de la Landing Page y version protitpo de la mobile app.* **We believe it delivers** *un impacto significativo en la presentación inicial del producto*  **to**  *usuarios potenciales, mejorando la experiencia de descubrimiento y generando interés en nuestros servicios.* **This will be confirmed when** *la página esté completamente funcional y recibamos retroalimentación positiva de los usuarios durante las primeras pruebas de usabilidad.*                                                             |
| **Sprint 1 Goal**                | Terminar de desarrollar la Landing Page y propocionar una primera version de la mobile app|
| **Sprint 1 Velocity**            | Velocidad estimada de 35 puntos. La velocidad del equipo se calculó considerando la capacidad del equipo y los puntos de historia completados en sprints anteriores.                                                                             |
| **Sum of Story Points**          | Se asignaron  puntos de historia a las tareas completadas, lo que refleja el trabajo realizado sobre la Landing Page y para el frontend y backend de la aplicación móvil.|

##### 6.2.1.2. Sprint Backlog 1.


El objetivo principal de este Sprint es concretar el desarrollo de una primera versión de la landing page, 
<table>
    <thead>
        <tr>
            <td>Sprint #</td>
            <td colspan="7" >Sprint 1</td>
        </tr>
        <tr>
            <td colspan="2" > User Story</td>
            <td colspan="6" > Work-Item / Task </td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td> Id </td>
            <td> Title </td>
            <td> Id </td>
            <td> Title </td>
            <td> Description </td>
            <td> Estimation (Hours) </td>
            <td> Assigned To </td>
            <td> Status (To-do / In-Process / To-Review / Done) </td>
        </tr>
          <!-- Fila de separación para User Story 1 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US01</td>
        </tr>
        <tr>
            <td> US01 </td>
          	<td> Página de Inicio </td>
          	<td> 01 </td>
          	<td> Inicio del desarrollo de la Landing Page </td>
            <td> Esta tarea marca el inicio del desarrollo de la Landing Page relacionada con nuestro producto final. </td>
            <td> 02 </td>
            <td> Machuca García, Celso Eduardo </td>
            <td> Done  </td>
        </tr>
          <!-- Fila de separación para User Story 2 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US02</td>
        </tr>
        <tr>
            <td> US02 </td>
          	<td> Pestaña“Sobre” </td>
          	<td> 02 </td>
          	<td> Desarrollo de sencción "Sobre" en la Landing Page </td>
            <td> Esta tarea se centra en el desarrollo de la sección interna "Sobre" de nuestra Landing Page, donde se proporciona información detallada sobre el proyecto </td>
            <td> 02 </td>
            <td> Machuca García, Celso Eduardo </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 3 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US03</td>
        </tr>
        <tr>
            <td> US03 </td>
          	<td> Pestaña “Contacto”</td>
          	<td> 03 </td>
          	<td> Desarrollo de la sección "Contacto" </td>
            <td> Esta tarea se enfoca en el desarrollo de la sección "Contacto", que proporciona información detallada sobre cómo ponerse en contacto con los responsables del proyecto. </td>
            <td> 02 </td>
            <td> Machuca García, Celso Eduardo </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 4 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US04</td>
        </tr>
        <tr>
            <td> US04 </td>
          	<td> Pestaña de ayuda al usuario </td>
          	<td> 04 </td>
          	<td> Desarrollo de la sección ayuda al usuario </td>
            <td> Esta tarea se enfoca en desarrollar la sección interna de la Landing Page que proporciona información relevante y útil para los usuarios que puedan tener dudas sobre el proyecto. </td>
            <td> 02 </td>
            <td> Machuca García, Celso Eduardo </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 5 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US05</td>
        </tr>
        <tr>
            <td> US05 </td>
          	<td> Registro de nuevo usuario </td>
          	<td> 05 </td>
          	<td> Desarrollo de la sección de registro para el usuario </td>
            <td> Esta tarea se enfoca en desarrollar la sección interna de la aplicación móvil que permite al usuario registrarse. </td>
            <td> 02 </td>
            <td> Romero Qwistgaard, Russell Stephen </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 6 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US06</td>
        </tr>
        <tr>
            <td> US06 </td>
          	<td> Iniciar sesión en la aplicación móvil </td>
          	<td> 06 </td>
          	<td> Desarrollo del inicio de sesisón para el usuario </td>
            <td> Esta tarea se enfoca en desarrollar la sección interna de la aplicación móvil que permite al usuario iniciar sesión con un token. </td>
            <td> 03 </td>
            <td> Romero Qwistgaard, Russell Stephen </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 14 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US14</td>
        </tr>
        <tr>
            <td> US14 </td>
          	<td> Buscar componentes </td>
          	<td> 14 </td>
          	<td> Desarrollo de la búsqueda de componente </td>
            <td> Esta tarea se enfoca en desarrollar las funciones internas que permiten buscar componentes para los usuarios clientes y sistema crud para los tipo administrador </td>
            <td> 03 </td>
            <td> Cantoral Sedamano, Alexander Alberto </td>
            <td> Done </td>
        </tr>
          <!-- Fila de separación para User Story 15 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US15</td>
        </tr>
        <tr>
            <td> US15 </td>
          	<td> Filtrar por categoría  </td>
          	<td> 15 </td>
          	<td> Desarrollo del filtro de categoría </td>
            <td> Esta tarea se enfoca en desarrollar la característica que permite usar filtros para seleccionar componentes en la aplicación móvil </td>
            <td> 02 </td>
            <td> Cantoral Sedamano, Alexander Alberto </td>
            <td> Done </td>
        </tr>
         <!-- Fila de separación para User Story 16 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US16</td>
        </tr>
        <tr>
            <td> US16 </td>
          	<td> Ver detalles de un componente  </td>
          	<td> 16 </td>
          	<td> Visualización de detalles del componente </td>
            <td> Esta tarea se enfoca en desarrollar la característica que permite usar filtros para seleccionar componentes en la aplicación móvil </td>
            <td> 02 </td>
            <td> Cantoral Sedamano, Alexander Alberto </td>
            <td> Done </td>
        </tr>
        <!-- Fila de separación para User Story 22 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US22</td>
        </tr>
        <tr>
            <td> US22 </td>
          	<td> Ver builds populares </td>
          	<td> 22 </td>
          	<td> Desarrollo de visualización de builds </td>
            <td> Esta tarea se enfoca en desarrollar la característica que permite ver en un apartado las builds populares en la aplicación </td>
            <td> 03 </td>
            <td> Casaverde De La Cruz, Ernesto David </td>
            <td> Done </td>
        </tr>
        <!-- Fila de separación para User Story 23 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for US23</td>
        </tr>
        <tr>
            <td> US23 </td>
          	<td> Calificar una build </td>
          	<td> 23 </td>
          	<td> Desarrollo de visualización de builds </td>
            <td> Esta tarea se enfoca en desarrollar la característica que permite calificar la builds mostradas en la sección de feed </td>
            <td> 02 </td>
            <td> Casaverde De La Cruz, Ernesto David </td>
            <td> Done </td>
        </tr>
         <!-- Fila de separación para Technical Story 1 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for TS01</td>
        </tr>
        <tr>
            <td> TS01 </td>
          	<td> Autenticación de usuarios </td>
          	<td> 27 </td>
          	<td> Desarrollo de IAM </td>
            <td> Esta tarea se enfoca en desarrollar el bounded context de IAM en el backend </td>
            <td> 02 </td>
            <td> Romero Qwistgaard, Russell Stephen </td>
            <td> Done </td>
        </tr>
        <!-- Fila de separación para Technical Story 3 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for TS03</td>
        </tr>
        <tr>
            <td> TS03 </td>
          	<td> Catálogo de componentes </td>
          	<td> 29 </td>
          	<td> Desarrollo de Catalogo </td>
            <td> Esta tarea se enfoca en desarrollar el bounded context de catalogo que permite usar a los componentes en el frontend y backend </td>
            <td> 03 </td>
            <td> Cantoral Sedamano, Alexander Alberto </td>
            <td> Done </td>
        </tr>
        <!-- Fila de separación para Technical Story 4 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for TS04</td>
        </tr>
        <tr>
            <td> TS04 </td>
          	<td> Búsqueda y filtros de componentes </td>
          	<td> 30 </td>
          	<td> Desarrollo de Filtros para Catalogo </td>
            <td> Esta tarea se enfoca en desarrollar el bounded context de catalogo que permite usar a los filtros de busqueda para buscar componentes</td>
            <td> 01 </td>
            <td> Cantoral Sedamano, Alexander Alberto </td>
            <td> Done </td>
        </tr>
        <!-- Fila de separación para Technical Story 7 -->
        <tr>
            <td colspan="8" style="text-align: center; background-color: #e0e0e0;">Work-Item / Task for TS07</td>
        </tr>
        <tr>
            <td> TS07 </td>
          	<td> Publicación de builds a comunidad </td>
          	<td> 34 </td>
          	<td> Desarrollo de Comunidad</td>
            <td> Esta tarea se enfoca en desarrollar el bounded context de comunidad que permite ver y publicar builds en el feed de los usuarios</td>
            <td> 03 </td>
            <td> Casaverde De La Cruz, Ernesto David </td>
            <td> Done </td>
        </tr>
    </tbody>
</table>


Link del board: https://trello.com/invite/b/681e3d7c63957fd64e2ce209/ATTI06f69cb3073c26dc6331093ca0ca15adA2FE2ACF/1acc0238-2510-358-buildmaster

##### 6.2.1.3. Development Evidence for Sprint Review.

En estos commits se puede observar los últimos updates y merge a la rama main que se hizo en el repositorio de la Landing Page, Frontend y Backend.

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Commited on (Date) |
|------------|--------|-----------|----------------|---------------------|--------------------|
| Landing Page | main | b442176fa7d5b8e54d45d7621ccaebe7648d5f45| Primera versión de la landing page| |09/05/2025|
| Landing Page | main | 3ce6d8568e8f2d3c522230d84a75a607f89a55a3| Correción pie de página| |13/05/2025|
| Landing Page | main | 254b730aac3eb012ee11d3063aaef18ef371fa92| Corrección| |13/05/2025|

Repositorio LP: https://github.com/1ACC0238-2510-358-BuildMaster/buildmaster-landing


| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Commited on (Date) |
|------------|--------|-----------|----------------|---------------------|--------------------|
| Backend | catalogue | 5a4abe7be73fbc8f24da943ac189491ff434ce93| feat | Added create component |10/05/2025|
| Frontend | catalogue | cadc6dbed9728d8b8413bfa87c3e0248db93f3ca |feat | Front and Back connected on local| |10/05/2025|
|  | catalogue |01dba4387481dc24c02fbdcc01c835a5d99df846|feat | provider bounded context finally|12/05/2025|
| Backend | dev |c54e723bd8ee4892c52757315d29770a94a344fc|Fix| Una sola navegacion|13/05/2025|
| Frontend | dev |7442dd2b876188787ecad7ed2e30b65b17bf8c47|feat|Bounded Context Comunity Finally|13/05/2025|

Repositorio backend: https://github.com/1ACC0238-2510-358-BuildMaster/BuildMasterApp


##### 6.2.1.4. Execution Evidence for Sprint Review.

En esta sección se evidenciará lo desarrollado para el sprint y se adjuntará pruebas. 

Vídeo con la ejecución de lp y front: 
https://upcedupe-my.sharepoint.com/:v:/g/personal/u20181b152_upc_edu_pe/EbIxWMbIqOFNtY2mL4kNORIBAdMv51lqnU2bjKoz0h-Bqw?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=uSe3i0


##### 6.2.1.5. Services Documentation Evidence for Sprint Review.

En esta sección se evidenciará los endpoints del backend de la aplicación móvil

Vídeo de evidencia de los endpoints:

https://upcedupe-my.sharepoint.com/:v:/g/personal/u20181b152_upc_edu_pe/EUHsfSElsUZEgI-oiHfND_MBZ5JmZU_QqSNrz9_4DeQPXA?e=udzs06&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D



##### 6.2.1.6. Software Deployment Evidence for Sprint Review.

Para el despliegue de este sprint solo se hizo deploy de la Landing Page y Bakend

Para el despliegue de la Landing Pages se usó la caracterísitica de githubpages. La cual facilita bastante el proceso, además de ello de gozar de una buena velocidad, es gratuita y el único costo sería no poder escoger el dominio pero lo hace ídoneo para startups.

[![Landing-Page.png](https://i.postimg.cc/prDVKj3b/Landing-Page.png)](https://postimg.cc/GTm1C4cq)

Para el despliegue del backend se uso render. Una herramienta que nos permite el despliegue de tanto la base de datos

[![render.png](https://i.postimg.cc/rmgsHxQ1/render.png)](https://postimg.cc/xJJ9JJr8)

[![render2.png](https://i.postimg.cc/yx4jfJYy/render2.png)](https://postimg.cc/47PpyxcY)

Para ello se requiere que tanto la base de datos como el programa hecho con springboot se tengan en los servidores de render, no tengan errores y esten conectados. Su único punto bajo es que los servidores con mejor conexión para nosotros sea los de Estados Unidos.

[![back.png](https://i.postimg.cc/hP3zgkTH/back.png)](https://postimg.cc/zVKXFPdj)
[![back-2.png](https://i.postimg.cc/1X8SKjXq/back-2.png)](https://postimg.cc/n9fNFTvF)

Link de deploy de LP: https://1acc0238-2510-358-buildmaster.github.io/buildmaster-landing/
Link de deploy del backend: https://backend-041m.onrender.com/swagger-ui/index.html#/

##### 6.2.1.7. Team Collaboration Insights during Sprint
En está sección se presentará los insights en los repositorios durante que se tuvieron durante el sprint

 - Repositorio de la Landing Page: https://github.com/1ACC0238-2510-358-BuildMaster/buildmaster-landing

 [![lp.png](https://i.postimg.cc/SQt4TkWY/lp.png)](https://postimg.cc/qgnWgfDp)

 [![lp-2.png](https://i.postimg.cc/1tCkjrN1/lp-2.png)](https://postimg.cc/Q97YB5bf)


- Repositorio de la mobile app: https://github.com/1ACC0238-2510-358-BuildMaster/BuildMasterApp/tree/dev

[![front1.png](https://i.postimg.cc/d08d65pD/front1.png)](https://postimg.cc/06yb208q)

[![front-2.png](https://i.postimg.cc/JzXB7T1K/front-2.png)](https://postimg.cc/K1ZYJD3g)

- Repositorio del backend: https://github.com/1ACC0238-2510-358-BuildMaster/Backend

[![Back-1.png](https://i.postimg.cc/JnCwVzpP/Back-1.png)](https://postimg.cc/HJzvbdDy)

[![back-2.png](https://i.postimg.cc/mgPKPHqm/back-2.png)](https://postimg.cc/xXS67c9m)

## Conclusiones


## Video About-the-team

## Bibliografía

- TechTarget. (s.f.). How to choose the right PC for business. SearchEnterpriseDesktop. Recuperado el 20 de abril de 2025, de https://www.techtarget.com/searchenterprisedesktop/tip/How-to-choose-the-right-PC-for-business

- ZDNet. (s.f.). How to choose the right PC: Everything you need to know about picking the right computer for work. Recuperado el 20 de abril de 2025, de https://www.zdnet.com/article/how-to-chose-the-right-pc-everything-you-need-to-know-about-picking-the-right-computer-for-work/

- Shapiro, J. (s.f.). Top 7 things to consider when buying a new computer to avoid disappointment. LinkedIn. Recuperado el 20 de abril de 2025, de https://www.linkedin.com/pulse/top-7-things-consider-when-buying-new-computer-avoid-

- Kingston Technology. (s.f.). Top 10 PC build mistakes beginners make. Recuperado el 20 de abril de 2025, de https://www.kingston.com/en/blog/gaming/top-10-pc-build-mistakes-beginners-make

- Justice IT Consulting. (s.f.). Justice IT Consulting. Recuperado el 20 de abril de 2025, de http://www.justiceitc.com/?trk=article-ssr-frontend-pulse_little-text-block

## Anexos

- To-be Scenario Mapping: https://miro.com/app/board/uXjVIE_P0Bw=/?share_link_id=102963333287 

- Video de Exposición del TP: 