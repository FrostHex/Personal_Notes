# ZBrush
--------------------------------------------------

# 1. 基础知识

## 1.1 不同视角观察模型
- 平移: 按住Alt + 左键右键拖拽空白处
- 缩放: 按住Ctrl+右键拖拽空白处 *(或者: 按住Alt, 左键右键拖空白处, 松开Alt继续拖)*
- 旋转: 左键右键拖拽空白处 (按住Shift, 旋转至标准的视角)
- 二维视角旋转: 按住shift + 右键拖拽, 松开shift + 右键继续拖拽
- 二维视角旋转90°: 按住shift + 右键拖拽一段距离

## 1.2 窗口透明度
顶栏右上角, 界面透明滑块。可把图片放ZBrush窗口下层, 直接对照

## 1.3 格式
- .ztl (zbrush tool) 载入工具格式; 右上角工具栏 "载入工具"、"另存为"; 小, 仅模型工具
- .zpr (zbrush project) 项目文件格式; 顶栏, 文件栏, "打开"、"另存为"; 大, 模型工具+历史记录
- .obj 可与其他软件互通; 右上角工具栏 "导入"、"导出"

## 1.4 开始建模
添加模型后, 点亮上栏左边的绘制(Edit)按钮, Ctrl+N 清除其他模型 \
生成多边形网格物体(PolyMesh3D)后按一下X可启用关于YZ平面的对称编辑


--------------------------------------------------
--------------------------------------------------
# 2. 笔刷
- 相反绘制: 按住Alt

## 2.1 笔刷图鉴
- MaskPen: 遮罩
  - 黑色部分将不受影响
  - 绘制: 按住 Ctrl, 左键绘制
  - 反选遮罩区域: 按住 Ctrl 左键点空白
  - 清除遮罩区域: 按住 Ctrl 左键拖空白 (无遮罩时为Dynamesh重新布线)
- Smooth: 按住Shift
- Standard: 半椭圆形突起
- Clay: 平坦地突起
- ClayBuildUp: 边界锐利地突起
- Move: 拖拽拉伸模型
- Move Topological: 拖拽拉伸模型, 笔触周围未连接的几何体不受影响
- TrimDynamic: 削平突起的表面
- DamStandard: 刻沟槽
- Chisel: 拖线绘制凸起
- inch: 收缩出锐利的边界
- CurveTube: 从模型上拉扯出一根管
  - 制作尖牙: 上方笔触栏, 曲线修改器, 点亮"大小", 调至 ![CurveTube制作尖牙]
- CurveTriFill: 画出形状任意的平板物体
- ZModeler: 打开多边形线框, 对小格进行编辑; 对小格的点、线、面(可编辑多边形组)右键可更改功能
- IMM Primitives: 为某一模型添加新的基本模型
- ClipCurve: 按住Ctrl+Shift绘制, 切割模型边角


--------------------------------------------------
--------------------------------------------------
# 3. 上栏
- Mrgb: 同时绘制材质和颜色
- Rgb: 绘制颜色
- M: 绘制材质
- Zadd: 笔刷加法模式
- Zsub: 笔刷减法模式


--------------------------------------------------
--------------------------------------------------
# 4. 左栏
- Brush 笔刷
- Stroke 笔触
- Alpha 绘制方式(如画点或画方)
- Texture 贴图
- Material 材质球


--------------------------------------------------
--------------------------------------------------
# 5. 右栏的左侧栏
- BRP渲染
- 调整工作区大小
- 透视
- 地网格
- 中心点(快速找到物体)
- 快捷移动缩放旋转物体
- 透明(此物体以外透明)
- 孤立(只显示此物体)
- 绘制多边形线框(显示模型格线), 快捷键 Shift + F


--------------------------------------------------
--------------------------------------------------
# 6. 右栏 (工具栏)

## 6.1 子工具
- 子工具包含所有的模型(导入的+创建的)
- 追加: 将新模型添加到当前子工具末端
- 插入: 将新模型添加到当前子工具后面

