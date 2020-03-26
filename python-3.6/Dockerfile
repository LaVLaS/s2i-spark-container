FROM registry.access.redhat.com/ubi7/python-36

ARG SPARK_VERSION=2.4.5
ARG HADOOP_VERSION=2.8.5
ARG JAVA_VERSION=1.8.0

USER root
RUN wget https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-without-hadoop.tgz &&\
    tar -C /opt/app-root -zxf spark-${SPARK_VERSION}-bin-without-hadoop.tgz &&\
    mv /opt/app-root/spark-${SPARK_VERSION}-bin-without-hadoop /opt/app-root/spark-2.4.5 &&\
    rm spark-${SPARK_VERSION}-bin-without-hadoop.tgz
RUN wget https://downloads.apache.org/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz &&\
    tar -C /opt/app-root -xf hadoop-${HADOOP_VERSION}.tar.gz &&\
    mv /opt/app-root/hadoop-${HADOOP_VERSION} /opt/app-root/hadoop-${HADOOP_VERSION} &&\
    rm hadoop-${HADOOP_VERSION}.tar.gz

RUN yum -y install java-$JAVA_VERSION-openjdk maven &&\
    yum clean all

ENV JAVA_HOME=/usr/lib/java-${JAVA_VERSION}

COPY /opt/spark-2.4.5-bin-without-hadoop/conf/spark-env.sh.template /opt/spark-2.4.5-bin-without-hadoop/conf/spark-env.sh
RUN /opt/app-root/hadoop-${HADOOP_VERSION}/bin/hadoop classpath >> /opt/spark-2.4.5-bin-without-hadoop/conf/spark-env.sh

USER 1001
RUN fix-permissions /opt/app-root
