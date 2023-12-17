# Labs DevOps Jenkins .Net Core

## Labs

### Lab 1: Crea los contenedores con docker compose

```bash
docker compose up -d
```

Esto creara dos contenedores, uno donde va a correr Jenkins en el puerto 9001 y otro donde va a correr un servidor esclavo con Debian 12.

### Lab 2: Configura Jenkins

Ingresa al contenedor de Jenkins.-

```bash
docker exec -it jenkins-master bash
```

Copia la clave de activación de Jenkins.-

```bash
cat /var/jenkins_home/secrets/initialAdminPassword
```

Prueba la conexión con el servidor esclavo.-

```bash
ssh remote_user@jenkins-slave
```

> Donde remote_user es el usuario que se configuro en el servidor esclavo y la contraseña es 1234.

### Lab 3: Ingresa al servidor esclavo

Ingresa al contenedor del servidor esclavo.-

```bash
docker exec -it jenkins-slave bash
```

Valida la versión instalada de .Net Core.-

```bash
dotnet --version
```

## Docker

### Crear imagen

Para crear la imagen de Jenkins Master utilizamos el siguiente comando.-

```bash
docker build -t jenkins-master -f ./jenkins-dockerfile/Dockerfile .
```

Para crear la imagen de Jenkins Slave utilizamos el siguiente comando.-

```bash
docker build -t jenkins-slave -f ./slave-linux-ockerfile/Dockerfile .
```

Agregar la imagen de Jenkins Slave al repositorio local.-

```bash
docker tag debian-slave-jenkins:0.0.1 paulo866/debian-slave-jenkins:0.0.1
```

> Donde paulo866 es el nombre de usuario del repositorio y debian-slave-jenkins es el nombre de la imagen.

Agregamos un comentario a la imagen de Jenkins Slave.-

```bash
docker commit -m "Comentario" debian-slave-jenkins:0.0.1 paulo866/debian-slave-jenkins:0.0.1
```

Subir la imagen de Jenkins Slave al repositorio local.-

```bash
docker push paulo866/debian-slave-jenkins:0.0.1
```

> Donde paulo866 es el nombre de usuario del repositorio y debian-slave-jenkins es el nombre de la imagen.

### Crear y correr contenedor

Para crear y correr el contenedor de Jenkins Master utilizamos el siguiente comando.-

```bash
docker compose up -d
```