## 6.2 几何体编辑
- 细分网格(让模型变精细): 右侧几何体编辑栏, 快捷键 Ctrl + D
    ### 6.2.1 Dynamesh
    · 动态网格 (按照模型重新拟合网格), 按住Ctrl 左键拖空白更新网格
    ### 6.2.2 ZRemesher
    · ZRemesher 重新绘制网格, 更高效的布线方式
    ### 6.2.3 修改拓扑
    · 镜像并焊接 \
    · 删除隐藏 (删除模型的隐藏部分) \
    · 封闭孔洞

## 6.3 图层
- 点加号新建图层
- 显示REC表示正在记录
- 点REC结束记录
- 点全部烘焙, 图层合并至本体

## 6.4 表面
- 编辑噪波 (左上灯箱给物体添加噪波)

## 6.5 变形
- 膨胀: 可搭配遮罩使用, 使某些部分膨胀

## 6.6 遮罩
- 模糊遮罩的边界

## 6.7 显示属性
- 双面显示: 可用于单面模型, 让模型转到背面也能看得见


--------------------------------------------------
--------------------------------------------------
# 7. 快捷键
- 绘制: Q
- 移动: W
- 缩放: E
- 旋转: R
- 透明(幽灵化): F
- 细分(增加模型面数): Ctrl + D
- 设置笔刷面板: 点右键 or 按住空格
- 调笔刷大小: 按住 S
- 调笔刷强度: 按住 U
- 吸取颜色: 按住 C
- 自定义按钮快捷键: 按住 Ctrl + Alt + 左键点想设置快捷键的按钮


--------------------------------------------------
--------------------------------------------------
# 8. 布尔运算
相减: 两个子工具, 被减者调至![布尔运算两个白球], 另一个一个调至 ![布尔运算一白球一黑球],可预览布尔渲染

## 8.1 法一: 
事先给两物体Dynamesh,向下合开后再Dynomesh(边缘锯齿)

## 8.2 法二: 
子工具, 布尔运算,生成布尔网格,在子工具上方找到布尔后的物体(接缝处有三角面不易Smooth),可几何体编辑,ZRemesher, 点亮保持参形组重新布线,再用ZModeler笔刷右键倒角, 左键拉接缝处


--------------------------------------------------
--------------------------------------------------
# 9. 多边形组
MaskPen遮罩后Ctrl+W可更改群组。按住Ctrl+Shift左健点可对群组
孤立选择。右侧工具栏多边形组自动分组可让分隔开的物体分出不同组


--------------------------------------------------
--------------------------------------------------
# 10. 模型操作

## 10.1 隐藏部分模型
- 隐藏区域外的部分: 按住 Shift + Ctrl 左键拖
- 显示全部: 按住 Shift + Ctrl 左键点空白

## 10.2 移动、缩放
- 点亮上栏左上的 ![移动的球状按钮] (3D通用变形操作器), 以及点亮移动轴或缩放轴
- 按住Alt移动轴可只移轴不移物体, 按任Alt点 ![移动的移至中心标志] 可将轴移至中心、点 ![移动的摆正标志] 摆正方向、点 ![移动的移至原始位置标志] 移至原始位置。点亮 ![移动的粘性模式] 移动物体时轴将不移动
- 同时移动多个物体: 点亮 ![移动的球状按钮] 后, 将按钮改成 ![同时移动多个物体] , 配合模型隐藏操作 (隐藏的模型此时显示为虚化), 可同时对所有 "实部" 进行移动等操作

## 10.3 弯曲模型 
按W, 齿轮图标, FFD柔性变形器, 按住Ctrl框选中心, 拖动箭头

## 10.4 给单面模型增加厚度
右栏变换目标, 储存变换目标 (记录所有的顶点位置) , 右栏变形, 拖一下膨胀滑块, 右栏变换目标, 创建差异网格 (创建一个有厚度的新的子工具) 


--------------------------------------------------
--------------------------------------------------
# 11. 材质
在同一模型不同子工具添加不同材质球: 开A Mrgb, 关Zadd,选子中工具, 上方色彩栏填充对象


--------------------------------------------------
--------------------------------------------------
# 12. 上色
开始上色: 上栏点亮Rgb, 关Zadd Zsub, 右侧子工具栏点亮画笔图标


--------------------------------------------------
--------------------------------------------------
# 13. 自定义UI
启用自定义: 顶栏, 首选项, 配置, 启用自定义
摆功能块: 按住 `Ctrl + Alt` 左键拖


