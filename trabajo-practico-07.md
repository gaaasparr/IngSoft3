4.1 Agregar Code Coverage a nuestras pruebas unitarias de backend y front-end e integrarlas junto con sus resultados en nuestro pipeline de build.
Desarrollo del punto 4.1:

4.1.1 En el directorio raiz de nuestro proyecto Angular instalar el siguiente paquete:
 npm install karma-coverage --save-dev

 ![image](https://github.com/user-attachments/assets/7f492bc8-d9c8-48cd-a96d-e40253598cd4)

4.1.2 Editar nuestro archivo karma.conf.js para que incluya reporte de cobertura

![image](https://github.com/user-attachments/assets/fedf26e4-b9cd-400d-a3d1-ee11323e7302)



4.1.3 En el dir raiz del proyecto EmployeeCrudApi.Tests ejecutar:
dotnet add package coverlet.collector

![image](https://github.com/user-attachments/assets/5ac4d518-47f1-4930-9eca-cc3d3bf6e10c)


4.1.4 Agregar a nuestro pipeline ANTES del Build de Back la tarea de test con los argumentos especificados y la de publicación de resultados de cobertura:


 
4.1.5 Agregar a nuestro pipeline ANTES del Build de front la tarea de test y la de publicación de los resultados.
 
4.1.6 Ejecutar el pipeline y analizar el resultado de las pruebas unitarias y la cobertura de código.


