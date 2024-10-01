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



Construimos la api y verificamos que funcione




Construimos el CRUD angular y verificamos que funcione

 

C. Navegar a http://localhost:7150/swagger/index.html y probar uno de los controladores para verificar el correcto funcionamiento de la API.

Funciona correctamente, me trae los empleados



D. Navegar a http://localhost:4200 y verificar el correcto funcionamiento de nuestro front-end Angular



E. Una vez verificado el correcto funcionamiento de la Aplicación procederemos a crear un proyecto de pruebas unitarias para nuestra API.

4.3 Crear Pruebas Unitarias para nuestra API
A. En el directorio raiz de nuestro repo crear un nuevo proyecto de pruebas unitarias para nuestra API



Instalamos las dependencias

cd EmployeeCrudApi.Tests 
dotnet add package Moq
dotnet add package xunit
dotnet add package Microsoft.EntityFrameworkCore.InMemory
C. Editar archivo UnitTest1.cs reemplazando su contenido por



D. Renombrar archivo UnitTest1.cs por EmployeeControllerUnitTests.cs



E. Editar el archivo EmployeeCrudApi.Tests/EmployeeCrudApi.Tests.csproj para agregar una referencia a nuestro proyecto de EmployeeCrudApi reemplazando su contenido por



F. Ejecutar los siguientes comandos para ejecutar nuestras pruebas G. Verificar que se hayan ejecutado correctamente las pruebas

Se ejecutaron correctamente:



H. Verificar que no estamos usando una dependencia externa como la base de datos.

I. Modificar la cadena de conexión en el archivo appsettings.json para que use un usuario o password incorrecto y recompilar el proyecto EmployeeCrudApi





J. Verificar que nuestro proyecto ya no tiene acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:



K. En la carpeta de nuestro proyecto EmployeeCrudApi.Tests volver a correr las pruebas L. Verificar que se hayan ejecutado correctamente las pruebas inclusive sin tener acceso a la BD, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieren de una dependencia externa para funcionar.



M. Modificar la cadena de conexión en el archivo appsettings.json para que use el usuario y password correcto y recompilar el proyecto EmployeeCrudApi



N. Verificar que nuestro proyecto vuelve a tener acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:
