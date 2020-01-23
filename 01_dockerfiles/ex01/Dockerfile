FROM debian

#port (EXPOSE = instruction indique les ports sur lesquels un conteneur écoute les connexions)
EXPOSE 10011 30033 9987/udp 

#installer tous les paquets
RUN apt update -y && apt upgrade -y
RUN apt install wget bzip2 tar -y

#Obtenir les derniers fichiers du serveurs
RUN wget https://files.teamspeak-services.com/releases/server/3.10.2/teamspeak3-server_linux_amd64-3.10.2.tar.bz2
#extraction 
RUN tar xvf teamspeak3-server_linux_amd64-3.10.2.tar.bz2
#suppression de l'archive telechargee
RUN rm teamspeak3-server_linux_amd64-3.10.2.tar.bz2

#run server
WORKDIR teamspeak3-server_linux_amd64
#acceptwr le  contrat de licence Teamspeak
RUN touch .ts3server_license_accepted

CMD ["./ts3server"]
#execution
#docker build -t ex01 .
#docker run -it -p  9987:9987/udp  -p 30033:30033  -p 10011:10011 ex01 
