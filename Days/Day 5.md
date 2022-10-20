1. win7管理员权限限制

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
   

2. win7当中启动项的路径
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


3. 密码找回
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


4. 通过PE破解操作系统密码
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

5. 使用PE进行备份
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


6. 使用PE进行数据还原（以此前进行过备份为前提）
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

