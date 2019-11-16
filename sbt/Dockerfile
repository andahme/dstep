ARG INPUT_JAVA_MAJOR=8

ARG INPUT_SBT_VERSION=1.1.1

ARG SBT_ARTIFACT=https://github.com/sbt/sbt/releases/download/v${INPUT_SBT_VERSION}/sbt-${INPUT_SBT_VERSION}.tgz



FROM andahme/debian AS distribution

ARG INPUT_SBT_VERSION

ARG SBT_ARTIFACT


ADD ${SBT_ARTIFACT} /tmp/sbt-${INPUT_SBT_VERSION}.tar.gz

RUN tar -zxf /tmp/sbt-${INPUT_SBT_VERSION}.tar.gz -C /opt --strip-components=1



FROM andahme/openjdk:${INPUT_JAVA_MAJOR}-jdk as sbt

ARG INPUT_SBT_VERSION


ENV SBT_HOME /opt/sbt-${INPUT_SBT_VERSION}

ENV PATH ${SBT_HOME}/bin:${PATH}


COPY --from=distribution /opt ${SBT_HOME}


RUN useradd --comment "SBT User" --create-home --uid 1011 sbt

#RUN sed -i -r -e "s/^#?(-sbt-boot ).*$/\1\/sbt\/boot/g" -e "s/^#?(-ivy ).*$/\1\/repository/g" ${SBT_HOME}/conf/sbtopts
RUN sed -i -r -e "s/^#?(-sbt-dir ).*$/\1\/sbt/g" -e "s/^#?(-ivy ).*$/\1\/repository/g" ${SBT_HOME}/conf/sbtopts

RUN mkdir -p /repository /sbt /workspace && \
    chmod 777 /repository /sbt /workspace


VOLUME /repository

VOLUME /workspace


USER sbt

WORKDIR /workspace


RUN sbt initialize


VOLUME /sbt

