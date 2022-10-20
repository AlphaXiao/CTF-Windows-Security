## 1. win7管理员权限限制

即使账户拥有管理员权限，也不能随意使用。默认情况下账户以普通用户的权限进行操作。当需要管理员权限是，必须手动启用权限
+ 直接执行账户创建：

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8784.png)


> 当一个属于管理员组的账户，想要行使管理员权限执行DOS命令时，首先在打开CMD界面时需要选择：

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8785.png)

> 之后才能顺利完成账户的创建

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8786.png)


Win7当中即使是administrators组当中的账户，在C盘（系统盘）根目录中，也无法创建文件

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8787.png)

- 解决方法（1）

> 使用真正的超级管理员账户——即administrator

在win7系统当中，真正的超级管理员账户默认是禁用的，用户所使用的仅仅是一个处于administrators组中的其它账户。
启动administrator账户的方法：**在“管理”当中，取消勾选administrator的“账户已禁用”**

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8788.png)

之后再次右击administrator账户，选择设置密码

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8789.png)

- 解决方法（2）

关闭win7系统对管理员权限的使用限制.在控制面板中，找到以下位置


![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8790.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8791.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8792.png)


在账户控制设置的界面中，将滑块拖拽到最下方

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8793.png)

 **【修改之后，一定要重启计算机方能生效】**
   

## 2. win7当中启动项的路径
 在win7中，启动菜单的路径为 `C:\users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Pograms\Startup`

因此，想要将脚本植入到启动项中的命令需要写作：

```
@echo off
Copy 1.bat "%userprofile%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup"
shutdown /s /t 30
```

- Windows xp/ windows server 2003
> 家目录：`c:\documents and settings\用户名`

启动项位置：`C:\Documents and Settings\用户名\「开始」菜单\程序\启动`

Windows 7/windows server 2008
> 家目录：`c:\users\用户名`

启动项位置： `C:\users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Pograms\Startup`


## 3. 密码找回
在操作系统的桌面，连续按5次shift键，可弹出粘滞键管理界面

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8794.png)

粘滞键工具所在位置

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8795.png)

当忘记密码时，设法令计算机强制关机一次
由于上次进入系统时强制关机，因此当再次进入系统时，会出现windows错误恢复界面。选择“启动启动修复”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8796.png)

之后系统会自动检测上次意外关机所产生的错误（其实检测不出来）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8797.png)

当系统要求尝试还原时，选择“取消”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8798.png)

经过很长、很长、很长、很长、很长、很长时间的等待后，当系统再次显示修复失败时，点击界面中的“查看问题详细信息”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8799.png)

接着，点击最下方的本地物理路径链接

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87100.png)

通过弹出的记事本工具，打开电脑中的文件

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87101.png)


通过查找所有类型的文件，在system32中找到sethc程序，并改成其它名字

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87102.png)

接着把同目录下的cmd程序改名成sethc

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87103.png)

之后重启电脑，在登录界面连续按5次shift键，弹出cmd命令行界面

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87104.png)

最后，在CMD中创建新用户或修改已有用户的密码即可


## 4. 通过PE破解操作系统密码
- 极简（最小）操作系统
> 使用方法： 将PE系统镜像插入到虚拟机的光驱当中（如果在真实机上，将含有PE系统的光盘或U盘插入电脑）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87105.png)

将计算机的开机启动顺序设置为光盘（U盘）作为第一启动项，此操作需要在Bios中进行操作。（在vmware虚拟机中，启动bios的快捷键为F2）

在开启时，计算机读取硬盘之前，迅速按下F2键，进入BIOS设置界面。（不同厂商的电脑，进入BIOS的快捷键也不同，通常为F2\F1\F6\F7\F8\DEL，在物理机中操作时，可提前在网上查看自己电脑的BIOS进入方法）

另外，如果使用vmware虚拟机，还可以通过菜单中的功能进入BIOS

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87106.png)


