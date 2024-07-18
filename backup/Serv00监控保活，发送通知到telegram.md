serv00保活定时发送消息，本来是参考这个项目   [Serv00_auto_script](https://github.com/curry-he/Serv00_auto_script)

看作者是发送到微信机器人和pushplus，虽然也有telegram的选项，但没有成功，sh和py脚本都有问题


将通知发送到 Telegram，需要先做准备工作

### 1. 创建 Telegram Bot 并获取 Token
首先，需要在 Telegram 上创建一个 Bot 并获取其 Token。你可以通过以下步骤创建一个 Bot：

打开 Telegram，搜索 @BotFather 并开始对话。

发送 /start 开始。

发送 /newbot 创建一个新 Bot。

按照提示给你的 Bot 取一个名字和用户名。

创建完成后，你会收到一个 Token，用于通过 Telegram API 发送消息。

token样式类似**123455:jklsdfjlksdjklfjlka**

### 2.  获取你的 Chat ID
你需要获取你的 Telegram Chat ID，用于将消息发送到特定的聊天窗口。可以通过以下步骤获取：

在 Telegram 中搜索并开始与 [@userinfobot](https://t.me/userinfobot)  [(https://t.me/userinfobot)](https://t.me/userinfobot)对话。

发送 /start。

你会收到一条包含你 Chat ID 的消息。

### 3.脚本修改

需要自己修改里面的参数

命令行使用以下命令,domains文件夹下执行(其他目录也行，自己改下参数路径）


```
# 使用 cat 命令创建脚本文件
cat << 'EOF' > Serv00-Renew.sh
#!/bin/bash

download_python_file() {
    local url="$1"
    local filename="$2"
    if command -v curl &> /dev/null; then
        curl -L "$url" -o "$filename"
    elif command -v wget &> /dev/null; then
        wget -O "$filename" "$url"
    else
        echo "错误：未找到 curl 或 wget。请安装其中之一以继续。"
        exit 1
    fi
    
    if [ $? -eq 0 ]; then
        echo "成功下载 $filename"
    else
        echo "下载 $filename 失败"
        exit 1
    fi
}

install_required_modules() {
    local filename="$1"
    echo "正在分析 $filename 所需的模块..."
    
    modules=$(grep -E "^import |^from " "$filename" | sed -E 's/^import //; s/^from ([^ ]+).*/\1/' | sort -u)
    
    for module in $modules; do
        if ! python3 -c "import $module" 2>/dev/null; then
            echo "正在安装模块: $module"
            pip3 install "$module"
        fi
    done
}

# 设置环境变量
export HOSTNAME="你的name.serv00.net"
export USERNAME="你的name"
export URL="http://你的name.serv00.net" #前提是你没有删除自己的默认网站，删除了就用自己搭建应用的网址
export SSH_PASSWORD="密码"
export BOT_TOKEN="2342342342342:dsfsddfsdfsfdfsfsdfsd" #上面获取的
export CHAT_ID="234234234"  #上面获取的

download_python_file "https://raw.githubusercontent.com/elderSword/Serv00_auto_script/master/Auto_connect_SSH-TG.py" "Auto_connect_SSH-TG.py"

install_required_modules "Auto_connect_SSH-TG.py"

pip uninstall --user telegram
pip install --user python-telegram-bot


python3 ~/domains/Auto_connect_SSH-TG.py
EOF

# 添加可执行权限
chmod +x Serv00-Renew.sh

# 执行脚本
./Serv00-Renew.sh
```

**Auto_connect_SSH-TG.py 必须使用我修改的路径下载，原来的脚本ssh有问题**


执行完毕看看TG消息

![image](https://github.com/user-attachments/assets/249c4b00-5467-42a3-9c5d-737452a12b5d)

如果是上图，最好先看看URL参数是否合适
正常是下图

![image](https://github.com/user-attachments/assets/79be9661-745a-48fc-805a-51c9a247caf9)



最后再添加corn job
这个间隔自己控制，我设置的是1小时检测一次

<img width="1116" alt="image" src="https://github.com/user-attachments/assets/f0f442fa-feea-400c-932a-7b473610ced1">


选Hourly
command：  sh ~/domains/Serv00-Renew.sh

