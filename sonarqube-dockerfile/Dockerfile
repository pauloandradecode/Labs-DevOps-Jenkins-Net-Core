FROM sonarqube:community

RUN apt-get update && \
      apt-get -y install sudo

RUN useradd -m sonarqube && echo "sonarqube:sonarqube" | chpasswd && adduser sonarqube sudo

USER sonarqube

# Aumentar el tamaño maximo del archivo
RUN echo 'vm.max_map_count=262144' >> /etc/sysctl.conf