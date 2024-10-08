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


Una vez descargado, corremos localmente. Estuve varias horas luchando para que funcione hasta que en algun foro perdido en intener encontre que simplemente modificando el archivo runtime.json podia hacer que se adapte a la version manualmente.

![image](https://github.com/user-attachments/assets/3f0d57b8-0239-43d2-aa4f-247ce8c651c3)

![image](https://github.com/user-attachments/assets/82085250-bd37-4563-9f6c-f876b2aa0cd0)

![image](https://github.com/user-attachments/assets/5819d709-cdcb-4b81-8891-35872c8f9338)

![image](https://github.com/user-attachments/assets/853b10af-3ebe-4d48-8cb0-41d5abdb1c83)




4.5 Habilitar el editor clásico de pipelines. Explicar las diferencias claves entre este tipo de editor y el editor YAML.

![image](https://github.com/user-attachments/assets/57784b3c-79da-4f78-b953-3e40319c79c3)

El editor clásico de pipelines en Azure DevOps ofrece una interfaz gráfica para configurar tareas de manera visual, ideal para usuarios no técnicos, pero no permite versionar el pipeline junto al código. Con el editor YAML utilizamos un archivo dentro del repositorio, lo que permite versionar los cambios, facilita la automatización y es más flexible para proyectos de mayor complejidad.
De manera muy resumida: El editor clásico es más sencillo de usar, pero YAML ofrece mejor escalabilidad, colaboración y control sobre el pipeline.

4.6 Crear un nuevo pipeline con el editor clásico. Descargar el resultado del pipeline y correr localmente el software compilado.

![image](https://github.com/user-attachments/assets/f50bffed-2a73-447e-ac5b-ff51eca7d4aa)

![image](https://github.com/user-attachments/assets/f815e95c-8cad-4d04-a820-98519c807053)

![image](https://github.com/user-attachments/assets/7c43a0e2-beff-42b6-b832-3ffdf9e6823b)

![image](https://github.com/user-attachments/assets/27319ca2-9fd0-452c-8052-b244bd8f4bdd)

![image](https://github.com/user-attachments/assets/30be4c5b-1670-406d-b0b8-25dd979478d7)

![image](https://github.com/user-attachments/assets/e2aa519a-065c-46a6-9db6-c68acbf3bd96)



4.7 Configurar CI en ambos pipelines (YAML y Classic Editor). Mostrar resultados de la ejecución automática de ambos pipelines al hacer un commit en la rama main.

Primero configuro CI en el pipeline hecho con el editor clasico y luego en el YAML
![image](https://github.com/user-attachments/assets/e6ffc21d-1794-474c-8a8c-51a954ebd452)

![image](https://github.com/user-attachments/assets/855fec93-81d4-43f3-8e86-8a2da29f02cf)

![image](https://github.com/user-attachments/assets/6710f3b6-d5d0-4c42-b5fc-70181cd2d3df)

Vemos como automaticamente se estaban actualizando ambos pipelines

![image](https://github.com/user-attachments/assets/1a8dfb11-bc7c-495f-b135-043f123362a9)

![image](https://github.com/user-attachments/assets/7c646e7c-804d-4e8c-8166-facb4d2e70be)


4.8 Explicar la diferencia entre un agente MS y un agente Self-Hosted. Qué ventajas y desventajas hay entre ambos? Cuándo es conveniente y/o necesario usar un Self-Hosted Agent?


Un agente de Microsoft (MS) es una máquina virtual preconfigurada y gestionada por Azure DevOps en la nube. Ofrece una configuración rápida y sin necesidad de mantenimiento del hardware, lo que lo hace ideal para proyectos con necesidades comunes. Su desventaja es que tiene limitaciones en la personalización y puede tener tiempos de espera en entornos con alta demanda.

Por otro lado, un agente Self-Hosted es una máquina física o virtual que tú configuras y gestionas. Ofrece mayor control y personalización, siendo útil cuando necesitas herramientas específicas, mayor capacidad de procesamiento o evitar las restricciones de los agentes MS. Sin embargo, requiere más mantenimiento y administración. Es recomendable usar Self-Hosted Agents cuando necesitas integración con infraestructuras locales, recursos especiales o para evitar costos adicionales por tiempo de ejecución.


4.8 Crear un Pool de Agentes y un Agente Self-Hosted

![image](https://github.com/user-attachments/assets/db3d9bb0-6f45-4a23-b48e-5d86e321ebbe)

4.9 Instalar y correr un agente en nuestra máquina local.

4.10 Crear un pipeline que use el agente Self-Hosted alojado en nuestra máquina local.


![image](https://github.com/user-attachments/assets/99bae89f-43b9-4285-b69c-84ad773cb81f)
![image](https://github.com/user-attachments/assets/3101fab9-2376-4005-bda6-912ba62ce526)
![image](https://github.com/user-attachments/assets/5f772f5d-592c-455c-b69a-5f7f157315e2)


4.11 Buscar el resultado del pipeline y correr localmente el software compilado.

![image](https://github.com/user-attachments/assets/469bdb20-2986-4a3e-a3a9-7d6ba4dfba39)

Nos encontramos con este problema que no llegue a solucionar a tiempo antes del 24?09 a las 23:59
![image](https://github.com/user-attachments/assets/2f0b075d-b622-45e8-85e0-2dab06681320)
![image](https://github.com/user-attachments/assets/fdb9e14a-6937-4361-9589-7805e535f689)







4.12 Crear un nuevo proyecto en ADO clonado desde un repo que contenga una aplicación en Angular como por ejemplo https://github.com/ingsoft3ucc/angular-demo-project.git

![image](https://github.com/user-attachments/assets/da0fc004-fc78-450d-bb78-669001bb6a02)

![image](https://github.com/user-attachments/assets/7e3fd8e3-372e-4362-a852-105415302d45)

![image](https://github.com/user-attachments/assets/42de8bc4-a940-4783-92e2-4cc1d6ff3890)


4.13 Configurar un pipeline de build para un proyecto de tipo Angular como el clonado.
![image](https://github.com/user-attachments/assets/06a35f7e-f6f5-4694-b76e-923cf3cfb801)


![image](https://github.com/user-attachments/assets/875a7ef1-27b2-42dd-9455-c7c576ec7eed)


4.14 Habilitar CI para el pipeline.

![image](https://github.com/user-attachments/assets/fbbf0075-8bcd-4545-8391-42a09faf4020)

![image](https://github.com/user-attachments/assets/115a79d4-3f90-4c8f-83a2-a012ae9b1637)



4.15 Hacer un cambio a un archivo del proyecto (algún cambio en el HTML que se renderiza por ejemplo) y verificar que se ejecute automáticamente el pipeline.

![image](https://github.com/user-attachments/assets/79c71a6a-fa09-4910-8636-1f82637c3a29)

![image](https://github.com/user-attachments/assets/492c34df-5ad9-4c61-a8ea-909d8069aead)

![image](https://github.com/user-attachments/assets/7331999a-35ca-4fd1-9521-378846d084b0)


4.16 Descargar el resultado del pipeline y correr en un servidor web local el sitio construido.

![image](https://github.com/user-attachments/assets/b8057b39-1c85-448b-8e25-9ed1dbedfdf8)

![image](https://github.com/user-attachments/assets/ad19fef8-f726-4333-a004-a9024aa0cc7b)

Podemos ver que cambio el footer

4.17 Mostrar el antes y el después del cambio.

![image](https://github.com/user-attachments/assets/11b174be-60b0-4c92-9e69-d3f5df90e93a)

![image](https://github.com/user-attachments/assets/2f0d4b82-93f6-454d-a413-083c1a8747df)




