# Labs DevOps Jenkins .Net Core

## Lab 1: Crea los contenedores con docker compose

```bash
docker compose up -d
```

Esto creara dos contenedores, uno donde va a correr Jenkins en el puerto 9001 y otro donde va a correr un servidor esclavo con Debian 12.

## Lab 2: Configura Jenkins

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

## Lab 3: Ingresa al servidor esclavo

Ingresa al contenedor del servidor esclavo.-

```bash
docker exec -it jenkins-slave bash
```

Valida la versión instalada de .Net Core.-

```bash
dotnet --version
```