--------------------------------------------------
--------------------------------------------------
# 14. 案例
THE KEY IS TO START LOW (从低模开始)

## 14.1 翼膜
- 新建一个平面, 细分两次
- 按Ctrl用马克笔画出形状
- Ctrl + W 分成两个多边形组
- (若需要挖洞则此时重复以上两步, 马克笔绘制洞) 
- 右栏, 几何体编辑栏, ZRemesher栏, 点亮保持多边形组, 平滑略大于0.5, ZRemesher
- 按住Ctrl + Shift 左键点翼膜的多边形组
- 右栏, 几何体编辑栏, 修改拓扑栏, 删除隐藏
- Move笔刷微调
- 右栏, 几何体编辑栏, ZRemesher栏, 点亮侦测边缘 (让边缘保持锐利) , ZRemesher
- 右栏, 几何体编辑栏, 动态细分, 修改厚度 (优点是无论操作如何, 翼膜厚度保持恒定)  (此时ZBrush显示双面但导入Unity仍是单面) 
- 子工具插入ZSphere, 搭好大概框架, 保证Z球中央与翼膜中央对齐, 之后添加中间的 (用于创造骨架弧度) 的Z球
- 右栏, 自适应蒙皮栏, DynaMesh分辨率调至0, 创建自适应蒙皮














--------------------------------------------------
--------------------------------------------------
[布尔运算两个白球]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAaABgDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD1HVvEmm6MIhczF5Z22wwQqXkkPso5rMbxvoDuhuL02MlvJmSG6QxOAVbBweo+lJpNvHdePddu5UVms44LaDI+4pXe2PqSPyrYu9OsZtTsrqWzhkuIiyxytGCyAqc4NACaZ4h0jWELafqEE+Oqq/zD6jrRWR4utILSbS9WtoY49Qjv4YUdVAMiO21kJ7jBJ+oooAnvrPVNK1q41fSbVb9L1EW5tTII2DICFdWPHTgg+grKSPxFpuur4g1BHuFu8xS6bbNv+zRqMqy9Nzdd2OueOlbCXE5nIM0mNv8AeNVbq4m/tO3HnSY+b+I/3aAGPLN4p8R2HlWtxDpmmP8AaZJJ4mj82bBCKAwBOMkk/SirSXE/mAedJ1/vGinYdj//2Q==

[布尔运算一白球一黑球]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAbAB4DASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD1zUNRtNKs3vL2dYYY+rMfyA9TWRdeIrZ7iyie1vYFluFxLNbsidzyT0/GodXtIdQ8YaNpzxK0NtHLfOp6My4RPyLk/hWzf28BSPfCrqHyVPQ4BNAGdqvjjw7o1wbe71FPPUAmOIGRhnpkLmtLTtWsNVhMtlcpKF4YA4ZD6EdQfrXmPhfR7SPTIdYltI/3mboxkcuxY7F/Fv8Ax1feqnikzeHYBq1s4i1K7lH2mfbwysCwXHr8ufYEUwPRvEAfT9X03XRE8kFsJILry1LMsb4IbA5IDKM+xJqLUvF3h0wxL/aMNzvk2+TAd7vlSNu0c81eur24jI2yY4HYVDMQtxbyqkYkMnLhBk/Ke+KAsc9oWga1YQpDNp0NxZKS1rG8+14V/hVxjkhfl496tf8ACGXOuziXxGYlhQMyWsDFsyMRl2YgdAAAAOBmt03twJHAk4B44FN+23PmEeacc9h60DaP/9k=


[移动的球状按钮]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAdABwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDoWZUUsxAUDJJ6CsW48X6PBKiCSWYSNtV4YWZWOcYBHX8KdrRW5vbewmk22vlvc3Kj/loiYAU+2WyfXGKlsdPS5iF3dxDzZV/dp2gTsq+h6ZI718zGMEuaZ4ijFK8i7aXtrfxGW1mWVQcNg8qfQjqD7GnyW0EzbpYY3bGMsoNYFyRp+qw3OMXImS3nYDHnxvwjH1IIxn2PtXR1E48tmiZK2qMDxVY3s1sl5p5JmiVo5IwMl42xuA9xgH8KtW+sLLAGSSzYAdftG3H1BGRWrVabTLC4lEs1nBI4OQzRgmqU04qMlsNSTVmYIjl8Qa9bTrKjWVnlpDEDsdwQVUMfvYPPHFdPSKiooVFCqOgAwBS1M581l0QpSuf/2Q==

