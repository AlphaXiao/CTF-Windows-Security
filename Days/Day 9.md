# 文件按共享服务与木马
## 1. 文件共享服务（SMB服务）

通过网络提供文件的远程读取、修改、写入，以及文件的上传和下载服务。

文件共享服务的端口：`445`


## 2. 设置共享文件夹

右击某个想要进行共享的文件夹，选择属性

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87196.png) 

接着在弹出的窗口中勾选“共享”下面的“共享此文件夹”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87197.png) 

## 3. 访问共享文件夹

在运行中 以 `\\x.x.x.x `的形式访问提供共享文件夹的服务器IP，

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87198.png) 

之后输入账号密码

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87199.png) 

账号无误的话，即可查看到服务器所提供共享文件夹

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87200.png) 

共享文件夹权限设置：

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87201.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87202.png) 

注意：虽然在共享界面可以设置用户的访问权限，但是，用户对共享文件夹所具有的真实缺陷，最终是共享权限和NTFS权限的交集（双方都赋予某个权限，用户才真正具有此权限）。

 

为了方便管理，建议将文件共享权限设置为完全控制，之后仅依靠ntfs权限即可单方面决定用户的权限。

 > 为什么不是把NTFS权限设置成完全控制？

因为只有共享服务是要NTFS 和 共享文件夹同时授权才能操作。Telnet和远程桌面都只依赖于NTFS，如果把NTFS设置成完全控制会有很大安全隐患。

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87203.png) 
 

## 4. 共享名：

当服务器中的共享文件夹实际名称不适合被远程客户看到时，可以通过共享名修改共享后的文件（文件夹）名称

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87204.png) 

## 5. 创建隐藏共享

在设置共享文件夹时，在共享名的后面添加`$`，则表示将此文件夹设置为隐藏共享

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87205.png) 

之后，需要访问该隐藏共享文件夹的用户，需要在连接共享服务器的IP时，手动输入共享名

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87206.png) 
 

## 6. 通过CMD实现共享文件的访问

a. 建立文件共享连接

 `net use \\192.168.1.1\ipc$ 密码 /user:用户`

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87207.png) 
 

b. 查看已将连接的文件共享服务器

 `net  use`

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87208.png) 


c. 删除远程共享文件夹中的内容

 通过`cmd`命令即可实现，只需将所操作的路径改为远程共享路径即可

`del  \\192.168.1.1\工作日报\123.txt`

 

> 注意：不仅是删除命令，其它CMD命令都与上述例子同理

 

断开已经建立的共享文件连接

`net use  \\192.168.1.1\ipc$ /del`

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87209.png) 

 

`ipc$` 是windows系统中默认开启的一个共享空连接，用来让远程用户连接测试连接时的账号密码是否正确 

 

## 7. 服务器端查看哪些文件夹提供的共享服务

`net share`

如果通过共享文件的路径打开了某个程序，并不代表在服务器端打开程序，而是将服务器端的程序临时保存到客户端，并在客户端打开

 

## 8. 使用at命令 让服务器段启动定时计划

在客户端使用 `net time \\192.168.1.1` 确定服务器端的时间

之后，在客户端的cmd界面中连接远程共享文件夹，并利用

at `\\192.168.1.1 15:09 d:\123.bat`  让服务器自动在15:09执行`123.bat`

假设123.bat为带有攻击性的脚本，则服务器遭受攻击

 

## 那个啥的使用方法（HUIGEZI）

使用工具时首先配置服务程序，在弹出的界面中填写攻击者的IP地址

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87210.png) 


使用工具时将生成的服务程序通过文件共享服务传给服务器端，再通过at命令定时启动

>开启远程共享服务的情况下

在攻击者自己的电脑上cmd `copy 生成的服务程序所在路径 \\被攻击者ip地址$ ` 

例如：`copy d:\123.exe \\192.168.1.1$` 在目标主机的c盘根目录就会出现这个文件

再在攻击方cmd设置开启时间 `net time \\192.168.1.1` 然后 `at \\192.168.1.1 触发时间 c:\123.exe`

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87211.png) 
 

## 9. 默认共享的取消

a. 使用`net share` 删除已经共享的文件夹

  - 例如 `net  share  c$  /del`

 

b. 在运行中通过`services.msc`命令打开服务管理界面，之后如下图操作

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87212.png) 

 

C. 通过批处理文件（写一个含有命令的.bat文件）将`c$ d$....admin$`全部关闭，之后将批处理文件放入开机启动当中

 
要知道Telnet，SMB服务啊，这些英文简写，渗透用到的一些工具一般里面都会涉及到英文名字而非中文，比如 `NTscan10` 暴力解码器。
 

 

 

 

 
