# 电脑相关
--------------------------------------------------

# 1. 功能软件

## 1.1 Apollo
该平台在简化动画制作流程、提高效率方面发挥了至关重要的作用。可同时查看所有assets, 不论储存在哪里。

## 1.2 MoonRay
光线追踪渲染器 \
用于HTTYD3, 这款基于物理的渲染器在电影中得到了应用。它具有超高的交互性, 能够更快速、高效地调整最终效果, 从而在更短的时间内迭代多次。这对于提升整体画面质量至关重要。

## 1.3 PREMO
动画软件 \
更流畅的交互性能使得细微的表情动作能够充分展现。不再需要调整数值列表或艰难地选取线框来调整控制器, 而是可以在触控屏上轻松地摆弄角色, 就像玩芭比娃娃一样轻松。


--------------------------------------------------
--------------------------------------------------
# 2. 网络相关 

## 2.1 查看电脑ip (win)
1. win + R
2. cmd
3. 输入 ipconfig /all

## 2.2 SSH in VSCode
1. Win + R, cmd, 输入ssh, 确保 Windows 支持 ssh
2. VSCode 安装Remote - SSH 插件
3. 左栏 ![VSCode远程资源管理器]
4. 连接远程服务器: 顶栏输入ssh 用户名@ip地址 -p 22

## 2.3 用网线连接nac(Linux)
1. nac连显示器, 输`ifconfig`, 看到ip地址
2. 试着在电脑上 ping 地址
3. 用ssh连


--------------------------------------------------
--------------------------------------------------
# 3. Vim
- 插入模式 i
- 回到命令模式 ESC
- 保存并退出 :wq
- 不保存并强制退出 :q!
- 不保存并强制退出当前宏 :qa!


--------------------------------------------------
--------------------------------------------------
# 4. 软件

## 4.1 OpenCV
Computer Vision 计算机视觉, 视频和图像, 二维

## 4.2 OpenGL
Graphics Library 三维


--------------------------------------------------
--------------------------------------------------
# 5. VSCode

## 5.1 配置文件
C:\Users\Frost\AppData\Roaming\Code\User\settings.json

## 5.2 调试
#### 单步调试
- Run, Step Over (F10): 不进入函数内部, 一步执行完函数
- Run, Step Into (F11): 进入函数内部

## 5.3 快捷键
#### 在文件中禁用折叠行(超出屏幕的文本显示在下一行)
`Alt + Z`

--------------------------------------------------
--------------------------------------------------
# 6. Windows 相关操作

## 6.1 PowerToys 窗口置顶
Win+ Ctrl + T


--------------------------------------------------
--------------------------------------------------
# 7. 其他知识
- x86架构: 是一种复杂指令集计算 (CISC) 架构, 指令集较为复杂, 适合高性能的桌面和服务器环境。x86处理器通常功耗较高。
- ARM架构: 是一种精简指令集计算 (RISC) 架构, 指令集相对简单, 主要目标是低功耗、高效能, 因此常用于移动设备、嵌入式系统等功耗敏感的环境。








--------------------------------------------------
--------------------------------------------------
[VSCode远程资源管理器]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAoAC8DASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDgaKK9Jt9Sj8PfDvT7+30+0nmlkIczxbs9KTdlcFq7Hm2aM12f/Cx7v/oD6V/4D/8A16P+Fj3f/QH0r/wH/wDr0wOMzzRXpmia+PE2m6rHd6bYxCG2LKYYdpzkV5nSbs7CTuFd3q//ACSrS/8Arqf6VwlehwwWuu/D+w05NStYJoXJdZWwRSlsxr4keeVvaJ4Q1DWrdrtWjt7RThp5Thf/AK9XLjwQ1vA0q6pZzFRnYj5Lewroda0830uk6DBO8Fm1pviaMZUvxy3tTCzZDpOiXPh3TdRubZ4dVtp4DG0ls4OzpzjnPSvO69I8LNZ6ZcWFjYyxTXMs7Q3oJySMHoP7vHWuH12BLfXr6GLGxLhwuPTcaGveGo2uzOpckDjiiimI6+38fJbxKi6DZ7lXaHzz9elT6R40sX086drVtMIEBWGW2b95Gp/h7cdKKKH3DyEXxL4b0GCSTw5Z3LXsoKGe6xmMe3WuMlleaRpZGLs53MT1JNFFLzHsf//Z