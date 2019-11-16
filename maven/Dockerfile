ARG INPUT_JAVA_MAJOR=11

ARG INPUT_MAVEN_VERSION=3.6.2

ARG MAVEN_ARTIFACT=http://ftp.wayne.edu/apache/maven/maven-3/${INPUT_MAVEN_VERSION}/binaries/apache-maven-${INPUT_MAVEN_VERSION}-bin.tar.gz



FROM andahme/debian AS distribution

ARG MAVEN_ARTIFACT

ARG INPUT_MAVEN_VERSION


ADD ${MAVEN_ARTIFACT} /tmp/apache-maven-${INPUT_MAVEN_VERSION}-bin.tar.gz

RUN tar -zxf /tmp/apache-maven-${INPUT_MAVEN_VERSION}-bin.tar.gz -C /opt --strip-component=1

COPY settings.xml /opt/conf/settings.xml



FROM andahme/openjdk:${INPUT_JAVA_MAJOR}-base AS maven

ARG INPUT_MAVEN_VERSION


ENV MAVEN_HOME /opt/maven-${INPUT_MAVEN_VERSION}

ENV PATH ${MAVEN_HOME}/bin:${PATH}


COPY --from=distribution /opt ${MAVEN_HOME}


RUN useradd --comment "Maven User" --create-home --uid 1011 maven

RUN mkdir /m2repository /workspace && \
    chmod 777 /m2repository /workspace


VOLUME /m2repository

VOLUME /workspace


WORKDIR /workspace

USER maven

