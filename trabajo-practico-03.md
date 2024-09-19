Trabajo Práctico 3 - Introducción a Azure Devops
1- Objetivos de Aprendizaje
Familiarizarse con la plataforma Azure Devops
2- Consignas a desarrollar en el trabajo práctico:
¿Qué es Azure DevOps?

Azure DevOps es una plataforma de Microsoft que ofrece un conjunto integrado de herramientas para la colaboración en el desarrollo de software. Permite a los equipos gestionar todo el ciclo de vida del desarrollo, desde la planificación y el seguimiento de tareas hasta la integración continua, entrega continua y la gestión de la calidad del software.

Beneficios de utilizar Azure DevOps en comparación con otras soluciones.

Integración Completa: Azure DevOps ofrece una integración fluida entre planificación, desarrollo, pruebas y despliegue, lo que facilita una visión completa del proceso de desarrollo.
Soporte para Git y TFVC: Ofrece soporte tanto para Git (sistema de control de versiones distribuido) como para TFVC (Team Foundation Version Control), lo que permite a los equipos elegir la solución que mejor se adapte a sus necesidades.
Automatización de CI/CD: Con Azure Pipelines, puedes automatizar el proceso de integración y despliegue continuo, lo que acelera la entrega de software y mejora la calidad.
Gestión de Proyectos: Azure Boards proporciona herramientas de gestión de proyectos basadas en Kanban y Scrum, lo que facilita el seguimiento y la organización del trabajo.
Integración con Otras Herramientas: Se integra fácilmente con herramientas como GitHub, Jenkins, Docker y Kubernetes, permitiendo una mayor flexibilidad y compatibilidad con tecnologías modernas.

Componentes Principales de Azure DevOps

Azure Repos
Sistema de control de versiones con Git o TFVC.
Funcionalidades clave: branching, pull requests, code reviews.
Azure Pipelines
CI/CD (Integración Continua y Entrega Continua).
Creación y gestión de pipelines para la automatización de build, test y deploy.
Azure Boards
Gestión de proyectos con Kanban y Scrum.
Seguimiento de tareas, bugs, y trabajo en curso.
Azure Artifacts
Gestión de paquetes (NuGet, npm, Maven).
Uso de feeds para compartir artefactos entre equipos.
Azure Test Plans
Herramientas para pruebas manuales y automatizadas.
Gestión de casos de prueba y reportes de calidad.
Integración con otras herramientas

GitHub, Jenkins, Docker, Kubernetes.
Marketplace de extensiones

Añadir funcionalidades adicionales a Azure DevOps.
3- Pasos del TP
3.1 Crear una cuenta en Azure DevOps

![image](https://github.com/user-attachments/assets/d8cbb488-b54e-4ef3-b654-0e8f3bc5d042)


3.2 Crear un proyecto Sample01
Primero le di acceso publico a todos

![image](https://github.com/user-attachments/assets/39455e3f-18c0-4f3e-a3b1-e8042ff2eec5)
Despues cree el proyecto

![image](https://github.com/user-attachments/assets/6abf3520-b765-4662-b19e-41f74e8618e0)


3.3 Crear un repo GIT desde cero
Cree un repo desde el panel de Azure

![image](https://github.com/user-attachments/assets/fc3b7111-2122-4cf1-b691-2f7d9b7041d9)
![image](https://github.com/user-attachments/assets/1fb41400-d632-4260-b612-90bbd2860f57)



3.4 Crear un proyecto Sample02

![image](https://github.com/user-attachments/assets/8de3de1b-ac95-4276-9b4f-f6c0361a5524)



3.5 Importar un repo desde GitHub: https://github.com/ingsoft3ucc/SimpleWebAPI.git

![image](https://github.com/user-attachments/assets/96560b13-43ba-4221-ae89-09df20a10419)
![image](https://github.com/user-attachments/assets/b3ece731-1c2a-414a-8abb-ff8c82e4bf80)
![image](https://github.com/user-attachments/assets/8230fd97-c7df-4fc5-bafe-938fc7e7dd80)


3.6 Realizar un cambio en un archivo, y subirlo al repo de ADO.

![image](https://github.com/user-attachments/assets/48cfd0b7-e405-49c4-8b10-113196f8c64b)


3.7 Crear un pipeline, solicitar acceso a jobs de paralelismo

![image](https://github.com/user-attachments/assets/0709b982-633b-487f-9b39-6783fd8e525d)
![image](https://github.com/user-attachments/assets/d42639b2-1991-4cd2-83b9-48748a28764a)
![image](https://github.com/user-attachments/assets/19adb360-fffe-4187-8af6-4e70e6f38504)
![image](https://github.com/user-attachments/assets/cc8712b2-0954-4438-90b3-ad80b6e82dbc)



3.8 Cambiar el tipo de proceso de Basic a Agile

![image](https://github.com/user-attachments/assets/4d33c5b1-1855-4b22-abbb-41594c7742a2)

![image](https://github.com/user-attachments/assets/bc72abd7-f96c-4ace-abed-cd6900cdd55a)

![image](https://github.com/user-attachments/assets/6889b3bc-4ab5-4be9-90e5-40e7a17a0cff)



3.8 Crear un sprint

![image](https://github.com/user-attachments/assets/ba21c59d-88f1-4e4f-a145-c7aeefccea62)
![image](https://github.com/user-attachments/assets/ee82b650-73ae-4598-8c4c-93082fcc2903)
![image](https://github.com/user-attachments/assets/c4da8a94-2bae-47f3-a695-23e00ce91e2d)



3.9 Crear User Stories
3.10 Crear Tasks y Bugs

![image](https://github.com/user-attachments/assets/55732e6a-4db2-45de-a1bc-16c339f8ee51)


4- Presentación del trabajo práctico.


Subir un al repo con las capturas de pantalla de los pasos realizados y colocar en el excel de repos (https://docs.google.com/spreadsheets/d/1mZKJ8FH390QHjwkABokh3Ys6kMOFZGzZJ3-kg5ziELc/edit?gid=0#gid=0) la url del proyecto de AzureDevops (
