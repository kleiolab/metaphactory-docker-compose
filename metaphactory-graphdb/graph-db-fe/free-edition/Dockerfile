FROM adoptopenjdk/openjdk11:alpine

# Build time arguments
ARG version=9.6.0
ARG edition=free

ENV GRAPHDB_PARENT_DIR=/opt/graphdb
ENV GRAPHDB_HOME=${GRAPHDB_PARENT_DIR}/home

ENV GRAPHDB_INSTALL_DIR=${GRAPHDB_PARENT_DIR}/dist

ADD graphdb-${edition}-${version}-dist.zip /tmp

RUN apk add --no-cache bash util-linux procps net-tools busybox-extras wget less curl && \
    mkdir -p ${GRAPHDB_PARENT_DIR} && \
    cd ${GRAPHDB_PARENT_DIR} && \
    unzip /tmp/graphdb-${edition}-${version}-dist.zip && \
    rm /tmp/graphdb-${edition}-${version}-dist.zip && \
    mv graphdb-${edition}-${version} dist && \
    mkdir -p ${GRAPHDB_HOME}

# install postgres jdbc driver
RUN curl -o /opt/graphdb/dist/lib/jdbc-postgresql-42.2.19.jar \
    https://jdbc.postgresql.org/download/postgresql-42.2.19.jar

ENV PATH=${GRAPHDB_INSTALL_DIR}/bin:$PATH

CMD ["-Dgraphdb.home=/opt/graphdb/home"]

ENTRYPOINT ["/opt/graphdb/dist/bin/graphdb"]

EXPOSE 7200
