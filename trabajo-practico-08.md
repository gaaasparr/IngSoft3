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

