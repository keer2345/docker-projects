# [Ultimate Docker Compose Tutorial](https://www.youtube.com/watch?v=SXwC9fSwct8)

 

## Network
```sh
docker network create mongo-network
docker network ls
docker network rm mongo-network
```
## Command line
Create Mongo container
```sh
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=supersecret \
  --network mongo-network \
  --name mongodb \
  mongo
```
Create Mongo-express container
```sh
docker run -d \
  -p 8004:8081 \
  -e ME_CONFIG_BASICAUTH_USERNAME=user \
  -e ME_CONFIG_BASICAUTH_PASSWORD=pass \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret \
  -e ME_CONFIG_MONGODB_URL=mongodb://admin:supersecret@mongodb:27017 \
  --network mongo-network \
  --name mongo-express \
  mongo-express
```


## Docker compose
`docker-compose.yml`

```yml
version: '3.8'

#####################################
# Prepare:
# sudo mkdir /docker
# sudo chmod 777 /docker
#####################################

services:
  mongodb:
    image: mongo
    container_name: mongodb
    restart: always
    ports:
      - 27017:27017
    volumes:
      - /docker/mongodb/data:/data/db
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: secret

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    restart: always
    ports:
      - 8004:8081
    environment:
      ME_CONFIG_BASICAUTH_USERNAME: user
      ME_CONFIG_BASICAUTH_PASSWORD: pass
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: secret
      ME_CONFIG_MONGODB_URL: mongodb://admin:secret@mongodb:27017
    depends_on:
      - "mongodb"
```

Run docker compose
```sh
docker-compose -f docker-compose.yml up

docker-compose up -d
docker-compose down -v
```

## Create database & collection & document
1. Create database name with `my-db`.
2. Click database `my-db`, then create collection name with `my-collection`.
3. Click collection `my-collection`, then click `New Document`:
```json
{
    "_id": ObjectId(),
    "myid": 1,
    "data": "some dynamic data loaded from DB"
}
```

## Connect own web application
### JS application

[docker-compose-crash-course](https://gitlab.com/twn-youtube/docker-compose-crash-course)

- Connects to database
- Displays the retrieved data

  

