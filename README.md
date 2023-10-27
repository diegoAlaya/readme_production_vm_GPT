# Readme Production VM GPT

### Notas:
- Todas las configuraciones de NGINX se encuentran listas, por lo que solo es necesario levantar el servicio y/o reiniciarlo según sea el caso
- Una vez que NGINX se encuentra levantado, se debe verificar su ejecucion, siempre deben existir solo 2 procesos (como se muestar en la foto), de existir mas puede haber problemas para capturar los ultimos cambios hechos al sistema. se deben cerrar todos los procesos de nginx y volver a iniciar
  
- Iniciar NGINX
```
start nginx
```

- Verificar procesos:
```
tasklist /fi "imagename eq nginx.exe"
```
![2023-10-26 19_28_35-Greenshot - copia](https://github.com/diegoAlaya/readme_production_vm_GPT/assets/90165804/0b8a4845-3efe-474c-b5a4-e7df57083b39)

- Cerrar NGINX
```
nginx -s quit
```



# Levantar Aplicación

1. Acceder a Máquina Virtual de Azure
2. Tanto el Backend como Frontend se encuentras en carpeta de **Documents/Github**
    -  gpt_alaya_bot
    -  alaya_documentsAI_front
3. Es recomendable levantar uno a uno los servicios solamente por temas de orden, en este caso:
    - gpt_alaya_bot
    - NGINX
    - _alaya_documentsAI_front_ no es necesario iniciar, ya que el build ya se encuentra realizado, y NGINX ya esta configurado.
4. gpt_alaya_bot: 
    -  Abrir Git Bash en la carpeta raiz del repositorio y ejecutar los siguientes comandos:
```
python -m venv venv
```
```
uvicorn main:app --reload --host 0.0.0.0 --port 81
```
![back](https://github.com/diegoAlaya/readme_production_vm_GPT/assets/90165804/c0367a0f-fd12-4f72-836d-36a0837ccfb0)

4. NGINX:
    - Ir al directorio **Documents/nginx-1.24.0** 
    - Se puede ejecutar NGINX a traves del .exe, recomiendo usar la linea de comando CMD.EXE para verificar los procesos corriendo de NGINX
    - Ir a la barra de la URL, escribir **CMD**, esto abirar CMD directo en el directorio y ejectar:
```
start nginx
```
![2023-10-26 19_32_43-Greenshot](https://github.com/diegoAlaya/readme_production_vm_GPT/assets/90165804/bd150323-e086-4baa-b74a-2e00557506bd)

-  Verificar procesos en ejecución

![2023-10-26 19_27_40-Greenshot](https://github.com/diegoAlaya/readme_production_vm_GPT/assets/90165804/353d2bac-ec61-40d4-9763-4c70eb9b1e67)

-  Acceder desde la dirección


```
http://20.127.237.59:80
```

## Actualización de app
-  Se encuentra instalado github desktop, por lo que a través del mismo solo es necesario realizar el fetch o pull en cada repositorio correspondiente.
###### Imagen de referencia:

![image](https://github.com/diegoAlaya/readme_production_vm_GPT/assets/90165804/b3d8cff7-5d76-4f25-a2d1-d0cfe5ec4a49)

-  Reinicar el backend de ser necesario con los comando ya descritos
-  Se puede actualizar todos los códigos sin necesidad de bajar el servicio de NGINX, solo basta con recargar los servicios de NGINX con el commando después de haber hecho las correspondientes actualizaciones:
```
nginx -s reload
```
