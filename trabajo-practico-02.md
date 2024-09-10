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
![image](https://github.com/user-attachments/assets/dbd25ca9-6636-4384-a0dd-ddc659cd7c8b)

Crear imagen etiquetándola con un nombre. El punto final le indica a Docker que use el dir actual
docker build -t mywebapi .
![image](https://github.com/user-attachments/assets/50e03ede-4309-474b-9b11-137f1e5aa653)

Revisar Dockerfile y explicar cada línea:

1. FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
Se utiliza una imagen base de ASP.NET Core 7.0 desde el registro de contenedores de Microsoft. Esta imagen incluye todo lo necesario para ejecutar aplicaciones ASP.NET Core.
AS base: Igual que en BDD renombramos, esta es una etiqueta permite hacer referencia a esta imagen en pasos posteriores del Dockerfile.
2. WORKDIR /app
Establecemos el directorio de trabajo dentro del contenedor en /app. Este será el directorio predeterminado en el que se ejecutarán los siguientes comandos.
3. EXPOSE 80
4. EXPOSE 443
5. EXPOSE 5254
En estos comandos abrimos los puertos 80, 443 y 5254 para el tráfico. El puerto 80 es el predeterminado para HTTP, el 443 para HTTPS, y el 5254 es el puerto que utiliza la aplicación.
6. FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
Usamos una imagen del SDK de .NET Core 7.0 para compilar la aplicación. A diferencia de la imagen de ASP.NET Core, esta imagen incluye todas las herramientas necesarias para desarrollar y construir aplicaciones .NET.
7. WORKDIR /src
Cambia el directorio de trabajo a /src, donde se colocará el código fuente para la compilación.
8. COPY ["SimpleWebAPI/SimpleWebAPI.csproj", "SimpleWebAPI/"]
Copiamos el archivo del proyecto SimpleWebAPI.csproj al directorio SimpleWebAPI/ dentro del contenedor. Esto es necesario para restaurar las dependencias antes de copiar el resto del código.
9. RUN dotnet restore "SimpleWebAPI/SimpleWebAPI.csproj"
Restauramos las dependencias del proyecto especificado (SimpleWebAPI.csproj) usando dotnet restore. Esto descarga los paquetes necesarios para compilar el proyecto.
10. COPY . .
Hacemos una copia de todo el contenido del contexto de construcción (el directorio donde está el Dockerfile) al contenedor en el directorio de trabajo actual (/src).
11. WORKDIR "/src/SimpleWebAPI"
Cambiamos el directorio de trabajo al directorio del proyecto (/src/SimpleWebAPI) dentro del contenedor.
12. RUN dotnet build "SimpleWebAPI.csproj" -c Release -o /app/build
Ejecutamos la compilación del proyecto en modo Release usando el comando dotnet build. El resultado es colocado en /app/build.
13. FROM build AS publish
Utiliza la imagen generada en el paso de compilación (build) para continuar con el proceso de publicación.
14. RUN dotnet publish "SimpleWebAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false
Publicamos la aplicación .NET para su despliegue, usando el comando dotnet publish. El resultado se coloca en /app/publish. La opción /p:UseAppHost=false indica que no se creará un ejecutable nativo (esto es útil para contenedores, ya que se usa dotnet <dll> para ejecutar).
15. FROM base AS final
Utilizamos la imagen base de ASP.NET (base) para crear la imagen final que se usará para ejecutar la aplicación.
16. WORKDIR /app
Nuevamente se cambia el directorio de trabajo a /app, esta vez en la imagen final.
17. COPY --from=publish /app/publish .
Copia los archivos publicados desde la etapa publish a la imagen final.
18. ENTRYPOINT ["dotnet", "SimpleWebAPI.dll"]
Establece el punto de entrada para el contenedor. Cuando el contenedor se ejecute, se ejecutará el comando dotnet SimpleWebAPI.dll, que iniciará la aplicación.
19. #CMD ["/bin/bash"]
Esta línea está comentada y no se ejecutará. Si se descomentara, indicaría que el contenedor debería iniciarse en modo interactivo con un shell Bash.
![image](https://github.com/user-attachments/assets/b418c68b-35e9-4503-b2fb-88fd4a636585)

Ejecutar un contenedor con nuestra imagen
![image](https://github.com/user-attachments/assets/009286a7-afdd-4d35-b644-5e0fd2288223)

Subir imagen a nuestra cuenta de dockerhub
![image](https://github.com/user-attachments/assets/78804d49-70f3-4e6b-b1ea-f621f56eab20)
![image](https://github.com/user-attachments/assets/ca85cfb4-065d-4ca8-8e7e-ff33cf55adc1)


8- Publicando puertos
En el caso de aplicaciones web o base de datos donde se interactúa con estas aplicaciones a través de un puerto al cual hay que acceder, estos puertos están visibles solo dentro del contenedor. Si queremos acceder desde el exterior deberemos exponerlos.

Ejecutar la siguiente imagen, en este caso utilizamos la bandera -d (detach) para que nos devuelva el control de la consola:
docker run --name myapi -d mywebapi
![image](https://github.com/user-attachments/assets/1df2179c-acfb-43a0-a1e4-2b178e50844a)

Ejecutamos un comando ps:
![image](https://github.com/user-attachments/assets/ca0189ca-cdfa-4ea4-b567-c078cbf61891)


Vemos que el contendor expone 3 puertos el 80, el 5254 y el 443, pero si intentamos en un navegador acceder a http://localhost/WeatherForecast no sucede nada.

Procedemos entonces a parar y remover este contenedor:

docker kill myapi
docker rm myapi

![image](https://github.com/user-attachments/assets/03b0f2f0-372a-416a-bb9d-9c13f1936365)

Vamos a volver a correrlo otra vez, pero publicando el puerto 80
docker run --name myapi -d -p 80:80 mywebapi

![image](https://github.com/user-attachments/assets/a1b1ca38-7063-47ff-a77f-2d0cbb10900c)

Accedamos nuevamente a http://localhost/WeatherForecast y vemos que nos devuelve datos.
![image](https://github.com/user-attachments/assets/7fb8645b-6991-4eaa-9709-c5df4e3b83c0)

9- Modificar Dockerfile para soportar bash
Modificamos dockerfile para que entre en bash sin ejecutar automaticamente la app
#ENTRYPOINT ["dotnet", "SimpleWebAPI.dll"]
CMD ["/bin/bash"]

![image](https://github.com/user-attachments/assets/8662dee7-72c5-408b-9da0-8833a4ea438e)

Rehacemos la imagen
docker build -t mywebapi .
![image](https://github.com/user-attachments/assets/c62fd614-f80e-4639-a04b-021b591d5e79)


Corremos contenedor en modo interactivo exponiendo puerto
docker run -it --rm -p 80:80 mywebapi
![image](https://github.com/user-attachments/assets/c3447d8d-f9a7-4ce7-8875-84694ccf2a89)

Navegamos a http://localhost/weatherforecast
Vemos que no se ejecuta automaticamente
Ejecutamos app:
dotnet SimpleWebAPI.dll
![image](https://github.com/user-attachments/assets/e643e12d-3ac3-45d9-ade3-54f4538dadd6)

-Volvemos a navegar a http://localhost/weatherforecast
![image](https://github.com/user-attachments/assets/9f01d295-5ca0-4bd7-8a6e-55bea1b4afd1)

Salimos del contenedor
![image](https://github.com/user-attachments/assets/e470f531-cafe-47b5-85d2-afe629424fb6)

10- Montando volúmenes
Hasta este punto los contenedores ejecutados no tenían contacto con el exterior, ellos corrían en su propio entorno hasta que terminaran su ejecución. Ahora veremos cómo montar un volumen dentro del contenedor para visualizar por ejemplo archivos del sistema huésped:

Ejecutar el siguiente comando, cambiar myusuario por el usuario que corresponda. En Mac puede utilizarse /Users/miusuario/temp):
docker run -it --rm -p 80:80 -v /Users/miuser/temp:/var/temp  mywebapi (lo hice en el puerto 8080, porque en este punto creo que el peurto esta ocupado en una instancia que yo mismo cree sin querer y si cierro la terminal no estoy muy seguro de como volver hasta este punto) 
![image](https://github.com/user-attachments/assets/84e7e726-62ba-4a9a-8500-5827369418c9)

Dentro del contenedor correr
ls -l /var/temp
touch /var/temp/hola.txt
![image](https://github.com/user-attachments/assets/59cb45a9-0fc6-434a-a0c7-45338d93ea98)

Verificar que el Archivo se ha creado en el directorio del guest y del host.
![image](https://github.com/user-attachments/assets/b0a777ce-51c6-4f2d-9724-0243e953525d)

11- Utilizando una base de datos
Levantar una base de datos PostgreSQL
mkdir $HOME/.postgres

docker run --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword -v $HOME/.postgres:/var/lib/postgresql/data -p 5432:5432 -d postgres:9.4

![image](https://github.com/user-attachments/assets/d59d5928-9d27-41bf-821e-787d1ecedf91)

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

![image](https://github.com/user-attachments/assets/c36cd6e0-4e5c-4c47-992d-afab4916a5b1)

Conectarse a la base utilizando alguna IDE (Dbeaver - https://dbeaver.io/, Azure DataStudio -https://azure.microsoft.com/es-es/products/data-studio, etc). Interactuar con los objectos objectos creados.

Explicar que se logro con el comando docker run y docker exec ejecutados en este ejercicio.

12- Hacer el punto 11 con Microsoft SQL Server
Armar un contenedor con SQL Server
Crear BD, Tablas y ejecutar SELECT
13- Presentación del trabajo práctico.
Subir un archivo md (puede ser en una carpeta) trabajo-practico-02 con las salidas de los comandos utilizados. Si es necesario incluir también capturas de pantalla.
