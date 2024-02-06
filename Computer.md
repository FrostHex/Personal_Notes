# 电脑相关

## 查看电脑ip (win)
1. win + R
2. cmd
3. 输入 ipconfig /all


------

## Vim

插入模式 i

回到命令模式 ESC

保存并退出 :wq

不保存并强制退出 :q!

不保存并强制退出当前宏 :qa!




------

## Shell

#### .sh脚本示例
```shell
#!/bin/bash 
# 上一行告诉操作系统用Bash解释器来执行该脚本 

# 设置变量
name="Alice"
age=30

# 打印
echo "欢迎 $name!"
echo "你的年龄是 $age 岁。"
```


#### 运行脚本
让脚本具有执行权限
``` 
chmod +x myscript.sh
```
运行
``` 
./myscript.sh
```


#### 用Bash解释器运行脚本
``` 
bash myscript.sh
```
