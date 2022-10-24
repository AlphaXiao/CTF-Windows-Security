# DHCP与域名
## 1. 那个啥的使用方法

使用工具时首先配置服务程序，在弹出的界面中填写攻击者的IP地址

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87213.png) 

使用工具时将生成的服务程序通过文件共享服务传给服务器端，再通过at命令定时启动

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87214.png) 

当服务器端在定时计划执行之后，攻击方的工具界面中会提示有设备自动上线

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87215.png) 

当成功控制目标设备之后，攻击者不仅可以任意上传或下载文件，同时在遇到可执行程序时，能够选择由本地打开还是远程打开

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87216.png) 

此外，通过该工具，攻击者还可以捕获被攻击方的桌面

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87217.png) 

当捕获屏幕后，还可以通过“发送鼠标和键盘”来远程代替被攻击方进行键盘、鼠标的操作

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87218.png) 

注意，被攻击的设备如果不进行muma的处理，则每次上线后都会被攻击者发现，并被控制。如果攻击者想要放弃对某台设备的监控，操作如下图

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87219.png) 


## 2. DHCP服务（Dynamic Host Configuration Protocol）

自动为客户机分配IP地址的服务

DHCP服务的优点

1、减少工作量

2、避免IP的冲突

3、提高IP的利用率

 

DHCP服务所提供的内容

IP地址、子网掩码、网关、DNS

 

DHCP服务的端口号

UDP 67/68

 

## 3. DHCP服务的工作原理

1）客户机发送DHCP Discovery 广播

 客户机通过该广播请求IP地址（发送的请求中包含客户机自己的网卡地址）

2）DHCP服务器接收到Discovery广播之后，会进行响应，发送DHCP Offer广播

 服务器响应提供的IP地址

3）之前发送了Discorvey广播的客户机，在接收到服务器的Offer广播时，发送DHCP Request广播

客户机选定IP地址，并广播请求IP的详细配置

4）服务器接受到Request广播后，发送DHCP ACK广播

ACK广播中包含IP地址，SM，网关地址，DNS地址，租期

 

租期：

当一台电脑通过DHCP服务器获取到IP地址后，IP都会有一定的租期。当IP地址的租期到达50%时，客户机会再次发送DHCP Request进行续约，如果续约成功，租期重新从0%开始计算。

如果服务器无响应，则继续使用IP到87.5%再次发送 DHCP Request进行续约。如果再无响应，到租期达到100%时，释放IP地址，并发送DHCP Discovery广播获取新的IP地址

 

4. windows2003搭建DHCP服务器

1）确保作为服务器的电脑，IP地址是手动配置的固定IP地址

2）在wondows2003的光驱中插入windows2003的系统安装盘，并读取光盘内容

3）在windows2003的关盘启动后，选择“安装可选的 windows组件”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87220.png) 

4）之后在界面中找到“网络服务”选项，并双击

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87221.png) 

 

5）双击“网络服务”之后，在新的窗口中，勾选DHCP选项

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87222.png) 

6）之后一路确定直到安装完成

7）安装完成之后，在开始菜单中，可以找到DHCP管理工具

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87223.png) 

8）在DHCP管理工具中，右击服务器图标，选择“新建作用域”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87224.png) 

9）创建作用域时，需要填写可用IP地址的范围及子网掩码

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87225.png) 

10）除了IP和SM之外，还需要确定租期

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87226.png) 

如果局域网对应的人员变动不大，租期可适当变长，如3天，5天等。如果局域网中人员的变动频繁（商场、饭店），则租期可设置较短，如30分钟

 

11）作用域创建完毕后，需要即可方可生效

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87227.png) 

 

关闭vmware自带的DHCP服务

在 vmware工具的菜单中，点击“编辑——虚拟网络编辑器”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87228.png) 

之后在弹出的界面中，选中虚拟机所在的vmnet，接着找到下方的“使用本地DHCP服务将IP地址分配给虚拟机”，并取消该项的勾选

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87229.png) 

由于DHCP所提供的IP地址有一定的租期，因此关闭上图的DHCP服务后，已经获取IP的计算机仍然会使用原有IP。此时，可使用

ipconfig  /release 释放当前的IP配置

之后再用

`iPconfig  /renew`  重新向dhcp服务器索取IP地址

 
## 5. DHCP中的保留地址

对于有特殊用户的IP，要求该IP必须只应用在唯一的指定电脑上，并且客户端还需要通过自动获取来得到该IP

  那么，就可以使用DHCP中的保留功能，将某个可分配的IP地址与计算机的MAC地址对应，在日后的IP分为中，被保留的IP地址只能配给对应的MAC网卡

操作方法：

 在DHCP管理工具中，右击“保留”，选择“新建保留”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87230.png) 

接着填写IP地址和网卡地址，使它们彼此绑定

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87231.png) 

DHCP占用攻击

命令： 在kali的命令行中  `pig.py eth0`

 
## 6. Windows2008 配置DHCP服务

1）将服务器的IP地址手动配置为固定IP

2）右击我的电脑（计算机），选择管理

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87232.png) 

3）接着在“角色”中添加角色

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87233.png) 


4）接着勾选DHCP服务，并点击下一步

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87234.png) 


5）在windows2008中，安装DHCP服务的同时，系统会要求配置一个DHCP地址池

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87235.png) 


6）之后将IPV6的DHCP设置为禁用

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87236.png) 


7）最后点击“安装”进行最后的服务安装

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87237.png) 


8）安装完成后，便可在开始菜单中找到DHCP管理工具

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87238.png) 
 

## 7. 域名

 就是IP地址的别名

因为IP地址是由无意义的数字组成，不便于记忆。因此才通过域名来代替IP地址，实现彼此的通信。

 

域名的命令规则

数字

字母(不区分大小写)  

连字符  

中文

 

域名的组成

  `www.`   `baidu.`    `Com`    ` .`

  三级域   二级域   顶级域     根域  

 顶级域（由供应商提供选择）

   国际域名的顶级域（后缀是组织、机构的名称）

   `Org`   `com`  `edu`  `net`  `cc`  `tv`

   国内域名的顶级域（后缀是国家、地区的名称）

  ` cn `  `.us`  `.JP`  `.hk`  `.tw`

 

二级域（由用户付费选择，不能选择他人已经使用的二级域）

 

三级域（由用户自由选择，无需付费）

 

## 8. DNS服务

域名解析服务——把域名解释为IP地址，并访问IP对应的服务器内容

端口：`53`

 
