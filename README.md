# Mojo-Webqq-Docker

使用docker来启动Mojo-Webqq，适用于不想在本机安装过多插件和应用，希望能快速推倒重启的童鞋。

灰灰官方也有[Dockerfile](https://github.com/sjdy521/Mojo-Webqq/blob/master/docker-image/Dockerfile)模板，但是用命令行方式启动带入模块及参数有些许麻烦。故在原有模版的基础上稍加改进，结合[Mojo-Webqq-Scripts](https://github.com/hzz1989/Mojo-Webqq-Scripts)来启动Mojo-Webqq，希望能带来用脚本启动时的熟悉体验。

## Mojo::Webqq项目地址:
[Mojo::Webqq](https://github.com/sjdy521/Mojo-Webqq)  
感谢[灰灰](https://github.com/sjdy521)的倾情付出.

## 使用方式：

1. 克隆项目。

```shell
git clone https://github.com/hzz1989/Mojo-Webqq-Docker.git
```

也可以直接下载解压：

```shell
wget https://github.com/hzz1989/Mojo-Webqq-Docker/archive/master.zip -O Mojo-Webqq-Docker.zip

unzip Mojo-Webqq-Docker.zip
```

2. 修改`login.pl`文件。

修改`login.pl`文件，添加或删减功能。

具体可参考：[Mojo::Webqq使用简介](http://www.huangzhongzhang.cn/mojo-webqq-shi-yong-jian-jie.html)

```shell
cd Mojo-Webqq-Docker
vim login.pl
```

3. 创建docker镜像。

```shell
# 添加daocloud加速器
sudo curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://929e52fa.m.daocloud.io
sudo systemctl restart docker

# 构建镜像
cd Mojo-Webqq-Docker
docker build -t mojo-webqq .
```

4. 启动镜像并扫描二维码。

（我这里直接加入了hosts启动。）

```shell
docker run -t \
--name Mojo-Webqq \
--env MOJO_WEBQQ_LOG_ENCODING=utf8 \
-p 5011:5011 \
-v /home/ubuntu/Mojo-Webqq-Docker:/root \
--add-host ssl.ptlogin2.qq.com:163.177.71.148 \
--add-host ui.ptlogin2.qq.com:182.254.38.53 \
--add-host smtp.qq.com:14.18.245.164 \
--add-host ptlogin4.web2.qq.com:14.17.41.156 \
--add-host w.qq.com:121.51.142.15 \
--add-host s.web2.qq.com:121.51.142.33 \
--add-host d1.web2.qq.com:182.254.38.67 \
--add-host qun.qq.com:182.254.104.46 \
--add-host www.tuling123.com:182.92.110.58 \
--dns 114.114.114.114 \
mojo-webqq
```

**示例**

![mojo-webqq-docker-eg](https://huangzz.xyz/uploads/mojo-webqq-docker-eg.gif)