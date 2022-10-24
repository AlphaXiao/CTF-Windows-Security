# 动态网站与FTP
## 1. IIS中的账户

 在创建web站点时，界面中会默认勾选“允许匿名访问网站”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87281.png) 

匿名访问，不是免账号/密码访问，而是在用户访问时，自动提供一个公用账号来访问网页

 

## 2. IIS中公用账号的填写位置

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87282.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87283.png) 

注意：在匿名访问处，填写的账号、密码，必须是 windows中当下存在的账号及正确的密码

 

## 3. 同服务器下发布多个网站的方法

> a. 方法一：将第2个网站的端口号设置为除80外的其它编号

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87284.png) 


当用户访问网站时，只需在IP地址的后方加上端口号

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87285.png) 
 

> b. 方法二：在网卡上添加第二个新的IP地址

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87286.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87287.png) 

之后，将网卡上新添加的IP分配给第二个网站即可

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87288.png) 


> C. 方法三：在IIS上，为每个网站配置不同的主机头（域名）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87289.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87290.png) 

同时，还要在DNS上将两个域名都对应到web服务器的IP地址上

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87291.png) 

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87292.png) 

IIS和DNS都配置完毕后，用户就可以通过不同的域名访问不同的网站了。


## 4. 动态网站

用户、页面、数据库，三者之间可以实现交互的网站。

动态网站语言：`asp  php  jsp`

 

IIS：`asp`       文件： `.asp`

Linux：`php`    文件： `.php`

## 5. 安装asp服务

1）打开windows2003的安装盘

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87293.png) 

2）双击“应用程序服务器”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87294.png) 

3）双击“Internet信息服务（IIS）”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87295.png) 

4）双击“万维网服务”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87296.png) 

5）勾选“Active Server Pages”(ASP)

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87297.png) 

6）一路点击下一步，完成服务的安装

7）ASP服务器启动之后，需要重新创建支持ASP的站点，在创建站点时，权限选择如下图所示。

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87298.png) 

8）站点创建完毕后，还需检查IIS是否开启了ASP支持

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87299.png) 

以及默认首页是否正确（通常ASP网站的默认首页为index.asp）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87300.png) 

 
## 6. win2008安装IIS

1） 右击我的电脑选“管理”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87301.png) 

2） 在角色选项中，选择“添加角色”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87302.png) 

 

4）尝试勾选“web服务（IIS）”，界面中会弹出窗口要求安装必备功能

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87303.png) 

之后点击下一步

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87304.png) 

5）默认安装下，站点只支持静态网页，如果需要动态支持，需要勾选ASP

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87305.png) 

之后一路下一步即可完成安装。


## 7. FTP服务

 远程实现文件的上传和下载、甚至修改

## 8. FTP服务对应的端口号

 21（控制端口）

 20（数据端口）

 

## 9. 安装FTP服务

1）打开windows2003的安装盘

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87306.png) 

3）双击“应用程序服务器”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87307.png) 

3）双击“Internet信息服务（IIS）”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87308.png) 

4）勾选“文件传输协议（FTP）服务”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87309.png) 

5）之后一路下一步即可完成服务的安装

 

## 10. ftp站点创建

1）在IIS中，找到FTP站点，之后新建

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87310.png) 

2）在创建时为站点指定IP地址，（默认端口21）

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87311.png) 

3）选择一个文件夹作为FTP文件上传或下载的目录

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87312.png) 

4）建议在FTP权限处，将读取和写书都赋予，之后通过NTFS权限限制用户

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87313.png) 

5）站点创建完毕后，建议关闭匿名访问的账号

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87314.png) 

 
## 11. 访问FTP站点

在客户机上，我的电脑中，地址栏内输入ftp://IP, 之后输入账号密码

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87315.png) 

 

## 12. win2008安装ftp服务

1）右击我的电脑选“管理”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87316.png) 

2）如果之前安装过IIS的web服务，则展开“角色”，可找到IIS服务器

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87317.png) 

3）右击IIS服务器，选择“添加角色服务”

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87318.png) 

4）之后在界面中勾选FTP服务器

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87319.png)

5）安装完成之后，即可在开始菜单中管理FTP站点

![img](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%87320.png) 

 
