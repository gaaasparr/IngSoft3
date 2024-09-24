 Pasos del TP
4.1 Verificar acceso a Pipelines concedido
![image](https://github.com/user-attachments/assets/ab31c085-4893-4b37-8f3a-3f5ba7fc4aca)

Al final corri todo en privado, porque tenía problemas con los permisos para correr en public
![image](https://github.com/user-attachments/assets/a59a391e-891d-4046-9f13-2eb0e9b9ee26)


4.2 Agregar en pipeline YAML una tarea de Publish.

![image](https://github.com/user-attachments/assets/bff6927c-48e1-46cb-8f3a-0a654a30d6dc)


4.3 Explicar por qué es necesario contar con una tarea de Publish en un pipeline que corre en un agente de Microsoft en la nube.

La tarea de Publish en un pipeline que corre en un agente de Microsoft en la nube es necesaria porque estos agentes son efímeros. Se destruyen al finalizar la ejecución y los archivos generados (artefactos) se pierden si no se publican. Publicar los artefactos permite que sean almacenados en un lugar centralizado, accesible en Azure DevOps, para que puedan ser utilizados en despliegues posteriores, mantenidos para auditoría. De esta manera podemos compartirlos con otros equipos o pipelines. Esto asegura la continuidad del proceso de CI/CD, facilita el despliegue y versionado del software.

4.4 Descargar el resultado del pipeline y correr localmente el software compilado.

![image](https://github.com/user-attachments/assets/0fd476e7-5ebd-4c5f-8d2a-b277a24772cf)

![image](https://github.com/user-attachments/assets/ea98f9f3-d1d4-4167-b372-d7fc8e99983a)


Una vez descargado, corremos localmente





4.5 Habilitar el editor clásico de pipelines. Explicar las diferencias claves entre este tipo de editor y el editor YAML.

![image](https://github.com/user-attachments/assets/57784b3c-79da-4f78-b953-3e40319c79c3)

El editor clásico de pipelines en Azure DevOps ofrece una interfaz gráfica para configurar tareas de manera visual, ideal para usuarios no técnicos, pero no permite versionar el pipeline junto al código. Con el editor YAML utilizamos un archivo dentro del repositorio, lo que permite versionar los cambios, facilita la automatización y es más flexible para proyectos de mayor complejidad.
De manera muy resumida: El editor clásico es más sencillo de usar, pero YAML ofrece mejor escalabilidad, colaboración y control sobre el pipeline.

4.6 Crear un nuevo pipeline con el editor clásico. Descargar el resultado del pipeline y correr localmente el software compilado.

![image](https://github.com/user-attachments/assets/f50bffed-2a73-447e-ac5b-ff51eca7d4aa)

![image](https://github.com/user-attachments/assets/082d4775-a46d-46a4-9a85-a5c40a8e0fe3)

![image](https://github.com/user-attachments/assets/373f7900-e621-43fb-95c3-9286b119ba50)

![image](https://github.com/user-attachments/assets/7c0c102e-85ec-4b19-94d8-1468bc8c57f6)

![image](https://github.com/user-attachments/assets/c79b3016-6519-46eb-8b3c-a64e216963de)



4.7 Configurar CI en ambos pipelines (YAML y Classic Editor). Mostrar resultados de la ejecución automática de ambos pipelines al hacer un commit en la rama main.

4.8 Explicar la diferencia entre un agente MS y un agente Self-Hosted. Qué ventajas y desventajas hay entre ambos? Cuándo es conveniente y/o necesario usar un Self-Hosted Agent?

4.8 Crear un Pool de Agentes y un Agente Self-Hosted

4.9 Instalar y correr un agente en nuestra máquina local.

4.10 Crear un pipeline que use el agente Self-Hosted alojado en nuestra máquina local.

4.11 Buscar el resultado del pipeline y correr localmente el software compilado.

4.12 Crear un nuevo proyecto en ADO clonado desde un repo que contenga una aplicación en Angular como por ejemplo https://github.com/ingsoft3ucc/angular-demo-project.git

4.13 Configurar un pipeline de build para un proyecto de tipo Angular como el clonado.

4.14 Habilitar CI para el pipeline.

4.15 Hacer un cambio a un archivo del proyecto (algún cambio en el HTML que se renderiza por ejemplo) y verificar que se ejecute automáticamente el pipeline.

4.16 Descargar el resultado del pipeline y correr en un servidor web local el sitio construido.

4.17 Mostrar el antes y el después del cambio.



![image](https://github.com/user-attachments/assets/99bae89f-43b9-4285-b69c-84ad773cb81f)

![image](https://github.com/user-attachments/assets/e2a92eda-89ad-460e-8cba-eebb5744f01c)


![image](https://github.com/user-attachments/assets/2fe4e5b7-fe99-4bda-94da-d7a7a9ef8d4f)


![image](https://github.com/user-attachments/assets/4540502a-81f3-4603-855b-a3c992b4d5dc)
