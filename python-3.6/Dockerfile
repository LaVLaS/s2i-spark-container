FROM registry.access.redhat.com/ubi7/python-36

ENV SPARK_VERSION 2.4.5
USER root
RUN yum -y install java-1.8.0-openjdk maven &&\
    yum clean all
USER 1001
RUN pip install -U pip && pip install pyspark==${SPARK_VERSION}
RUN fix-permissions /opt/app-root
