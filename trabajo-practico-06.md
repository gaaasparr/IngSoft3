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

![Captura desde 2024-09-30 20-26-42](https://github.com/user-attachments/assets/6165713e-c732-46ce-8879-d0abd0723f2d)



C. Navegar a http://localhost:7150/swagger/index.html y probar uno de los controladores para verificar el correcto funcionamiento de la API.

![Captura desde 2024-09-30 22-51-36](https://github.com/user-attachments/assets/817591ed-b1a5-418d-95cd-fed398464c15)

Acá podemos ver que el método Get trae los empleados de la BDD correctamente


D. Navegar a http://localhost:4200 y verificar el correcto funcionamiento de nuestro front-end Angular

![Captura desde 2024-09-30 22-57-14](https://github.com/user-attachments/assets/d8491ebb-d2af-4aca-aaf6-7448724cdc62)



E. Una vez verificado el correcto funcionamiento de la Aplicación procederemos a crear un proyecto de pruebas unitarias para nuestra API.

![Captura desde 2024-09-30 21-08-18](https://github.com/user-attachments/assets/e81a2c97-8ace-4368-9bb9-c84dfa1a812b)


4.3 Crear Pruebas Unitarias para nuestra API
A. En el directorio raiz de nuestro repo crear un nuevo proyecto de pruebas unitarias para nuestra API




Instalamos las dependencias

cd EmployeeCrudApi.Tests 
dotnet add package Moq
dotnet add package xunit
dotnet add package Microsoft.EntityFrameworkCore.InMemory

C. Editar archivo UnitTest1.cs 

Editamos el archivo con el codigo proporcionado en el desarrollo del TP


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


![Captura desde 2024-09-30 20-18-48](https://github.com/user-attachments/assets/e1150fe0-f6a0-4e9c-93fd-8163caa3ec2b)


N. Verificar que nuestro proyecto vuelve a tener acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:

![image](https://github.com/user-attachments/assets/fb544951-4056-4779-8a40-2dc02393f548)

4.4 Creamos pruebas unitarias para nuestro front de Angular:
A. Nos posicionamos en nuestro proyecto de front, en el directorio EmployeeCrudAngular/src/app

![image](https://github.com/user-attachments/assets/e82c5cf4-77d5-4e04-81f7-a52e6d246e66)


B. Editamos el archivo app.component.spec.ts reemplazando su contenido por:

![image](https://github.com/user-attachments/assets/25021c86-f1e4-4f69-a265-dc84eaa46380)


C. Creamos el archivo employee.service.spec.ts reemplazando su contenido por:

![image](https://github.com/user-attachments/assets/6723bf1a-10ef-489f-9b84-b1a65e7e4b3f)


D. Editamos el archivo employee.component.spec.ts ubicado en la carpeta employee reemplazando su contenido por:

![image](https://github.com/user-attachments/assets/01c4fa81-e3cb-422b-8958-b9392ee225cd)


E. Editamos el archivo addemployee.component.spec.ts ubicado en la carpeta addemployee reemplazando su contenido por:

![image](https://github.com/user-attachments/assets/f7dd09e7-6fa2-42a5-9a37-1d509c26167c)



F. En el directorio raiz de nuestro proyecto EmployeeCrudAngular ejecutamos el comando ng test

![image](https://github.com/user-attachments/assets/90da8d75-4be3-4d1b-82b6-23191e386ec1)

No funciona porque no tengo chrome instalado enn mi PC, asi que lo descargamos y continuamos

G. Vemos que se abre una ventana de Karma con Jasmine en la que nos indica que los tests se ejecutaron correctamente

![image](https://github.com/user-attachments/assets/37bb3080-b0e4-4496-90cf-630943a81a47)


H. Vemos que los tests se ejecutaron correctamente:

![image](https://github.com/user-attachments/assets/8d5d102a-3f97-420e-a7ab-3cde4f04c87f)


I. Verificamos que no esté corriendo nuestra API navegando a http://localhost:7150/swagger/index.html y recibiendo esta salida:

![image](https://github.com/user-attachments/assets/3944de91-de57-460e-99c9-e8763239b375)


J. Los puntos G y H nos indican que se han ejecutado correctamente las pruebas inclusive sin tener acceso a la API, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieres de una dependencia externa para funcionar.

4.5 Agregamos generación de reporte XML de nuestras pruebas de front.
Para cuando integremos nuestras pruebas en un pipeline de Build, vamos a necesitar el resultado devuelto por nuestras pruebas para reportarlas junto a las pruebas de back que se reportan automaticamente.

A. Instalamos dependencia karma-junit-reporter

![image](https://github.com/user-attachments/assets/2113fb23-ccc7-4eee-8b46-fbec373adde1)


B. En el directorio raiz de nuestro proyecto (al mismo nivel que el archivo angular.json) creamos un archivo karma.conf.js con el siguiente contenido

![image](https://github.com/user-attachments/assets/f5b515de-bb67-4970-9b36-cbd490de2c56)

![image](https://github.com/user-attachments/assets/23463f7c-7cda-4abe-8762-218cc12e7b48)



C. Ejecutamos nuestros test de la siguiente manera:

![image](https://github.com/user-attachments/assets/f2d2e001-cc42-4cda-9971-21131b374ff2)



D. Verificamos que se creo un archivo test-result.xml en el directorio test-results que está al mismo nivel que el directorio src

![image](https://github.com/user-attachments/assets/94f0a285-769b-44c4-a4ef-e25869d11a7b)



4.6 Modificamos el código de nuestra API y creamos nuevas pruebas unitarias:
A. Realizar al menos 5 de las siguientes modificaciones sugeridas al código de la API:

Escenarios a probar:
Validar que el nombre no esté repetido.
Verificar que el nombre no tenga más de 100 caracteres.
Verificar el formateo correcto del nombre (primera letra de cada nombre en mayúscula y el apellido en mayúsculas).
Verificar que el nombre no contenga caracteres especiales o números.
Verificar que el nombre no sea trivial o genérico.

![image](https://github.com/user-attachments/assets/73c1a649-63a6-4d35-ab0b-b541703b98dc)

B. Crear las pruebas unitarias necesarias para validar las modificaciones realizadas en el código

Creamos las pruebas para cada uno de los 5 escenarios

![image](https://github.com/user-attachments/assets/1f670f20-180f-47ea-a9a2-2009ccaefad7)

![image](https://github.com/user-attachments/assets/b9e13388-563c-4f31-91bf-7874d46ae02a)

![image](https://github.com/user-attachments/assets/60b84437-d9f1-4a97-a013-0218aab5efba)




Buildeamos los test y los corremos
![image](https://github.com/user-attachments/assets/19564454-c6e9-4bab-a40a-b67a8564d70b)

hay errores asi que nos ponemos a ver que pasa hasta que se solucionen esos errores, con las advertencias creoq ue podemos seguir operando.


![image](https://github.com/user-attachments/assets/602aefad-3906-4a5f-a47a-af37aa827582)

![image](https://github.com/user-attachments/assets/b5de135e-833e-426b-b883-227ef782a5c0)

Cuando corremos los tests tambien explota todo asi que nos ponemos a modificar uno por uno.

ESTE ES EL COODIGO DEFINITIVO OPTIMIZADO

![image](https://github.com/user-attachments/assets/ccb60697-ce0d-4af9-b15e-5748a05f9618)


![image](https://github.com/user-attachments/assets/19b9e5f3-9ac9-4c4f-8c54-fae12ac8d1a4)

![image](https://github.com/user-attachments/assets/a3be44e5-1a85-4fb8-b6aa-ee6908ee72ac)

ahora mucho mejor, solo dos tests estan fallando

![image](https://github.com/user-attachments/assets/1177c4c3-fa80-49dd-8f29-c47f69d08ac1)

Todo funcionando, al final del proyecto dejo adjuntados los archivos employeecontroller.cs y employeeControllerUnitTests.cs


4.7 Modificamos el código de nuestro Front y creamos nuevas pruebas unitarias:
A. Realizar en el código del front las mismas modificaciones hechas a la API. B. Las validaciones deben ser realizadas en el front sin llegar a la API, y deben ser mostradas en un toast como por ejemplo https://stackblitz.com/edit/angular12-toastr?file=src%2Fapp%2Fapp.component.ts o https://stackblitz.com/edit/angular-error-toast?file=src%2Fapp%2Fcore%2Frxjsops.ts

Instalamos la libreria de toast



Abrimos el archivo src/app/app.config.ts y agregamos las importaciones necesarias para ToastrModule y BrowserAnimationsModule.



Tambien importamos el css con los estilos de los toast



Agregamos las validaciones en AddEmployee y las probamos




C. Crear las pruebas unitarias necesarias en el front para validar las modificaciones realizadas en el código del front.

Creamos las pruebas unitarias en addemployee.component.spec



Las ejecutamos exitosamente

 

6. Subir el proyecto
Link a repo: https://github.com/cettipao/AngularCrud-UnitTests