之后在BOOT选项中，将CD-ROM Drive调整到第一位（选中后按+号）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87107.png)

启动项顺序调整完毕后保存并退出（vmware中是F10键，其它版本的硬件，使用BIOS时注意查看界面中的按键说明）

保存并退出BIOS之后，系统将重启，并进入到CD-ROM所引导的PE系统当中

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/108.png)

在PE系统中找到windows密码修改工具

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87109.png)

Windows操作系统中，用户的账号和密码都保存在SAM文件当中，SAM文件的位置通常在
`C:\windows\system32\config\SAM`
（PE系统中如果C盘符被占用，则在D盘中查找）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87110.png)


在密码修改工具上，确定SAM文件的路径后，工具会自动将SAM文件中所保存的用户名列出

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87111.png)

选中一个用户名，点击修改密码

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87112.png)

注意，密码修改完毕之后需要点击工具上的“保存修改”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87113.png)

密码修改完毕后重启电脑【并进入BIOS】，将CD-ROM Drive的顺序置于Hard Drive的下方

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87114.png)

最后，进入操作系统，使用刚修改的密码进行登录即可

## 5. 使用PE进行备份
使用方法：将PE系统镜像插入到虚拟机的光驱当中

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87115.png)

启动电脑后进入BIOS，将第一启动项设置为CD-ROM Drive

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87115.png)

之后保存，并重启电脑，进入PE系统

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87117.png)

在PE系统的工具中，找到“一键Ghost还原”工具

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87118.png)

在一键ghost工具中，选择“备份系统”，之后选择索所要备份的分区以及备份文件保存的位置（通常所备份的分区和保存备份文件的分区是2个不同的区）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87119.png)

接着，点击上图中的“确定”开始备份。之后等待备份工具自动完成备份工作。

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87120.png)

备份完毕之后，重启电脑【并进入BIOS】，将CD-ROM Drive的顺序置于Hard Drive的下方

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/121.png)

之后再次重新，进入操作系统，即可在电脑找找到分区备份所产生的文件


## 6. 使用PE进行数据还原（以此前进行过备份为前提）
使用方法：将PE系统镜像插入到虚拟机的光驱当中

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87122.png)

启动电脑后进入BIOS，将第一启动项设置为CD-ROM Drive

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87123.png)

之后保存，并重启电脑，进入PE系统

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87124.png)

在PE系统的工具中，找到“一键Ghost还原”工具
在一键Ghost工具中，选择“还原系统”，之后选择备份文件及想要还原的分区

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87125.png)

选择完毕后，点击上图中的确定，进行数据还原，并等待工具自动完成还原工作。

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87126.png)

备份完毕之后，重启电脑【并进入BIOS】，将CD-ROM Drive的顺序置于Hard Drive的下方

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87127.png)

再次重启后，进入操作系统，电脑中的数据及文件将还原到之前数据备份时的状态。

## 7. 使用PE安装操作系统

使用方法：

首先，在计算机的硬盘上下载操作系统的iso镜像
 
之后，关闭电脑，将PE系统镜像插入到虚拟机的光驱当中

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87128.png) 

启动电脑后进入BIOS，将第一启动项设置为CD-ROM Drive

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87129.png) 


之后保存，并重启电脑，进入PE系统

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87130.png) 


在PE系统的工具中，找到“系统安装器大全”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87131.png) 

打开“系统安装器大全”进入程序界面

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87132.png) 

工具打开后，暂时放置不用操作

在PE系统中找到虚拟光驱工具

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87133.png) 


在虚拟光驱中加载操作系统的iso安装镜像

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87134.png) 

 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87135.png) 

 

选中ISO文件后，虚拟光驱会在电脑中以一个独立盘符的形式显示操作系统的ISO安装程序

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87136.png) 

 

保持虚拟光驱程序的启动，回到操作系统安装工具的界面，并选择安装程序所在的虚拟光驱

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87137.png) 

 

