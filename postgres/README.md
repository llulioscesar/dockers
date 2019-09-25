# Docker Postgres

## Info
- **Contenedor nombre**: postgres
- **Puero**: 5432
- **Usuario**: postgres
- **Contraseña**: 1234
- **Imagen**: postgres:alpine

## Usando docker-compose
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
      - ./datos:/var/lib/postgresql/data
~~~
~~~
docker-compose up -d
~~~
