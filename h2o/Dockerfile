#  Author: Huang Geyang
#  Docker Hub ID: yomeo
#  Date: 2019-02-14


FROM harisekhon/centos-java:jre7
# > 100MB smaller than centos

ARG H2O_VERSION=3.22.1.3

ENV PATH $PATH:/h2o/bin

LABEL Description="H2O" \
      "0xData H2O Version"="$H2O_VERSION"

#COPY h2o-$H2O_VERSION /h2o

WORKDIR /

RUN bash -c ' \
    set -euxo pipefail && \
    apt-get update && \
    apt-get install -y --no-install-recommends wget unzip && \
    # 3.x url has changed
    wget -t 100 --retry-connrefused http://h2o-release.s3.amazonaws.com/h2o/rel-xu/3/h2o-${H2O_VERSION}.zip && \
    unzip h2o-${H2O_VERSION}.zip && \
    rm h2o-${H2O_VERSION}.zip && \
    ln -s h2o-${H2O_VERSION} h2o && \
    apt-get purge -y wget unzip && \
    apt-get autoremove -y && \
    apt-get clean'

EXPOSE 54321

CMD java -jar /h2o/h2o.jar
