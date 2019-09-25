# Docker Compose

# Instalar Docker
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

## Inicio automatico
~~~
sudo systemctl enable docker
~~~

## Acceso no ROOT
~~~
sudo groupadd docker
sudo usermod -aG docker $USER
~~~

## [Instalar Docker Compose](https://docs.docker.com/compose/install/)
Mas informacion en [Docker Compose](https://docs.docker.com/compose/install/)
~~~
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
~~~
~~~
sudo chmod +x /usr/local/bin/docker-compose
~~~

## Comandos docker
Reemplazar **<nombre_del_contenedor>** por el nombre real. **Ejemplo**
~~~
docker start postgres
~~~

- **Iniciar contenedor**
~~~
docker start <nombre_del_contenedor>
~~~
- **Detener contenedor**
~~~
docker stop <nombre_del_contenedor>
~~~
- **Eliminar contenedor**
~~~
docker rm <nombre_del_contenedor>
~~~
- **Ejecutar comando dentro del contenedor**
~~~
docker exec -it <nombre_del_contenedor> <comando o instruccion a ejecutar>
~~~

# Crear contenedor con Docker Compose
~~~
docker-compose up -d
~~~

# Contenedores
- Postgres
- MariaDB
- Prestashop
- Nginx Proxy

