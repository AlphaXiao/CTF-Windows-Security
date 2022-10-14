# 学习用户与组、win8虚拟机下载配置
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
