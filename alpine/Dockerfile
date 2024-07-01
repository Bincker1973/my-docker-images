FROM alpine:latest
LABEL authors="bincker"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories

ENTRYPOINT ["bash"]