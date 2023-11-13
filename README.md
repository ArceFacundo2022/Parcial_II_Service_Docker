# Parcial Docker-Swarm-Rest-Soap

## Alumno: Arce Facundo

## Configuración del Entorno

1. **Clonar el Repositorio:**

   git clone <URL del repositorio>
   cd <nombre-del-repositorio>

2. **Pasos a seguir:**

1- Cree una nueva carpeta que englobe completamente los 4 servicios, y luego cree las cuatro carpetas una por cada servicio que contendran todo el codigo y paguinas para levantar imagenes.

2- comenzando con la carpeta db ahi se encuentra el docker file para levantar la imagen y un archivo datos.sql que contendra los comandos en sql para crear la tabla de personas al momento de crear los contenedores.

   En esta carpeta utilize estos comandos

	docker build -t image_swarm_basededatos . --> me para en la carpeta de la bd
	docker run -p 3306:3306 --name basededatos_container -e MYSQL_ROOT_PASSWORD=root1 -d image_swarm_basededatos --> (Por si se desea probar que la img actue bien)

3- luego comienzo con la carpeta rest_service en la cual contendra el docker file y los archivos para levantar el servicio REST para insertar un nuevo registro en la tabla de personas

	docker build -t image_swarm_rest . ---> creo la imagen de mi rest_service
	docker run -p 8080:8080 --name rest_service_container -d image_swarm_rest  --> (Por si se desea probar que la img actue bien)


4- Ahora en la carpeta soap-service coloco los archivos e docker file para ser usados para levantar la img del servicio soap

	docker build -t image_swarm_soap .  ---> me pocisiono en la carpeta soap_service
	docker run -p 8888:8888 --name soap_service_container -d image_swarm_soap  --> (Por si se desea probar que la img actue bien)

5- Creo una carpeta front que contrenda un index.html que es donde se mostrar todo y se hara las peticiones a estos servicio y su respectivo dockerfile

	docker build -t parcial_swarm_front_service . ---> me posiciono en la carpeta front 
	docker run -p 80:80 --name front_service_container -d image_swarm_front  --> (Por si se desea probar que la img actue bien)

6- Ahora que contamos con las 4 imagenes podemos levantar los servicios de cada uno

primero hago
	docker swarm init
despues inicializo el swarm
	docker stack deploy -c docker-compose.yml parcial_swarm


#### Imagenes
* Base de datos - imagen: image_swarm_basededatos
* Servicio Rest - imagen: image_swarm_rest
* Servicio Soap - imagen: image_swarm_soap 
* Front - imagen: image_swarm_front

### Inicializar Docker Swarm

	1)- docker swarm init
	2)- docker stack deploy -c docker_compose.yml parcial_swarm