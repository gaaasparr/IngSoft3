# IngSoft3
#### 1- Instalar Git

git instalado en la pc

![image](https://github.com/user-attachments/assets/524634da-9012-4a39-8ae3-fef71a7e5428)


#### 2- Crear un repositorio local y agregar archivos
  - Se creó un repositorio local junto con su respectivo readme y con un mensaje incluido. usamos cat para ver el contenido

![image](https://github.com/user-attachments/assets/04b35fd0-3acf-4645-ae0b-22b2d715ba4d)



#### 3- Configuración del Editor Predeterminado
 - Instale Notepad ++ y para configurarlo como editor predeterminado utilicé el seguiente comando



   
#### 4- Creación de Repos 01 -> Crearlo en GitHub, clonarlo localmente y subir cambios
  - Crear una cuenta en https://github.com
  - Crear un nuevo repositorio en dicha página con el Readme.md por defecto
  ![image](https://github.com/user-attachments/assets/8d42d73f-0d9b-4b23-971a-284bd92f3d19)

  - Clonar el repo remoto en un nuevo directorio local
    ![image](https://github.com/user-attachments/assets/ab409461-149c-4744-a863-e9cd650f9e90)
    ![image](https://github.com/user-attachments/assets/a3a4bb83-dea7-4254-9cc2-d8440ecf6b8a)
    
  - Editar (o crear si no existe) el archivo .gitignore agregando los archivos *.bak
  - Crear un commit y porveer un mensaje descriptivo
    ![image](https://github.com/user-attachments/assets/6cee44ff-4db3-4cf2-9ff9-b3301f2bf8bd)

  - Intentar un push al repo remoto
![image](https://github.com/user-attachments/assets/2c316d58-8b01-45ac-8cd2-e403ffd49601)
![image](https://github.com/user-attachments/assets/34ce1acf-5281-4155-8623-6c4f0eb15d89)


  - En caso de ser necesario configurar las claves SSH requeridas y reintentar el push.

#### 5- Creación de Repos 02-> Crearlo localmente y subirlo a GitHub
  - Crear un repo local
  - Agregar archivo Readme.md con algunas lineas de texto
  - Crear repo remoto en GitHub
  - Asociar repo local con remoto
  - Crear archivo .gitignore
  - Crear un commit y proveer un mensaje descriptivo
  - Subir cambios.

#### 6- Ramas
  - Crear una nueva rama
  - Cambiarse a esa rama
  - Hacer un cambio en el archivo Readme.md y hacer commit
  - Revisar la diferencia entre ramas

#### 7- Merges
  - Hacer un merge FF
  - Borrar la rama creada
  - Ver el log de commits
  - Repetir el ejercicio 6 para poder hacer un merge con No-FF

#### 8- Resolución de Conflictos
  - Instalar alguna herramienta de comparación. Idealmente una 3-Way:
    - P4Merge https://www.perforce.com/downloads/helix-visual-client-p4v:
![alt text](p4merge.png)
    - Se puede omitir registración. Instalar solo opción Merge and DiffTool.
 - ByondCompare trial version https://www.scootersoftware.com/download.php
    - Configurar Tortoise/SourceTree para soportar esta herramienta.
    - https://www.scootersoftware.com/support.php?zz=kb_vcs
    - https://medium.com/@robinvanderknaap/using-p4merge-with-tortoisegit-87c1714eb5e2
  - Crear una nueva rama conflictBranch
  - Realizar una modificación en la linea 1 del Readme.md desde main y commitear
  - En la conflictBranch modificar la misma línea del Readme.md y commitear
  - Ver las diferencias con git difftool main conflictBranch
  - Cambiarse a la rama main e intentar mergear con la rama conflictBranch
  - Resolver el conflicto con git mergetool
  - Agregar .orig al .gitignore
  - Hacer commit y push

#### 9- Familiarizarse con el concepto de Pull Request

  - Explicar que es un pull request.
  - Crear un branch local y agregar cambios a dicho branch. 
  - Subir el cambio a dicho branch y crear un pull request.
  - Completar el proceso de revisión en github y mergear el PR al branch master.


#### 10- Algunos ejercicios online
  - Entrar a la página https://learngitbranching.js.org/
  - Completar los ejercicios **Introduction Sequence**
    ![image](https://github.com/user-attachments/assets/4426060f-ea83-4e81-bf9b-a5b5fa12b3a6)

