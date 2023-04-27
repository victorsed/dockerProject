FROM mcr.microsoft.com/mssql/server:2017-latest

ENV ACCEPT_EULA=Y
ENV MSSQL_SA_PASSWORD=password

# Mise à jour du système d'exploitation Ubuntu 16.04
RUN apt-get update && apt-get -y upgrade

# Copie des 3 fichiers vers le dossier /tmp/database/
COPY entrypoint.sh SqlCmdStartup.sh SqlCmdScript.sql /tmp/database/
RUN chmod +x /tmp/database/entrypoint.sh && chmod +x /tmp/database/SqlCmdStartup.sh
CMD cd /tmp/database/ && ./entrypoint.sh 

#Volume a créer dans le docker-compose
#VOLUME [ "D:\ProgramData\DockerDesktop\volumes\mssqlsrv2017:/var/opt/mssql/data" ]