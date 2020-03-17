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


# Load data into snapshot
1- add s3 endpoint (default name for cli script is es2.s3)
http PUT :9200/_snapshot/es2.s3 type=s3 settings:='{
            "base_path": "prod",
            "bucket": "gazelle-esbackups",
#            "readonly": "true",
            "region": "us-east-1"
        }'
2- load latest snapshot using cli tool
- list snapshots
impala.es --lsi "*"
- restore desired snapshot
impala.es --snapname [snapshot_name] --restore --rename-to gz.\* --silent
- create required aliases for gazelle.api to work with
impala.es --ns gz.\* --auto-alias
3- load standard data
standards.init_db [gazelle configuration]
