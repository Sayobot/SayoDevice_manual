
# 屏幕设置

> ## 修改屏幕图片

1.点击**资源管理**选项卡，点击左上角的添加“+”按钮。
<br/>
![](/img_screen/main.jpg) 
<br/>
2...1. 在弹出页面点击左上角打开一个图像；
<br/>
2...2. 在工具条右侧修改输出分辨率；**（O3C，屏幕分辨率最大为160x80，超出会导致显示不正常）**
<br/>
2...3. 调整缩放图片，直接输入分辨率或点击 “+” “-” ；拖动框选需要的部分；
<br/>
2...4. 点击“√”确认。
<br/>
![](/img_screen/1.jpg)
![](/img_screen/2.jpg)
<br/>
3.点击**提交更改**。等待键盘下载完成（屏幕显示进度条）
<br/>
![](/img_screen/3.jpg) 
<br/>
4.点击**屏幕**选项卡；左上角可以选择“主屏幕”、“启动屏幕”、“待机屏幕”；左侧是屏幕图层，依次向下绘制；
<br/>
![](/img_screen/4.jpg) 
<br/>
5.选择一个图层（注意不要点击第一图层，清屏在大多数时候是必须的），在右侧修改图层（具体参数在文档最后解释）
<br/>
![](/img_screen/5.jpg) 
<br/>

6.错误恢复
<br/>
如果不小心设置了错误的图片导致无法使用
<br/>
按住旋钮，重连数据线，松开旋钮。在菜单里选择 “设备”->“恢复出厂”

> ## 图层参数
### 空
    空图层
### 纯色
    设置一个矩形纯色区域
### 内置组件
    内置小组件。
    1=空
    2=按键力度条，纵向
    3=按键力度条，横向
    4=CPU Load
    5=bangocat
    
### 内置计数器
    按键计数器
### ASCII 字符串
    设置一个文本

### 内置图标
    内置图片

### 素材
    自定义图片
### 清屏
    清屏。放在第一个图层

### 偏移 X/Y
    图层偏移量，相对于左上角。偏移后的组件不能超出屏幕

### 按键对应
    对应按键事件

### 显示
    根据对应按键是状态选择性显示

### 最大位数
    显示数字的最大位数
---