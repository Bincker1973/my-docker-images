# ZTNCUI
自建 ZeroTier Web 控制台  
编译至 ztncui ([https://github.com/key-networks/ztncui](https://github.com/key-networks/ztncui))
## 用法
1. 安装并启动你的zerotier-one
2. 执行命令  
   ```bash
   docker run --net host \
     --name ztncui \
     --restart unless-stopped \
     -e ZT_TOKEN="$(sudo cat /var/lib/zerotier-one/authtoken.secret)" \
     -e HTTP_ALL_INTERFACE=yes \
     -e HTTP_PORT=8080 \
     -e HTTPS_HOST=0.0.0.0 \
     -e HTTPS_PORT=8443 \
     -d bincker1973/ztncui
   ```
   > 最好不要直接讲HTTP暴露到网络中，要么使用https，要么使用nginx代理后用https
