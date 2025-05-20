# Linux ROS2
--------------------------------------------------

# 1. 安装相关

## 1.1 安装.deb文件
```shell
sudo dpkg -i package-file-name.deb
```
修复依赖关系:
```shell
sudo apt install -f
```

## 1.2 便捷启动程序
例如, Groot2软件的安装位置是`~/dev_ws/Groot2/bin/groot2`, 每次都需要cd进这个目录, 用`./groot2`命令来启动程序。**为了能打开终端后在任何位置都可以用`groot2`命令直接启动这个程序**: 
1. 在 `.bashrc` 文件内添加一行 `export PATH="$PATH:~/dev_ws/Groot2/bin"`
2. 终端内运行命令`source ~/.bashrc`


# 1.3 删除用户密码
```shell
sudo passwd -d 用户名
``` 


--------------------------------------------------
--------------------------------------------------
# 2. 终端基础命令
```shell
# 列出终端所在路径
pwd

# 列出当前目录下的文件
ls

# 创建文件夹
mkdir 文件夹名

# 创建文件
touch 文件名.后缀

# 删除文件
rm 文件

# 递归删除文件
rm -R 文件夹名

# 进入目录
cd 文件夹名

# 返回上一层目录
cd ..

# 用更高权限安装应用/库
sudo apt install 应用名/库名

# 卸载软件包
sudo apt remove 软件包名

# 卸载软件包和配置文件
sudo apt purge 软件包名

# 在 NVIDIA Jetson 系列开发板上查看 CPU GPU 资源使用情况
sudo -H pip install jetson-stats
jtop
```


--------------------------------------------------
--------------------------------------------------
# 3. 功能包 & 节点

## 3.1 安装依赖
```shell
cd ~/dev_ws/src
sudo pip install rosdepc
sudo rosdepc init 
rosdepc update
```

```shell
cd ~/dev_ws
rosdepc install -i --from-path src --rosdistro humble -y
```

## 3.2 创建功能包
```shell
cd ~/dev_ws/src
ros2 pkg create --build-type ament_cmake package_name    # C++
ros2 pkg create --build-type ament_python package_name   # Python
```

## 3.3 编写程序
#### C++
- 在ROS2中, C++功能包中的.hpp文件通常用于声明类、结构体、模板和函数原型。然而, 它也可以包含函数体。这种做法在模板类或者内联函数的定义中比较常见。将函数体放在.hpp文件中可以让编译器在编译时期就看到函数的定义, 这对于模板和内联函数的优化非常重要。但是, 这样做可能会增加编译时间, 并且如果函数定义在多个地方被包含, 还可能导致链接错误。
- 通常的做法是在.hpp文件中声明, 在.cpp文件中定义。这样做的好处是保持代码的清晰结构, 提高编译效率, 并避免潜在的链接问题。但是, 对于模板类和内联函数, 由于它们需要在编译时期被实例化或优化, 所以它们的定义通常会放在.hpp文件中。

#### Python
```python
rclpy.spin(node)
    # 阻塞型循环, 不断查看队列, 若队列里有数据则进入回调函数处理
rclpy.spin_once(node)
    # 循环执行一次节点
```

## 3.4 构建功能包
排除某些功能包
```
在功能包目录中放置名为COLCON_IGNORE的空文件
```
构建
```shell
sudo apt install python3-colcon-ros
source /opt/ros/humble/setup.bash
cd ~/dev_ws
colcon build
```
```shell
# 只构建几个功能包
colcon build --packages-select my_package1 my_package2
```

package.xml储存功能包需要的依赖
编写python功能包时需要在setup.py中

```
entry_points={
    'console_scripts': [
        '节点名 = 功能包名.文件名:函数名',
        ...
```

## 3.5 节点的终端命令
```shell
# 运行功能包中的某个节点
ros2 run 功能包名 节点名

# 列出节点
ros2 node list

# 查看节点信息
ros2 node info 节点名
```


--------------------------------------------------
--------------------------------------------------
# 4. 话题
单向

## 4.1 话题消息的类型结构
由.msg文件定义
```msg
# 例如: 
# 通信数据
int32 x
int32 y
```
```
例如uint8[] xxx可表示数组
```

## 4.2 话题的终端命令
```shell
# 列出话题
ros2 topic list

# 查看节点信息
ros2 topic info /话题名

# 打印话题
ros2 topic echo /话题名

# 往话题发送一次消息
ros2 topic pub /话题名消息类型 消息 --once

# 往话题周期性发消息
ros2 topic pub --rate 频率赫兹 /话题名 消息类型 消息

# 录制 (保存到终端所在目录)
ros2 bag record /话题名

# 回放
ros2 bag play /话题名
```

--------------------------------------------------
--------------------------------------------------
# 5. 服务
节点间的你问我答, 双向。服务器唯一, 客户端可不唯一\
.srv文件定义数据结构:
```srv
# 例如: 
# request结构体 (客户端发送的请求)
int64 a
int64 b
---
# response结构体 (服务器端返回的应答)
int64 sum
```

## 5.1 查看接口数据结构在哪定义
```shell
ros2 service type /服务名
```

## 5.2 命令行请求服务器
```shell
ros2 service type /服务名
```


--------------------------------------------------
--------------------------------------------------
# 6. 通信接口
标准消息类型存放处于`/opt/ros/humble/share/`

列出系统内全部接口定义
```
ros2 interface list
```

查看某接口定义
```
# 查看标准定义例如
ros2 interface show sensor_msgs/msg/Image

# 查看功能包自定义例如
ros2 interface show 功能包名/action/xxx
```

查看功能包定义的接口
```
ros2 interface package 功能包名
```

自定义消息类型后需要放入CmakeLists, 例如: 
```
rosidl_generate_interfaces(${PROJECT_NAME}
    # 功能包目录下的
    "srv/GetObjectPosition.srv"
    ...
    )
```

引用自定义消息类型(python)
```python
from 功能包.其中某个文件夹 import 接口
# 例如: 
# 目录结构: learning_interface/srv/GetObjectPosition.srv
# from learning_interface.srv import GetObjectPosition
```


--------------------------------------------------
--------------------------------------------------
# 7. 动作
完整行为的流程管理, 一直有反馈, 就像有进度条, 可以把控进度

.action文件定义数据结构:
```
#目标
bool enable
---
# 结果
bool finish
---
# 反馈 (当前执行到的位置) 
int32 state
```

```
ros2 action list
ros2 action info /动作名
ros2 action send_goal /动作名 动作数据结构  "变量: 数值"
# 例如: 
# ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 3.14}"
    # 需要周期反馈结尾再加 --feedback
```


--------------------------------------------------
--------------------------------------------------
# 8.其他
- RCLCPP_INFO函数需要一个C风格的字符串作为参数。因此, 你需要调用.c_str()来将std::string对象转换为C风格的字符串。

## 8.1 ros2 run 命令传递参数给节点
- argc: 传递给节点的参数数量
- argv: 字符串数组, 包含了传递给节点的所有参数
```cpp
#include "rclcpp/rclcpp.hpp"
#include <iostream>

int main(int argc, char * argv[])
{
    rclcpp::init(argc, argv);

    // Print all command line arguments
    for (int i = 0; i < argc; ++i) {
        std::cout << "Argument " << i << ": " << argv[i] << std::endl;
    }

    // Your node logic here

    rclcpp::shutdown();
    return 0;
}
```

## 8.2 打印消息
- WARN: 程序遇到可能会影响其正常运行但不一定会导致错误的情况 \
    (例如, 如果输入数据不在预期的范围内, 或者某个操作需要的时间比预期的要长)
- ERROR: 程序遇到错误, 但仍然可以继续运行
- FATAL: 程序遇到无法恢复的错误, 无法继续运行
```cpp
RCLCPP_DEBUG(this->get_logger(), "我是DEBUG级别的日志, 我被打印出来了!");
RCLCPP_INFO(this->get_logger(), "我是INFO级别的日志, 我被打印出来了!");
RCLCPP_WARN(this->get_logger(), "我是WARN级别的日志, 我被打印出来了!");
RCLCPP_ERROR(this->get_logger(), "我是ERROR级别的日志, 我被打印出来了!");
RCLCPP_FATAL(this->get_logger(), "我是FATAL级别的日志, 我被打印出来了!");
```
![ROS2打印消息]







如果你的服务端节点可能会被长时间阻塞, 你可以考虑以下几种策略来确保服务请求能够及时处理: 

1. **多线程处理**: 你可以在服务端节点中使用多线程, 每个线程处理一个服务请求。这样, 即使一个线程被阻塞, 其他线程仍然可以处理新的服务请求。

```cpp
rclcpp::Service<my_service>::SharedPtr service =
  node->create_service<my_service>("my_service", 
    [](const std::shared_ptr<my_service::Request> request, 
       std::shared_ptr<my_service::Response> response) {
      std::thread([](std::shared_ptr<my_service::Request> request, 
                     std::shared_ptr<my_service::Response> response) {
        // 处理服务请求
      }, request, response).detach();
    });
```

2. **异步处理**: 你可以使用异步编程模型来处理服务请求。这样, 即使处理服务请求的函数需要长时间运行, 也不会阻塞事件循环。

```cpp
rclcpp::Service<my_service>::SharedPtr service =
  node->create_service<my_service>("my_service", 
    [](const std::shared_ptr<rmw_request_id_t> request_header, 
       const std::shared_ptr<my_service::Request> request, 
       std::shared_ptr<my_service::Response> response) {
      // 创建一个新的 future 对象
      std::future<void> future = std::async(std::launch::async, []() {
        // 处理服务请求
      });
    });
```





--------------------------------------------------
--------------------------------------------------
# Raspberry Pi 下的 Python 工程
## 虚拟环境下缺失 Raspbot_Lib 依赖
``` shell
# 进入虚拟环境，例如/home/pi/WorkSpace/env

# (env) pi@yahboom:~/py_install $ ls
# build dist Raspbot_Lib Raspbot_Lib.egg-info README.md setup.py

# (env) pi@yahboom:~/py_install $ whereis python3
# python3: ...   /home/pi/WorkSpace/env/bin/python3   ...

cd ~/py_install
sudo /home/pi/WorkSpace/env/bin/python3 setup.py install
```

