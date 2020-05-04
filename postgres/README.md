# Docker Postgres

## Info
- **Contenedor nombre**: postgres
- **Puero**: 5432
- **Usuario**: postgres
- **Contraseña**: 1234
- **Imagen**: postgres:alpine

## Cree un volumen para la persistencia Postgres
~~~
docker volume create --name postgres-data
~~~

## docker-compose (Unix)
~~~
version: '3.1'
services:
  postgres:
    container_name: postgres
    restart: always
    image: postgres:alpine
    ports:
      - "5432:5432"
    environment:
      POSTGRES_PASSWORD: "1234"
    volumes:
      - postgres-data
  postgres-data:
    image: busybox
    volumes:
      - ./data:/var/lib/postgresql/data
~~~

## docker-compose (Windows)
~~~
version: '3.1'
services:
  postgres:
    container_name: postgres
    restart: always
    image: postgres:alpine
    ports:
      - "5432:5432"
    environment:
      POSTGRES_PASSWORD: "1234"
    volumes:
      - postgres-data
  postgres-data:
    image: busybox
    volumes:
      - ./data:/var/lib/postgresql/data
~~~
~~~
docker-compose up -d
~~~
