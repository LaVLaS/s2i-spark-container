FROM registry.access.redhat.com/ubi7/python-36

ENV SPARK_VERSION 2.4.4
ENV JAVA_VERSION 1.8.0

USER root
RUN yum -y install java-$JAVA_VERSION-openjdk maven &&\
    yum clean all

USER 1001
RUN pip install pyspark==$SPARK_VERSION
RUN fix-permissions /opt/app-root
