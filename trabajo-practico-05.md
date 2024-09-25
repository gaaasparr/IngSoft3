4- Desarrollo:
4.1. Crear una cuenta en Azure

![image](https://github.com/user-attachments/assets/346dd8d3-ddd0-44b8-a9b6-34f9b9990a85)

Es increible pero no puedo pasar el paso mas simple de validar mi identidad, ya probe con mayusculas, con numeros, sin numeros, con otros mails, con distintas tarjetas.

![image](https://github.com/user-attachments/assets/b6e2ebd3-e6bc-49b3-85ee-483274a3fc22)

Finalmente esta es mi cuenta, pedi toda la informacion de la tarjeta prestada asi que voy a intentar realizear todos los trabajos lo mas rapido posible para eliminar los datos de la tarjeta.


4.2. Crear un recurso Web App en Azure Portal y navegar a la url provista

![image](https://github.com/user-attachments/assets/d3492b3e-c8d9-4d51-abd3-b91e94cf9690)

![image](https://github.com/user-attachments/assets/355d3a91-a765-45e5-bc05-5864a29d6a00)

![image](https://github.com/user-attachments/assets/945ad280-d3ac-432e-93ab-68f13c7b1bdd)

Creamos todo segun el paso a paso visto en clase y guardamos el template para mas tarde

![image](https://github.com/user-attachments/assets/05f1a95c-1928-45f4-9c43-71ab169332b1)

![image](https://github.com/user-attachments/assets/7b2cb7fe-3a1d-4999-87bb-f6564a0d87ba)

![image](https://github.com/user-attachments/assets/9bd9a87f-eae2-4727-bf4f-01dc2828440f)

Obtuvimos el siguiente problema al querer chequear el funcionamiento de la web, pero luego reonfiguré el DNS y funcionó

![image](https://github.com/user-attachments/assets/db91c838-4370-48ef-bca7-ab00a6a7dc22)

![image](https://github.com/user-attachments/assets/ee295692-d8da-4c2e-b9a5-9453be23fbb7)


4.3. Actualizar Pipeline de Build para que use tareas de DotNetCoreCLI@2 como en el pipeline clásico, luego crear un Pipeline de Release en Azure DevOps con CD habilitada

Copie el codigo brindado en clases en el YAML de Sample 02 y corrio todo perfecto

![image](https://github.com/user-attachments/assets/1e7e5540-71fa-4b98-a2bc-c9841a92c33e)

Luego active el pipeline release manual

![image](https://github.com/user-attachments/assets/74488d00-21d5-47bd-bb12-9e39206107db)

![image](https://github.com/user-attachments/assets/211865e5-efe2-4cd8-8ed2-c590404348bf)

![image](https://github.com/user-attachments/assets/c8a96e95-fda8-470a-81bf-d3563936da68)

Tuve un problema ya que la ceutna que cree con la tarjeta que me prestaron no es la misma que donde realice el trabajo 4 entonces no encuentra mis subscripción.

![image](https://github.com/user-attachments/assets/c424ee3c-a74d-475a-9236-c6b7e50f425c)

4.4. Optimizar Pipeline de Build

El codigo ya está optimizado en el material brindado

![image](https://github.com/user-attachments/assets/71240594-0614-42b7-9536-615fb5240d3a)




4.5. Verificar el deploy en la url de la WebApp /weatherforecast

4.6. Realizar un cambio al código del controlador para que devuelva 7 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio

4.7. Clonar la Web App de QA para que contar con una WebApp de PROD a partir de un Template Deployment en Azure Portal y navegar a la url provista para la WebApp de PROD.

4.8. Agregar una etapa de Deploy a Prod en Azure Release Pipelines

4.9. Realizar un cambio al código del controlador para que devuelva 10 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast se muestra lo mismo.

4.10. Modificar pipeline de release para colocar una aprobación manual para el paso a Producción.

4.11. Realizar un cambio al código del controlador para que devuelva 5 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast aun se muestra la versión anterior.

4.12. Aprobar el pase ya sea desde el release o desde el mail recibido. image

4.12.1. Notar que se puede dar la aprobación pero posponer su aplicación hasta una determinada fecha

4.13. Esperar a la finalización de la etapa de Pase a Prod y luego corroborar que en la url de la webapp_prod/weatherforecast se muestra la nueva versión coinicidente con la de QA. image

4.14. Realizar un pipeline (no release) que incluya el deploy a QA y a PROD con una aprobación manual. El pipeline debe estar construido en YAML sin utilizar el editor clásico de pipelines ni el editor clásico de pipelines de release.
