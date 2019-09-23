# Docker Prestashop

## Info
- **Puerto**: 8080

## File
~~~
version: '3.1'
services:
  prestashop:
    container_name: prestashop
    restart: always
    image: prestashop/prestashop:latest
    ports:
      - "8080:80"
    environment:
      PS_INSTALL_AUTO: 0
      PS_DEV_MODE: 0
      PS_DEMO_MODE: 0
      PS_LANGUAGE: es-mx
      PS_COUNTRY: co
    networks:
      - default
      - mariadb_default
networks:
  default:
    driver: bridge
  mariadb_default:
    external: true
~~~
