# Backend 1- DOCKER PROXY
Autor(es): Buzo Zamora Elian

Ultima Actualización: 13/09/2024 (Sin concluir readme aun)
## Contenido
* Requisitos
* Resumen general
* Pasos a desarrollar

## Requisitos
* Software de Docker (version mas reciente)
* Imagen de Nginx (Puede obtenerla de Docker Hub)

### Resumen general
Crear un contenedor con NGINX mapeando el puerto 8080 de nuestra maquina host al puerto 80 del contenedor. Debemos crear en nuestro server un nuevo "location" (lo veremos mas adelante) para que al entrar a dicho location, el cual sera /pagina, nos despliegue un hola mundo de python usando Flask.


# Pasos a desarrollar
* Abrimos una nueva terminal con nuestro software de Docker corriendo. Escribimos el comando: docker run --name minginx -d -p 8080:80 nginx. 
* 
