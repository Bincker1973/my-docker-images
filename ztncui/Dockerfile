FROM debian:12 as builder
ENV NODEJS_MAJOR=16
ARG PROXY="socks5://192.168.2.9:7890"

RUN sed -i "s/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list.d/debian.sources && \
    apt update -y && \
    apt install -y git && \
    git config --global http.https://github.com/.proxy "${PROXY}" && \
    git clone https://github.com/key-networks/ztncui && \
    apt install -y curl && \
    curl -sL -o node_inst.sh https://deb.nodesource.com/setup_${NODEJS_MAJOR}.x && bash node_inst.sh && rm -f node_inst.sh && \
    apt install -y nodejs git golang-go python3 make && \
    npm config set registry https://registry.npmjs.org && \
    npm install -g node-gyp pkg yarn && \
    cd ztncui/src && yarn install && \
    pkg -c ./package.json -t "node${NODEJS_MAJOR}-linux-x64" bin/www -o ztncui && \
    tar czf /artifact.tar.gz --transform 's,node_modules/argon2/build/Release/,/,' ztncui node_modules/argon2/build/Release/

FROM debian:12
ENV TZ=Asia/Shanghai

WORKDIR /opt/key-networks/ztncui
VOLUME ["/opt/key-networks/ztncui/etc"]

COPY --from=builder /artifact.tar.gz .
COPY --from=builder /ztncui/src/etc/default.passwd etc/passwd

RUN sed -i "s/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list.d/debian.sources && \
    apt update -y && apt upgrade -y && \
    apt install -y curl nodejs git && \
    tar xf artifact.tar.gz -C /opt/key-networks/ztncui

EXPOSE 3000/tcp

ENTRYPOINT [ "./ztncui" ]