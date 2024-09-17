# Backend 1- DOCKER PROXY
Autor(es): Buzo Zamora Elian

Ultima Actualización: 13/09/2024
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
* Abrimos una nueva terminal con nuestro software de Docker corriendo. Escribimos el comando: docker run --name minginx -d -p 8080:80 nginx. Con este comando estamos CREANDO y CORRIENDO un nuevo contenedor, le asignamos un nombre, lo corremos en segundo plano (-p) y estamos mapeando el puerto 8080 de nuestra maquina host al puerto 80 del contenedor y estamos creando dicho contenedor con la imagen de NGINX.
* Ahora accedemos al contenedor con el comando: Docker exec -it IDDELCONTENEDOR bash. Con este comando accedemos a la terminal del contenedor. Podemos indicar el ID del contenedor o bien, el nombre que le asignamos.
* Dentro del contenedor, creamos un usuario con el comando: adduser elian. Estamos creando un usuario de nombre elian. Para cambiarnos a ese usuario el comando es: su elian.
* Dentro del contendor necesitamos instalar algunos paquetes, pero para ello requerimos actualizar el manejador de paquetes de nuestro contenedor. Corremos el comando: apt update. Con esto actualizamos la lista de paquetes disponibles para descargar.
* Instalamos Python3.11 en el contendor con el sig. comando: Apt install -y Python3.11.
* Instalamos VirutalEnv con el comando: Apt Install -y python3.11-venv. VirtualEnv es una herramienta que se utiliza para crear un entorno Python aislado.
* Instalamos PIP para instalar librerías de Python. Ejecutamos el comando: apt install -y python3-pip.
* Instalamos vim que es un editor de codigo, como lo es visual studio, pero para Linux. Corremos el comando: Apt install vim.
* Después de instalar todo, accedemos al usuario que creamos con el comando: su elian.
* Dentro del usuario, accedemos a nuestra carpeta home. Para eso hacemos uso del comando: cd home. cd indica change direction, y con este comando nos podemos desplazar entre carpetas del contendor. Dentro de home debe haber una carpeta con el mismo nombre de usuario (si no la hay la creamos, ya que aqui guardaremos el proyecto, el comando es mkdir carpeta, este comando crea una carpeta en el directorio actual).
* Dentro de la carpeta de nuestro usuario, crearemos un entorno virtual. El comando es: python3 -m venv mientorno. Una vez creado entramos a dicho entorno virtual con el comando: source mientorno/bin/activate.
* Sabremos que estamos dentro del venv porque aparecera (mientorno) en la terminal. Creamos un archivo de nombre hello.py con el comando sig: vim hello.py. Vim por defecto crea un archivo si el archivo especificado no existe, en este caso se creará un archivo de nombre hello.py.
* Una vez abierto Vim, entramos al modo de Inserción y ponemos el ejemplo de Flask que viene en la página: https://flask.palletsprojects.com/en/3.0.x/quickstart/. Solo vamos a modificar el parametro de app.route, escribimos "/pagina".
* Guardamos el archivo saliendo del modo de Inserción y guardamos con :wq. Este comado guardará el archivo con los cambios realizados y saldrá del archivo.
*(Aun dentro del Entorno Virtual) procedemos a instalar Flask. Flask es un microfamework de Python para desarrollo web. Escribimos el comando: pip install flask.
Pip es un sistema de gestión de paquetes utilizado para instalar y administrar paquetes de software escritos en Python.
* A continuación nos salimos del entorno virtual con el comando: deactivate. En el contenedor nos salimos de nuestro usuario con: exit.
* En el contenedor, vamos a modificar un archivo de nombre conf.d. Nos posicionamos en la raiz del contenedor y accedemos a la siguiente ruta: /etc/nginx/conf.d. Escribimos el comando: 
cd /etc/nginx/conf.d. Si listamos los archivos (comando:ls) nos debe aparecer un archivo de nombre default.conf.  Lo abrimos con Vim. Escribimos el comando: vim default.conf.
* El codigo mostrado, no vamos a modificarle nada. Vamos a agregar un bloque de codigo que es el siguiente:
  location /pagina{
  proxy_pass http://127.0.0.1:5000;
  }
  Este location, asigna el puerto 5000 (del servidor) para desplegar nuestro hello world de     
  Python. Nosotros podemos acceder a dicho location entrando a la dirección: http://127.0.0.1:8080/pagina.
*El siguiente paso es reiniciar el contenedor por completo. Hay que salirnos de la terminal del contenedor y corremos el comando: docker restart iddelcontenedor.
* Ahora, volvemos a ingresar al contenedor, luego a nuestro usuario del docker y nuevamente entramos a nuestro entorno virtual con los comandos previamente mencionados y vamos a correr nuestra aplicacion de flask con el comando: flask --app hello run. 
* Si entramos a la pagina http://127.0.0.1:8080/ nos desplegará
  "Welcome to NGINX" lo que indica que el servidor, esta corriendo correctamente. Nótese que e  
  estamos especificando el puerto 8080, el cuál es el que mapeamos para nuestra maquina host.     Si escribimos http://127.0.0.1:8080/pagina nos desplegará el "Hello World" que hicimos con      Flask.



  
