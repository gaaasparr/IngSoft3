4.1.1 Crear archivos DockerFile para nuestros proyectos de Back y Front

![image](https://github.com/user-attachments/assets/45a83199-0346-4c0c-ac49-468658230b31)


4.1.2 Crear un recurso ACR en Azure Portal siguiendo el instructivo 5.1

![image](https://github.com/user-attachments/assets/ea905c1b-4f50-486b-853b-454ecfc0670a)


4.1.3 Modificar nuestro pipeline en la etapa de Build y Test

![image](https://github.com/user-attachments/assets/f198c68b-dc39-4b7b-924a-826f44e420af)

![image](https://github.com/user-attachments/assets/bd899164-2620-4cc5-bd82-bfacad90089d)

4.1.4 En caso de no contar en nuestro proyecto con una ServiceConnection a Azure Portal para el manejo de recursos, agregar una service connection a Azure Resource Manager como se indica en instructivo 5.2

![image](https://github.com/user-attachments/assets/5db5901f-e1c6-4475-9aae-45cbfaa44d7b)

4.1.5 Agregar a nuestro pipeline variables

![image](https://github.com/user-attachments/assets/46b365dc-d667-4cfe-9fb1-54b083db7bdc)

4.1.6 Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Build y Test

![image](https://github.com/user-attachments/assets/6c0f6a24-5013-41c3-8396-c7ea1f0e8b92)

4.1.7 - Ejecutar el pipeline y en Azure Portal acceder a la opción Repositorios de nuestro recurso Azure Container Registry. Verificar que exista una imagen con el nombre especificado en la variable backImageName asignada en nuestro pipeline

![image](https://github.com/user-attachments/assets/ea79c97c-994a-4795-a08c-936f3b3970ee)


4.1.10 - Ejecutar el pipeline de nuevo y podemos ver los nuevos resultados

tuve un problema con el path api, pero descubri que noestaba descomprimiendo el archivo y por eso no encontraba a /api, entonces agregué una task

- task: ExtractFiles@1
  displayName: 'Descomprimir API en carpeta api'
  inputs:
    archiveFilePatterns: '$(Pipeline.Workspace)/drop-back/EmployeeCrudApi.zip'
    destinationFolder: '$(Pipeline.Workspace)/drop-back/api'

Y el resultado fue:

![image](https://github.com/user-attachments/assets/3fee5a9b-7eab-4772-afdd-b0c5b9f9a625)

![image](https://github.com/user-attachments/assets/acddbe31-baca-4f74-86a8-b2b7481a8be0)

4.1.8 - Agregar tareas para generar imagen Docker de Front (DESAFIO)
A la etapa creada en 4.1.6 Agregar tareas para generar imagen Docker de Front

![image](https://github.com/user-attachments/assets/75fcb3bb-5ff3-41b2-a4bb-e285d024a3d5)

![image](https://github.com/user-attachments/assets/239af781-4863-4e69-a8e5-9c039dcce81a)

![image](https://github.com/user-attachments/assets/a0db2e0f-5b44-496a-a84d-cbadaa896fc5)


4.1.9 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción de Imagenes Docker y subida a ACR

![image](https://github.com/user-attachments/assets/c8f4d648-ad1a-49a7-83aa-961c57c8dca1)

![image](https://github.com/user-attachments/assets/cc44dd6b-a160-40fd-8cbb-61b8ba318e88)



Acceso administrativo para ACR desde azure CLI

![image](https://github.com/user-attachments/assets/bf732102-5fce-4d44-adeb-be0d74536517)

![image](https://github.com/user-attachments/assets/9da3b223-f104-4ecc-a6ed-01ab0fe482a7)


Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back

![image](https://github.com/user-attachments/assets/5ca5b5b9-2fed-4675-a0be-d392a506d68d)

4.1.10 - Ejecutar el pipeline y en Azure Portal acceder al recurso de Azure Container Instances creado. Copiar la url del contenedor y navegarlo desde browser. Verificar que traiga datos.

![image](https://github.com/user-attachments/assets/75ebbb22-ac55-4c42-a5eb-1e134bf69c95)

![image](https://github.com/user-attachments/assets/c7e02af7-ca02-492b-a58e-54c054c66c25)

Funciona supuestamente todo pero cuadno vamos a buscarlo en le buscador no aparece nada, cuando vamos a nuestro ACI a buscar 

![image](https://github.com/user-attachments/assets/ed840841-e088-4918-9ccb-dc5e259abd57). 



Vemos que el proceso de esta killeando cada vez que lo arrancamos, asi que tenemos que descargar el docker para correrlo de manera local

![image](https://github.com/user-attachments/assets/f61ff376-e8e3-4a08-b5cf-e96c1571a73d)

Finalmente corregimos allgunos errores que se ignoraban cuando se levantaba el pipeline y tenemos el BACK funcionando

![image](https://github.com/user-attachments/assets/0decdcfe-8839-4e58-8733-4d22d190667b)

4.1.11 - Agregar tareas para generar un recurso Azure Container Instances que levante un contenedor con nuestra imagen de front (DESAFIO)
A la etapa creada en 4.1.9 Agregar tareas para generar contenedor en ACI con nuestra imagen de Front
Tener en cuenta que el contenedor debe recibir como variable de entorno API_URL el valor de una variable container-url-api-qa definida en nuestro pipeline.
Para que el punto anterior funcione el código fuente del front debe ser modificado para que la url de la API pueda ser cambiada luego de haber sido construída la imagen. Se deja un ejemplo de las modificaciones a realizar en el repo https://github.com/ingsoft3ucc/CrudAngularConEnvironment.git

![image](https://github.com/user-attachments/assets/56c794af-a360-4744-a41f-d223e950d928)

Se creó un stage muy parecido al del back para montar la imagen del Front con la siguiente variable

![image](https://github.com/user-attachments/assets/cce58f3d-3979-4c35-9e93-77209d4379af)

Variable API_URL

![image](https://github.com/user-attachments/assets/bec7cbd0-ec54-4fa8-a34d-6371eb980d83)


Se modificaron y crearon los siguientes archivos para que corra correctamente el Front

![image](https://github.com/user-attachments/assets/6d6ebd9f-ec85-417c-b229-c28ee2ea4ec5)

![image](https://github.com/user-attachments/assets/45c86eaf-1760-4f41-ba7f-5765a0aacf78)


![image](https://github.com/user-attachments/assets/d832b787-0fbd-4ac3-bafa-3106a1375f8f)


![image](https://github.com/user-attachments/assets/9d53c482-68b1-4ca1-926c-7bc1320a7d7c)


![image](https://github.com/user-attachments/assets/669b8582-0058-4b61-bd4f-a55f362cba2e)

FRONT FUNCIONANDO

![image](https://github.com/user-attachments/assets/04edfb0e-1dd0-4a95-85dd-5f94c5180084)

4.1.12 - Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en ACI.
