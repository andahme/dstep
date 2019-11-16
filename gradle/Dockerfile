ARG INPUT_JAVA_MAJOR=8

ARG INPUT_GRADLE_VERSION=4.10.2

ARG GRADLE_ARTIFACT=https://services.gradle.org/distributions/gradle-${INPUT_GRADLE_VERSION}-bin.zip



FROM andahme/debian:testing AS distribution

ARG GRADLE_ARTIFACT

ARG INPUT_GRADLE_VERSION


RUN apt-get update && apt-get install --yes --no-install-recommends unzip

ADD ${GRADLE_ARTIFACT} /tmp/gradle-${INPUT_GRADLE_VERSION}.zip


WORKDIR /opt

RUN unzip /tmp/gradle-${INPUT_GRADLE_VERSION}.zip



FROM andahme/openjdk:${INPUT_JAVA_MAJOR}-jdk AS gradle

ARG INPUT_GRADLE_VERSION


ENV GRADLE_USER_HOME /gradle

ENV GRADLE_HOME /opt/gradle-${INPUT_GRADLE_VERSION}

ENV PATH ${GRADLE_HOME}/bin:${PATH}


COPY --from=distribution /opt/gradle-${INPUT_GRADLE_VERSION} ${GRADLE_HOME}


RUN mkdir /gradle /drone && \
    chmod 777 /gradle /drone


VOLUME /gradle

VOLUME /drone


