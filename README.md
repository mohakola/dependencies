# Gazelle dependency services

This repository installs and initiates 4 services with docker-compose: elasticsearch(2.4), kibana(4.5), mongodb(latest), redis(latest)
and exposes their ports as local services.
It maps configuration files for each service and handles data persistency in the current folder.

## Install services

1- install docker

2- install docker-compose

3- cp elasticsearch.yml.tml to elasticsearch.yml

4- add required elasticsearch config and/or aws secret keys to elasticsearch.yml accordingly

5- to add additionall service instances, uncomment related lines in docker-compose.yml and create esdata* and snapshot* folders accordingly

6- run ```docker-compose up -d```

## Test services

1- test elastic search running ```"http :9200"```

2- test mongodb running "mongo" client

3- test redis-server running "redis-cli" and then "set key value"


## Load data and prepare environment

1- add s3 endpoint (you can use httpie or curl)

        http PUT :9200/_snapshot/prod type=s3 settings:='{
            "base_path": "prod",
            "bucket": "gazelle-esbackups",
            "readonly": "true",
            "region": "us-east-1"
        }'

2- load latest snapshot using cli tool

- list snapshots

        impala.es --lsi "*" -r prod

- choose and restore desired snapshot (--silent to pre-approve all confirmations)

        impala.es --snapname [snapshot_name] --restore --rename-to "gz.*" -r prod [--silent]

- create required aliases for gazelle.api to work with

        impala.es --ns gz.\* --auto-alias

3- load standard data

        standards.init_db [gazelle configuration]
