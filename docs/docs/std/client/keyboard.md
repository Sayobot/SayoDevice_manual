
# 按键设置

> ## 设置单个按键

鼠标点击一个按键，按键模式改为 **默认**，  
在 **组合键** 或 **一般键** 中选择你需要的按键即可。  
如果需要，**组合键** 可以选择 **多个**。


举几个栗子

- **设置字母 A**  
点击一般键右边的小键盘图标，选择字母A即可  
![](/img/A.jpg)

- **设置 Ctrl 键**  
点击组合键选择 **Left Ctrl** 即可。  
一般键选择 **None** 表示不选。  
键盘有两个Ctrl，*Left*是左边的，*Right*是右边的。  
![](/img/Ctrl.jpg)  
---

> ## 设置组合快捷键

按键模式改为 **默认**，  
在 **组合键** 或 **一般键** 中选择你需要的按键即可。

- **设置 复制 快捷键 Ctrl+C**  
![](/img/Ctrl+C.jpg)

- **设置 截图 快捷键 Win+Shift+S**  
![](/img/win+shift+s.jpg)

注：（不懂请忽略此条）发送组合键后自动延迟10ms后再发送一般键，这样是因为有些软件（例：远程桌面）不会把**同时**按下的键识别为快捷键，必须有先后；只设置单键不会有延时。

---



> ## 设置两组连续的按键操作

按键模式改为 **二步操作**，  
然后设置两组按键即可，方法同 **默认** 模式。  

- **设置一键粘贴+回车**  
![](/img/2setp_paste+enter.jpg)  

---  


> ## 设置鼠标 左键、右键、中键等

按键模式改为 **鼠标**，  
在 **鼠标键** 中选择你需要的按键即可。  

- **设置鼠标左键**  
![](/img/mouse_key_left.jpg)  

---  

> ## 设置鼠标光标移动、滚轮

按键模式改为 **鼠标**，  
在 **鼠标键**  不要选择按键，  
**X** 是横向移动，负数左移。正数右移。数字越大速度越快。  
**Y** 是竖向移动，负数上移，正数下移。数字越大速度越快。  
**Scroll** 是鼠标滚轮。负数下滚动，正数上滚动。  

- **设置为向上滚动**  
![](/img/scroll_up.jpg)  

---  

> ## joystick按键

这个属于额外的加载项，仅适用于windows。mac系统 **！不要！** 开启。  
在设备选项里的HID功能开启 **joystick** 保存重插，  
按键模式改为 **游戏控制器**，  
然后选择按键编号。  
这个按键和游戏手柄的任何按键都没关系，需要游戏支持自定义按键才行。  
就不放图了。

---  

> ## 按键分层（FN）
此键盘通常支持多种键盘配置，可以使用按键来切换层级

鼠标点击一个按键，按键模式改为 **FN**，选择你想切换到的按键层级;  
当按住这个按键后，再按其他键，此时生效的是设定的FN层功能；  
松开FN键后恢复基本层功能。  

如果有按键灯，你可以在灯光选项卡设置不同层灯光不同颜色，以查看层级状态
- 设置一个FN键  
![](/img/FN1.jpg)  

---

> ## 按键分层（SW）
区别于FN的按住生效，此功能是直接切换到对应层级。

鼠标点击一个按键，按键模式改为 **SW**，选择你想切换到的按键层级;  
当按下这个按键后，切换到设定的FN层功能；  
你可能还需要在目标层设置一个SW用来回到基本层。  

- 单一按键对应一层  
设置一个按键模式为SW且每层都是同样。

- 单键循环层级
选择一个按键；  
在基本层设置SW 1，FN1层设置SW 2，FN 2层设置SW 3...最后一层设置一个SW 0.

---