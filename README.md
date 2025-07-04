# S-UI
**高级Web面板•专为SagerNet/Sing-Box打造**


> **免责声明：** 本专案仅供个人学习与交流，请勿用于非法目的，请勿在生产环境中使用

**如果你觉得这个项目对你有帮助，不妨给一个**:star2:


## 快速概述
| Features                       |      Enable?       |
| ------------------------------ | :----------------: |
|多协议	                         | :heavy_check_mark: |
| 多语言	                         | :heavy_check_mark: |
| 多客户端/入站                   | :heavy_check_mark: |
| 高级流量路由接口                | :heavy_check_mark: |
| 客户端 & 交通 & 系统状态        | :heavy_check_mark: |
| 订阅服务 （link/json + info）  | :heavy_check_mark: |
| 深色/浅色主题                  | :heavy_check_mark: |
| API 接口                      | :heavy_check_mark: |

## API 文档

[API 文档](https://github.com/alireza0/s-ui/wiki/API-Documentation)

## 默认安装信息
- 面板端口: 2095
- 面板路径: /app/
- 订阅端口: 2096
- 订阅路径: /sub/
- 用户/密码: admin

## 安装并升级到最新版本

```sh
bash <(curl -Ls https://raw.githubusercontent.com/laowangi888/s-ui-cn/master/install.sh)
```

## 安装旧版本

**第 1 步：** 要安装所需的旧版本，请将版本添加到安装命令的末尾。例如，版本，ver `1.0.0`:

```sh
VERSION=1.0.0 && bash <(curl -Ls https://raw.githubusercontent.com/laowangi888/s-ui-cn/$VERSION/install.sh) $VERSION
```

## 手动安装

1. 从 GitHub 获取基于您的作系统/架构的最新版本的 S-UI: [https://github.com/laowangi888/s-ui-cn/releases/latest](https://github.com/laowangi888/s-ui-cn/releases/latest)
2. **可选** 获取最新版本的 `s-ui.sh` [https://raw.githubusercontent.com/laowangi888/s-ui-cn/master/s-ui.sh](https://raw.githubusercontent.com/laowangi888/s-ui-cn/master/s-ui.sh)
3. **可选** 复制 `s-ui.sh` to /usr/bin/ and run `chmod +x /usr/bin/s-ui`.
4. 将 s-ui tar.gz 文件提取到您选择的目录，然后导航到提取 tar.gz 文件的目录。
5. 复制 *.service 文件 到 /etc/systemd/system/ 然后运行 `systemctl daemon-reload`.
6. 使用  `systemctl enable s-ui --now` 启用自动启动和启动 S-UI 服务
7. 使用  `systemctl enable sing-box --now` 启动 sing-box 服务

## 卸载 S-UI

```sh
sudo -i

systemctl disable s-ui  --now

rm -f /etc/systemd/system/sing-box.service
systemctl daemon-reload

rm -fr /usr/local/s-ui
rm /usr/bin/s-ui
```

## 使用 Docker 安装

<details>
   <summary>点击了解详情</summary>

### 用法

**第 1 步:** 安装 Docker

```shell
curl -fsSL https://get.docker.com | sh
```

**步骤 2:** 安装 S-UI

> Docker compose 方法

```shell
mkdir s-ui && cd s-ui
wget -q https://raw.githubusercontent.com/laowangi888/s-ui-cn/master/docker-compose.yml
docker compose up -d
```

> 使用 docker

```shell
mkdir s-ui && cd s-ui
docker run -itd \
    -p 2095:2095 -p 2096:2096 -p 443:443 -p 80:80 \
    -v $PWD/db/:/usr/local/s-ui/db/ \
    -v $PWD/cert/:/root/cert/ \
    --name s-ui --restart=unless-stopped \
    alireza7/s-ui:latest
```

> 构建您自己的镜像

```shell
git clone https://github.com/laowangi888/s-ui-cn
git submodule update --init --recursive
docker build -t s-ui .
```

</details>

## 手动运行 ( contribution )

<details>
   <summary>点击了解详情</summary>

### 构建并运行整个项目
```shell
./runSUI.sh
```

### 克隆存储库
```shell
# clone repository
git clone https://github.com/laowangi888/s-ui-cn
# clone submodules
git submodule update --init --recursive
```


### - 前端

访问 [s-ui-frontend](https://github.com/alireza0/s-ui-frontend) 前端代码

### - 后端
> 在此之前构建一次前端！

To 构建后端：
```shell
# 删除旧的前端编译文件
rm -fr web/html/*
# 应用新的前端编译文件
cp -R frontend/dist/ web/html/
# 编译
go build -o sui main.go
```

要运行后端（从root的根文件夹）：
```shell
./sui
```

</details>

## 语言

- 英语
- 波斯语
- 越南语
- 中文 （简体）
- 中文 （繁体）
- 俄语

## 特点

- 支持的协议：
  - 常规:  Mixed, SOCKS, HTTP, HTTPS, Direct, Redirect, TProxy
  - 基于V2Ray: VLESS, VMess, Trojan, Shadowsocks
  - 其他协议: ShadowTLS, Hysteria, Hysteria2, Naive, TUIC
- 支持 XTLS 协议
- 用于路由流量的高级接口，包括 PROXY Protocol、External、和 Transparent Proxy、SSL Certificate 和 Port
- 用于入站和出站配置的高级界面
- 客户的流量上限和到期日期
- 显示在线客户端、入站和出站流量统计信息，以及系统状态监控
- 能够添加外部链接和订阅的订阅服务
- 用于安全访问 Web 面板和订阅服务的 HTTPS（自备域 + SSL 证书）
- 深色/浅色 主题

## 推荐系统

- Ubuntu 20.04+
- Debian 11+
- CentOS 8+
- Fedora 36+
- Arch Linux
- Parch Linux
- Manjaro
- Armbian
- AlmaLinux 9+
- Rocky Linux 9+
- Oracle Linux 8+
- OpenSUSE Tubleweed

## 环境变量

<details>
  <summary>点击了解详情</summary>

### 用法

|     变量       |                      类型                      |    Default    |
| -------------- | :--------------------------------------------: | :------------ |
| SUI_LOG_LEVEL  | `"debug"` \| `"info"` \| `"warn"` \| `"error"` | `"info"`      |
| SUI_DEBUG      |                   `boolean`                    | `false`       |
| SUI_BIN_FOLDER |                    `string`                    | `"bin"`       |
| SUI_DB_FOLDER  |                    `string`                    | `"db"`        |
| SINGBOX_API    |                    `string`                    | -             |

</details>

## SSL 证书

<details>
  <summary>点击了解详情</summary>

### Certbot

```bash
snap install core; snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot

certbot certonly --standalone --register-unsafely-without-email --non-interactive --agree-tos -d <Your Domain Name>
```

</details>

## 随时间推移的观星者
[![Stargazers over time](https://starchart.cc/alireza0/s-ui.svg)](https://starchart.cc/alireza0/s-ui)
