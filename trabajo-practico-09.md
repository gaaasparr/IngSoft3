4.1 Modificar nuestro pipeline para incluir el deploy en QA y PROD de Imagenes Docker en Servicio Azure App Services con Soporte para Contenedores
Desarrollo del punto 4.1:

4.1.1 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción y Pruebas y de la etapa de Construcción de Imagenes Docker y subida a ACR realizada en el TP08
Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back utilizando un AppServicePlan en Linux

![image](https://github.com/user-attachments/assets/7e8bfc1a-5965-4a8e-aedb-ccf172110c3e)

![image](https://github.com/user-attachments/assets/9061268d-17b5-4338-8cd2-20cf76393780)

![image](https://github.com/user-attachments/assets/196e04ec-8ab0-4c73-bae5-ca9d640e17d2)

![image](https://github.com/user-attachments/assets/ec2a0490-e1f8-4cf3-b5d1-f504b1ba22ff)

Chequeamos que este todo funcionando

![image](https://github.com/user-attachments/assets/58b116c0-97d3-4db5-8bf3-7a7e16794176)

            
4.2 Desafíos:

4.2.1 Agregar tareas para generar Front en Azure App Service con Soporte para Contenedores

![image](https://github.com/user-attachments/assets/8b7e3ebe-25a8-4aae-818a-4591eeb6b247)

![image](https://github.com/user-attachments/assets/9009ddf0-83db-44e0-8383-1085bbe43c12)

![image](https://github.com/user-attachments/assets/cee56082-a6d3-4ebe-9ba0-78aff335e4dd)


4.2.2 Agregar variables necesarias para el funcionamiento de la nueva etapa considerando que debe haber 2 entornos QA y PROD para Back y Front.



4.2.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en Azure App Services con Soporte para Contenedores.



4.2.4 Agregar etapa que dependa de la etapa de Deploy en QA que genere un entorno de PROD.



4.2.5 Entregar un pipeline que incluya:

A) Etapa Construcción y Pruebas Unitarias y Code Coverage Back y Front

B) Construcción de Imágenes Docker y subida a ACR

C) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps

D) Deploy Back y Front en QA con pruebas de integración para ACI

E) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps con Soporte para contenedores

F) Aprobación manual de QA para los puntos C,D,E

G) Deploy Back y Front en PROD para Azure Web Apps

H) Deploy Back y Front en PROD para ACI

I) Deploy Back y Front en PROD para Azure Web Apps con Soporte para contenedores
