~~~
version: '3.1'
services:
  mongodb:
    image: 'mongo'
    restart: always
    container_name: 'mongodb'
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: test
    volumes:
      - ./init-mongo.js:/docker-entrypoint-initdb.d/init-mongo.js:ro
      - ./mongo-volume:/data/db
    ports:
      - 27017:27017
~~~

~~~
db.createUser(
	{
		user: "local",
		pwd: "test",
		roles: [
			{
				role: "readWrite",
				db: "viedomanolo"
			}
		]
	}
)
~~~
