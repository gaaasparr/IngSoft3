4- Desarrollo:
 Una vez corridos todos los comandos de los prerequisitos arrancamos

 4.1 Creación de una BD SQL Server para nuestra App
A. Montar una img/imagen Docker de SQL Server 

Uso mi contenedor de docker 

![Captura desde 2024-09-30 19-42-22](https://github.com/user-attachments/assets/e56af2f0-ec42-465e-83ab-d8ca0d784ebb)


B. En caso de optar por la opción de montar la img/imagen de docker, una vez levantada el contenedor, conectarse y ejecutar el siguiente script:

Ejecutamos el script (cambie GO por ";")


![Captura desde 2024-09-30 19-52-45](https://github.com/user-attachments/assets/42c9769d-dc80-488c-bda0-ac5b2303b8e6)



4.2 Obtener nuestra App
A. Clonar el repo https://github.com/ingsoft3ucc/Angular_WebAPINetCore8_CRUD_Sample.git

![Captura desde 2024-09-30 20-01-04](https://github.com/user-attachments/assets/9ca8e544-7ee6-45a6-a6cd-e48ac2e2854a)


B. Seguir las instrucciones del README.md del repo clonado prestando atención a la modificación de la cadena de conexión en el appSettings.json para que apunte a la BD creada en 4.1

Le cambiamos la cadena de conexion para que apunte a nuestra db

![Captura desde 2024-09-30 20-18-48](https://github.com/user-attachments/assets/0cbba38b-e8a4-4c34-9412-029cab934c08)


Construimos la api y verificamos que funcione


![Captura desde 2024-09-30 20-20-38](https://github.com/user-attachments/assets/68965fad-33af-4ea5-84ec-bc081cb8f7ff)

![Captura desde 2024-09-30 20-24-00](https://github.com/user-attachments/assets/3075b8da-1c3e-4f9b-8210-3883408e54ea)


Construimos el CRUD angular y verificamos que funcione

![Captura desde 2024-09-30 20-23-49](https://github.com/user-attachments/assets/4f108dd5-ddfa-4e5a-8798-30dad896b2c7)


![Captura desde 2024-09-30 22-57-14](https://github.com/user-attachments/assets/674d3b5e-e480-4b16-a505-f8c1c07882b8)


C. Navegar a http://localhost:7150/swagger/index.html y probar uno de los controladores para verificar el correcto funcionamiento de la API.

![Captura desde 2024-09-30 22-51-36](https://github.com/user-attachments/assets/817591ed-b1a5-418d-95cd-fed398464c15)

Acá podemos ver que el método Get trae los empleados de la BDD correctamente


D. Navegar a http://localhost:4200 y verificar el correcto funcionamiento de nuestro front-end Angular

![Captura desde 2024-09-30 22-57-14](https://github.com/user-attachments/assets/d8491ebb-d2af-4aca-aaf6-7448724cdc62)



E. Una vez verificado el correcto funcionamiento de la Aplicación procederemos a crear un proyecto de pruebas unitarias para nuestra API.



4.3 Crear Pruebas Unitarias para nuestra API
A. En el directorio raiz de nuestro repo crear un nuevo proyecto de pruebas unitarias para nuestra API

![Captura desde 2024-09-30 20-26-42](https://github.com/user-attachments/assets/1f1d3fef-ffd6-47f5-9e9d-0c5aed20c299)


Instalamos las dependencias

cd EmployeeCrudApi.Tests 
dotnet add package Moq
dotnet add package xunit
dotnet add package Microsoft.EntityFrameworkCore.InMemory

C. Editar archivo UnitTest1.cs 

![Captura desde 2024-09-30 21-40-33](https://github.com/user-attachments/assets/29c9d4a0-115d-4516-b546-406f9178721c)


D. Renombrar archivo UnitTest1.cs por EmployeeControllerUnitTests.cs

![Captura desde 2024-09-30 21-38-49](https://github.com/user-attachments/assets/9998389f-8428-4b63-8a5d-254cd875d4dd)


E. Editar el archivo EmployeeCrudApi.Tests/EmployeeCrudApi.Tests.csproj para agregar una referencia a nuestro proyecto de EmployeeCrudApi reemplazando su contenido por

![Captura desde 2024-09-30 21-40-33](https://github.com/user-attachments/assets/b1b6b4c9-c18a-451b-8743-892f804afb9a)


F. Ejecutar los siguientes comandos para ejecutar nuestras pruebas G. Verificar que se hayan ejecutado correctamente las pruebas

![Captura desde 2024-09-30 23-12-40](https://github.com/user-attachments/assets/7662798c-30f4-48d0-ada8-fcbb2b9287c0)

![Captura desde 2024-09-30 23-13-00](https://github.com/user-attachments/assets/fa2384ff-dc3f-48cf-bae3-5ee5dd14f9cf)


H. Verificar que no estamos usando una dependencia externa como la base de datos.

![image](https://github.com/user-attachments/assets/c13d2102-58d2-4a40-9607-b346897dc6f9)

I. Modificar la cadena de conexión en el archivo appsettings.json para que use un usuario o password incorrecto y recompilar el proyecto EmployeeCrudApi

![Captura desde 2024-09-30 23-18-48](https://github.com/user-attachments/assets/f4b88202-46ae-4e1e-975c-09aebd37962d)



J. Verificar que nuestro proyecto ya no tiene acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:

![Captura desde 2024-09-30 23-20-59](https://github.com/user-attachments/assets/dc75571e-0ce1-44ff-915c-d5f0221e1ea9)


K. En la carpeta de nuestro proyecto EmployeeCrudApi.Tests volver a correr las pruebas 

![image](https://github.com/user-attachments/assets/bb557044-74f4-43e2-b371-34b657f1a4a2)


L. Verificar que se hayan ejecutado correctamente las pruebas inclusive sin tener acceso a la BD, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieren de una dependencia externa para funcionar.



M. Modificar la cadena de conexión en el archivo appsettings.json para que use el usuario y password correcto y recompilar el proyecto EmployeeCrudApi



N. Verificar que nuestro proyecto vuelve a tener acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:
