# Quickly
Command

docker network create zabbix-glpi-net && \
docker run -d --name zabbix-db --network zabbix-glpi-net -e MYSQL_DATABASE=zabbix -e MYSQL_USER=zabbix -e MYSQL_PASSWORD=zabbix -e MYSQL_ROOT_PASSWORD=zabbix --restart=always mariadb:11.3 && \
docker run -d --name zabbix-server --network zabbix-glpi-net -p 10051:10051 -e DB_SERVER_HOST=zabbix-db -e MYSQL_DATABASE=zabbix -e MYSQL_USER=zabbix -e MYSQL_PASSWORD=zabbix --restart=always zabbix/zabbix-server-mysql:alpine-trunk && \
docker run -d --name zabbix-web --network zabbix-glpi-net -p 8080:8080 -e ZBX_SERVER_HOST=zabbix-server -e DB_SERVER_HOST=zabbix-db -e MYSQL_DATABASE=zabbix -e MYSQL_USER=zabbix -e MYSQL_PASSWORD=zabbix --restart=always zabbix/zabbix-web-apache-mysql:alpine-trunk && \
docker run -d --name glpi-db --network zabbix-glpi-net -e MYSQL_DATABASE=glpi -e MYSQL_USER=glpi -e MYSQL_PASSWORD=glpi -e MYSQL_ROOT_PASSWORD=glpi --restart=always mariadb:11.3 && \
docker run -d --name glpi --network zabbix-glpi-net -p 80:80 -e MYSQL_HOST=glpi-db -e MYSQL_DATABASE=glpi -e MYSQL_USER=glpi -e MYSQL_PASSWORD=glpi --restart=always diouxx/glpi:latest
