1- Instalar Docker Community Edition
Diferentes opciones para cada sistema operativo
https://docs.docker.com/
Ejecutar el siguiente comando para comprobar versiones de cliente y demonio.
docker version

![image](https://github.com/user-attachments/assets/745f8e13-7e9a-47a5-ac56-c4d36e14765c)

2- Explorar DockerHub
Registrase en docker hub: https://hub.docker.com/
Familiarizarse con el portal
![image](https://github.com/user-attachments/assets/0e1e84e8-c302-4eff-a22c-e21882461090)


3- Obtener la imagen BusyBox
Ejecutar el siguiente comando, para bajar una imagen de DockerHub
docker pull busybox
![image](https://github.com/user-attachments/assets/aa430563-d174-4299-8e94-f854fbff42ea)

Verificar qué versión y tamaño tiene la imagen bajada, obtener una lista de imágenes locales:
docker images
![image](https://github.com/user-attachments/assets/0c4b9f86-f440-453f-bd42-0ba70b6f1dfd)

4- Ejecutando contenedores
Ejecutar un contenedor utilizando el comando run de docker:
docker run busybox

![image](https://github.com/user-attachments/assets/c2e98845-f740-44a3-abc6-28e284bb1b65)

Explicar porque no se obtuvo ningún resultado

Este comando ejecuta el contenedor utilizando la imagen busybox. Sin embargo, no se obtuvo ningún resultado porque no se especificó ningún comando a ejecutar dentro del contenedor. El contenedor ejecuta y termina inmediatamente ya que no hay un proceso que lo mantenga activo.

Especificamos algún comando a correr dentro del contenedor, ejecutar por ejemplo:
docker run busybox echo "Hola Mundo"

![image](https://github.com/user-attachments/assets/5c3a753c-005b-4d79-9b73-f1c43914b4e0)

Ver los contenedores ejecutados utilizando el comando ps:
docker ps

![image](https://github.com/user-attachments/assets/1aabcfd0-52b4-4a9b-8278-327b01a4e939)

Vemos que no existe nada en ejecución, correr entonces:
docker ps -a

![image](https://github.com/user-attachments/assets/c8897f76-97bf-4063-bda9-3821f467a3d9)

Mostrar el resultado y explicar que se obtuvo como salida del comando anterior.

Con este comando vemos la lista de todos los contenedores, incluidos los que ya se han detenido. Al ejecutar esto, vemos una lista de contenedores que fueron ejecutados y se detuvieron, incluidos aquellos en los que se utilizó busybox echo. El estado del contenedor indicará que finalizó con éxito (exit 0).

5- Ejecutando en modo interactivo
Ejecutar el siguiente comando
docker run -it busybox sh
Para cada uno de los siguientes comandos dentro de contenedor, mostrar los resultados:
ps
uptime
free
ls -l /

![image](https://github.com/user-attachments/assets/6b42a731-7c22-4860-8f79-43312baa9ca0)

Salimos del contenedor con:
exit
6- Borrando contenedores terminados
Obtener la lista de contenedores
docker ps -a
![image](https://github.com/user-attachments/assets/dda49c4c-26bb-4ad2-8273-e013b8b7ad0d)

Para borrar podemos utilizar el id o el nombre (autogenerado si no se especifica) de contenedor que se desee, por ejemplo:
docker rm elated_lalande
Para borrar todos los contenedores que no estén corriendo, ejecutar cualquiera de los siguientes comandos:
docker rm $(docker ps -a -q -f status=exited)
![image](https://github.com/user-attachments/assets/5853bd01-3209-4221-8d4e-0143cb300930)

docker container prune
![image](https://github.com/user-attachments/assets/3c9a3b60-d1e2-4bd2-b49a-028c37dc3d23)

7- Construir una imagen
Conceptos de DockerFile
Leer https://docs.docker.com/engine/reference/builder/
Describir las instrucciones
FROM: Define la imagen base que se usará para crear la nueva imagen.
RUN: Ejecuta un comando dentro de la imagen durante el proceso de construcción. 
ADD: Copia archivos o directorios desde el sistema de archivos del host a la imagen. A diferencia de COPY, ADD también puede extraer archivos .tar.
COPY: Similar a ADD, pero solo copia archivos o directorios.
EXPOSE: Indica qué puerto debe estar disponible para la red externa. 
CMD:Define el comando por defecto que se ejecutará cuando se inicie un contenedor.
ENTRYPOINT: Especifica el comando principal que se ejecutará en el contenedor. A diferencia de CMD, ENTRYPOINT no puede ser sobrescrito. 
A partir del código https://github.com/ingsoft3ucc/SimpleWebAPI crearemos una imagen.
Clonar repo
Crear imagen etiquetándola con un nombre. El punto final le indica a Docker que use el dir actual
docker build -t mywebapi .
Revisar Dockerfile y explicar cada línea
Ver imágenes disponibles
Ejecutar un contenedor con nuestra imagen
Subir imagen a nuestra cuenta de dockerhub
7.1 Inicia sesión en Docker Hub
Primero, asegúrate de estar autenticado en Docker Hub desde tu terminal:
docker login
7.2 Etiquetar la imagen a subir con tu nombre de usuario de Docker Hub y el nombre de la imagen. Por ejemplo:
docker tag <nombre_imagen_local> <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
7.3 Subir la Imagen
Para subir la imagen etiquetada a Docker Hub, utiliza el comando docker push:
docker push <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
7.4 Verificar la Subida
docker pull <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
8- Publicando puertos
En el caso de aplicaciones web o base de datos donde se interactúa con estas aplicaciones a través de un puerto al cual hay que acceder, estos puertos están visibles solo dentro del contenedor. Si queremos acceder desde el exterior deberemos exponerlos.

Ejecutar la siguiente imagen, en este caso utilizamos la bandera -d (detach) para que nos devuelva el control de la consola:
docker run --name myapi -d mywebapi
Ejecutamos un comando ps:

Vemos que el contendor expone 3 puertos el 80, el 5254 y el 443, pero si intentamos en un navegador acceder a http://localhost/WeatherForecast no sucede nada.

Procedemos entonces a parar y remover este contenedor:

docker kill myapi
docker rm myapi
Vamos a volver a correrlo otra vez, pero publicando el puerto 80
docker run --name myapi -d -p 80:80 mywebapi
Accedamos nuevamente a http://localhost/WeatherForecast y vemos que nos devuelve datos.
9- Modificar Dockerfile para soportar bash
Modificamos dockerfile para que entre en bash sin ejecutar automaticamente la app
#ENTRYPOINT ["dotnet", "SimpleWebAPI.dll"]
CMD ["/bin/bash"]
Rehacemos la imagen
docker build -t mywebapi .
Corremos contenedor en modo interactivo exponiendo puerto
docker run -it --rm -p 80:80 mywebapi
Navegamos a http://localhost/weatherforecast
Vemos que no se ejecuta automaticamente
Ejecutamos app:
dotnet SimpleWebAPI.dll
-Volvemos a navegar a http://localhost/weatherforecast

Salimos del contenedor
10- Montando volúmenes
Hasta este punto los contenedores ejecutados no tenían contacto con el exterior, ellos corrían en su propio entorno hasta que terminaran su ejecución. Ahora veremos cómo montar un volumen dentro del contenedor para visualizar por ejemplo archivos del sistema huésped:

Ejecutar el siguiente comando, cambiar myusuario por el usuario que corresponda. En Mac puede utilizarse /Users/miusuario/temp):
docker run -it --rm -p 80:80 -v /Users/miuser/temp:/var/temp  mywebapi
Dentro del contenedor correr
ls -l /var/temp
touch /var/temp/hola.txt
Verificar que el Archivo se ha creado en el directorio del guest y del host.
11- Utilizando una base de datos
Levantar una base de datos PostgreSQL
mkdir $HOME/.postgres

docker run --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword -v $HOME/.postgres:/var/lib/postgresql/data -p 5432:5432 -d postgres:9.4
Ejecutar sentencias utilizando esta instancia
docker exec -it my-postgres /bin/bash

psql -h localhost -U postgres

#Estos comandos se corren una vez conectados a la base

\l
create database test;
\connect test
create table tabla_a (mensaje varchar(50));
insert into tabla_a (mensaje) values('Hola mundo!');
select * from tabla_a;

\q

exit
Conectarse a la base utilizando alguna IDE (Dbeaver - https://dbeaver.io/, Azure DataStudio -https://azure.microsoft.com/es-es/products/data-studio, etc). Interactuar con los objectos objectos creados.

Explicar que se logro con el comando docker run y docker exec ejecutados en este ejercicio.

12- Hacer el punto 11 con Microsoft SQL Server
Armar un contenedor con SQL Server
Crear BD, Tablas y ejecutar SELECT
13- Presentación del trabajo práctico.
Subir un archivo md (puede ser en una carpeta) trabajo-practico-02 con las salidas de los comandos utilizados. Si es necesario incluir también capturas de pantalla.
