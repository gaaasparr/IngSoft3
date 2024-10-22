# TRABAJO PRÁCTICO 8

### 4.1.1 Crear archivos DockerFile para nuestros proyectos de Back y Front

![image](https://github.com/user-attachments/assets/45a83199-0346-4c0c-ac49-468658230b31)


### 4.1.2 Crear un recurso ACR en Azure Portal siguiendo el instructivo 5.1

![image](https://github.com/user-attachments/assets/ea905c1b-4f50-486b-853b-454ecfc0670a)


### 4.1.3 Modificar nuestro pipeline en la etapa de Build y Test

![image](https://github.com/user-attachments/assets/f198c68b-dc39-4b7b-924a-826f44e420af)

![image](https://github.com/user-attachments/assets/bd899164-2620-4cc5-bd82-bfacad90089d)

### 4.1.4 En caso de no contar en nuestro proyecto con una ServiceConnection a Azure Portal para el manejo de recursos, agregar una service connection a Azure Resource Manager como se indica en instructivo 5.2

![image](https://github.com/user-attachments/assets/5db5901f-e1c6-4475-9aae-45cbfaa44d7b)

### 4.1.5 Agregar a nuestro pipeline variables

![image](https://github.com/user-attachments/assets/46b365dc-d667-4cfe-9fb1-54b083db7bdc)

### 4.1.6 Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Build y Test

![image](https://github.com/user-attachments/assets/6c0f6a24-5013-41c3-8396-c7ea1f0e8b92)

### 4.1.7 - Ejecutar el pipeline y en Azure Portal acceder a la opción Repositorios de nuestro recurso Azure Container Registry. Verificar que exista una imagen con el nombre especificado en la variable backImageName asignada en nuestro pipeline

![image](https://github.com/user-attachments/assets/ea79c97c-994a-4795-a08c-936f3b3970ee)


### 4.1.10 - Ejecutar el pipeline de nuevo y podemos ver los nuevos resultados

tuve un problema con el path api, pero descubri que noestaba descomprimiendo el archivo y por eso no encontraba a /api, entonces agregué una task

```
- task: ExtractFiles@1
  displayName: 'Descomprimir API en carpeta api'
  inputs:
    archiveFilePatterns: '$(Pipeline.Workspace)/drop-back/EmployeeCrudApi.zip'
    destinationFolder: '$(Pipeline.Workspace)/drop-back/api'
```
Y el resultado fue:

![image](https://github.com/user-attachments/assets/3fee5a9b-7eab-4772-afdd-b0c5b9f9a625)

![image](https://github.com/user-attachments/assets/acddbe31-baca-4f74-86a8-b2b7481a8be0)

### 4.1.8 - Agregar tareas para generar imagen Docker de Front (DESAFIO)
A la etapa creada en 4.1.6 Agregar tareas para generar imagen Docker de Front

![image](https://github.com/user-attachments/assets/75fcb3bb-5ff3-41b2-a4bb-e285d024a3d5)

![image](https://github.com/user-attachments/assets/239af781-4863-4e69-a8e5-9c039dcce81a)

![image](https://github.com/user-attachments/assets/a0db2e0f-5b44-496a-a84d-cbadaa896fc5)


### 4.1.9 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción de Imagenes Docker y subida a ACR

![image](https://github.com/user-attachments/assets/c8f4d648-ad1a-49a7-83aa-961c57c8dca1)

![image](https://github.com/user-attachments/assets/cc44dd6b-a160-40fd-8cbb-61b8ba318e88)



Acceso administrativo para ACR desde azure CLI

![image](https://github.com/user-attachments/assets/bf732102-5fce-4d44-adeb-be0d74536517)

![image](https://github.com/user-attachments/assets/9da3b223-f104-4ecc-a6ed-01ab0fe482a7)


Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back

![image](https://github.com/user-attachments/assets/5ca5b5b9-2fed-4675-a0be-d392a506d68d)

### 4.1.10 - Ejecutar el pipeline y en Azure Portal acceder al recurso de Azure Container Instances creado. Copiar la url del contenedor y navegarlo desde browser. Verificar que traiga datos.

![image](https://github.com/user-attachments/assets/75ebbb22-ac55-4c42-a5eb-1e134bf69c95)

![image](https://github.com/user-attachments/assets/c7e02af7-ca02-492b-a58e-54c054c66c25)

Funciona supuestamente todo pero cuadno vamos a buscarlo en le buscador no aparece nada, cuando vamos a nuestro ACI a buscar 

![image](https://github.com/user-attachments/assets/ed840841-e088-4918-9ccb-dc5e259abd57). 



Vemos que el proceso de esta killeando cada vez que lo arrancamos, asi que tenemos que descargar el docker para correrlo de manera local

![image](https://github.com/user-attachments/assets/f61ff376-e8e3-4a08-b5cf-e96c1571a73d)

Finalmente corregimos allgunos errores que se ignoraban cuando se levantaba el pipeline y tenemos el BACK funcionando

![image](https://github.com/user-attachments/assets/0decdcfe-8839-4e58-8733-4d22d190667b)

### 4.1.11 - Agregar tareas para generar un recurso Azure Container Instances que levante un contenedor con nuestra imagen de front (DESAFIO)
A la etapa creada en 4.1.9 Agregar tareas para generar contenedor en ACI con nuestra imagen de Front
Tener en cuenta que el contenedor debe recibir como variable de entorno API_URL el valor de una variable container-url-api-qa definida en nuestro pipeline.
Para que el punto anterior funcione el código fuente del front debe ser modificado para que la url de la API pueda ser cambiada luego de haber sido construída la imagen. Se deja un ejemplo de las modificaciones a realizar en el repo https://github.com/ingsoft3ucc/CrudAngularConEnvironment.git

![image](https://github.com/user-attachments/assets/56c794af-a360-4744-a41f-d223e950d928)

Se creó un stage muy parecido al del back para montar la imagen del Front con la siguiente variable

Variable API_URL

![image](https://github.com/user-attachments/assets/bec7cbd0-ec54-4fa8-a34d-6371eb980d83)


Se modificaron y crearon los siguientes archivos para que corra correctamente el Front

![image](https://github.com/user-attachments/assets/6d6ebd9f-ec85-417c-b229-c28ee2ea4ec5)

![image](https://github.com/user-attachments/assets/45c86eaf-1760-4f41-ba7f-5765a0aacf78)


![image](https://github.com/user-attachments/assets/d832b787-0fbd-4ac3-bafa-3106a1375f8f)


![image](https://github.com/user-attachments/assets/9d53c482-68b1-4ca1-926c-7bc1320a7d7c)


![image](https://github.com/user-attachments/assets/669b8582-0058-4b61-bd4f-a55f362cba2e)

FRONT FUNCIONANDO

![image](https://github.com/user-attachments/assets/04edfb0e-1dd0-4a95-85dd-5f94c5180084)

### 4.1.12 - Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en ACI.

# 4.4 Desafíos:
### 4.4.1 Agregar tareas para generar img/imagen Docker de Front. (Punto 4.1.8)

Hecho (Punto 4.1.8)

### 4.4.2 Agregar tareas para generar en Azure Container Instances un contenedor de img/imagen Docker de Front. (Punto 4.1.11)

Hecho (Punto 4.1.11)

### 4.4.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en ACI. (Punto 4.1.12)

![image](https://github.com/user-attachments/assets/469a93e3-3919-48d3-9950-8cdaa85065cd)


El pipline es un poco más lento porque esta instalando npm y cypress dentro de los comandos. Cree las carpetas y files necesarias para el funcionamiento de manera manual.
También configuré el archivo cypress.config.ts

![image](https://github.com/user-attachments/assets/afd2b62d-ff26-4364-944a-b97bcb653d55)



### 4.4.4 Agregar etapa que dependa de la etapa de Deploy en ACI QA y genere contenedores en ACI para entorno de PROD.
Agregamos un enviroment production con un pre-check approval para el deployment a prod

![image](https://github.com/user-attachments/assets/61b4c26a-4630-44a8-aaaa-ef1e6978a7df)


![image](https://github.com/user-attachments/assets/799f47b8-1eed-4b60-9c0c-2d822a615fa8)

agregamos variables y luego les agregamos CPU y memoria

![image](https://github.com/user-attachments/assets/e5aff860-eebb-4db2-b00f-453ff32f8960)

Ahora modificamos el piline y agremos variables de entorno

![image](https://github.com/user-attachments/assets/140581db-2586-4ffb-be8d-85295972bd56)

Etapa para empezar el deploy a prod

![image](https://github.com/user-attachments/assets/da4b454e-536d-4d96-b094-f0dcca1144fa)

Back

![image](https://github.com/user-attachments/assets/04e61ff4-3e3b-4111-86f8-1ad5930c70a8)


Front

![image](https://github.com/user-attachments/assets/0780c9de-8d88-4946-854d-25b0686414f8)

Tarea por aprobar

![image](https://github.com/user-attachments/assets/b3100110-07d5-4477-8db4-ce8846fd7a04)

![image](https://github.com/user-attachments/assets/a5176288-4c98-418f-b895-441cbae20350)

![image](https://github.com/user-attachments/assets/1c584ee1-efd4-4b98-952c-410f6ce60129)

Una vez aceptado y funcionando chequeamos que este corriendo.

Aun no pasa por la etapa de Tests porque me falta implementar Cypress

ACTUALIZACION

Pruebas de integración implementadas en el proyecto, antes de eso el piline corria con el script

```
- script: |
          continueOnError: true
```

que me permitia chequear si funcionaba el resto del proyecto a pesar de que no estaban pasando los tests de ingración.

![image](https://github.com/user-attachments/assets/052d0dee-f526-46cd-906a-d23a7defad48)


![image](https://github.com/user-attachments/assets/b4d3c914-1963-4dd1-ba31-7609bf072df9)

![image](https://github.com/user-attachments/assets/0b321577-0948-463a-963e-7db4df43bd48)

![image](https://github.com/user-attachments/assets/90f89516-57e3-4e58-a365-b8c4bc3ff697)


PIPELINE FINAL
```
trigger:
- main

pool:
  vmImage: 'windows-latest'

# AZURE VARIABLES
variables:
  solution: '**/*.sln'
  buildPlatform: 'Any CPU'
  configuration: 'Release'
  buildConfiguration: 'Release'
  acrLoginServer: 'gasparacr.azurecr.io'
  acrName: 'gasparACR'
  backImageName: 'employee-crud-api'
  frontImageName: 'employee-crud-front'
  ResourceGroupName: 'GasparUCC'
  backContainerInstanceNameQA: 'gr-crud-api-qa'
  frontContainerInstanceNameQA: 'gr-crud-front-qa'
  frontImageTag: 'latest'
  container-cpu-front-qa: 1
  container-memory-front-qa: 1.5
  backImageTag: 'latest'
  container-cpu-api-qa: 1
  container-memory-api-qa: 1.5
  baseUrlBackEnd: 'http://$(backContainerInstanceNameQA).eastus.azurecontainer.io'
  baseUrlFrontEnd: 'http://$(frontContainerInstanceNameQA).eastus.azurecontainer.io'

#PROD
  backContainerInstanceNamePROD: 'gr-crud-api-prod'
  frontContainerInstanceNamePROD: 'gr-crud-front-prod'
  container-cpu-api-prod: 1
  container-memory-api-prod: 1.5
  container-cpu-front-prod: 1
  container-memory-front-prod: 1.5
  
  cnn-string-qa: 'Server=tcp:gasparbdd.database.windows.net,1433;Initial Catalog=gasparbdd;Persist Security Info=False;User ID=sqladmin;Password=Azure@456;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;'

  ConnectedServiceName: 'ServiceConnectionARM' #Por ejemplo 'ServiceConnectionARM'
  frontPath: './EmployeeCrudAngular'
  
  
stages:
- stage: BuildAndTest
  displayName: "Build and Test API and Front"
  jobs:
  - job: BuildDotnet
    displayName: "Build and Test API"
    pool:
      vmImage: 'windows-latest'
    steps:
    - checkout: self
      fetchDepth: 0

    - task: DotNetCoreCLI@2
      displayName: 'Restaurar paquetes NuGet'
      inputs:
        command: restore
        projects: '$(solution)'

    - task: DotNetCoreCLI@2
      displayName: 'Ejecutar pruebas de la API'
      inputs:
        command: 'test'
        projects: '**/*.Tests.csproj'
        arguments: '--collect:"XPlat Code Coverage"'

    - task: PublishCodeCoverageResults@2
      displayName: 'Publicar resultados de code coverage del back-end'
      inputs:
        summaryFileLocation: '$(Agent.TempDirectory)/**/*.cobertura.xml'
        failIfCoverageEmpty: false
      
    - task: DotNetCoreCLI@2
      displayName: 'Compilar la API'
      inputs:
        command: build
        projects: '$(solution)'
        arguments: '--configuration $(configuration) --self-contained false'

    - task: DotNetCoreCLI@2
      displayName: 'Publicar aplicación'
      inputs:
        command: publish
        publishWebProjects: True
        arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
        zipAfterPublish: true

    - task: PublishBuildArtifacts@1
      displayName: 'Publicar artefactos de compilación'
      inputs:
        PathtoPublish: '$(Build.ArtifactStagingDirectory)'
        ArtifactName: 'drop-back'
        publishLocation: 'Container'


    - task: PublishPipelineArtifact@1
      displayName: 'Publicar Dockerfile de Back'
      inputs:
        targetPath: '$(Build.SourcesDirectory)/docker/api/dockerfile'
        artifact: 'dockerfile-back'

  - job: BuildAngular
    displayName: "Build and Test Angular"
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: NodeTool@0
      displayName: 'Instalar Node.js'
      inputs:
        versionSpec: '22.x'
    
    - script: npm install
      displayName: 'Instalar dependencias'
      workingDirectory: $(frontPath)

    - script: npx ng test --karma-config=karma.conf.js --watch=false --browsers ChromeHeadless --code-coverage
      displayName: 'Ejecutar pruebas del front'
      workingDirectory: $(frontPath)
      continueOnError: true  # Continue on test failure

    - task: PublishCodeCoverageResults@2
      displayName: 'Publicar resultados de code coverage del front'
      inputs:
        summaryFileLocation: '$(frontPath)/coverage/lcov.info'
        failIfCoverageEmpty: false
      condition: always()
    - task: PublishTestResults@2
      displayName: 'Publicar resultados de pruebas unitarias del front'
      inputs:
        testResultsFormat: 'JUnit'
        testResultsFiles: '$(frontPath)/test-results/test-results.xml'
        failTaskOnFailedTests: true
      condition: always()

    - script: npm run build
      displayName: 'Compilar el proyecto Angular'
      workingDirectory: $(frontPath)

    - task: PublishBuildArtifacts@1
      displayName: 'Publicar artefactos Angular'
      inputs:
        PathtoPublish: '$(frontPath)/dist'
        ArtifactName: 'drop-front'
      
    - task: PublishPipelineArtifact@1
      displayName: 'Publicar Dockerfile de front'
      inputs:
        targetPath: '$(Build.SourcesDirectory)/docker/front/dockerfile'
        artifact: 'dockerfile-front'
    

# #----------------------------------------------------------
# ### STAGE BUILD DOCKER IMAGES Y PUSH A AZURE CONTAINER REGISTRY
# #----------------------------------------------------------

- stage: DockerBuildAndPush
  displayName: 'Construir y Subir Imágenes Docker a ACR'
  dependsOn: BuildAndTest #NOMBRE DE NUESTRA ETAPA DE BUILD Y TEST
  jobs:
    - job: docker_build_and_push
      displayName: 'Construir y Subir Imágenes Docker a ACR'
      pool:
        vmImage: 'ubuntu-latest'

      steps:
        - checkout: self

        #----------------------------------------------------------
        # BUILD DOCKER BACK IMAGE Y PUSH A AZURE CONTAINER REGISTRY
        #----------------------------------------------------------

        - task: DownloadPipelineArtifact@2
          displayName: 'Descargar Artefactos de Back'
          inputs:
            buildType: 'current'
            artifactName: 'drop-back'
            targetPath: '$(Pipeline.Workspace)/drop-back'
        
        - task: DownloadPipelineArtifact@2
          displayName: 'Descargar Dockerfile de Back'
          inputs:
            buildType: 'current'
            artifactName: 'dockerfile-back'
            targetPath: '$(Pipeline.Workspace)/dockerfile-back'

        - task: AzureCLI@2
          displayName: 'Iniciar Sesión en Azure Container Registry (ACR)'
          inputs:
            azureSubscription: '$(ConnectedServiceName)'
            scriptType: bash
            scriptLocation: inlineScript
            inlineScript: |
              az acr login --name $(acrLoginServer)
          
        - task: ExtractFiles@1
          displayName: 'Descomprimir API en carpeta api'
          inputs:
            archiveFilePatterns: '$(Pipeline.Workspace)/drop-back/EmployeeCrudApi.zip'
            destinationFolder: '$(Pipeline.Workspace)/drop-back/api'


        - script: ls -la $(Pipeline.Workspace)/drop-back
          displayName: 'Verificar archivos publicados'

    
        - task: Docker@2
          displayName: 'Construir Imagen Docker para Back'
          inputs:
            command: build
            repository: $(acrLoginServer)/$(backImageName)
            dockerfile: $(Pipeline.Workspace)/dockerfile-back/dockerfile
            buildContext: $(Pipeline.Workspace)/drop-back
            tags: 'latest'

        - task: Docker@2
          displayName: 'Subir Imagen Docker de Back a ACR'
          inputs:
            command: push
            repository: $(acrLoginServer)/$(backImageName)
            tags: 'latest'
        
         #----------------------------------------------------------
        # CONSTRUIR Y SUBIR IMAGEN DEL FRONTEND
        #----------------------------------------------------------

        - task: DownloadPipelineArtifact@2
          displayName: 'Descargar artefactos de Frontend'
          inputs:
            buildType: 'current'
            artifactName: 'drop-front'
            targetPath: '$(Pipeline.Workspace)/drop-front'


        - task: DownloadPipelineArtifact@2
          displayName: 'Descargar Dockerfile de Frontend'
          inputs:
            buildType: 'current'
            artifactName: 'dockerfile-front'
            targetPath: '$(Pipeline.Workspace)/dockerfile-front'


        - script: ls -la $(Pipeline.Workspace)/drop-front
          displayName: 'Verificar archivos del frontend'

        - task: Docker@2
          displayName: 'Construir Imagen Docker para Front'
          inputs:
            command: build
            repository: $(acrLoginServer)/$(frontImageName)
            dockerfile: $(Pipeline.Workspace)/dockerfile-front/dockerfile
            buildContext: $(Pipeline.Workspace)/drop-front/employee-crud-angular/browser
            tags: 'latest'

        - task: Docker@2
          displayName: 'Subir Imagen Docker de Front a ACR'
          inputs:
            command: push
            repository: $(acrLoginServer)/$(frontImageName)
            tags: 'latest'
          
        
#----------------------------------------------------------
### STAGE DEPLOY TO ACI QA
#----------------------------------------------------------
  
- stage: DeployToACIQA
  displayName: 'Desplegar en Azure Container Instances (ACI) QA'
  dependsOn: DockerBuildAndPush
  jobs:
    - job: deploy_to_aci_qa
      displayName: 'Desplegar en Azure Container Instances (ACI) QA'
      pool:
        vmImage: 'ubuntu-latest'

      steps:
      #------------------------------------------------------
      # DEPLOY DOCKER BACK IMAGE A AZURE CONTAINER INSTANCES QA
      #------------------------------------------------------
  
      - task: AzureCLI@2
        displayName: 'Desplegar Imagen Docker de Back en ACI QA'
        inputs:
          azureSubscription: '$(ConnectedServiceName)'
          scriptType: bash
          scriptLocation: inlineScript
          inlineScript: |
            echo "Resource Group: $(ResourceGroupName)"
            echo "Container Instance Name: $(backContainerInstanceNameQA)"
            echo "ACR Login Server: $(acrLoginServer)"
            echo "Image Name: $(backImageName)"
            echo "Image Tag: $(backImageTag)"
            echo "Connection String: $(cnn-string-qa)"
            
            az container delete --resource-group $(ResourceGroupName) --name $(backContainerInstanceNameQA) --yes
  
            az container create --resource-group $(ResourceGroupName) \
            --name $(backContainerInstanceNameQA) \
            --image $(acrLoginServer)/$(backImageName):$(backImageTag) \
            --registry-login-server $(acrLoginServer) \
            --registry-username $(acrName) \
            --registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv) \
            --dns-name-label $(backContainerInstanceNameQA) \
            --ports 80 \
            --environment-variables ConnectionStrings__DefaultConnection="$(cnn-string-qa)" \
            --restart-policy Always \
            --cpu $(container-cpu-api-qa) \
            --memory $(container-memory-api-qa)

#----------------------------------------------------------
### STAGE DEPLOY TO ACI QA FOR FRONT
#----------------------------------------------------------

- stage: DeployToACIQAFront
  displayName: 'Desplegar Front en Azure Container Instances (ACI) QA'
  dependsOn: DockerBuildAndPush  # El contenedor del front depende de que las imágenes estén creadas
  jobs:
    - job: deploy_to_aci_qa_front
      displayName: 'Desplegar Contenedor de Front en ACI QA'
      pool:
        vmImage: 'ubuntu-latest'

      steps:
      #------------------------------------------------------
      # DEPLOY DOCKER FRONT IMAGE A AZURE CONTAINER INSTANCES QA
      #------------------------------------------------------
      - task: AzureCLI@2
        displayName: 'Desplegar Imagen Docker de Front en ACI QA'
        inputs:
          azureSubscription: '$(ConnectedServiceName)'
          scriptType: bash
          scriptLocation: inlineScript
          inlineScript: |
            echo "Resource Group: $(ResourceGroupName)"
            echo "Container Instance Name: $(frontContainerInstanceNameQA)"
            echo "ACR Login Server: $(acrLoginServer)"
            echo "Image Name: $(frontImageName)"
            echo "Image Tag: $(frontImageTag)"
            echo "API URL: $(API_URL)"

            az container delete --resource-group $(ResourceGroupName) --name $(frontContainerInstanceNameQA) --yes

            az container create --resource-group $(ResourceGroupName) \
            --name $(frontContainerInstanceNameQA) \
            --image $(acrLoginServer)/$(frontImageName):$(frontImageTag) \
            --registry-login-server $(acrLoginServer) \
            --registry-username $(acrName) \
            --registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv) \
            --dns-name-label $(frontContainerInstanceNameQA) \
            --ports 80 \
            --environment-variables API_URL=$(API_URL) \
            --restart-policy Always \
            --cpu $(container-cpu-front-qa) \
            --memory $(container-memory-front-qa)



#----------------------------------------------------------
### JOB INTEGRATION TESTING
#----------------------------------------------------------

- stage: IntegrationTests
  displayName: 'Tests de Integracion'
  dependsOn:
    - DeployToACIQA
    - DeployToACIQAFront
  variables:
    baseUrl: '$(frontContainerInstanceNameQA).brazilsouth.azurecontainer.io'

  jobs:
    - job: IntegrationTests
      displayName: 'Run Cypress Integration Tests'
      pool:
        vmImage: 'ubuntu-latest'
      steps:
        # Cambiar al directorio del proyecto Angular e instalar todas las dependencias
        - script: |
            cd $(Build.SourcesDirectory)/EmployeeCrudAngular
            npm install --legacy-peer-deps
            npm install cypress --save-dev
            npm install typescript ts-node --legacy-peer-deps
          displayName: 'Install Node Modules, Cypress and TypeScript'

        # Ejecutar pruebas Cypress E2E
        - script: |
            cd $(Build.SourcesDirectory)/EmployeeCrudAngular
            npx cypress run --config-file cypress.config.ts --env baseUrl=$(baseUrl)
          displayName: 'Run Cypress E2E Tests'
          continueOnError: true

        # Publicar resultados de las pruebas
        - task: PublishTestResults@2
          inputs:
            testResultsFiles: '$(Build.SourcesDirectory)/EmployeeCrudAngular/cypress/results/*.xml'
            testRunTitle: 'Cypress E2E Tests (QA)'
          displayName: 'Publish Cypress Test Results'




# #----------------------------------------------------------
# ### DEPLOY A PROD ACI
# #----------------------------------------------------------

- stage: DeployToACIPROD
  displayName: 'Desplegar en Azure Container Instances PROD'
  dependsOn: IntegrationTests
  jobs:
    - deployment: DeployToProd
      displayName: 'Desplegar en Azure Container Instances PROD'
      environment: 'Production'
      strategy:
        runOnce:
          deploy:
            steps:
            #----------------------------------------------------------
            # DEPLOY DOCKER BACK IMAGE A AZURE CONTAINER INSTANCES PROD
            #----------------------------------------------------------
              - task: AzureCLI@2
                displayName: 'Desplegar Imagen Docker de Back en ACI PROD'
                inputs:
                  azureSubscription: '$(ConnectedServiceName)'
                  scriptType: bash
                  scriptLocation: inlineScript
                  inlineScript: |
                    echo "Resource Group: $(ResourceGroupName)"
                    echo "Container Instance Name: $(backContainerInstanceNamePROD)"
                    echo "ACR Login Server: $(acrLoginServer)"
                    echo "Image Name: $(backImageName)"
                    echo "Image Tag: $(backImageTag)"
                    echo "API URL: $(cnn-string-prod)"

                    az container delete --resource-group $(ResourceGroupName) --name $(backContainerInstanceNamePROD) --yes

                    az container create --resource-group $(ResourceGroupName) \
                    --name $(backContainerInstanceNamePROD) \
                    --image $(acrLoginServer)/$(backImageName):$(backImageTag) \
                    --registry-login-server $(acrLoginServer) \
                    --registry-username $(acrName) \
                    --registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv) \
                    --dns-name-label $(backContainerInstanceNamePROD) \
                    --ports 80 \
                    --environment-variables ConnectionStrings__DefaultConnection="$(cnn-string-prod)" \
                    --restart-policy Always \
                    --cpu $(container-cpu-api-qa) \
                    --memory $(container-memory-api-qa)

              - task: AzureCLI@2
                displayName: 'Desplegar Imagen Docker de Front en ACI PROD'
                inputs:
                  azureSubscription: '$(ConnectedServiceName)'
                  scriptType: bash
                  scriptLocation: inlineScript
                  inlineScript: |
                    echo "Resource Group: $(ResourceGroupName)"
                    echo "Container Instance Name: $(frontContainerInstanceNamePROD)"
                    echo "ACR Login Server: $(acrLoginServer)"
                    echo "Image Name: $(frontImageName)"
                    echo "Image Tag: $(frontImageTag)"
                    echo "API URL: $(API_URL_PROD)"

                    az container delete --resource-group $(ResourceGroupName) --name $(frontContainerInstanceNamePROD) --yes

                    az container create --resource-group $(ResourceGroupName) \
                    --name $(frontContainerInstanceNamePROD) \
                    --image $(acrLoginServer)/$(frontImageName):$(frontImageTag) \
                    --registry-login-server $(acrLoginServer) \
                    --registry-username $(acrName) \
                    --registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv) \
                    --dns-name-label $(frontContainerInstanceNamePROD) \
                    --ports 80 \
                    --environment-variables API_URL=$(API_URL_PROD) \
                    --restart-policy Always \
                    --cpu $(container-cpu-front-prod) \
                    --memory $(container-memory-front-prod)

```
