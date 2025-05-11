## Capítulo VI: Product Implementation, Validation & Deployment
### 6.1. Software Configuration Management.
#### 6.1.1. Software Development Environment Configuration.
#### 6.1.2. Source Code Management.
#### 6.1.3. Source Code Style Guide & Conventions.
#### 6.1.4. Software Deployment Configuration.
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
            <td> Esta tarea se enfoca en desarrollar la sección interna de la aplicación web que permite al usuario registrarse. </td>
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
            <td> Esta tarea se enfoca en desarrollar la sección interna de la aplicación web que permite al usuario iniciar sesión con un token. </td>
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
            <td> Esta tarea se enfoca en desarrollar la característica que permite usar filtros para seleccionar componentes en la aplicación web </td>
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
            <td> Esta tarea se enfoca en desarrollar la característica que permite usar filtros para seleccionar componentes en la aplicación web </td>
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

TODO: *Imagen del board*
Anexo #

##### 6.2.1.3. Development Evidence for Sprint Review.
##### 6.2.1.4. Execution Evidence for Sprint Review.
##### 6.2.1.5. Services Documentation Evidence for Sprint Review.
##### 6.2.1.6. Software Deployment Evidence for Sprint Review.
##### 6.2.1.7. Team Collaboration Insights during Sprint.

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