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

En el primer intento no funciona porque falta dar acceso administrativo para ACR desde azure CLI

![image](https://github.com/user-attachments/assets/bf732102-5fce-4d44-adeb-be0d74536517)

![image](https://github.com/user-attachments/assets/9da3b223-f104-4ecc-a6ed-01ab0fe482a7)


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

