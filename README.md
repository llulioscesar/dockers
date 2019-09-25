# Docker Compose

## Instalar Docker
- Debian/Ubuntu y derivados
~~~
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
~~~

~~~
sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
~~~

~~~
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
~~~

# Comando
~~~
docker-compose up -d
~~~

# Contenedores
- Postgres
- MariaDB
- Prestashop

