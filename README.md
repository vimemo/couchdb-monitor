volumes
==========
```
docker volume create --name couchdb_data
docker network create --attachable couchdb_data

docker volume create --name grafana_data
docker network create --attachable grafana_data

docker volume create --name prometheus_data
docker network create --attachable prometheus_data
```


couchdb cluster setup
======================

```
curl -X POST "http://localhost:5980/_cluster_setup" \
     -H "Content-Type: application/json" \
     -d '{"action":"enable_cluster", "username":"admin", "password":"pass", "bind_address":"0.0.0.0", "port":5980, "node_count": 1}'

curl -X POST "http://localhost:5980/_session" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
     -d 'name=admin&password=pass' \
     --cookie-jar couchdb-cookies.txt

curl -X POST "http://localhost:5980/_cluster_setup" \
     -H "Content-Type: application/json" \
     -d '{"action":"finish_cluster"}' \
     --cookie couchdb-cookies.txt
```

docker misc
==============
```
docker inspect <container-id>
docker exec -it <container-id> bash

curl admin:pass@docker.for.mac.localhost:5984/medic

docker network create -d bridge --subnet 192.168.0.0/24 --gateway 192.168.0.1 dockernet

docker-compose ps
docker-compose down
docker-compose up
docker-compose run <service>
```
