soure [https://github.com/thingsboard/thingsboard-gateway](https://github.com/thingsboard/thingsboard-gateway)

diff [98109540a1e2534d6a42ba2b04110b5f4684b487](https://github.com/Liberately/thingsboard-gateway-android/commit/98109540a1e2534d6a42ba2b04110b5f4684b487) \
Android 平台下 termux 中 [cryptography](https://pypi.org/project/cryptography/) 没有 Built Distributions \
并且因为 [Tier 2 without Host Tools](https://doc.rust-lang.org/nightly/rustc/platform-support.html#tier-2-without-host-tools) 无法在 termux 中进行编译构建 \
所以需要移除所有与cryptography相关的代码(grpc,opcua,tls,x509)

diff [fbd4a44a87c4beb6cef54ca648d14e712fa74219](https://github.com/Liberately/thingsboard-gateway-android/commit/fbd4a44a87c4beb6cef54ca648d14e712fa74219) \
Android平台下没有命名管道 `/tmp/gateway`无法使用 所以修改 manager_address 从 `/tmp/gateway` 为 `('127.0.0.1', 9999)` \

# 用于在 Android termux 中使用的 ThingsBoard IoT Gateway

```bash
pkg install python3
git clone --recurse-submodules https://github.com/Liberately/thingsboard-gateway-android.git --depth 1
cd thingsboard-gateway-android
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
python setup.py install
vim thingsboard_gateway/config/tb_gateway.json
python3 ./thingsboard_gateway/tb_gateway.py
```

# 用于在 Android termux 中使用的 MQTT 代理

## 安装 mosquitto
```bash
pkg install mosquitto
vim /data/data/com.termux/files/usr/etc/mosquitto/mosquitto.conf
```
## 修改 mosquitto 配置
添加以下配置开放外部连接
```config
allow_anonymous true
listener 1883 0.0.0.0
```

## 启动 mosquitto
```bash
mosquitto -c /data/data/com.termux/files/usr/etc/mosquitto/mosquitto.conf
```