Windows操作系统的安装文件为 `sources\install.wim`

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87138.png) 



接着，在工具上选择将操作系统安装在哪个分区上

> **注意：**

1、在PE中由于显示系统占用盘符，因此客户机上的真正C盘会变为D盘

2、通常情况下，系统所在分区和引导所在分区为同一个分区

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87139.png) 


安装时，工具会要求对所选分区进行格式化

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87140.png) 


此后，工具将自行完成后续的安装工作

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87141.png) 

待PE完成操作系统的前期安装后，重启电脑【并进入BIOS设置】，将CD-ROM Drive的顺序调整到Hard Drive 下方!
[img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87142.png)

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87143.png)

再次重启，进入操作系统，完成后续安装

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87144.png) 

最后完成安装

## 8 将ISO版的PE系统，写入U盘

将ISO镜像写入U盘需要使用专门的U盘引导写入工具，例如：

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87145.png) 

ULtraISO安装

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87146.png) 


选择程序的安装路径

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87147.png) 

连续点击下一步，到注册界面

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87148.png) 

如果拥有注册码，可填写，反之可以选择“继续试用”

准备一个空U盘，并插入电脑

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87149.png) 

之后打开ULtraISO工具，在工具界面的“文件——打开”中选择想要拷入U盘的ISO文件

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87150.png) 

选中ISO镜像之后，将下方的路径选为U盘所在的盘符

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87151.png) 

当ISO镜像和U盘路径都选定后，通过“启动——写入硬盘映像”将ISO拷入U盘

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87152.png) 

在执行写入之前的界面，确定路径是否正确，并将写入方式定为“USB-HDD+”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87153.png) 

写入U盘之前先执行U盘的格式化

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87154.png) 

格式化完毕后，点击界面中的“写入”按钮

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87155.png) 

之后程序将自动完成ISO到U盘启动的写入工作

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87156.png) 

U盘启动写入完毕后，U盘所在盘符的卷标（分区名称）将发生改变

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87157.png) 

打开作为启动工具的U盘，可看到里面包含ISO镜像中的各种文件及引导

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87158.png) 

## 9. 磁盘的压缩（win7以上操作系统的功能）

在win7操作系统的磁盘管理中，可以通过“压缩卷”功能将一个大的分区进行无损拆分（无论动态磁盘还是基本磁盘）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87159.png) 

 

## 10. win7磁盘管理

在win7及win7以上操作系统中，基本磁盘具备了动态磁盘的扩展卷功能

但是，win7基本磁盘在扩展时，只能使用后续的连续磁盘空间进行扩展

# Dos命令进阶、变量与流程控制

1. if命令 (if表示程序中的判断条件)

- 格式： `if  判断条件  判断如果成功所执行的命令`

- 例： 
```
set /p num=请输入一个数字
If  %num%==0  echo 您输入的数字为0
```

上述例子中，如果用户输入0，则显示“您输入的数字为0”，如果用户输入的是其它数字，则不显示任何内容

2. `&` 该符号表示命令与命令之间的分隔，可以实现在同一行中编写多条命令

- 格式：`命令1  & 命令2 & 命令3 &....`

3. `exit` 命令  退出当前程序

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87160.png) 


4. `if not` 命令

-  格式：`If  not`  判断条件  不符合条件时执行的命令

- 例：
```
   set /p age=请猜猜我的年龄

   If not %age%==18  echo  您猜错了
```

在上述例子中，只要用户输入的不是18，就显示“您猜错了”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87161.png) 


5. `:` 与 `goto`

通过:可以设置一个跳转目标

之后当程序执行过程中需要goto时，可跳转到指定的位置

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87162.png) 


## 作业

制作一个批处理脚本，

通过用户先择，可以执行创建普通用户，创建管理员用户，修改当前用户密码，定时关机

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87163.png) 

 

 

 

 

 

 

 