## 虚拟环境下使用gpio
```shell
# 去官网查文档
pip install rpi-lgpio
```










--------------------------------------------------
--------------------------------------------------
# Robocup无人机仿真 (ROS1 Melodic)

## 欧拉角
roll pitch yaw \
缺点: 有万向锁 \
如果飞机俯仰角到达±90°时, 滚转运动和偏航运动的旋转轴重合了

## 四元数
四元数 w+xi+yj+zk 可以完备地表示任何一个旋转状态

## 强行关闭gazebo所有进程
```
killall -9 gzclient
killall -9 gzserver
```

## 用键盘控制无人机飞行

```
cd ~/PX4_Firmware
roslaunch px4 indoor1.launch
```

等Gazebo完全启动, 新开终端

```
cd ~/XTDrone/communication/
python multirotor_communication.py iris 0
```

新开终端

```
cd ~/XTDrone/control/keyboard
python multirotor_keyboard_control.py iris 1 vel
```

按 I 把向上速度加到0.3以上, 按 B 切offboard模式, 按 T 解锁。

飞到一定高度后可以切换为‘hover’模式悬停, 再利用键盘控制飞机, 或运行自己的飞行脚本。

![无人机目录]









--------------------------------------------------
[无人机目录]:data:image/jpeg;base64,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snY8BTjPU9eKq2Xi7Rb65Ftb6gRKchVeJlz9CeK42W0+zeENJhud4h1K8El5n05GD7YArofG1jp9v4ajnghRJbdkMDL1zjjFJPS43GweL32a7oqbjhnO7Hc5GK3tV1bT9GUT6jciINwAFLE/gK5nxE7TSeGnlXLMFLbu5O2nSQpe/E2SG+VZIobdGt0b7obnJ/LFUtvmyW76+R0el63p2tRb9PullVeSpQq35HmlsNSstSSY2U3m+Q+yRcEEN1xzXM6nHFa/EbS30yJVkuflujH3XBOT+OKabiLwr4t1Kafatvdwm7U+rDC4/Sm9NStzdvvEFummapLYzq9zYRkspQkK2MjPrWbpY8b3cVtdz6rpS20yq5QWbbiCM4zuo8OaKlz4bmS+YxPqTM0pXgkZOP0NUtTgv/BX2a8tNTuLyyaVIGtrp92NxCgrj0os07MUrdDtQQR0we+OlFIhDKGGQGAODS0CCiiikMKKKKACiiigAooooAKKKKACiiigAooooAKKKKACloFFABSUtFACUUUUAFFFFABRRRQAUUUUAFRX9pb6pYyWV3EJIZRgj+tS0UAc1beDXs5kYeI9QkhjYbbZgm1QO3TNQ+MH8PLeW51LUG0m7X/V3aYBx6c/4V1dMkigkx51vHNjpvQNijrcDiPCdrFP4vuL+2upr+2jtwhvJsZkbPQY4xzWteeCbea6llstSvNMErbpYrcKVc/iDXRosaDEUSxj0VQKWgdynpul2mkWa2lnGY4wcnHc+pq5z6iiiiwg/GiiigAooooAKKKKACiiigAooooAR8BC7MFVBliewrhNfk03xtqNjZaZP9oeGXdcPHysceD1/Gu9zwR2PWo0ighJ8uBIyepSMDP5UWGirf6bYahp/wDZ89ujQuuEz0HuKxrXwPaLdxyXWrXd/FC2Y4Jgu2P8gK6Xrzj6U7ijqIy9d8P22vRxRSTPC0DBopo8blwc4GeOcVHq/hq31WG2D3M0V1br8l2gG8cY57Vr8dutL81JIDF0Pwxb6NM11JdyX16/DXM+N5HpxxS+IPDNj4mWFL15UEDZBQDLj0rY+tFMFoZ9/pCX1gtotzPalMbZYgM8dOtZdr4Kt476K61DU7vVDFkxpchQqn14A5FdJRTvqAAEdTnjFFFFIAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAFozSUUALmikooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKXNJRQAUUUUAFFFFABRRRQAUUUUAFFFFAH/9k=

