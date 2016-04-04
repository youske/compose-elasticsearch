FROM frolvlad/alpine-oraclejdk8:slim
MAINTAINER youske miyakoshi <youske@gmail.com>

ENV PACKAGE="bash"\
    PATH=/embulk/bin/:$PATH

RUN adduser -S -h /home/embulk embulk

RUN apk add ${PACKAGE} --no-cache && apk add wget ca-certificates --no-cache -t dltool
RUN mkdir -p /embulk && mkdir -p /embulk/bin && \
    wget  -q --no-check-certificate "http://dl.embulk.org/embulk-latest.jar" && \
    mv embulk-latest.jar /embulk/bin/embulk && chmod +x /embulk/bin/embulk

COPY Gemfile /Gemfile
RUN embulk bundle && embulk bundle show
RUN apk del dltool && rm -rf /tmp/* /var/cache/apk/*

USER embulk
WORKDIR /home/embulk
CMD ["bash"]
