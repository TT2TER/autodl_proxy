v2raya等deb包为24/7/9能获取到的版本，除非有重大bug，本仓库不主动更新，请自行寻找最新版包

如遇到v2ray等重大安全bug欢迎提pr

# 本项目只做指南，提供autodl中快速科研思路，请勿用作违法用途
# 本项目不能教会你如何获取代理链接以及如何开启代理，请勿打扰

# 使用方法
首先想办法将这个项目解压在autodl-tmp文件夹下，然后执行以下
## 1. 安装代理软件

使用的是 v2raya，文档[点这里](https://v2raya.org/docs/prologue/introduction/)

```bash

sudo apt install /root/autodl-tmp/autodl_proxy/installer_debian_x64_2.2.5.6.deb
sudo apt install /root/autodl-tmp/autodl_proxy/v2ray_5.16.1_amd64.deb
sudo apt install /root/autodl-tmp/autodl_proxy/xray_1.8.16_amd64.deb

v2raya
```
开启端口转发在本机电脑打开：$ssh -L 2017:localhost:2017 user@remote_server$

http://127.0.0.1:2017


## 2. 使用代理
开启代理：

```bash
export http_proxy="http://127.0.0.1:20171" && export https_proxy="http://127.0.0.1:20171"
```

关闭代理：

```bash
unset http_proxy && unset https_proxy
```
## 进阶使用方法，将代理开关添加到 `~/.bashrc` 中

可以直接将 `pon` 和 `poff` 命令加入到 `~/.bashrc` 中，这样您可以在每次启动新终端时通过输入 `pon` 或 `poff` 来启用或禁用代理。

以下是具体步骤：

### 1. 编辑 `~/.bashrc` 文件

```bash
vim ~/.bashrc
```

### 2. 在文件末尾添加以下内容

```bash
# Function to enable proxy
function pon() {
    export http_proxy="http://127.0.0.1:20171"
    export https_proxy="http://127.0.0.1:20171"
    echo "Proxy enabled: $http_proxy"
    
    # Check connection to Google
    if curl -s --head --request GET http://www.google.com | grep "200 OK" > /dev/null; then 
        echo "Connection to Google successful"
    else
        echo "Failed to connect to Google"
    fi
}

# Function to disable proxy
function poff() {
    unset http_proxy
    unset https_proxy
    echo "Proxy disabled"
}
```

### 3. 保存并退出编辑器

按 `Esc` 键，然后输入 `:wq` 并按 `Enter` 键保存并退出编辑器。

### 4. 使更改生效

运行以下命令使更改立即生效：

```bash
source ~/.bashrc
```

### 5. 使用 `pon` 和 `poff` 控制代理

现在，您可以在终端中使用 `pon` 和 `poff` 命令来启用或禁用代理：

启用代理：

```bash
pon
```

禁用代理：

```bash
poff
```

这样，您就可以方便地在终端中控制代理的开关，而无需每次都编辑脚本文件。