[移动的移至中心标志]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAfABIDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD0vVfFFppqQosNxcXNy22CBIXBc9+SOAO5rLh8W3dhe41rSja208oRbiF2kVHIGFYFQRnoD61q6oMeIdJfgkLOFB9do/wNcQY1GieIC2o3N032R5bpZpSwjm6rgfwkEdB6CmB6L/adsf8Ant/34f8AwopmnSzyaZavLjzGhQt9dozRRYCj4oY2kVlqo+5YXKvKfSNgVY/huz+FZXiMLql7D4ft1BGoXCzXTIMfuEAJJPuQB+ddFNZXtzC8E91byRSKVdTbn5geCPvVk6J4Zl0rUL66jvxNLIUjVpotxjjVRhBz0pAdGsaogUAAKMCiqvlaj/z+Qf8AgOf/AIqigD//2Q==

[移动的摆正标志]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAXABMDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDstbuLnQNC1TU7V7+6uI52WONCCMkAbiAvQdT9KwdBHiTSPDbarHqltr1kxae7+yTN55zyxDNxkf3cDpXQ29/e33xEl0q3n8qxsIDcXKhQTK7nCqSegAGeK3riz03TNJ1B0t4baF45JJyiBQ3y8scdTigRW022g1bTbfULTVtRaC5jEkZMwBwRn0orn/AutXGn+CdJtZNE1ScpbgiSKFSrKSSuCWHYiigZTGqReHfE+o+Iot99aamVjmjX5ZIWToRuwCuDyM5o1XX38bwjS4El0/SGYG8uJCDJMg58tFUnGe5PaiigR1EfivRbeJIImdI41CqojOAAOBRRRSuM/9k=


[移动的移至原始位置标志]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAiAB0DASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD2asPxTr2l6TpssF9drDJcwusaYLE/KcnABwB69KxvGfiY+E7CXybu9vb/AMhpUh2ptRRxvcheFz+Z4pLHw61l4dutZvNQuLnVLyz8y4ncKcfLnYoK/KvPQUAdFJ4g0m2jsTLfxBb4hLZwdyyHjgEcdxWpXnvjPwra6bpb+IbK6lt7mxZZxF8vlTNuXAKgYBJx8wH1zWzYa9a3CvHfavc6ZeRYE1rdNCrIT3BK4ZT2IoAT4ixifwo9nj/j9ube3PHUNKuRWl4ldbLwhqbRjAgspCo9MKcVT8QG11uxigjubu1khuEuI5RYyPhkORkFeRmszVZ9efRLq2mkstQt5IikhktJ7d2U8HoGFAjDn1jVdQ8Ba7Bq9wtxLa/ZGWQRhD+8EbkEDjgmvRbzSdO1Eo97Y29yyjCmWJXI+mRXnt/pertZ6jZDTAE1K8tn3RM7rDFHsBByoJ4Tt616ANXtDnAuOP8Ap1l/+JoAv1R1vjR7n/c/rRRQMv0g70UUAf/Z

[移动的粘性模式]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAAaABQDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD1O0k1FbGAJaWxAjUf8fBHb/crBtvGmryvcl/DMjwW1y9vLNbXAl2svcrt3Y6dAataxrsumaNp1lp4RtU1FRFaLIflU7eXb2Uc478CszW9Mbw34LttItbqQzahfRQ3NznDytI/7xs9iefwoEdFYazc6raLd2FvazwOSA32hhyOCCCmQRRWja2kFjax21tEscUahVVRgAUUDOU8XfZR4AijuxH+9WKJJH6xk4yynsQMkY9Kq6d4QvNSs7W7n1e+iRLuO7gtJ281UVfug7uQSPfvWDqEaXGn6WkyLKolUgOMgH15rVllkExxIw59aBHoMkjq2FiZxjqMUVwKzSjOJX/76NFAz//Z

[同时移动多个物体]:data:image/jpeg;base64,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

[CurveTube制作尖牙]:data:image/jpeg;base64,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