
VLESS + REALITY


CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -ldflags "-s -w -buildid=" ./main


xray run [-c config.json]


xray run -c config.json


xray tls ping www.shopee.ph

ShortID 生成
openssl rand -hex 4

./xray x25519
# 输出：
# Private key: <你的私钥>
# Public key: <你的公钥 - 填入 FlClash>


[ec2-user@ip-172-31-37-57 XXXray-core]$ ./xray x25519
PrivateKey: gHb14UNmm2F5czUjv2FkUXmwLIyiRYAJMWMYvI1qLkU
Password (PublicKey): Mp0owuyq9zTX8dwr6x_Od4VQDFq6cRLs1-IVjkUR4Wk
Hash32: v0pNWTuShZ5Kc9h4ikdC5I2h4ARqWnmOyg6Cg2ToLsw

python3 -m http.server 8080

./xray uuid


启动	systemctl start xray	立即启动服务
停止	systemctl stop xray	立即停止服务
重启	systemctl restart xray	停止并重新启动（常用于修改配置后）
开机自启	systemctl enable xray	设置为开机时自动运行
禁用自启	systemctl disable xray	取消开机自动运行
查看状态	systemctl status xray	最常用，查看运行情况及最近日志


1. 检查443端口是否正确（注意不要同时开启Nginx等其他443端口的程序）
sudo ss -lpnt | grep xray

   
2. 验证“回退”逻辑是否生效（REALITY 核心验证）:
curl -I -v --sni www.microsoft.com https://你的服务器IP
期望结果： 如果看到返回的是微软的证书信息和 HTTP 状态码，说明 REALITY 的“伪装迷彩”已经完美生效了。

3. AWS 安全组 (Security Group) 和 系统防火墙 (iptables/ufw) 放行443端口
sudo ufw allow 443/tcp

#### FlClash 了。记住这几个关键点：

UUID：必须完全一致。

Public Key：使用你生成私钥时对应的那个公钥。

Flow：填 xtls-rprx-vision。

SNI：填 [www.microsoft.com](https://www.microsoft.com)。




/usr/lib/systemd/system/xray.service

编辑后刷新配置：
sudo systemctl daemon-reload

# 1. 让服务立刻在后台跑起来
sudo systemctl start xray

# 2. 设置为开机自动启动
sudo systemctl enable xray

# 3. 查看网络日志
sudo journalctl -u xray.service -n 50