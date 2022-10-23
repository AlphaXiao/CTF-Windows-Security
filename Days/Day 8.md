# NTFS与tlenet服务
## 1. 远程桌面组

通过远程桌面访问一台计算机时，除administrator之外，任何想要远程访问的账号都必须属于远程桌面组（remote desktop）

 

## 2. NTFS权限

NTFS格式的分区中，文件/目录 对不同 用户/组 所设置的权限

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87174.png) 


一般情况下，当对磁盘进行格式化时，磁盘的类型（文件系统）会有2种选项——FAT32或NTFS

FAT32:不支持超过4个G的单个文件的读写，没有权限设置

NTFS：没有对单个文件大小的限制，可配置NTFS权限

 

## 3. NTFS权限的继承

默认情况下，子文件夹的（文件）的NTFS权限将于父级文件夹的NTFS权限一致（从父目录继承NTFS权限），集成来的NTFS权限，默认不得修改。

如果想要任意修改文件的NTFS权限，首先需要取消文件的权限继承

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87175.png) 

## 4. 通过修改NTFS权限可以使文件（文件夹）只能被创建者本人读取和操作（删除NTFS当中其它的用户和组，只保留创建者自己的账号）

 

但是，管理员账号可以强制更改文件的所有者（特别权限）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87176.png) 

确定之后重新进入NTFS权限界面，即刻任意修改

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87177.png) 


NTFS权限不仅可以设置给账户，也可以设置给组，当设置某个组的权限后，属于该组的所有用户都将享有相同的权限

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87178.png) 
 

当一个账户同时属于多个组时，每个组的NTFS权限将叠加在一起，成为账户的权限。

 

> 注意：除了同盘符下的移动操作外，其它任何移动或复制都会使原有的NTFS权限失效，变为继承父级目录的NTFS权限。

 

## 5. windows2008开启远程桌面服务

右击“我的电脑”选“属性”，之后点击“改变设置”


![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87179.png) 


之后在“远程”标签中，选择“允许运行任意版本远程桌面的计算机连接”


![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87180.png) 
 

启动远程桌面服务之后，即可在其它计算机上尝试远程访问。

 

注意：在windows2008中，同一个账号不允许同时登录（无论本地登录还是远程登录）

 

RDP远程桌面服务

 

## 6. telnet服务

通过命令远程控制计算机的服务

 

开启telnet服务

 

在开始菜单中，找到“服务”选项

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87181.png) 
 

或者在运行中执行“services.msc”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87182.png) 

上述方法都可以打开服务管理界面

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87183.png) 

之后，在服务列表中，找到telnet

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87184.png) 

双击telnet服务，在弹出的窗口中将服务启用

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87185.png) 

telenet服务的端口号为23，可通过netstat -an进行查看

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87186.png) 

确认端口已开启之后，就可以在另一台电脑上尝试访问服务器的telnet。方法：在cmd命令界面中输入telnet ip

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87187.png) 
 

在客户端使用telnet连接服务器时，telnet会首先会尝试将当前客户端电脑的账号密码当作telnet连接的账密进行连接，此时通常选择不用本地账号尝试（N）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87188.png) 

之后，telnet会要求用户手动输入telnet连接的账号密码

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87189.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87190.png) 

注意：在telnet连接时，输入密码不会在命令界面显示（使用时不要误以为是键盘输入失败）

连接成功之后，telnet界面的视觉效果与普通cmd命令界面基本相同，但此时输入的命令影响的不是本地电脑而是telnet远程连接的电脑

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87191.png) 

 

由于本地cmd命令和telnet远程命令是在同一个界面中进行的，因此，鉴定当前命令是对哪台设备实施的，需要通过界面的标题来判断

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87192.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87193.png) 
 

另外，通过exit命令可以断开已经建立的telnet连接

 

## 7. windows 2008开启telnet

Window2008中，默认在服务列表无法找到telnet，要想使用telnet，首先要安装此服务

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87194.png) 

之后 在列表中勾选telnet服务器（如有需求也可将telnet客户端一同勾选）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87195.png) 

之后点击下一步，安装

安装之后，并不证明服务已经启动，还需要在服务管理界面中启动telnet方可（参照windows2003的启动方法）

 

 

 
