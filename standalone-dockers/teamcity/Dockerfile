FROM openjdk:latest
MAINTAINER Piotr Joński <yoyo@wp.eu>

ARG TEAMCITY_VERSION=10.0.4
ARG USER_ID=2000
ARG USER_NAME=jetbrains
ENV PORT=8111

RUN groupadd --gid ${USER_ID} ${USER_NAME} && \
    useradd --create-home --home-dir /teamcity --uid ${USER_ID} --gid ${USER_NAME} ${USER_NAME} && \
    chown --changes ${USER_NAME}:${USER_NAME} /teamcity

USER ${USER_NAME}
WORKDIR /teamcity

RUN mkdir backups data logs conf temp && \
    curl --location "https://download.jetbrains.com/teamcity/TeamCity-${TEAMCITY_VERSION}.tar.gz" > teamcity.tar.gz && \
    tar -xf teamcity.tar.gz && \
    rm -f teamcity.tar.gz && \
    mv TeamCity/* . && \
    mkdir -p data/lib/jdbc && \
    curl --location "https://jdbc.postgresql.org/download/postgresql-9.4.1212.jar" > data/lib/jdbc/postgresql-9.4.1212.jar && \
    rm -rf TeamCity && \
    rm -rf devPackage

EXPOSE ${PORT}
CMD [ "/bin/bash", "/teamcity/bin/teamcity-server.sh", "run" ]
