FROM debian:12.0-slim

# Install dependencies
RUN apt-get update && \
    apt-get install -y wget

RUN apt-get update && \
    apt-get install -y git

RUN wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb

RUN dpkg -i packages-microsoft-prod.deb

RUN rm packages-microsoft-prod.deb

RUN apt-get update && \
    apt-get install -y apt-transport-https && \
    apt-get update && \
    apt-get install -y dotnet-sdk-6.0 && \
    apt-get update && \
    apt-get install -y dotnet-sdk-7.0 && \
    apt-get update && \
    apt-get install -y dotnet-sdk-8.0

# Instalamos openssh-server para permitir el acceso remoto por el puerto 22
RUN apt-get update && \
    apt-get install -y openssh-server

# Instalamos Java LTS
RUN apt-get update && \
    apt-get install -y default-jdk

# Creamos el usuario remoto y le asignamos una contraseña
RUN useradd remote_user && \
    echo "remote_user:1234" | chpasswd && \
    mkdir /home/remote_user/.ssh -p && \
    chmod 700 /home/remote_user/.ssh && \
    mkdir -p -m0755 /var/run/sshd

# Copiamos la clave pública del host para permitir el acceso remoto
# COPY remote-key.pub /home/remote_user/.ssh/authorized_keys
RUN mkdir -p /home/remote_user/.ssh
RUN touch /home/remote_user/.ssh/authorized_keys  

# Asignamos los permisos correspondientes
RUN chown remote_user:remote_user -R /home/remote_user && \
    chmod 400 /home/remote_user/.ssh/authorized_keys

# Creamos el directorio de trabajo
RUN mkdir /var/jenkins && \
    chown remote_user:remote_user -R /var/jenkins && \
    chmod -R 777 /var/jenkins

# Exponemos el puerto 22 para permitir el acceso remoto
CMD /usr/sbin/sshd -D