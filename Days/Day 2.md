# Day2 学习磁盘划分与简单系统命令和dos命令
1. 把我的电脑图标设置到桌面上（右键→属性→桌面→自定义桌面）
2. 点击我的电脑看看除C盘以外的盘是否格式化。若没有格式化，右键选择格式化→快速格式化→确定
3. 右键我的电脑→管理→磁盘管理。若是在安装操作系统时没有划分磁盘，就可以在这里进行划分

### 基本磁盘和动态磁盘
安装操作系统时计算机上自带的第一块磁盘默认为基本磁盘；系统安装完毕之后，新插入的磁盘默认为动态磁盘。

基本磁盘：不能随意扩展

动态磁盘：可以随意扩展

### 动态磁盘的特点
1. 当某一个分区的空间不够时，动态磁盘可以从任意空余的磁盘空间中选择一部分，扩大当前分区的容量
2. 动态磁盘的某个分区，可以不是硬盘中连续的存储空间

### 动态磁盘不同种类的对比

|       | 磁盘数量 | 区域 | 空间要求 | 磁盘利用率 | 性能 |
| ---------- | ---------- | ---------- | ---------- |---------- | ---------- |
|     简单卷       |   1        |       >=1     |       无     |      100%      |      一般      |
|     跨区卷       |     >=2       |     >=2       |      无      |     100%       |     一般        |
|     带区卷      |      >=2      |     >=2       |      要求一致      |    100%        |     快！       | 
|     镜像卷     |      2      |       2     |     要求一致       |      50%      |      一般      |  
|     RAID-5     |      >=3      |       >=3     |     要求一致       |     (n-1)/n       |      较快      | 



### 数据恢复
镜像卷： 镜像卷中，当有一块磁盘损坏时，另一块磁盘仍然可以正常访问，且其中包含原分区中的所有数据

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8748.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8749.png)


算坏的镜像卷虽然可以正常访问，但还应及时修复先将一半的镜像卷还原成简单卷

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8750.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8751.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8752.png)


接着为简单卷添加镜像，使其重新变为镜像卷

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8753.png)


RAID-5 卷： RAID-5 卷中，当有一块磁盘损坏时，另外几个磁盘仍然可以正常访问，且其中包含原分区中的所有数据。

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8754.png)


另外，当【动态】磁盘的数量足够时（大于等于 3），右击损坏的 RAID-5 卷可以进行修复

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8755.png)

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8756.png)


### 磁盘转换
基础磁盘可以在磁盘管理当中转化成动态磁盘

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8757.png)


> 基本磁盘转化为动态磁盘:数据不丢失；动态磁盘转化为基本磁盘:数据会丢失

### DOS 命令提示符界面
打开 DOS 命令提示界面
1. 通过开始菜单的附件，找到

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8758.png)

2. 通过“运行”功能，启动命令提示符界面（ `widnows 键+R` ）

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8759.png)


在运行界面输入 `cmd`

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8760.png)

3. 命令提示符程序的真实位置

![image](https://github.com/AlphaXiao/CTF-Windows-Security/blob/main/Days/pictures/%E5%9B%BE%E7%89%8761.png)

### 系统命令：
1. `color` 颜色		改变命令提示符界面的背景和文字颜色查看颜色	`color ?`
`Color` 命令后方需要 2 位 16 进制数字，前一位表示背景色，后一位表示前景色（文字颜色） `Color 0A`

2. `dir`   显示对应位置中的文件及文件夹 dir	默认只显示非隐藏的文件夹和文件

显示指定目录下的文件内容 `dir d:\`
`dir e:\i386`

显示所有文件及文件夹（包含隐藏文件） `dir /a`

3. 路径
> 相对路径（相对于说话人[命令提示符]所在位置）; 绝对路径（以盘符为起始，不受说话人位置的影响） 

相对路径 `..\abc`	`.\777\123.txt`	`abc\666.txt` 

绝对路径 `C:\123\web`	`D:\wenjian\jimi\1.doc`
注意：文件夹或文件的名称有含空格时，完整的路径需要包含在 `""`（半角）中间 `"C:\documents and settings\1.txt"`
`"..\abc\wo de you xi\game.exe"`

4. cls 清屏 清除命令提示符界面中之前所输入的命令和执行结果


5. cd 改变当前位置
`cd ..`	跳出到上一级文件夹

`cd "C:\documents and settings"`

注意：`cd` 命令虽然可以改变路径，但不能跨盘符（分区）

6.`C:`   `D:`   `E:`	改变所在的盘符（分区）
