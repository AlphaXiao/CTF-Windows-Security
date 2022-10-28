# DNS服务与web服务
## 1. windows2003上的DNS服务器配置  

1）要求服务器的IP是手动配置的静态IP地址

2）打开windows2003的系统盘，选择“安装可选windows组件”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87239.png) 

3）之后在弹出的窗口中双击网络服务

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87240.png) 

4）接着勾选“DNS”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87241.png) 

5）最后一路点击下一步完成安装

6）安装完成之后，即可在开始菜单中找到DNS管理工具

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87242.png) 

7）在管理工具中，右击服务器图标，选择新建区域

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87243.png) 

8）在创建时选择主要区域

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87244.png) 

9）之后选择正向查找区域

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87245.png) 
 

> 在填写域时，写到二级域即可

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87246.png) 

10）区域创建完毕之后，正向查找区域中找到新建的区域，并在右侧选择“新建主机”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87247.png) 

11）在弹出的窗口中输入一个前缀，程序会自动组成一个三级域名，下方需要填写的IP则是与该三级域名对应的IP地址

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87248.png) 

12）域名解析记录创建完毕之后，在客户机上，将网卡的DNS服务器地址设置为刚刚配置DNS服务的设备IP

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87249.png) 
 

13）客户机所选择的DNS服务器指定之后，即可尝试通过Ping命令，访问所解析的域名

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87250.png) 

递归查询：客户机与本地DNS服务器之间

迭代查询：本地DNS服务器与公网上的DNS服务器之间的解析过程

 

客户机问本地DNS-----本地DNS知道答案并回答（递归）

本地DNS问外网DNS----本地DNS不知道答案，逐层询问外网DNS服务器（迭代）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87251.png) 

## 2. DNS转发

当客户机访问的域名在指定DNS服务器中无法找到相应的解析时，DNS服务器可寻求其它DNS服务器的帮助，这一寻求帮助的过程叫做DNS转发

设置方法：

1） 右击DNS管理工具中的服务器，选择“属性”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87252.png) 

2） 之后在窗口中的“转发器”选项中，填写另一台DNS服务器的地址。

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87253.png) 

3） 转发器设置完毕之后，如果当前DNS服务器遇到无法解析的域名，则转交给转发器中的设备进行处理

查看是哪个服务器上的DNS为你解析的当前地址 `ns lookup`

查看某个域名是谁解析的 `ns lookup 域名`

## 3. DNS反向解析

通过IP地址解析出设备的域名（名字）

操作方法：

1）在反向查找区域处选择“新建区域”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87254.png) 

2）在弹出的窗口中输入IP地址的前3段

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87255.png) 

之后一路下一步直到区域创建完成

3）在所创建的反向区域中新建**PTR（指针）**

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87256.png) 

4）在窗口中填写IP 地址的最后一段以及对应的名称

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87257.png) 

通过`ns lookup 域名`命令可以看到解析该域名的服务器的名字

## 4. 别名解析

如果多个域名同时代表一个IP，并且由一个域名A作为主要域名，那么，其它的域名可以解析成域名A的别名

操作方法：

1）在正向解析区域中，某个域名的解析记录列表下右击，选择“新建别名”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87258.png) 

2）在弹出的窗口中，首先输入作为别名的域（三级域），之后在下方的文本框中，输入源域名（可通过旁边的按钮浏览查找）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87259.png) 

3）解析记录创建完毕后，即可通过客户机尝试访问

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87260.png) 
 

总结

正向解析：A记录

反向解析：PTR记录

别名解析：CNAME记录

 

### 客户机访问域名的顺序

> 当DNS解析过一个域名就会把解析出来的ip地址和对应的域名放到DNS缓存中，当用户第二次访问同样的域名，服务器会直接从DNS缓存中找到对应ip，这也就是为什么第一次访问某个网站速度慢，第二次登录就会快很多的原因。如果原域名对应的ip地址发生变动，有可能用户就访问不到，因为服务器会直接去DNS缓存中找历史记录而不是去找对应的DNS服务器解析，这就有可能出现DNS缓存中的ip地址与变动后的ip地址不同，访问不到。可以通过清除客户机DNS缓存解决。

**DNS缓存----本机hosts文件---本地DNS服务器**

hosts文件的位置

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87261.png) 
 

【病毒-禁止访问网站】

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87262.png) 

禁止访问 `www.baidu.com` 和 `www.hao123.com`

 

### 客户机清除DNS缓存

`ipconfig  /flushdns`

 

### DNS服务器解析域名的顺序

**DNS高速缓存--本地DNS解析记录--DNS转发器--根提示**

> 从别的DNS服务器解析（DNS转发器）来的域名会保存到高速缓存中

> 如果原域名ip地址发生变动，清除了客户机DNS缓存还是访问不到，有可能是因为DNS服务器高速缓存中仍有原解析信息备份，可以再次清除高速缓存解决问题

DNS服务器高速缓存的位置：

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87263.png) 

清除缓存

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87264.png)  

### Windows安全运维
安全运维工作者要经常清理DNS高速缓存，也要让客户机清理本地DNS缓存，避免拿到过时ip地址无法访问某些域名。

## 5. WEB服务

提供网页的浏览服务，使客户机能够通过浏览器访问网站中的页面。web服务器可以将网站发布出去，让网民进行访问。

HTTP协议端口号：`80`

## 6. 可提供web服务的工具

微软：`IIS`

Linux：`Apache`

`Tomcat/nginx`

第三方工具：`phpstudy/XAMPP...`

## 7. 开启IIS服务器

操作步骤

1）要求服务器的IP是手动配置的静态IP地址

2）打开windows2003的系统盘，选择“安装可选windows组件”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87265.png) 

3）在界面中双击“应用程序服务器”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87266.png) 

4）接着双击“Internet信息服务（IIS）”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87267.png) 

5）再然后，双击“万维网服务”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87268.png) 

5）之后勾选“万维网服务”界面中的新的“万维网服务”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87269.png) 

6）之后一路下一步，完成安装

7）安装完成之后，即可在开始菜单中找到IIS管理工具

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87270.png) 

 

8）IIS安装完毕后，会发布一个默认的网站

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87271.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87272.png) 

9）在自己搭建新网站之前，建议将IIS的默认网站删除

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87273.png) 

 

## 8. 在IIS中创建新网站

1）右击“网站”选择“新建------网站”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87274.png) 

2）在创建网站的界面中，需要将本机的IP地址指定给网站，同时，默认的端口为80

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87275.png) 

3）选择一个文件夹作为网站的根目录

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87276.png) 

4）在网站根目录中放入网站程序、网页等元素

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87277.png) 

5）在IIS管理器中为刚刚创建网站指定默认首页

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87278.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87279.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87280.png) 