[ROS2打印消息]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAByAw4DASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDzEAswUDJPSpJbaeHHmRkE9B1NFr/x9xf71bCsz+JSrsWAbgNyBSbOerVcHp2bMMqw6ow+qkUuxwMmNwPXaa2LSZr37TFOAwjyytjpTtV85ZWC3UYTA/d456UX1sZ/WXz8jWv9eRi7XAyUcD12mkwc4wfyrp5VP2gKXRozAP3IHOcdapXaKNbtlCgDYvH4UkyYYvmdrdLmMFY9EY/Rc0+K3mnJEaFiOord1FGtrhLe1ZITK5YuR19qoQCaDW1jd8Nk7tnANNO5UMS5w5l2uZrAqxVhgjqKdHG8rhI1LMegFSXv/H9N/v1Z0TI1JCDjihPS5vKo1Sc/K5SlikhfZIu1vSmkEdQR9RirKz7b1nlHmncQN3OK0rmCO416NHChPLDEAcdBRczlWcGlJdG/uMXawGSjAepU0FHAyUcD1KmtiUrN++juA0UMoDJg8DNJeieYtLFOkturAlVGMDNFyViLtJq39ehkbHxny3x67TSYOM4OPXHFbV359ypNrcI8SoMxgYNRrIk2gzbIlQKcD1PSi4LEOyduqXpcyQCegJ+gzShWIyEYj1Cmt7S7YWqKrRbpZlySRnaKqaY0ouRG06xxq/MbD71Fw+s35rLb8TLCseiMfoM0YOcbTn0xzW3G4jS4iSRLeYyAqGHaorUyW+qpHcxq8rkYY9MUXD6w9dNjJ5zjBz6UFWX7ysv1GK2LaGFtRvJpdoWIkjIzg81W1FGeGO6E/mxuSBx0NFyo11Kajb+tyhSlXHVGH1U1Pp4U30QZC4z0rVvS8dlKxZZmD5Rl/gobsOpX5JqNtzDKOBkxuB7qaTa2M7Gx67TitZbqdNMZ7ghzOdqKR29auSIQsuNrReVxB3B9aGzKWJcd1+Jz2xyMiNyPXaaNjnpG5+imtqQy3EMaWdwgIU7o8cmoNMnujM298RQglgfX0ouV7d8rlbb+uxl+Wzf8smP/AAEmgITwI2OOwXpWzFc/aLVvJnjhmeQnBHUE8VXia+ivTbqq+aWy7EdqLjVeTumrNf12M4Kx4CMcdgKMNnG059Mc1qXEo/tVxazJEDwzY4Jq6yJ57OioZzFmNzwGOetFyZYlxSbW6OfCOWC7SGPQEYp0sEsBAlQrnp71pamki6dBLNgXGcEr171HqbM1nZlmLHYeT9aLlxrOTjbZtr7jOqV7WeOMSPGVQ9CahrV1h3L2se9tpRRjPHQUM0nNqcYrqZVFbRsLHz/sqh/MMe8Pu4HGabZ6bFMio8DksD+83gDp6daLmX1qCV2Y9Fa5s7C1tYpLje7O207Tj8abBZW7zSbIXnjDYVg4XA/Gi4/rMbN2djKorohotlG+2XeSzALhulQ/2TbMfNRHaMA/JuAJI96XMjNY2k+5idenP0orcitbS2voG8pj5gPybwdv1qBre2vdUaCKJoyGYsSw5xTuWsVFvbS17mTRW3JplswRlRovnwVMgYkfhUV1baZHJPAjOskRwGJyG5ouEcVCTskzJorUvbKGG3zBC8ny580OCPy61lN900zanUVRXQ943jCl1IDcjPem1vSpaTLZQzq7PIuFIONvNQWunRlzG8DyfPt3hwoHPvSuYLFR5byRkU6ON5XCRqWY9AK1Y9Nt0acMDM6MAsYYKcZ96i08Rx6mUaOSNjnbhsFaLlPEJpuPQz2UoxVhgg4IoVWdwqjJPQVoRWiT3128zEpCSW55NU55YGZWto3ix6tk0JlxqczskNlglgYLKhUmmVo6uWaO0LMSfK6n61UuvsxKfZgwG359x70JhTqOUU2tyEDJA9atS2H2eFXlmUF/uBec/jVeMlZAwQOR/CRkGtmZ2j063keC3Q7j8hT37UyK1SUZRS6mZcWUkA3bgw2gnnpmp7XS/tFoLgzBAWKgbc9Kt382Ud2iiVTGgB2cn1/Ki0uILezijEvyM/BIJ+bvSOd1qrpprf8A4BWm0jy7aSZZw3ljJG3FZ4ViMhGP0Umt68niRJreSTAPysQhqs87WukQNbkDMmM+oxQOjXqcuut3p0MkKxOAjE+wpdj5x5b59NprpPLAglnjKQPJHuJI6Gq1h5rS3Je5jdxEcSY4FK5Sxd03bb+uxh7WHBVh9RRg4zg49a6QIGtWZwsjeU+ZQODUGjW0U+luZFDbG3D3xzRcPriUXJrZ2MMRuzAeW/Jxypq0mmyy3DwxOpKDJJOK0rP7bcu8ySwlFJzGy/dH50wM0mouGhWNRGAqrg5HrxTuKWIldpW0RmXNlLaqjOVKvwCpzU66RcNsG+MM4yFLDNOuo7eWySS3kKpGcBGHT3q+uRaJOXtWlR9qyGPtigJ15qKtvr0+4xobZ5btbc/KxbbnHFLHaPIszDdtiyMhc5NasULQy26ybS/nrkjvTrXzBbwBJ1iVpjuUj73zGi4pYmW6/rf/ACMmKxmmtfPjGTuxtPBp0NjuWVriTyRFjOVz1qzctLLcSOkvl+VIBsTgHnrU8widbvz3KqUj570FOtP7/vWq/wAyh9ms8j/Tv/IZps1hIlyYYiJfl3Z6cU8Radkf6S3UdjUt80aako8544/LHzL1xQWpyUrJvZ7oiTSrpoHl2AbO2etQS2s8KhpE2g981ppNbJZODdzFXOA+TxWfdPGdoiuJJR33E0BSqVJSae3oyvSU4qwUMVIB6HHWkHDA4zz0pnWWhYbbY3MsyrHjgjnn0prWMiwrIrA7hnGcVpRO50eR3gt4sEYDJ978Ke8++3icxQqoQ5bZ04pHne3qX+djG8gm284bjg8jaf51PBpdzPDJIEwFXcM/xc1es0lk0yRpJUUHG1D2FW18uOBN1w6mSMRheeCDmgKmKlG6jvcw4rGaSV42VlZFyeM1JDpc84XY6At0UsAa0LB7xry6JlGwDBcnofpVGyIfWA27fk/e9aC/a1HzWa0V+5GdOm+0rAGRnYE8MMDFKNPLy+TFMrygEsOwA96XTdo1Jyy5Xa+QO/NWLUwNLKYbeSIeXJkucg8UFTqVItq+yKsumzRRiTcjKWC/KwPJpkVm73TW7EKy5z+FT2SsdOk8tMkSK2PXBzVuzurObUHf7LIsjBiTvGOlApVakVLra/6GSkLyQvMv3UGWqWGwuZim1Plfoc1MJ4ZbWS3tLV0Lj5izA4FWrK2lkMUUd4pYNkY449DQVUrSim3p6/8AAKE+nXMDupQEJ3zTYIreRCZbny2z02E1q31rLHNPG94qmQ8Z5AGKwnG3cM5x3oHRqOrDf7v+CX4rC1mJCXvQZJMZwKpbcylEO/nAPrVu9/0eOOCPhHXc3qTUNmdt7CemGH86ZUHLlc73XQidGjco4ww6ikqxqL79QmbOcsar0lqjaDcopsktiBdREnADVpXkr2Orm8ULIrH5fesy3i8+5jhzjzGxn0rS1XRrfTr4WUd8ss27a+TwtFiJ0lOV32sV21PEZS3gWEMcvj+Kkub6C5Yu1mokIA3Yq9ceFb63jhd54CJ/9WBn5/pUMvh3UIb+SydAJY4/MPpjGf607CVGmndDH1gM/mrbKs2zYHx2ximjVeVeS3WSZBgSGrEvhq6giWSe5t4ty7grZyRSW3hq/uYlcNHGXzsR87nx6UrC+r0rbEA1VpFUXUKz7W3KT1Bp9o7XurC6IVFBJb2p+l6JHqFzLaTXX2e5Td+7PfFZksflyvGTnY2M0aJ2B0I2fLp0JLwhr2Yg5Bbg1Y0ZlXUkLMFGOpp2i6SNXupIWnEKxpvZj6U2PS2vNQ+y6cxuRnG/0+tCXQuUE6bhfpYikUWl6xmjEoySBU8+rebcJcJbqki4GfUelMn0i8g1M6cY99wCBtWpn0G4W6itlngklkONq5yp96OwnRi7OW6IJNQRo2jjt1jR23OAPvUhvkWFore3WFX+/gfeFWLnQp7Z1jNzbySM4TYmcg5xS3ug3FipMtzblxjMa53UaAqMNrFZb+OGNltrZYmYYZsckVJFqUUVmbYWilW+8fU0tzoV/aaWmozx7IXOAD1pdP0K/wBStJ7q3QeVAMsx/pTtuJ0YPdbkdvrF3bybvOdlAwFJ4FMjvY1fzZbcSzA53tVmz0K4voQ8E8DOwyIudxpbbw9d3FsbhpYYIw23Muev4UD9jT3S3KovY3laW4tlmkJyCe1PTU8Xf2maESOuNn+zipbLQL7ULp4LVVk2dZB92oLXS7q7u3tok+aMkOx6LjrmlYHRg+nkP/tNRcvMtuoWQHzE7NUU975qxxpEscUZyEHekvbM2UojM8U3vHnH60llZz39yILddznn6D1oSvsCowi72JTqJW9W5ihSLaMbVHBpZdSDQSQwwLEspy+O9WZvDl3CqSGeBonYr5q52g+9Ofwzei0e5imgnRDg+XnOaLB7CF1psULi+ed4iFCLEMKo6Cp21fLvKtuqzuu0yVNP4bvoLeWbfE5hGZI1zuQe9Rf2JcpZi5nkigBGVSTO5h7UaWB0INJWIYr6OD5obVVmwf3mKYL1xaPAqgGRtzv3NXovDd9Lb+ajRFtpfyudxA70208O313AJgY4gxIRZM5cjsKLB7KG9ilb3FvCAXtVkkByGI6VZh1hozM0kCyPLwW7gelSQ6BcSsUa5t4ZA+zy5M7s5xUh8L6glxLDIYoxEBukbO3k4xTtcJUYT+JGeLi13ljZKVxwuOlPe/WV082ANFGuEj/u1ZXw7f8A2uS3cKnlDc0rfdx60y50d7C5hS9mVIZhlZk6Ee1Fh+yjuVri4e9ZIlUIg4RB0FWdUGy3tYywLIpyB25o1rSBpM0SLOJ0lTerD0rPRN8ioONxxSWuwnSScbbIbWtqke8W06spRVQHHbpRrOjwaSUiF551wyqxjHYEZrLMbhdxRgPWjcc6blJSvsa99qEcFyDBEpkMQHmVCmtFfLLW6tJGu1WNZ3lybd2xtvrilEcjDIRj+FFjJYamo2auT3N61zCkbIAFOc1JbakILUW7wCRVbcM+tU1jkfJVGbHXAoEchGQjEfSixo6UHHltoaT67K7q3kqNpBxioxq742PEGjwdy+uapeXIW2iNi3pirFjpt1qNz9ngjJcKWOR6UWRCw1JaJDTdotwk0EIiKHp61KdSAufPhgEbnO4/3s9aqyQyxSGN0YMCVxjqRTTHIrbWRgfTFBbpQe6LTX0PmrLFahGU5qCeb7RcvMyj52yRTCjqMsjAepFKY5FXc0bAepFFhxpxi7ouR36rG8NrbiIyjaTTDpVyRjK8+9VOvHrV/VdHk0uWNNxlDpu3DOBRsJU3F+47fj+o5tT8sxq1splgGFf0oj1ghEWWASGNiyk+uc1nrHIy7lRio7gULHI+diM2OuBRYn6vTtqi2b+J52nltQ7k5B9KcuqD7YbqWASPjC+wo0nTV1G6aKa4W1RUZvMfpkDpVNoyJmjT59pIBHenaw/YQtt5FsakFuZJUgVVlHzp2aoHMdxIiQQCIk4+tLbW8clykV1IbdGONx7VY1rSv7JvBbiYTBl3Bh3FLaxUaUY6xHaxgLbR7gWSPDY7c1UubhbgoViWLauPlHWoSpU4IIPoams7d7m6SJIXmJOSidSPaiwoU1FJdv1Io3ZJFZH2MDww7VfumgkS2ja6EhXczuM9+1bd74fkiazt7XSHaOZw0ksmN6gHkcHGKo65oUlmsssdpLEI8ZzjaR7Uxyp8zT7FWK+tpS0c6kIqkRk/TvTI5Ld4obZp9gibf5h6E9x+ldJpml6fJotpMbKKWR872bOah17TrGDQJZ47OKGZWAVlznqKDP6vHozJvZVupZMasvlOeEOcY/KqqahHHAtvJbrMsTZVsdan03w9darC8ttNCNgyytnIHrTZfD97Hp8t8pSW3ibazpnrRYIYeKjy7r7vyIxqzMZfPiEqyjG30FNgv4bdpPLtFEcilWTFW4/C+oSZJaKNRH5hZ84AqJdBupLryIZYZcKWaRM7UHvSsUqFO2i0IxqzIUWOFUhUEeX2OetINVeIKtrEIUByVHetSy8JXvnrNJGtzbjp5XRz6c01NLsILa6kvreczxTBfLixgBmwBz6UWQewp9jPGpW7rJGbbyxKcuycHNEN1bwkyQHyZG+UHuB6n61Jd2FmuuxWlu7+S4XcG+8pPUVs3Hhq0jN2v2K8hWEHZM+3a1FhfV4WsjBuZYLuLasojEZyFb+L3qJzDKY7VXWOJOshHDH1q9p+l4tbqS7jUk2azRe2Wxmra+F5ZNLijheCS+l/e7OdwXptpjVJJWTKEN1FLqXnPcCOKNgQpz82PSkiuLExweez7o5S3ynoM5q8ukaXeTWtkl6sF4AUkUdGfPFRl7PS9Ht3k0+3uZZHcM8gOeGI7UEPDx7v+v8AhzKcxz6gzeaEjLZDGrZu7SUXIlLhWCKu08nFWbHVLC6vobdtFswsjBSQGyM/jVZrPTDc3K3F99mKTOqoPQHjtQXKipW12IB/ZuRzcdf7wqS4urb7YZUUyKEAUH6961LnSdDTR7SYajsLyMDJ/e4HHSsO9htIZFFpdfaFI5b0oD2Kvdtls/Z5lbbeRwRS8tGQciqk7wCJ4UG8o3ySDuMf41XqW1ge5uUijiaVmP3F6n6UBGlyvcnubvdYw2asHWPnd6e1U8kEEdRyK6q98PyRWlslno8jfaPmkeTG+PBxjg4qvrXh17cyNFayQ7QnPG3kcmguEFBWRmTyJJpwjkuxLK7LnOflGafDeW6utvIC0AH3vU/4VZvNGzBaTI0AWR1jdos4ySADzWg3hrTP7O8v7eBOkrq0v+726UGfsI2s2YSSwNDcRFwgd8r9M1P/AGjCQq7uOi/7Huau2ugQPot1cNc27FG+V+cgZFMs7bQbq3u5vIu1+yxhyPl+bkD+tAnh4vcoW/kQPcSPeI5K7QMH56i0wwx3PnSzLGE6A5+ar1haabdJfXRhuDDAMpGAN3brUkcWnXFpc391ZPCsLiNYoR1yM5OaCnRumr7mRb3JtrozooY/MAD05NWbfUGeWQzyYQxsFUdASKv/ANk2F1JaNaiZI7iCSQq+MgqQBVW00/fpWoSvbsZIpFWMkcgc5oHKlCW6ILTUnh2RyKPKAIIXqalguNOgnaUCck54LDvTJtPWHSrO6csjzyMrg9gMc1raZoektfCOe+L7oi4RvTB5oJlQg79LmXay6fB5hRpQzJgbiMVBHcQwtGlupRM/OzdTU93p1lBYLc2960244UHoaWDVbaGFI20i0lZRgu27LfrQNUVdttu5DLcwzXEqzgvCWyjDqvHaqgRXk2b9ik43N2roLq6sYNOYT6RaR3My/u1TOUHqeazNH0ttXvGt1lEZWMvk+1BcYKKshmpSRPPGIpBIqIBuH0qtE4jlVyoYKc7T0NI67JHTrtYr+RpKAjBRjyj55RNO0gQIGP3R0FMoooKSsrIsaf8A8hK2/wCugrQ8VI0nia6RFLMW4A6npWXbSiC7imYZEbZIrS1vU7DUL831iZUnZssGXAH0o6oZ0V7Z3Kp4bLW8oCD5iR0+Y9avxkahcX8hOZ7SFkPqVIzmuDfVdQkUK927AdB6VEt3cozus7hpBhiD94U77/P8QS/T8DqvEtzYQyWiXVkZZDHkPk8Dj3o1Ozu73WtNu7KN2ttkeHT7qhQN1clLNLOQZXZyBgZ7VLFf3kMXlR3DrGf4QaE7O4rHS2csU/jqd4sbdjgkdzg5rl7v/j8m/wB81o6DqWn6XcNdXXmtPtYIAMg5GOTWZNIJZ5JAMB2JqLWa9P1Kve5u+D/+Py8/69/61Q0T7W2qRJarIwaT5wg7U/QNVt9Ku5ZLlWaOWPYdoyRVV7tLe6Z9LmkSM9Cy4NUtHcm100dmIpLfxreSSWzF2h/chxw5wOBVRmMVnFqc+liG+jn2pEM5lXJz/IVy0mo3ssivJcuzp91u4pHv7ySRZHuHZ0+6T2oKudFdWcBtP7YFjJZ3KTgiFs/vctz1NOvLSLVLO51GWxl0+4j2lGbOHOenJrmpb67nZWlnZypyue1LNf3lwoE1wzgHIHSkI6iS2vrnwPEbiGbc1wSxYdF45rT002kkEllY6hbtbRW/IVuS3qa4c6rqBj2G7fZjG3HFV4ppYSxicpuGDjvT7itovL/O50nhmAW+oRj7A8rFiEu1ztUeoqW2P2ktpU2myXkAnyLhc/0Nc2moXscPlJcMsYGNoFEV/eQR+XFcMi+go6jOp0KyntPFhtLRpZrOPnIHAPHBp2mCa0tdZCWRkuzKSInBBK88jFcpDf3ltkQ3DpuOTjqaP7RvfP8AO+0v5uMbqOgG1r1gJjYeTaCC9uFw8C568Y6+tL4d02+s/Eb20ymCaONi8bDkjB4rBe6uJJxO8zGUdGJ5FKby5Nx9oM7mb+/nmhA9UdXrVuZfDiC2t5LRDOR5D8FzxyKguIn00abo0MvlXDuJJyT0OCMGucmvry4ZTNcO5U5X2qOSaaWXzZJGaT+8TzQtAZ6DcRLu1MGCS3cL++uGHyyjio71ReanJBc6an2D7PkXOTgcDmuHl1C9ni8uW5dk9KDf3jQeQbhzFjG3PajoCOm03SrnRrSXV5YZpZHDJbRDnKnufyFarFZU0y9is3uZC+CB92I5GScVw66rqCoEF2+0DAB5xTI7+9iRljuHVWOSBTuFkzpzaxXfie91KUYtrUFnYH5S/OP1qG11D+3bOa1uobohpzIkkCg4yRwfbiuaFxOI2jErBHOWGetOgvLm2UrBMYweoApLsDd3c9AkCP8AaUjBnigtljlgX7zkN3rnvF0ZFtp7qGiiMY2W79Yxk1gRXlzBI0kU7o7dTnOacLkXF0r6jNI8f8RAyQPYUbsFobHi7/WWH/XD+tYUH/HxF/vitHX9VttVnga1Vljhj2DcME1mRtslRz/C2aUdPvf5g9jpdfAPi6zBGQRD/IVuTfaZtQvobuAJYCEbNygLuwcc/Wua1PWdMvdQtr6FZRPEU3qV4wuP8Kq6zrc+p3busrrCwGE6YxR0S9Q/4B2Wm6bLEfs80k0sZtd/liNfKHynHPXNZup6xLo9jpSwQoF8vL5X74x0rlhql+ECC7kCgYx7VBJNLMFEkhYLwue1N7gdxpEE0qW16jSxRXcu4QwRqwAx/FnpW1IBZytBDAioRkjaK8yh1G9gjEcVy6IOgHag6heMcm5kJ+tD8hdbs7+dQ1pPcL5iXPQtBGrPt+h4qnaapu8TQR2wmgLwMJBKgBkbjBrjE1C8R963LhsYz7U17u5kmWZ5mMi9GHBFOTux9Dq9GS7uNcuf7U80SRrJ5AZAD35A79qu2lxDLe2cU0FzLcxs7ebcRKuRjpxXEvqF5JIsj3DF0+63QilfUr2Rgz3LEr0OMYpdgN288RSy3lzZz2aTp9o/doB93B6CrOuQTalp9xfRyz28MZybaeNVA9lxya5ISyCXzQx35zu96tC/luZFS/uJXgz8wUc0W0sF9SmOo+or0aaS9Oq2kMkB/s/7P+9JX5SM9Sa48/8ACOY4a8z2/df/AF6pyandyK0Qu5Gh6AH0oeqsB3OkadJDcWaiWYwTsxEUUashXd/ETzVG0JYz6bBDcWrm4IWeGMMD8x65rk49TvooxHHdOqjoB2oTU76NSqXLKDyeKOoHTeHbXULfxBdWnzTw7JN7KoKscH9ai0e2ltoNVkitz/aCN+7Qr8wBJ5A+lc7DqN5bZ8q5aPccn3NIL+7E5nFwwlIwWHejpYOtyS7kv5bqI6gJPM3LjzFAPX2rW8V7v7Yttgy3lDA981kR3aT3aS6nK7xqQSVXmrOu6pDql+s9qrKiJtXPBo/l9Q7ia82oNqWdTg8m42/dxjiqVtGJZthuVtxj/WM2AKbNPLcSeZNI0jerUkZUSqWj8xQeUP8AF7UAdPrN5a27aTHG0jupB88nqARmk1uOVYXeNGmdysrEk/Kq84/EVQuL65uJYb5NM8uKFfKjAyVDHp+PFRQ61e2UU9rPH5izEMyycEUlJPZgbltqTpJp6m2gMd1nIDHC9Ki1nU/sxnRG0+cLIyiNJWLAfSqtje6ixSc6SbqFeIRyAv0I6029nCrJc3PhtY/MJJkLsBk1PtIXtdBYteDLW4k/tGRIJCjW+AwHBOataXKbLw/b290rJHPceXIrduM1ysOo3tsmyC4aJP7oqOW6uZhiSZmGd2PetL6gj0TUYo7KC8S4hMscdo2V9RkVz+myW17o+o22m2xinYZEYJJYY5xXOvfXcoYPcO24YOT1HpUcM0tvIJIXaNx3FL1C2x2OmyppXhlLbUTPDdTSfuFUZdeeeD+FU9OE0FhfNBJ++EymP7Tw0hyc/jWLBquoea2xzLLIMAlQSPpU39r3Q2KbbJh3AezHqfrmhu7DoW9ZurUXlr9ps088DdOkZOCSOB9c1p3Nxpt1cWGnTWjq7Q8jccpwfeuefVfMaOSeyR7hOshYgt6ce1JBqM0FzJeS23mzsPlkYkbPpRcDbM0Di9igcMINPSNvY+YOKurc2Y1COEW+Ln7LxLk9c1zdnqUkdjeRR2KySzp+9n3HIXIPTp1FWx4o1HyNwto/IVPJ3Y/HrjrSugE0Oe2l1TTlEeLlJ8M3Zhk1Nc6n/Z+i2w+zwy75Zf8AWE8fOayLO8bSpPPa2BlfLQu5I2+49a0rG/1p9MjitLAzRKzN5nl7sknPpScopXbANM8Q+bqdvH9htV3OBkE5HNRwm7TUtQe2sY7oCZt2/Py8n0q5Fe+I4pVk/ssnbzjyAP6VinV7q3uHIYRHzWdk9yeQaIzjL4XcDYvtbmgsrbNravGWK+WxOY371iah5z3Qlmt1gMoBVV+7g1fOs28a/aTo0QMu4CRpWwSRyRWZ9teUQLLiWO34Vfb61QFjVdJm0mSFJpEk86PzFZDkYzVa1j824VPPSDJ/1jnAX8aW8u5b2cyyn2Veyj0qJCBIpK7wDyvrQB02sXVtb6ZpcUbvM+xiLjd23c1JrUbSwOUDyNcIjls8xoo+Yis2e/nuBb3MeliOCzUogBJUE85JqGPWL+yW5gmXIuEIYOMFQR2pKSeiYG2txp0el6UkMLBmm+Rz3IIzWhqV9EIpI5beBbXMm9wTw+OPxzXKLqVxZ21vBJagGEMY3bjhu9O/tmYw7prZZbRhtKliAW9c+tF0Bc02SytfCd1KA9xMcB0k4VTkdMVV0c507WSev2Yf+hCo2vy+iyWkGnrHGxzJMrE5pLfUGttMns0sBvuF2PNk5xnPT8KLoC94aW9bTNT+wNtm28HGcdKdcefLol6st4l3IZ1G9MYB29OKwEadA0cZkXd95VOM1bL3dnZTafJbOvnOJDkYIwMUXWwG1NZ3FppFpMLjyLi0hc/Lz1Oe9Q2GvahJoWoStfEsrx4O1eM59qybHUr3THcwk5dcMJPmyPxq9H4k1XyJPLjj8oEb8RjHtnii6AiW5kv9ObUNRuDdR2zhfKIABycdq6TQn0l5ke5s2gBjbyVH3tu3k8npiudfxLeyWhgaKLG4MGCgdDnpiq9pqlydTa6VRPMysNo7Ag9qYF/VZtMjtkSOxzCy4tpecfz61j2H/IRtgf8AnpS22pTW9s9tG6tHIMEEA4+lXtKs723mjuxpEl2mMpkED65FTKUY/E7AVtZOdbvPZxj8hVzwuZhqknkwvM3kMCqDJxxzUN9p2qT3M95Lp8yBzvb5DhR0qhFPLbuXikMbYxkGiMozTs7gJJnzpMjB3tkenNNoySSSck80VQBRRRQBNZIsl/BG4yrOARXU3en2F74pbR/s4ghjPDKeTxXMad/yE7b/AK6CulvLqKy+IbT3BaOISfM2O2K87Fc3tPdevK2vXQd7JszdO8Pme6mW6jdIhEzxHB+bBxVzUPDFpa6IbiKRjeR8yJ6L/wDqxW2niHR7qS4hluDEsAMcDhfvKeT+tZ0nibTJtRvc2rqJoCglL5BOAPu1yKtipzvytW1sXaKYp8K6W00dsI5kd7bzvtDE7QdoOPTvUV/4StIFsmgkZxIwWf2zjBFW5vEtpLdi0acmzktthYLyrbQBRF4h06HWLeNpi9p5Sq7behUcGs1PGKz12v8A15+QnZ39P8jP0m0tIfElxpD2yzQ/Ph2PIwDiucu0WO8mRRhVcgCuk0maO58czTQEvE3mFWx1GDXO33/H/cf9dDXpUG/au/8AKvv1HO2tu5reErW3utQn+0wiVY4twUnHOagsobTWNV/0lltIt2NiclvYVc8GZ+33eBn/AEf+tZujwxPqaSTzi3WJ9xLL15qZN+0qu+yX5E/ZNGXw1HJ4pfSrV2EKAMWIyQMD/GpG0GzbVLe0WznjjkfaZSWIbnBrQm1Oxt/Est4l8Ggu4/L3KuChwBn9KqS30Vtpq6dHqRlnkm8xZ258oAnvn3rmVSvLl1ey7/N/I0ajf+uxRu7HTF1BLKKyuIWMwj8yQtgjODjNLrWn6Zp07W0dncI4IAmctt/wq7d38CaT9kmvluruSVWSYJjy8H1pZL+CDSbiG+vlv5Z9qxjZ9z3zzVxnUvF69t3rtr/w5GhVv9BsLbwymoQTtNP5hVm/h7dPzqfR/C1tc6RLeX0jJIyboEB5PuamQ2EfhSPTzqEbTJKZSu3gjjj9KlsPFGmzTzPdWbQ4h8tAJMg+wHas5VMQ6bULuzevW3Qenuv+t/8AIydD0/TdUkjtpLW4EjcNOu7ap9T2qdNE06DSWvJoJ7thL5Y8rPT14p+izxWcyXQ1BYLUtua3xlsemaLC7U3j3Mepra2hl3eQVzx9M1pUlU55crdtO/3f8NoLQg0LRtM1e/KSyvDGThIerfj3puleHlv7u8Llvs1oxBA6t1wP0rQ0270x/FEmrC4S2gX5Qmzk9Of0psF3aQrqOn/2hsF2/mRzIMY68H86U6ta8lFvZfLv87FJK2vcwtXtI7S4CRWkluCM4ck5/Ol0PTo9U1NbaaTYm0sffAzitHWLuzvDYae100iwjEtwRk84/PFGltpGl+ImzctNbhCI5dpGGwe35V0e1n7B6Pms+5Dtv6D77R9KtdNXUDBNEolKNA7EMwHcZ5oi0rRbvSTdRpJbO8nlxF2JDHr3qzrGoWlzpSWdzeLc3BmJWRFwEXjr+tVNS1HT/tun2UTF7CzxuYDG8881zwdaUVq73ffZfnfzKdlqWrnw1p6xXscaSxyWqZWZidsp46du9Q3nhuHTrIeZbTXNxs3MykgJ+A61qXeuWUcd67Xiz28i/wCjwhOVPHX9aifWLIX7ax/aDtGYcG1OeTxxj8KxhVxOl72+erstP60HZGTpOmaZqaPGbW4idY2bzzu2gj9KedI0210iG7mtri6eR3UmPdgAHGeKn0m6isWa4n1FDasGLW4Xk5OcU3SrsQyi4k1NY7QSM/2YrnjOcda2nOrzNpuy9fPTb/gE2Rn6Xb6ZeXHkvY3EhZ8BkLHYM96t2vhmKfxDPZmb/Q7dvnlz05xj60trPG+pTX1rfpZwvLuMRXkrnNXLnxTprXTW8dixgaQM0ivtLHPU8U6k6/M1Tvqvu+/r6CexSn8NxP4ofTrRiLWM5Z2P3VqLXrCz0HV4fsYM8O3fh+/OK1NT8U6ct9cpb2TSRT4DSCTaTzms7xXqOn6g1v8AYom3JGAW3Zxz0xRRliJTh7RPlt+m7K0u/T/Ib4rtraCWykt4RD50O9lBzzmsOEBp41PQsAa6HxhnGmZBH+jd/rXPwf8AHxF/viuvCtvDpvz/ADJludB4mihiv4NMtLRI96R4fPJJAqvceEtStonZjCzxruaNZAWA9cVd8Rg/8JfYnacYh5x7CtTUrm00jWLy8nui7ywrGIgORkEf1rhjXqQp01DVtX73ehVtdTmYPDd5cQeZFLAz7N/lCQbsdelSweEdSnt4Z90CLOMxh5ACeM4rpLPVdHtCssdxEkX2baQYgZN+0g/N1xXP69qyTWunLaXDboE5A42nFXDEYmpPlSsu7XqKysVbfw5eTyNG0sETq5QLJIFJP41ah8FavNGzgQrtOCGkANaej6jp62NpNLcxi5D7rlpo95PH8OelaV14k0t7lmS6O0j+7WdTFYpTcYR/BglFtdjlX8K6hHM6SPAiIMmQyAL+dWtL8IyTap9mvpYkTYWBWT73uPWtUa7YyWb2qTxiR8splj3L9CDVBdb8vxFbS31xFLEkTRhoowoXOOw+lP22LnGS2dn01+Q7R3MqTw/cfbza280EpJblZAQqj19KefC+oGeGOJoZhMSFdJAVyOozWjpdxY6Lq88jXUcyXYfa4TOzPTI/GrcGtfZbq3Sa9tjaoXOIYQuCe/FXPEYhO0NVbs9dwsjFuvCmpWsTOfKkKPsZY3DFTnHSq2o6HPpiE3E8HmKcNGsgLA/Sll1C4fVpzDdskc0xbcT75BrY1W8s7jSp/t80N1et/qXgiCtn1JHWtvaV4Sipa37LUVonK/411us+FXla3fTxEgaHcYzJ8zn2Fcltf/nm/X+6a7ebUtOXULTVRfEi2hx5WOS2elGLnUjKLp+fn6Cic7Z+Hbu8UbJYEkYkLG8gDH8KSDw9eSwPPI8UEaPs3SuFyc44zXU6bqukRPZ3KzxR7WLT+ZEGfO7Iweo4qjaagjTzeZfW7WMkxYxSxBjjJ6Z6Vh9axDctLW8mVaJneG9LE99MXjguRGj/ALppducA8j1qjaaTc6neTpbIqLGx3F2wqD61taI+lQa9cX0d0Le22uiIwyecjP0pllcWVumpaa94ALvDJOBx1zirdaopycV0XR6d/uFbp5mOYf7Kv4i5hugSOEcMOaveKrSCDU4EtohEJYgxXPGSay7mzSzuIo451uMsvKL71s+MRnU7QNlR5AyfTk1s3++g77p/1YOjMfUdOm0u6+zztGz4zmNtw/OmWLQpdo88xhRed4Tfg/TvUuqQ20F3stbtrqPb/rGBzn05qC1aJZwZrdrhcY8tTgk10RblSu+3p+DJ6nYanFY3Fzpk0moXCoxBGy2wjnIxnBwDVPxBb2ksc6xXLyMrKq/uMAE9t1Gs3F7Pd6XbxxiNQvmeURtC4IxmnX0CarYTSWs4CQffCnln7cfXvXk0k4ckm9Plpr6Gj6mppwdNJtbZ1dZYs7lQE9ah1tHn0Oa0iV3kZs/MMYAOao28NwJtMMUkrsvMwWQkjgdaq620ks9yttYX8TiVsyGZ2Uj6VEKV6yafW/4+oX0IdQ0Hy7OxmskeVpow8owTtzWrb+E9OM8bXMrpb+Rvds/xZxiprDxFp9lodlG0hafPlyrj7q4p+t69o0Vo9vAHvI5JOAG2FV+tXKripNU0nu9f6/AlWsmZdr4dtVbVftUUs32I/u0TOWGAe31rRj8G6bK5PmugeEtGhPKN2Bon8TWf2a8uLR/Knlh+VCM/NwME/hTbjXbF7ae7juCLmeHlMcKwGBipcsXLXVf0v+DqV7raG6RoNha2P2y6lkhuRIVD7cqq5xn0qKwmY2d7DpksTL9oXZLLGOct8x59a0m10XuhQpYPbiU4+0rOBhcdxnrWTDEn2GeCf5jeyZRofk8vaeuB0FJOc+Z1d7rT0fb/AIOwJWSKurCZPEcFxcWpCgKv7tPv7epArd1G4jhjmldpZY7pN0UQsQNoPqR0rC1N71by1gtGd44lAjmYlskjDHP9Kvpq15LrNraJIJYbeMrLJtyCcHrWlSDlGD00X4L5OwkyrZWMdlZ3WzJMunI7Z7EyAVfTS9NktoNMktp44/L817hckFs4zVWK5kvE1SXySsUNosSuPuthwetaypqHmo4li+yfZfu+YN3X0qKs5p3bs79/JDRlWV7Hc31jp8mnK9oSY4pGOCVzz+tQy2moS6FajTyyqksgO1yv8ZxVbw/dXEupWkDDMEE+8tj7vJ6nsKty2N9e6JbNZTKgWWXd+/EefnP51vOKp1EtFqt9vtCWqItMsNdXU7dpWkKBxuzKTxmmwPM19fRQ6dFclZ3JZ2xjk+1Sabo2sR6lA8lypRXBYfbAeM+magSwW5vrx2vWti9w4QI+CxB5zg1blFyd2notvXyYjcuvtR0a0VdKt2cSNmPePl4HPSuU1aR2utklols6DBVDnNX7q3vbgRw26XgniLLI+5lVkA4PpnrWfd2oX7NKkzTi4AOCcsD3B71eFhGD1ffv/mEncp1NaeV9rjM0piQHJcLux+Her2v2+n211CmnhlHlfvVZt2HzWfbNEtyhmhaaPPMatgt+Ndin7SnzJPX7ydmddqiWN1a6bNJqM4RlPzR22EfnuAcZqPxDFYFLgefI6xiIn9zjHy8Dd71BrE95Pb6TaxQiFXRj5JGMfNxmp7pF1S0mMMyAW6B5xkfMyjgY7jrXjwi4csm9Ne2mvoaFd7K2ubDTpo7aVd0yqN5JBGRnk/pW5cwi30x0k0pPJjmkwoOTjselZKahe3Om6WPk2M7M4AAChSDVm+vZGR7qFpJWUOqw7zllIxuxU1FUlJJ931fcFYpabJp0/h+8MVlIz7txUMTjkUml61ezWOqPIYC0MAZD5C8HcBUUF1dxeDbmPyhAFwocJtLjI796r6PFIukavKUYIbYAMRwfmHeul04tTcv5lbr1RN9i3oM9zd2+qXPmW6XBX78iKFHT14FLHJdaZpN9MLiGefzlAk4kAG3pWdo9xYR6bfwX8jIso+XapJJ49KsCS0k8P3pt4TBCLhQQW3E/L1qp07VJaaXXT0BPQux3K3b6XPeNCrS20ylygUZ3DGaSz0Nl0fUk+22h8yVCCJRgdaS2Gn6ppn2Cy2u9vC21pzs5PPGabZaDeRaLfQObUSStGVH2hecZzWLaimr8uq0f+K4ynqFvHaaXYWyPFcTpK7OISGJHGOlbWlTsl9Ht0kBXhYliuCDtPBGKzYNFu7HRpZNtut0ZFETrKpxzzz2rT0TWrmx1FrUzRz3BRjKxAKrgE4H+NFd81KSh71r9fn06AtzF1F3k0uM/2YYXfklU+4Pc4rMgubx3jghuZV3HaoEhArXub291Sze5triNVIzPCxC7fp6/hWTpcUkup2wijZ8Pk7RnArupaU5cyWl/61Je5ev7+ayik0yK4ldulw7MTk+g9qXwta295qzRXSb4xCzYz34qnrP/ACG73/roP5Cp/D88dvqTPJci3XymG8pu/DFKULYduO7Vw6mdKAJ5QOgdgPpmm0shzLIQcguTn15pK7FsSFFFFMB0TvHMjx/fU5X61f1W+1O+2tqCR5zwyphj9apW3/H1F/vVpXkjv4hVHcsok4UnjpWcoxck7am0IJxb9EZJQ45jbHupoKMBkowHuprc1Azi6Km6iaLeP3QBz0q3eKUiuWmZJINgCoo5U4o59DX6tq1fY5jYQM7Gx/unFAUkZCEj2XIrq3QgAuyNbiHmMDnJHWs6e5NjcwW1uiiJwCwx97dQp3dgnhuRXb0KWn6pfaYG+xqo3AgsYySPoarrFPdyuyIXcnLV0qROIYxA0ca+a+5SPvD0rIjmA8QE2+6KNnPyjilHl5m0tRSocqV3oytY6heaTctJbMEkI2tuGeKjnln1G53vGjSN2jXA/Knaj/yEZ/8AfNT6ISNViIODTUY/HbWxlyfvPZ362KUsDwNtkj2E9qZtxwVx7EYq0bjF80k4M2GOAxrVu4I7rW7ZGVVVo9xA6dqrmta5SpKV+V7GDsIH+rIB/wBmjyyoz5bD32mt2cC4DNDcq0cEgDRgHgA//Wpl99pmVpIZ0lt125VR0FLnKeHsm7mL5fGfKbHrtNJjIzgkeuK3bn7RPD/olxG8QjG6NRzUdvJFLoVwqQquwde5ORRz6B7Bc1rmMFBPC5PsM0uwtz5ZPuFzW/pFutosReLfLcdMj7q1W095lvDH56RRiT5kYfep82thKhom3uZOzd0Qt9FzSbMfLsP0xW9Gwja6jikS2lLjbuHbFQQNJb6si3caySsRtY9MUlK4OhbqZGMcYx7YpSpXgoR9RityG2hk1i6kk2hYgWGRxnmq2pI01sl2twJoiSOAeDQp7BKg0m77X/AywAOgFLsYfwMP+AmrFgFN9EHjLrnlfWtm+LpZTsWWUhspt/5Z/WnKVhU6PPFyvsc95ZHPlMPfaaNh+95bfXbWzHeXA0qWW5IfzflQH+dXSMRuRt8ryj+47g0nNouOHUtmcwEzyEJ9wuaNuT9zJ9hzXRGGK3SK0iuFhklBPQ5J9P1pNOtfsL5li8yaUsBxwBRzh9Wd0r+vkc9s3fwFvouaUKx6Ix+ik1voksduRZovmeeRLng4zUNy08GrfZ7RgvmAMwHQetClcToWV7mNsboI2+m00+CV7WdZY1XepyA65H5Vq3d5LJqpjgmSLYNpc9DVv7LDLeLNKFIjh3l8cOc9aTkrajWH5m1F7GRf6hfarNG13y6jagCbQBVeSGe2ZTIhQ9VzV/UleW2W7juRLGGxxkbTRqju+n2Rdix2nk/WlG0UlFWRLpLW72Vxl1r2oXnlmd4maIgowTDDHTmob37bdyG9ukyzAAv0yKqVravJJi0j8xthRcrnjoKFCMLcqsRGPNFtvYydq9cCjitttP09Z0tcSGV49wbdwDjNNs9LilASS3lYnI8wOABx6VXOi/q872MbAPUCjA9BWw1hYWtqktyXZi+3apx2psVhbNPJ5cUlxED8pVguB+NPnTE6EkZOAewoAA6AV0SaJZrK6Sl+WAXB6ZFM/se0d98KyMiqcpuGSR70vaIv6rUMAAdAvX0FG1R/CBW9FZWtte28jQvtk48suCVPvUElva32qtbwRPG25ixLDBx6U+cl0GlvqZHHSnwSm2mWaJU3KcjcuR+VbMukW7AFUeHD4IZwdw9sVHdWemRTT2yyOskf3XY8HnpS5k1YHh5rVkZ8Q35/5Z2f/fisxjucuQoJOTgVq3lhBBah4oJJcrnzVYYH4dayW+6aVOEI35VYzqQlDRjniZArOmN3QkdabtX0FdBKlnLBYRXIdnddq7TjbzUFvpcXnNHJBJKN+AysAAPxpqZq8O76P+rGMQp6gGlSIyMI403E9AK2I9KgWa4Rg0rRkbY1YA4P1qGxMUOqhTFLEei4YArTUr7EujJNcxSgllsLkSIiCRD0dcj8qlvb+71a5WS5ZXlxtG0YFWFsxdandGZyUhYlznk1TuJbcsrWkckWD1ZgTUpRclK2pMoON30GS28tuQJYyhPSmo7RuHRirKcgjqK0tYZnt7JmYsTF1P1NU7r7L+7+y7vu/PuPeqTutQqQUW7PsD3l1PLvkuZHdht3M3OPSrBtJrCESG68oyY2qh+9+IqlE22VW2B8fwkZBrdnfZpdtI9rbIdzfuynv2qWktEh04qSbZnuL/T2aWK6dSyhmZHweau2p1O7sxcNqsyqzFdpYnNO1GYFHkMEKr5SAHbyf/1UWVxBb2UUXnjy2c7SwP3u9Q4xerWpsqcFOz2Kk2imO3lnFwr+WMkbSM1mBSfuoT/ujNdHezwxpPayTBQflZghqtpikaZcGCZIyH4dh2q1J2uxSoxc+WJi7Gz/AKts/wC6c0bDnGxs+m3mt+xEzx3h+0RmXtLjgcVYAU30irsSZYDukI4J45oc7BHDXV7nMYYZGGGeoxjNS+fcrxvlGV245HHpXQSxoNjTKslxFGzbgOG7iq2n3LXqBp1VmSQbWx0yaL36CeH5XZvcy0uL0IkCyzqgOFXkAZ61Yt7O9E01vaz4+XMmG2hh/WtvEqFt5imdpGEZI4Udx+VUQxk1ORWt1iURABVxyOeeKlNO+hbw6ha7KE639haLC1wwt5Tjaj/KfwqZNP1NmRhcYZ1woMgzj0pt3Dby2Eb20uI42wIyOh9a0kX/AERLhjZtPG+1ZCh6Y/nTduxMaUXJ9vUxbRbn7SbSOV4jKdr4PB+tEcNzLFIokkEcGcAZxn2rVhgeGa2Eu0yfaFyR3p9n5otrdY7hIladt6sD8/zGhtbhGitmZEFrdyW32qF3yrY25waWGyeTzpbicwGIgksCTknrVq6kmkuZXim8nyZANicA89annEUgvPtEpRSkR3U7iVOP9fMi+1zFdn9vzYPGMNVKWxngvPLgbzGUbg68cU4W+m7h/ph6jsanv2SPVFAuHij8sDevcUlFR2RLimrv8GQjS7yWKW4ZDuB5yeWqu9vcW22R0KYPBz3rVSe3jsZFN/MRIeHyeKzbyRDtWO7ede+4niqTewThBK6GyX13NIJJLmV3C7QzNkgelQpI8W7Y7LuGGwcZpCrBQxUgHocUDhgcZ56etNRSVkjnNBLe4jsfNkvPKgx8oBzz6YFJ5V7CqXUVy28pjIbBC46VehYtokrva20QDDAZOGxT3nEltC/2eBFEZJbb04qNOx1+yjb5GU813Np433MrxA8xnOB71Pb22pzWEsaSSLAqbvL3cPz6VasUml0mRpJEVSBtQ9hV1fLjt03XTr5kQjC84Ug5pOy0SHCinq+xz0NhNJLJGVKNGu4/Lmp7fTbyeLZFIoWQ5MZYDJ9xWjp8l899dkyjYow0hPQ8VnWJD64G3B8t971q7tkezgrebI/7OuVuVt1dTIwJG1hxinjT5nlEMVyHmAJZc8KB70ml7Bqr7lyu2TIHfmrNmbZppjBbyRfupMlzkHih3FGEWV5bK9ht8mbdEzAEK+RnPFR29tOL14FkMUqhskH25qWxVv7Lk8tCzLIjYHfBzV2yurKfUpJPssqyMGLfMMdDSelxxpxk10uY0cUjwPMnCIPm5q1ZQahHKj2peIvxvRscU9Z4JLOW2s7WVTIBuLMDgZq5Y2s8nkxR3qlg2Rt449DTk9NRQpptdTOurC8jnlMilyDlnJ61HBb28qEy3SxEH7pQmti/tbiOa4jkvVVpG43cgDFc+42bhnOO/rRF3QqkFTlsaMOm20zEJqC8DJPlnAqgU/elEO/nAI71cvh9miit4uEdQzerGq9mdt5C3o4/nVImaV1GxG6NGxVxtYdQaSrWqNv1KZs5yaq0J3VyJx5ZNIfbnFzETwN1aOqK9vqv2wbWTdlcd6zI08yVUzjccZq3d2CW1wLdLjzZScFc9KT3RpBvkenYWe/tppTMtmElJzupf7Uczyy+WNsq7WX8MZplxpstqjNJLFleqgnNNbT7hLRbplAjY4FL3Sm6t395N/az/a1nEYACbCvqMYpx1ZH2tJaK8iZ2N6en5U1dHuGt/PEsPl/3smoYtOuJ4ZJYwCkfU0e6O9b7ySTVJZEiBUBo3L7vXNTWrNf6sLpUWMA5eqH2aT7N9ox+7zjPvUllbR3c3lPP5TH7vPWnZdCVObav5BfkNfzkHIL8GptGYLqcZZgo9TVSeIwTvCTkocZqSytTeXSwB9m7+L0oSXKK8vbXtrckmjFpesbiISKSSF9ann1hZZ4547URyR8A+o9Kqy2q/aRBbSGds449aLmxntJ1gkX526AUrJ2uPmnG/LsTSamjIyRWwiEjZkx/FSf2hHHC0VtbCEPjefUUyXT5YQoZ49zEDYDyM0s+mzW65eSLPHygnNHujvV3HR6hFBGRbWoikYYL0+DU4ILNrcWQIcfMfWo5NMmij3vJEvGdpJzTF065Nm13sxEO5ofKCdVPREtvrN5bzK4mcovRCeMU1L+EyGWe286XOd5qOzsLi+ZlgXO0ZJNOg0+W4yEkjDZxtY8k0/duJOq0uwv22GWZpbq1EzseD6VIuqKbwXM1uJCuNg/u4qOLTLiXzMlY/LOGL01NPnluvs8W2RvVelHuher23LDauv2tp0tgokBEi/3qhuL8SxxwxQiKFG3bB3NRGzn+1G2C5kB5AoubVrYgNIjH/ZPSklHQJTqtO5O+pD7ZHcwW6QmMY2qODT5dVVopUgthF5x/eH1qjHG0sixoMs3QVbl0m4iQuWjZQcMVJ+X602o9QjOq03Ejur5rgQqqCNIRhVFWm1oFjL9mX7QV2+ZUX9kXBieRJInCDLbSaT+yLkxlspkDds/ixS90pe2Tuh41cHY8tsrzR52yelNh1m+im8w3DsMk7c8VFHp80kJmLJGvbf3+lPg0yWcDZNDljgKSc07RJvVdhV1FDI000HmysSQx7U2HUXiuJLhkDSOMA/3acukXRZ1OxNh25boT6U1dNmMjxu8cbKcEOetL3R/vk7kMEsKMxuIPPz61bGrusq7YlEKrt8rtimto92s3lkL93cW7AU3+yrr7QsPy5YZDdiKPdYJVo7ISe7+1RJa28IhjJztHc1Y1VfLs7SJmBdVOQO3NVJ7M27qJJoypPJQ9Kfe2K2scUiTeakoyDmjTQLztK66FOtjVImkjtZ0ZSiqoPt0rHq9dafHawI7XOZHAITNN9Cad+WSsXb/UYYJ1MMKtL5QHmenFQx63tWIvbB5IhhWNZe1sZwcUAMRkAketJRVhuvNu60LV1ftdQrGUC7W3ZqS11IQWn2aSASIG3D61RAJ6AmgKxOACaqytYj2k+bmvqara/I0m/wAhR8wOPpUa6yw4aEMhBDL65rOwfQ0YOcYOaXLEp16j6ll7tBcRzW8PlFDnHrUzamguRcw2wil53H+9nrVOGCSeYRIp3HtSSxPDIyOpBU4NFkLnmlctyahC0qyx2uxw27NV7mf7TdPOy43tkrURBHUEUYOM4OKaSRMpykrM0ItRRInhtbYRtKNpJqP+x7sjGF596p7WxnacetITgZ5/Oi3YfPdWkajamsQijktFaW3GFf0pI9ZIiVJoBKUfcp985qrc2T28cUmdwlXPHaq4DHoCaSSZcqlSLsXm1GGS5a4mtAzkgjHbFKNUVr03U1sJGxhR6CqABJwATUttb/aLhYmcRg9WboKLJE+0m2Wv7UC3jzx24VZP9YnZqrytFcyIltbiEk9PWo54xFO8auHCnAYd6RUHmKJCY1J5b0oSW6CU5PSRo6yNkVpGWBZI8NjtzVO6uUuPL2QLFsXB2/xe9PvrEWflMs3mrKu4HNVaIpWHVlLmd1bYdG7Ryq6PsYHhvStC7aGWO1ia8WUruZ5BnjPOPrWfGjSSqiqWJPQdTWvNpbR2kZg0+RmlPzFxymPTFDtcKak4uyGRX9rPuiuBhEQiMnoTjqaZFJbPDBaNcBBC3meY3Qk9R+lOv9JeJSyW8iFY1PTg+tT6XaWsulpM0CSSGRgSfSp0tc2Sm5crEvpBdzS41mPyXOQhz0/KqMF7FbQS2skCzxs2c1qXdlaLp9xJ9mSNkUFSM9c1j2thNdxtIjIqJ1ZqI2sKpzqatu/66i/bUSGeGGARpN29Kl/tZzHtaIFvLMZb1BqFLCaS7W2jZHduhXpSpp073TWxZEkXjDd6domalVW3oSw6vJFFGhjDlMjJ7g9RSjVVjKiC2WNAdxX1NRXOmz2rqjshcnG1etNuNPuLWaOGVQGkxtx70e6xuVaK16E0GooRNFcITDKxb5eqn2qSC7t4SZYG8qVvkUnsPU/WqkVjNJfC1x84PI+lX/7NgF66XEUkSeWGRVHJofKVH2jIbqS3vIdqTLEIjkK38fuKicwS+VZpIscSfekbox9aS9hto4IJLfeDJ1R+oHrWjHosDNCvkXLiQcyKBtFF0kJRnOTSRFDdQzaqJnuRFDEwIVv4sDtSRXFg0Vt58jho5S3y9huzzUNtYZvow67oGlCc96ktdLEsMsrNGC7FIlY89cZpOxUXN9O/6FV/LuNSZvOVIy24M3SrjXdnMLoTO4Vgirt6nB61H9gghh+z3koguS3B9qctvBYR3TSxJcmMIVLZxgn2p6EpSW9iDGl5H7y46juKlubu0+2mVVMyCMKgP171F/aNrkD+zbfkgdW/xp95b2hvSDItrGYwwA6ZzR6ivp7tiZhbTowS9hgil5aNgciqVw9usTwp85R/kkHdcf41cisdOaxmk+2Bip4f0qjPDaxoDBd+c2eRQrBPmteyJrq8DafDZKwcR87h/KqWSCCOo5FFGCSAOp4FUlYxlJyd2aM8qyaWI5bxZpZHXPXKjNPhvbVXW1ly1uo5f1P+FSppjJp7Tpp8sk2MbZBxz3GKbNo7i2iP2aRHK5JA7471F0dPLUWtvzIElgaC5iMgQO+V+masHUoCFUtx0X/Y9zVZbBn08uBH5icnGc49DVm20q1+zyma4HmGEOB/c5odgj7ToRWvkwPcySX0bkptAGfnNQ6T5Md15806RBDwGzlvpVm00mN7mePz4pFjXgk9/Wo7W2sJblbWTzTJnBZANv4U7rUSjK8XZFS1ujaXjXCqH+8AD0OTVq31FnmkNw4VDG4VR0BI7UyKCzub8QxiURqrFsgZOPSpIYrW6nMPkNFHErNvA+ZsfpQ7ExU1sxlnqjQhIpEUQgENs6mpbe40y3uWmDXDEg8ZHeo/s1nPa+dbiVSJFUhgO5xSwWKDVZbd0LRoGxn2Bo0GufTqPtJNNt/NKSTbmTA3kYNV47iC3eNLYMq5zI7dT7VHDa77Ged9waIAj35qe2sLV/JeW62hz93t9KNBJydkkhJrqCe5mS4y8JbKOvVeO1UwiySbN4RScbm7VoXen2iS3BjuuI/4R24qtbXUMEZWSzimOfvOTn9Ka20JmnzWkSarJE9xGIZVkVEALL06VUicRyo5UMFOdp71qRXFp5Jnn06BY+ijJyx/Os1EFxdBFAQSNgD0yaF2FNa819wuZhPcPKsYjDfwjoKjqW6tza3LwFtxTvUVNWtoRK/M77klt/x9Rf71Xr7/AJGD/gdZ8TiOZHPRTmreo3NtcXH2i3LiRjkgjGKT+JM0g17NrzRY1H7Ncai9ukDCZmA3ZPpWjJCszzWgniYCL5Iw3Ocelc35snmeZuO/ruoWWRZPMVyH/vd6nk0saRxCUm7bv8DSRWXw3MpzkTAfqav28SW0NrAbiNA4JdGbBO7pXPebJsKbztJyR70NI7sGZiWHQ+lNxuEa6jZpbK343Ni6s5Y9MlhSJm2zHAUds1n6ejJqcKupUgng/SmLe3SZ2zNz1qSyuYUu/tF2zsy8javU0JNEynCUk1pb/MZqP/IRn/36n0T/AJCkdVbqUT3UkqjAdsgVJp1ylpepNICVXqBQl7thcy9tzdL/AKjcyi8k8gMWLEfKOa3J42XW7V5Y22+X1YcZ4rEnmiS5Mtm7jPJLLimyXlzLjzJmbHI9qLN2KjUjC6eupsSfvY55bi08p4pR5bZPz89KhlhivIZLlreS2kTBy2cMfSsx7q4kxvlLbelEl1PKAJJSQOg6UuVlOvF7o1BFFqMbPLbSW7pGMSHODS2aXU2i3W9JGyPl47ZFZT3dxImxpSV9OlOW+ukTYsxCgYxim4uwlWimm/M3NNWJPs8EFzECeZRu+Yn0qjaxCLUSTbtcYk+V0yQKy1kdX3q2G9RUkd3cRLtSUqD7Ucutxe2TSTWxqvJtuLi3e3e5R2BLLnjj2pqWz2urxQ2pdo2KswA+77GsyO6uIs+XKRu5PehLqeNy6SkMepoUWhutF6vubsCNFqt6WhJcodinvwao30ayafDM9v5FwzldmTzVBry5eQSNMSw6GmyTyzMGkcsR09qSg9Bzrxkmrd/xLlpZ3VtqkEcimFzyN3pWleR7rK88uNoCD85bo/TpWC880jh3kZmXoc9KdLd3Ey7ZJSw9Kbi2TCtGCaS/qxfZGsNMSPJWa5OTk9FrTdD5jqUbzvJ/1/8ADXNSSSSkF3LEcDNSG8uTH5ZmbbjGKTi2VCuo9NDflO+e2hFoJYGUhpMnA9TWfaW8cE9zdknyYSQhz1Pas9bq4SPy1lYL6UzzJPL8vedmc4o5WgdeLabX9WN6ErcaVFO0bzuJiSi+pPeo7uEX2spxtEcYaXB4GKx4riaAERSFQeopFmlBYhzl/vHPWjl1ug+sJxUWu1/kb1pNHfrfE7mUD5UXqRnpTprvybe1H2QlgMeUM5C1z0UskL7o3Kn2p/2q483zfNO/1o5BrFWW2v8AwblvUrSGK1iuI0aJpOsbU7Uf+QdZf7p/nVFpWnkBuHZh3PtVnULu3nhghtw22IYywxmnZ6Ec8WpNaaFGtTV/v2f+6v8AIVl1o3l5aXUMJG8TRADG3g4pvdEU2uWSuazNP9sSIQgW3k5Y7eOnrRY2zRmJRI5jkBKqqAqRjuax77U5LplEbssYQKV6dKrpeXKIEWZgo6CoUHY6XiIKXf8ApGxd3JsLCPyY1B83G4jtii133CvepuhV3xtiQMc496w3lkkXa7kgHODTormeFSschUHtTUNDN4i8vI60IILhlWMfO65yPaoBtl3SONsgRtpRQT+Armjd3BOTM2c5zmkFzOrBhKwI6UvZs1eLjtY2/tgS9tdhkWXOGeRAu6mr58+t+XeBvKBYplQB7VjSXE0zBpHyR0PSle6uJNu+Unb09qfIZPEX3/r1N6WSIyLFKszv5nyl4woH5VW1DUyl/c27QIYidoQDoc9ay3vLmQAPKTjpxUTOzOXZssTnJoUO4SxLa903Z1e8smMJkgEceWjdAFP0PWsBvumrBu5pAEllbyz94Adqm26R3kn/AO+P/r00rGc5KpaxrCW6WPT0iizGw+c7cjGaW3t/Lk8yJ3WOSXAWNA2eec56VhteTLmOKZvKHCgjnFMju7iJdscrKOuKXIzb6xHqjcysN7cwLHIhcriSNA2D+NVoYru31rywTJu+8QoPHvWat5coSVlIJ6nrSJd3Ebs6SkM3U0KLRMq8X06mtb2+3VbwtEfMXJiUjqay7uW7lIN2GB7blAprXU7yCRpSXHQ0NO08i/aZCyA8kDmmk0ZzqRkrLTX+rl3V/wDj1sv+uX9TUGoNdMYftUQjwnycYyKdqV3BcrAkAbZEu3LDGaqSSyS48xy20YGe1EUOrNNuz6IIlLSqocIT/ETgCta8lih0y2QSNK+5sSZ6c81jjGQSMj0q5Lfo4gVbZUSHOF3ZyT3ptEQkkmX70O8PmJukeSNcDPTb1NMivXjs7aUQx7ZJPLxuPbHNU4NUngeRiA4kBBU9h7UR6jt2q8CvEmNsecYI75qeVmvtY3unY1NSufs8kyr9mZVOBH5h3flVWxkiGlXck0W5C33QenSoJtRtp5nlk09C7nJPmHrVIythlUlUY/dzTUdLBKqufmWu5raekRhurmErbjbsQucAGn3sGbyxuUcOHYBmQ8E5rF8x/L8vcdvXFKJpQqqHO1TkD0o5dbiVZcvK1/w9zb8gS+I5Gc4WNNxLHgYFPlhNxbxzCZJnjn5KHOAW4rC8+XLN5hywwT60iSyRAhHKg8kCkovTyK9vHXTe5pzx+TrLzXMcqwgn5lHftU1ufM1OSTzXIaMHdMMAVmpqV2rAmTfjswBp39oyFCrqG3H5j0yOwo5XawvawvfzuWr6bdYqbqFFmLfKVPUVN9rtI9KTdA4V5MqNx5GOtZ8l/wCehE8Ic5+Q5xtpjXfmTq8sQeNBhY84AFPlF7VXbTNhRBBeW1tE3ImVtp6gVHFLbRxWYmjLsZ22nJ4+aqEOpeXem7kgWSTOVy2NtOg1maCNESJCEctyM980uVlqrD+vkLcyQm6mSUEv5gKN+NXJp/s6XkhjV/ki4Y8Vk/aFa8NxJEHyc7c45qwmrTRmZgiEy4HzDOAOlNoiNRa6/wBaiDVhkf6JB1H8RqxetI+rK8UCyMYwdnaoP7XuM/6uL/vgf4UyfUppp3mACM6hTj65osLnVrN/gXTeyxWcubWFCp+eMms+6le4jSU26Rp0BTvU39oxOweazWSTu28jP4VXmunlEiKoSORt20c4OMcUJCnNNbjpLGWKxjvCymOQ4AB5H1quPvAZxz19KlmuWlRIwNsadFBqGqRlK19DZ3RW+hy75jOxYcq3CntzUgYyWMUuWk2rtC56nGKzWvENmtstuFXcGY7vvYNOi1OeK6EygYAwE7YqeVnR7WOnoXLM20GlziRXaQHDk9jnpWgbjy7eILDG25drkn+D/wDXWCl8VWVWiDCVtxBNO/tSbOdo5Pzf7Q9Pak4tlRrRirFzTvsn227k3McL8qDoR9aq6a4k1dHChQT0HamxX8UHnGO0VTIMA7z8oplldrZyGTyBI/8ACS2NtOz1M+dXjrsTaTvOrt5f39r7frmrkJufOlFzOjsIpPkGMrxWKsjrIXRirEnke9S21y1vI7gbi6FTk+tNoUKiSSNCys5G0xlZvL3kOh78c0um6ldPfsj3G4BW/hHoazILiW2lWSNzlegJyPyq2ut3aMWVYgx7hB/hSaZUKkVbVqwlvcXGoo8MtzlFXcQFAzVvTnsZdhe3KQhvvep9qrJrM6q6mKPDjHCgVWe8lkljdsfu+igYFFmxKpGNne5rak1hHJMyQGSIuN59DjvWDIQQxUYHarIvpVupLhQAZDkqeRUIZfN3ugcE5K5xmnFWIqTU3dFvVeJIAOnljj8BVe0z9ri2gk7xgDvzT727+2TK4jEYVcBQc1XVirBlOCOQaa2FNpzuizqW7+0Jd6lWzyG6iq1K7tI5d2LMepNJQlZWJnLmk2FFFFMkKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAI5SQowe9NnJEYwcUUUAPj5jWn0UUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAf/2Q==