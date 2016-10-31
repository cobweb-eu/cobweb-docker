FROM ubuntu:wily
MAINTAINER doublebyte <joana.simoes@geocat.net>

RUN apt-get update && \
    apt-get install -y postgresql-client

#expose data dirs as external volumes
RUN mkdir -p /usr/local/geoserver-cobweb/data && \
    mkdir -p /usr/local/geonetwork-cobweb/data && \
    mkdir -p /usr/local/postgresql-cobweb/data

#enabling logging on Geoserver
RUN mkdir -p /usr/local/geoserver-cobweb/data/logs
COPY ./logging.xml   /usr/local/geoserver-cobweb/data/logging.xml
COPY ./PRODUCTION_LOGGING.properties   /usr/local/geoserver-cobweb/data/logs/PRODUCTION_LOGGING.properties

#Create default workspace and datastore for Geoserver
RUN mkdir -p /usr/local/geoserver-cobweb/data/workspaces && \
    mkdir -p /usr/local/geoserver-cobweb/data/workspaces/myworkspace && \
    mkdir -p /usr/local/geoserver-cobweb/data/workspaces/myworkspace/mydatastore

COPY ./default.xml   /usr/local/geoserver-cobweb/data/workspaces/default.xml
COPY ./namespace.xml /usr/local/geoserver-cobweb/data/workspaces/myworkspace/namespace.xml
COPY ./workspace.xml /usr/local/geoserver-cobweb/data/workspaces/myworkspace/workspace.xml
COPY ./datastore.xml /usr/local/geoserver-cobweb/data/workspaces/myworkspace/mydatastore/datastore.xml

#export backed  volumes 
VOLUME ["/usr/local/geoserver-cobweb/data", "/usr/local/geonetwork-cobweb/data", \
"/usr/local/postgresql-cobweb/data", "/var/log/postgresql"]

CMD ["tail","-f","/dev/null"]
