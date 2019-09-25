# Nginx Proxy

## Info
- **Puerto**: 80
- **Contenerdor nombre**: nginx-proxy
- **Imagen**: [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy)

## Crear red
Ejecutar antes de crear el contenedor
~~~
docker network create nginx-proxy
~~~

## SSL Contenedor
Si desea que el proxy inverso se conecte a su backend usando HTTPS en lugar de HTTP, configúrelo **VIRTUAL_PROTO=https** en el contenedor de backend.
> **Nota** Si usa **VIRTUAL_PROTO=https** y su contenedor de back-end expone los puertos **80** y **443**, nginx-proxy usará HTTPS en el puerto 80. Esto es casi seguro que no es lo que desea, por lo que también debe incluirlo **VIRTUAL_PORT=443**.

## Usando Docker
~~~
docker run -d -p 80:80 --name nginx-proxy --net nginx-proxy -v /var/run/docker.sock:/tmp/docker.sock jwilder/nginx-proxy
~~~

## Usando docker-compose
~~~
docker-compose up -d
~~~

## docker-compose.yml
~~~
version: "3.1"
services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    container_name: nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro

networks:
  default:
    external:
      name: nginx-proxy
~~~

# Agregar contendores al proxy

## Ejemplo

### Usando Docker
Reemplazar **blog.midominio.com** por su dominio o subdominio

**--expose 80** permite que el trafico fluya hacia el contenedor en el puero **80**

**--net nginx-proxy** asegura que estamos usando la red Docker que creamos anteriormente.

**-e VIRTUAL_HOST=blog.midominio.com** dirigir cualquier tráfico que solicite ese dominio a este nuevo contenedor Docker

~~~
docker run -d --name blog --expose 80 --net nginx-proxy -e VIRTUAL_HOST=blog.midominio.com wordpress
~~~
