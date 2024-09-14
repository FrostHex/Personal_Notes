# Shell (Linux)
--------------------------------------------------

# 1. 基础

## 1.1 .sh脚本示例
```shell
#!/bin/bash 
# 上一行告诉操作系统用Bash解释器来执行该脚本 

# 设置变量
name="Alice"
age=30

# 打印
echo "欢迎 $name!"
echo "你的年龄是 $age 岁。"

# 定义宏
readonly pi=3.14

# 加$使用 变量、宏 
echo $pi
sleep $(($time + 5)) # 等待2+5秒
```

## 1.2 运行脚本
- 让脚本具有执行权限
``` shell
chmod +x myscript.sh
```
- 运行脚本
``` shell
./myscript.sh
```
- 用Bash解释器运行脚本
``` shell
bash myscript.sh
```


--------------------------------------------------
--------------------------------------------------
# 2. Shell脚本内用xfce4终端执行命令

## 2.1 Ubuntu用终端安装xfce4: 
```shell
sudo apt-get install xfce4-terminal
```
#### 常用格式: 
```shell
xfce4-terminal  --tab -e  'bash -ic " 指令 ; bash ; " '  -T "标签名" &

sleep 2  # 等待2秒

xfce4-terminal  --tab -e  'bash -ic " 指令 ; 指令 ; 指令 ; bash ; " '  -T "标签名" &
# 只要更改 想在终端中运行的指令 就行
# 一个标签页运行多个指令 中间用;隔开

xfce4-terminal  --tab -e  'bash -ic "cd .. ; ls ; bash ; " '  -T "标签名" &
# --tab 为了打开新的标签页, 而不是新开xfce4终端
# -e 表示要执行后面的命令
# -i 让窗口可以交互
# -c 表示后面跟随一个命令
# 执行 cd .. 和 ls 指令, 中间用;隔开
# bash; 为了让终端保持开启
# & 让多个 xfce4 终端可以同时运行
# -T "标签名" 设定这个标签页的名称
```