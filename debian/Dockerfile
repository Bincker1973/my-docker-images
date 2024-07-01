FROM debian:latest
LABEL authors="bincker"

RUN sed -i "s/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list.d/debian.sources

ENTRYPOINT ["bash"]