FROM registry.access.redhat.com/ubi7/python-36

ARG PKG_ROOT=/opt/app-root
ARG SPARK_VERSION=2.4.5
ARG HADOOP_VERSION=2.8.5
ARG JAVA_VERSION=1.8.0

USER root
RUN wget https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-without-hadoop.tgz &&\
    tar -C ${PKG_ROOT} -zxf spark-${SPARK_VERSION}-bin-without-hadoop.tgz &&\
    mv ${PKG_ROOT}/spark-${SPARK_VERSION}-bin-without-hadoop ${PKG_ROOT}/spark-${SPARK_VERSION} &&\
    rm spark-${SPARK_VERSION}-bin-without-hadoop.tgz
RUN wget https://downloads.apache.org/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz &&\
    tar -C ${PKG_ROOT} -xf hadoop-${HADOOP_VERSION}.tar.gz &&\
    rm hadoop-${HADOOP_VERSION}.tar.gz

RUN yum -y install java-$JAVA_VERSION-openjdk maven &&\
    yum clean all

ENV JAVA_HOME=/usr/lib/jvm/jre

RUN cp ${PKG_ROOT}/spark-${SPARK_VERSION}/conf/spark-env.sh.template ${PKG_ROOT}/spark-${SPARK_VERSION}/conf/spark-env.sh &&\
    echo "HADOOP_CONF_DIR=$(${PKG_ROOT}/hadoop-${HADOOP_VERSION}/bin/hadoop classpath)" >> ${PKG_ROOT}/spark-${SPARK_VERSION}/conf/spark-env.sh

USER 1001
RUN fix-permissions ${PKG_ROOT}
