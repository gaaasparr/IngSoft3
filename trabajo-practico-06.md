![image](https://github.com/user-attachments/assets/3e309940-512f-47a9-801f-f020bca4fea8)
4- Desarrollo:
Prerequisitos:
4.1 Agregar Code Coverage a nuestras pruebas unitarias de backend y front-end e integrarlas junto con sus resultados en nuestro pipeline de build.
Desarrollo del punto 4.1:

![image](https://github.com/user-attachments/assets/3e309940-512f-47a9-801f-f020bca4fea8)

4.1.3 En el dir raiz del proyecto EmployeeCrudApi.Tests ejecutar:
dotnet add package coverlet.collector
4.1.4 Agregar a nuestro pipeline ANTES del Build de Back la tarea de test con los argumentos especificados y la de publicación de resultados de cobertura:

4.1.5 Agregar a nuestro pipeline ANTES del Build de front la tarea de test y la de publicación de los resultados.

4.1.6 Ejecutar el pipeline y analizar el resultado de las pruebas unitarias y la cobertura de código.

4.2 Agregar Análisis Estático de Código con SonarCloud:
SonarCloud https://www.sonarsource.com/products/sonarcloud/ es una plataforma de análisis de calidad de código basada en la nube que ayuda a los equipos de desarrollo a detectar errores, vulnerabilidades de seguridad, malas prácticas y problemas de mantenibilidad en el código. Proporciona análisis estático de código para múltiples lenguajes, como Java, .NET, JavaScript, TypeScript, Python, y más, ofreciendo métricas detalladas sobre la cobertura de pruebas, duplicación de código, complejidad ciclomatica, y deuda técnica. Además, SonarCloud se integra fácilmente con sistemas de CI/CD y plataformas de control de versiones como GitHub, Azure DevOps y Bitbucket, lo que permite un análisis continuo del código en cada commit o despliegue.

La plataforma destaca por ofrecer un tablero interactivo donde se pueden visualizar y priorizar los problemas detectados, facilitando la refactorización y la mejora de la calidad del código. SonarCloud permite a los equipos identificar vulnerabilidades y puntos críticos de seguridad, además de generar informes de cobertura de pruebas automatizadas, ayudando a mantener el código limpio, seguro y fácil de mantener a lo largo del ciclo de vida del desarrollo.

Resumen de Métricas de Calidad de Código en SonarCloud
Coverage (Cobertura de Código): Mide el porcentaje de código cubierto por pruebas automatizadas.
Bugs (Errores): Identifica problemas que podrían causar fallos en el código en tiempo de ejecución.
Vulnerabilities (Vulnerabilidades): Detecta posibles puntos de riesgo que podrían comprometer la seguridad del código.
Code Smells: Indica malas prácticas o patrones de código que, aunque no causan fallos, afectan la calidad y mantenibilidad.
Duplications (Duplicación de Código): Mide el porcentaje de código duplicado en el proyecto, lo que afecta la mantenibilidad.
Maintainability (Mantenibilidad): Evalúa la facilidad con la que el código puede ser modificado o extendido sin introducir nuevos errores.
Technical Debt (Deuda Técnica): Estima el tiempo necesario para corregir todos los problemas de calidad del código.
Reliability (Fiabilidad): Mide la probabilidad de que el código funcione sin errores.
Security Hotspots (Puntos Críticos de Seguridad): Indica áreas del código que deben ser revisadas manualmente por posibles problemas de seguridad.
Cyclomatic Complexity (Complejidad Ciclomática): Mide el número de caminos lógicos independientes en el código, indicando su complejidad estructural.
Cognitive Complexity (Complejidad Cognitiva): Evalúa la dificultad de entender el código, considerando aspectos de legibilidad y comprensión.
Maintainability Rating: Clasifica el proyecto en una escala de A a E según la deuda técnica y la facilidad de mantenimiento.
Branch Coverage: Mide la cobertura de las ramas de decisión en el código (por ejemplo, en estructuras if, else o switch).
Complexity per Function: Mide la complejidad promedio de las funciones dentro del proyecto.
Complexity per Class: Mide la complejidad promedio por clase, ayudando a evaluar la arquitectura y el diseño del sistema.
Lines of Code (LoC): Cuenta el número total de líneas de código en el proyecto, excluyendo comentarios y espacios en blanco.
Comment Density (Densidad de Comentarios): Mide el porcentaje de líneas de código que son comentarios, útil para evaluar la documentación interna.
Issues (Problemas): Cuenta el número total de problemas detectados en el código, que pueden clasificarse como bugs, vulnerabilidades o code smells.
Security Rating: Proporciona una clasificación general de la seguridad del código, en una escala de A (mejor) a E (peor).
Reliability Rating: Clasifica la confiabilidad del código en una escala de A a E, basada en la cantidad y gravedad de los errores detectados.
Security Remediation Effort: Estima el tiempo necesario para resolver todos los problemas de seguridad identificados en el código.
Uncovered Conditions: Mide el número de condiciones lógicas que no están cubiertas por las pruebas automatizadas.
Duplicated Blocks: Cuenta los bloques de código que se repiten en el proyecto.
Unresolved Issues: Indica el número de problemas detectados que aún no han sido resueltos.
Desarrollo del punto 4.2: Demostración de cómo integrar SonarCloud en un pipeline de CI/CD y cómo leer los reportes de análisis estático.

4.2.1 Integraremos SonarCloud para analizar el código fuente. Configurar SonarCloud en nuestro pipeline siguiendo instructivo 5.1
Antes de nuestra tarea de Build del Back:

    
    - task: SonarCloudPrepare@2
      inputs:
        SonarCloud: 'SonarCloud' #Nombre de nuestra Service Connection a SonarCloud
        organization: 'ingsoft3ucc'  #Nombre de nuestra organizacion SonarCloud
        scannerMode: 'MSBuild'
        projectKey: 'Angular_WebAPINetCore8_CRUD_Sample'  #Key de nuestro proyecto en SonarCloud
        projectName: 'Angular_WebAPINetCore8_CRUD_Sample' #Nombre de nuestro proyecto en SonarCloud
      displayName: 'Prepare SonarCloud'
    
Despues de nuestra tarea de Build del Back:

  - task: SonarCloudAnalyze@2
    inputs:
      jdkversion: 'JAVA_HOME_17_X64'
    displayName: 'Analyze SonarCloud'
   
 - task: SonarCloudPublish@2
   displayName: 'Publish SonarCloud'
   inputs:
     pollingTimeoutSec: '300'
4.2.2 Vemos el resultado de nuestro pipeline, en extensions tenemos un link al análisis realizado por SonarCloud
image

4.2.3 Ir al link y analizar toda la información obtenida. Detallar en la entrega del TP los puntos más relevantes del informe, qué significan y para qué sirven.
image

4.3 Pruebas de Integración con Cypress:
Cypress https://www.cypress.io/ es una herramienta de pruebas tanto de integración como unitarias diseñada para probar aplicaciones web. Facilita la escritura, ejecución y depuración de pruebas automáticas en tiempo real dentro del navegador. A diferencia de otras herramientas de pruebas, Cypress se ejecuta directamente en el navegador, lo que le permite interactuar con la página web de manera más eficiente, proporcionando feedback rápido y detallado sobre las pruebas.

Características clave de Cypress:
Pruebas en tiempo real: Ver los resultados de las pruebas en el navegador mientras se ejecutan.
Automatización completa del navegador: Cypress controla el navegador para simular la interacción del usuario.
Rápida retroalimentación: Ideal para desarrollo ágil con integración continua.
Depuración sencilla: Acceso a capturas de pantalla y videos de las pruebas fallidas.
