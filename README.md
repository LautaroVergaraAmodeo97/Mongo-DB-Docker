# Tutorial para crear un entorno de MongoDB en Docker

En este tutorial vamos a crear un contenedor Docker para poder trabajar con MongoDB y así poder desplegar todos los proyectos que usted desee.

Espero que le sea de utilidad este tutorial y ahora vamos a comenzar a realizarlo.

# Paso a paso para la creación de MongoDB en Docker

- Paso 1

Vamos a proceder a crear un archivo compose.yml en la shell que usted está usando.

´´´
touch docker-compose.yml
´´´
El comando touch permite crear un archivo. En este caso utilizamos lo que es YAML ya que permite una fácil lectura para los humanos.

´´´
cat > docker-compose.yml
´´´
El comando cat > sirve para unir archivos y visualizarlos para una mejor lectura.

- Paso 2

Ahora vamos a proceder a crear el documento docker-compose.yml 

´´´
version: '2.2'

services:
  mongo:
  image: mongo:4.0.4
  restart: always
  container_name: monguito
  environment:
    - MONGODB_USER="user"
    - MONGODB_PASS="pass"	
    
  volumes:
    - ./monguitodata:/data/db
    - ./monguitodata/log:/var/log/mongodb/
  ports:
    - "27017:27017"     
´´´

Ahora vamos a explicar el paso a paso de cada linea para una mejor comprensión.

1-Crear un archivo YAML: Crea un archivo llamado docker-compose.yml en el directorio donde deseas mantener tus configuraciones de Docker.

2-Definir los servicios: En el archivo YAML, define los servicios que deseas ejecutar. En este caso, solo tienes un servicio llamado mongo.

3-Configurar el servicio mongo:

  *Especifica la imagen Docker que deseas utilizar. En este caso, es mongo:4.0.4.
  
  *Asegúrate de que el servicio se reinicie automáticamente en caso de falla     
  (restart: always).
  
  *Darle un nombre al contenedor utilizando container_name: monguito.
  
  *Define las variables de entorno para el usuario y la contraseña de MongoDB   
  (MONGODB_USER y MONGODB_PASS).
  
  *Configurar los volúmenes para persistir los datos y los registros.
        ./monguitodata:/data/db: Mapea el directorio local monguitodata al directorio
        ./data/db dentro del contenedor para persistir los datos de MongoDB.
        ./monguitodata/log:/var/log/mongodb/: Mapea el directorio local 
        monguitodata/log   al directorio /var/log/mongodb/ dentro del contenedor 
        para persistir los registros de MongoDB.
  *Abre el puerto 27017 del contenedor para que pueda ser accesible desde fuera (ports: - "27017:27017").


- Paso 3

  Crear archivos para poder correr el comando en una terminal

  ´´´
  touch mongo.sh
  ´´´
  El comando sh contiene un script interno para que la computadora ejecute perfectamente

  -Paso 4

Ahora vamos a crear una carpeta para guardar todo.
 ´´´
  mkdir monguitodata && cd monguitodata; cd monguitodata || mkdir log
  ´´´
El comando mkdir monguitodata va crear un directorio llamado monguitodata.

El comando && continúa con la siguiente acción si la acción anterior era correcta.

El comando cd monguitodata cambia al directorio recién creado llamado monguitodata.

El comando ;: ejecuta la siguiente acción independientemente del resultado de la acción anterior.

El comando cd monguitodata || mkdir log: Intenta cambiar al directorio monguitodata. De no existir crea un directorio llamado log.

