# Day1 VMware安装与基础配置

## VMware安装

1. 点击下一步

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%871.png)

2. 点接受，下一步

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%872.png)

3. 这里选择安装路径，尽量不要放到C盘，点更改修改安装路径

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%873.png)

4. 将这一条勾选上，下一步

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%874.png)

5. 默认，下一步

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%875.png)

6. 安装

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%876.png)

7. 完成安装

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%877.png)

8. 找到下载好的路径，打开，然后输入秘钥，下边提供了几个自己试

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%878.png)

ZF3R0-FHED2-M80TY-8QYGC-NPKYF

YF390-0HF8P-M81RQ-2DXQE-M2UT6

ZF71R-DMX85-08DQY-8YMNC-PPHV8

ZF3R0-FHED2-M80TY-8QYGC-NPKYFYF390-0HF8P-M81RQ-2DXQE-M2UT6ZF71R-DMX85-08DQY-8YMNC-PPHV8

## 下载XP系统并调试

>  用XP镜像下载XP系统

### 如果操作虚拟机完毕之后，鼠标无法从 vmware 中移出,使用快捷键：`ctrl+alt`

### 虚拟机的桌面无法全屏显示（四周有黑边）

解决方法 1：

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%879.png)

> 缺点：当全屏显示时，画面清晰度降低，并且表象变形解决方法 


解决方法2：安装 vmware tools
在虚拟机启动的情况下，点击下图的选项

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8710.png)

一直点击下一步完成安装,安装完成之后关闭虚拟机，点击配置虚拟机的显示器

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8711.png)


接着将虚拟机显示器的分辨率调整到与物理机分辨率相近的数值

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8712.png)


重启启动虚拟机之后，vmware tools 会自动调节虚拟机的画面至最佳视觉效果，我们将“拉伸客户机” 设置为“自由拉伸”即可

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8713.png)


### Vmware tools 的功能

（1）调整虚拟机画面的视觉效果
（2）实现虚拟机和物理机之间的 `剪贴板共享`

### 虚拟机和物理机之间的共享文件夹

设置共享文件夹

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8714.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8715.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8716.png)


共享的文件夹，在虚拟机的网上邻居中可以查看（再虚拟机中将网上邻居图标调出）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8717.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8718.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8719.png)


右击网上邻居，把共享文件夹映射到虚拟机上

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8720.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8721.png)

设置完毕之后，即可在虚拟机的“我的电脑”中找到共享文件夹（以映射的盘符命名）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8722.png)

如果在虚拟机中不做文件夹的映射，也可以在网上邻居的资源管理器中找到共享文件夹

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8723.png)


### 虚拟机快照

将虚拟机某个时刻的状态记录下来，日后可通过该快照快速将虚拟机还原到之前的状态。

1. 拍摄快照

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8724.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8725.png)


2. 还原快照
   ![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8726.png)


选择之前拍摄好的快照，之后点“转到”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8727.png)

### 虚拟机克隆

以当前某个虚拟机的状态为基础，重新复制出一个新的虚拟机。

注意：

1. 虚拟机的克隆需要以虚拟机快照为基础
2. 用户克隆的快照不能是虚拟机启动时的快照

> 步骤：关闭虚拟机，在关闭状态下，拍摄一个快照

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8728.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8729.png)


接着便可以用关机时的快照进行克隆

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8730.png)

克隆时，具有“链接克隆”和“完整克隆”两种选项

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8731.png)

1. 使用链接克隆，所生成的文件较小，但必须依赖于源虚拟机


3. 使用完整克隆，所生成的文件较大，但不会收到源虚拟机的影响。

> 注意：克隆出的虚拟机除了状态和文件与源虚拟机完全一致之外，计算机名也会源虚拟机相同。
> 当两台同名的计算机处于同一个网络当中时，会发成通信错误，因此，建议将克隆出的虚拟机进行改名。方法：

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8732.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8733.png)


### 虚拟机的迁移

将虚拟机文件夹移动到其它位置或其它电脑之后，可以通过 vmware 重新打开，但是在首次打开时，会出现如下提示


![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8734.png)


> 我已移动该虚拟机:不修改虚拟机中的任何信息（计算机名、SID、网卡地址等） 

> 我已复制该虚拟机:重新生成新的唯一标识

### Windows 操作系统的历史版本

个人版： DOS
Win3 
Win95 
Win98 
Win me 
Win xp 
Win vsita
Win 7
Win 8
Win 10

服务器系统： winNT
Win server 2000
Win    server 2003
Win    server 2008
Win    server 2012
Win    server 2016

### windows2003 安装

1. 之前的步骤与 winxp 一致
2. 服务器的连接数量，根据需要登录改服务器的人数而定

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8735.png)


3. 服务器版的windows 操作系统，要求用户务必填写密码，且密码必须符合 3/4 原则。1、数字	2、小写字母	3、大写字母	4、标点
   3/4 原则：密码必须至少同时包含上述 4 种字符中的 3 类。
4. 服务器版的windows 操作系统，在进入桌面之前需要通过用户手动输入 ctrl+alt+del 组合键，进行验证

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8736.png)


由于 window server 要求的组合键验证与物理机上打开任务管理器的快捷键冲突，因此在 vmware 上专门设置了快捷键发送按钮。

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8737.png)


5. 完成安装之后，参照安装XP 系统的步骤，为虚拟机安装 vmware tools，并拍摄快照
6. Window server 操作系统，在界面中关机时，需要填写“注释”内容方可关机（打个空格即可）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8738.png)


### 取消开机时的组合键验证（实验环境中可取消，生产环境中建议保留）

开始菜单中打开“运行” 之后输入 `gpedit.msc`

在“计算机配置”--Windows 设置--安全设置--本地策略--安全选项当中，找到“交互式登录： 不需要按 ctrl+alt+del”这一项

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8739.png)

将此项改为启用

### 密码复杂限制（实验环境中可取消，生产环境中建议启动）

开始菜单中打开“运行” 之后输入 `gpedit.msc`

在“计算机配置”--windows 设置--安全设置--账户策略--密码策略--密码必须符合复杂性要求

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8740.png)


### 在操作系统当中划分硬盘

当安全系统时如果存在未划分的硬盘空间，那么，在进入操作系统之后，可以按照以下操作进行磁盘划分

1. 右击我的电脑选择“管理”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8741.png)

2. 在磁盘管理中，黑色区域表示未划分的磁盘，右击此处，选择“新建磁盘分区”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8742.png)


3. 在界面中选择主磁盘分区

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8743.png)


4. 选定盘符之后，执行快速格式化

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8744.png)


5. 在磁盘管理界面中，右击某块磁盘，选择“更改驱动器号和路径”，可以修改当前分区的盘符

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8745.png)

### 在虚拟机上添加新的硬盘

1. 在虚拟机关闭的状态下进行操作，虚拟机设置中可以添加设备

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8746.png)


2. 添加新的硬盘之后，进入虚拟机的操作系统，并进入磁盘管理界面。系统会提示对新插入的硬盘进行初始化

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8747.png)
