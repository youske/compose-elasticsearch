# alpine linux with elasticsearch
#
from frolvlad/alpine-oraclejdk8:slim
MAINTAINER youske miyakoshi <youske@gmail.com>

ENV ELASTICSEARCH_VERSION=2.3.0
ENV ELASTICSEARCH_BASE=/elasticsearch
ENV DFILE=elasticsearch-${ELASTICSEARCH_VERSION}.tar.gz
ENV DOWNLOAD_URL=https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/${ELASTICSEARCH_VERSION}/${DFILE}
ENV PATH=${ELASTICSEARCH_BASE}/bin:$PATH

# elasticsearch user
RUN addgroup elasticsearch && adduser -S elasticsearch -h /elasticsearch -G elasticsearch -D -H

RUN apk add bash --no-cache && \
    apk add wget ca-certificates glibc glibc-bin --no-cache -t dltool
RUN wget -q --no-check-certificate ${DOWNLOAD_URL} -O- | tar -zx && \
    ln -s -f elasticsearch-${ELASTICSEARCH_VERSION} /elasticsearch && \
    chown -R root:elasticsearch elasticsearch-${ELASTICSEARCH_VERSION}

COPY config /elasticsearch/config

RUN mkdir -p /elasticsearch/plugins && \
    mkdir -p /eslogs && chown -R elasticsearch:elasticsearch /eslogs && \
    mkdir -p /esdata && chown -R  elasticsearch:elasticsearch  /esdata


    #    plugin install river-csv -url https://github.com/AgileWorksOrg &&

RUN echo "hoge" && \
#    plugin install mobz/elasticsearch-head && \
#    plugin install elasticsearch/elasticsearch-river-twitter/2.6.0 && \
#     plugin install elasticsearch/elasticsearch-lang-python/2.7.0 && \
#     plugin install elasticsearch/elasticsearch-lang-javascript/2.7.0 && \
#     plugin install polyfractal/elasticsearch-inquisitor && \
#     plugin install elasticsearch/elasticsearch-analysys-kuromoji/1.6.0 && \
#    plugin install com.github.kzwang/el;asticsearch-image/1.2.0 && \
#    plugin install elasticsearch/kibana && \
#    plugin install royrusso/marvel && \
    plugin install royrusso/elasticsearch-HQ/v.2.0.0


RUN apk del dltool && rm -fr /tmp/* /var/cache/apk/*


EXPOSE 9200 9300

USER elasticsearch

WORKDIR ${ELASTICSEARCH_BASE}
CMD ["elasticsearch","-Des.network.host=0.0.0.0"]
#CMD ["sh"]
