# Docker MariaDB

Permisos remotos
~~~~
docker exec -it mariadb mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '1234' WITH GRANT OPTION;
~~~~
