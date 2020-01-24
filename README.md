# This repository installs and initiates 3 services with docker-compose: elasticsearch(2.4), mongodbi(latest), redis(latest)
# and exposes their ports as local services.
# It maps configuration files for each service and handles data persistency in the current folder.

1- install docker
2- install docker-compose
3- cp elasticsearch.yml.tml to elasticsearch.yml
4- add required elasticsearch config and/or aws secret keys to elasticsearch.yml accordingly
5- to add additionall service instances, uncomment related lines in docker-compose.yml and create esdata* and snapshot* folders accordingly
6- run docker-compose up -d

# Test
1- test elastic search running "http :9200"
2- test mongodb running "mongo" client
3- test redis-server running "redis-cli" and then "set key value"

