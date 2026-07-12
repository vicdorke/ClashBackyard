Mihomo 服务端部署教程

本项目基于开源脚本 clash-for-linux-install 搭建。
原理简述
该脚本运行时会自动将 mixin.yaml 与你自己的 mihomo 配置文件合并生成最终的 runtime.yaml,合并时如有冲突,以 mixin.yaml 为准。
因此你需要做两件事:

修改 mixin.yaml(主要是端口、密码等运行时配置)
在你自己的 mihomo 配置文件末尾追加 listeners: 部分(服务端监听配置)

下面提供两个示例文件供参考:

mixin.yaml

MihomoVPS.yaml

请自行托管自己的MihomoVPS.yaml到你自己的GitHub(或其他任意地方),文件中所有 XXX 占位符替换成自己的实际值即可使用。

💡 如果你已经有自己的客户端配置文件,也可以直接把示例里的 listeners: 部分复制过去、改一下参数,同样能用,只是配置风格可能不如示例顺手。


💡 如果需要用到面板(Dashboard)等功能,记得同步修改 mixin.yaml 里的端口和密码。


部署步骤
1. 克隆并安装脚本

git clone --branch master --depth 1 https://github.com/nelvko/clash-for-linux-install.git \
  && cd clash-for-linux-install \
  && bash install.sh

安装过程中会提示你输入服务端的订阅地址。
3. 关闭本机代理
安装完成后,先关闭本机代理模式(避免影响后续调试):
bashclashoff -e
4. 定位安装目录
默认安装目录为 /root/clashctl,后续配置文件都在 /root/clashctl/resources 目录下。
5. 覆盖 mixin.yaml
用改好的 mixin.yaml 覆盖 /root/clashctl/resources/mixin.yaml。
6. 准备证书目录
新建证书文件夹,把你自己网站的 TLS 证书放进去:
/root/clashctl/resources/certs/fullchain.pem
/root/clashctl/resources/certs/privkey.pem

💡 初次调试建议先用 Shadowsocks 这类不依赖证书的协议跑通,确认基础链路没问题后,再逐步启用需要 TLS 证书的协议(VLESS、Hysteria2 等)。

6. 更新服务端配置
bashclashsub update 1
配置更新后即可生效。
