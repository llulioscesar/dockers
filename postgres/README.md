# Docker Postgres

## Info
- **Contenedor nombre**: postgres
- **puero**: 5432
- **usuario**: postgres
- **contraseña**: 1234

## File
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
