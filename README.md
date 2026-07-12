本项目基于以下脚本：

https://github.com/nelvko/clash-for-linux-install

先给两个样例，需要你自己托管在你的github等其他什么乱七八糟的地方。
里面XXX自己改一下就能用了，这个脚本的原理是他自己有一个mixin.yaml会和你自己的mihomo配置文件合成成一个runtime.yaml文件运行，所以你需要修改mixin.yaml配置，和在你的mihomo配置文件底下加上listeners: 之后的服务端配置。

初次使用你也可以用你自己的客户端文件加我的listeners: 配置改一下大概就能自己用了，只是可能不太顺手。

要用面板什么的功能还是要改一下mixin文件，主要是端口和密码

mixin.yaml

MihomoVPS.yaml

```
git clone --branch master --depth 1 https://github.com/nelvko/clash-for-linux-install.git \
  && cd clash-for-linux-install \
  && bash install.sh
```

然后输入你的服务端订阅地址之后

关闭本机代理
`clashoff -e`

默认安装目录是  root/clashctl

/root/clashctl/resources  此目录

覆盖mixin.yaml

这里新建一个证书目录，把你的网站证书tls放进来，初次运行可以先试试ss，这些不要证书的协议，能跑通再说。

新建证书文件夹，tls

/root/clashctl/resources/certs/fullchain.pem

/root/clashctl/resources/certs/privkey.pem

更新服务端配置

clashsub update 1
