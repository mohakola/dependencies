FROM elasticsearch:2.4.5-alpine
#NAME ES:2.4.6
#RUN ES_JAVA_OPTS="-Djavax.net.ssl.trustStore=/path/to/trustStore.jks" plugin install cloud-aws -b
#COPY --chown=elasticsearch:elasticsearch /opt/elasticsearch-docker/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml 

## install the amazone cloud plugin
RUN plugin install cloud-aws -b && plugin install mapper-size -b
