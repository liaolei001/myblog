title: 使用vps搭建ssr
tags:
  - 网络
categories: []
author: 廖磊
date: 2019-03-04 23:05:00
---

## **教程很简单，整个教程分三步**：
第一步：购买VPS服务器

第二步：一键部署VPS服务器

第三步：一键加速VPS服务器 （锐速安装，推荐）

### **第一步：购买VPS服务器**

VPS服务器需要选择国外的，首选国际知名的vultr，速度不错、稳定且性价比高，按小时计费，能够随时开通和删除服务器，新服务器即是新ip。

vultr注册地址:[http://www.vultr.com](https://www.vultr.com/?ref=8046196)（全球15个服务器位置可选，KVM框架，最低2.5美元/月。）

![](https://www.vultr.com/media/banner_1.png)

虽然是英文界面，但是现在的浏览器都有网页翻译功能，鼠标点击右键，选择网页翻译即可翻译成中文。

注册并邮件激活账号，充值后即可购买服务器。充值方式是paypal（首选）或支付宝，使用paypal有银行卡（包括信用卡）即可。paypal注册地址：[https://www.paypal.com](https://www.paypal.com/)（paypal是国际知名的第三方支付服务商，注册一下账号，绑定银行卡即可购买国外商品）

~~2.5美元/月的服务器配置信息：单核 512M内存 20G SSD硬盘 带宽峰值100M 500G流量/月 (此配置已下架)~~

5美元/月的服务器配置信息： 单核 1G内存 25G SSD硬盘 带宽峰值100M 1000G流量/月

10美元/月的服务器配置信息： 单核 2G内存 40G SSD硬盘 带宽峰值100M 2000G流量/月

20美元/月的服务器配置信息： 2cpu 4G内存 60G SSD硬盘 带宽峰值100M 3000G流量/月

40美元/月的服务器配置信息： 4cpu 8G内存 100G SSD硬盘 带宽峰值100M 4000G流量/月

**<font color="red">vultr实际上是折算成小时来计费的，比如服务器是5美元1个月，那么每小时收费为5/30/24=0.0069美元 会自动从账号中扣费，只要保证账号有钱即可。如果你部署的服务器实测后速度不理想，你可以把它删掉（destroy），重新换个地区的服务器来部署，方便且实用。因为新的服务器就是新的ip，所以当ip被封时这个方法很有用。当ip被封时，为了保证新开的服务器ip和原先的ip不一样，先开新服务器，开好后再删除旧服务器即可。</font>**

计费从你开通服务器开始算的，不管你有没有使用，即使服务器处于关机状态仍然会计费，如果你没有开通服务器就不算。比如你今天早上开通了服务器，但你有事情，晚上才部署，那么这段时间是会计费的。同理，如果你早上删掉服务器，第二天才开通新的服务器，那么这段时间是不会计费的。在账号的Billing选项里可以看到账户余额。

温馨提醒：同样的服务器位置，不同的宽带类型和地区所搭建的账号的访问速度会不同，这与中国电信、中国联通、中国移动国际出口带宽和线路不同有关，所以以实测为准。可以先选定一个服务器位置来按照教程进行搭建，熟悉搭建方法，当账号搭建完成并进行了bbr加速后，测试下速度自己是否满意，如果满意那就用这个服务器位置的服务器。如果速度不太满意，就一次性开几台不同的服务器位置的服务器，然后按照同样的方法来进行搭建并测试，选择最优的，之后把其它的服务器删掉，按小时计费测试成本可以忽略。
**账号充值如图**：

![](https://raw.githubusercontent.com/Alvin9999/pac2/master/pp100.png)
![](https://raw.githubusercontent.com/Alvin9999/pac2/master/pp101.png)
**开通服务器步骤如图**：
![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac%E6%95%99%E7%A8%8B01.png)

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac%E6%95%99%E7%A8%8B02.png)

#### 选择vps操作系统时，建议选择centos6，可以省去更换内核的操作

![](https://raw.githubusercontent.com/Alvin9999/crp_up/master/pac%E6%95%99%E7%A8%8B04.png)
## **第二步：部署VPS服务器**


购买服务器后，需要部署一下。因为你买的是虚拟东西，而且又远在国外，我们需要一个叫Xshell的软件来远程部署。Xshell windows版下载地址：

[国外云盘1下载](http://45.32.141.248:8000/f/d91974d046/)

[国外云盘2下载](https://nofile.io/f/eb5dUzYMQK4/Xshell_setup_wm.exe) 提取密码：666

[国外云盘3下载](https://www.adrive.com/public/NdK3Ez/Xshell_setup_wm.exe) 密码：123

如果你是苹果电脑操作系统，更简单，无需下载xshell，系统可以直接连接VPS。打开**终端**（Terminal），输入ssh root@ip 其中“ip”替换成你VPS的ip, 按回车键，然后复制粘贴密码，按回车键即可登录。粘贴密码时有可能不显示密码，但不影响， [参考设置方法](http://www.cnblogs.com/ghj1976/archive/2013/04/19/3030159.html) 如果不能用MAC自带的终端连接的话，直接网上搜“MAC连接SSH的软件”，有很多，然后通过软件来连接vps服务器就行，具体操作方式参考windows xshell。
**部署教程：**
下载xshell软件并安装后，打开软件

[![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell11.png)](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell11.png)

选择文件，新建

[![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell12.png)](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell12.png)

随便取个名字，然后把你的服务器ip填上

[![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell13.png)](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell13.png)

连接国外ip即服务器时，软件会先后提醒你输入用户名和密码，用户名默认都是root，密码是你购买的服务器系统的密码。

### 如果xshell连不上服务器，没有弹出让你输入用户名和密码的输入框，表明你开到的ip是一个被封的ip，遇到这种情况，重新开新的服务器，直到能用xshell连上为止，耐心点哦！如果同一个地区开了多台服务器还是不行的话，可以换其它地区。

[![](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell14.png)](https://raw.githubusercontent.com/Alvin9999/PAC/master/xshell14.png)

[![](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/xshell2.png)](https://raw.githubusercontent.com/Alvin9999/PAC/master/ss/xshell2.png)

用xshell连上服务器后，执行以下命令
```
wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh
```
[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416111750.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416111750.jpg)

若提示：wget :command not found  
请执行：yum install wget -y  
[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416111931.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416111931.jpg)

设置一下连接密码，

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416112048.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416112048.jpg)

设置端口。

然后按任意键开始安装，等一会后，出现下列提示，说明SSR安装成功。
![](https://www.baishitou.cn/wp-content/uploads/2018/03/QQ%E6%88%AA%E5%9B%BE20180802123036.jpg)
这张图注意保存  
因为 Vultr 的所有机房都位于国外，当晚上上网高峰期来临时，在连接速度上会比较慢，所以我们有必要安装一些程序来加速连接速度。本次推荐安装的是锐速加速软件，个人认为目前在提速方面，相比于最新的 Google BBR 拥塞控制算法，锐速尚有优势。
###  锐速安装
用Xshell连接服务器后，执行下面命令。

```
uname -r
```

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416104151.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416104151.jpg)

回车后输出当前系统内核版本。主要分三种情况：

_1、结果以 2 开头，例如 2.6.32-696.18.7.el6.x86_64。_

这种输出结果说明我们的服务器为 CentOS6 x64 系统，大家直接查看第三步进行锐速安装即可。

_2、结果以 3 开头，例如 3.10.0-693.11.6.el7.x86_64。_

这种输出结果说明我们的服务器为 CentOS7 x64 系统，大家直接查看第四步进行锐速安装即可。

_3、结果以 4 开头，例如 4.12.10-1.el7.elrepo.x86_64。_

这种输出结果说明我们的服务器已经安装 Google BBR 拥塞控制算法，此时已经无法继续安装锐速。

我用的是 CentOS7 x64 ，所以就以 CentOS7 x64 的来安装

首先更换内核，执行下面命令

```
yum install net-tools -y && wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install
```

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416105731.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416105731.jpg)

等待内核更换完毕后系统会自动重启并断开连接。

系统重启后，Xshell 软件会断开连接。等待 1~2 分钟服务器即可重启完毕，我们重新连接服务器再次连接服务器，输入下面安装命令

```
yum install net-tools -y && wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install
```

回车

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416103832.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416103832.jpg)

按回车键继续，系统会自动安装锐速，同时会先后要求我们设置锐速的三项信息。按照下图提示，我们每次都直接回车继续即可。

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416103917.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416103917.jpg)

出现下面信息，就说明锐速安装成功了。

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416104011.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416104011.jpg)

若你的系统选择是CentOS6 x64，不需要更换内核，直接执行下列安装命令

```
wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install '2.6.32-642.el6.x86_64'
```

安装步骤一路回车就行了。

电脑连接：

下载连接工具Shadowsocks
[点击下载](https://www.baishitou.cn/download/2675/)
打开后，把连接参数输入。

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416112946.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416112946.jpg)

在电脑右下角Shadowsocks 图标上单击右键。启用系统代理。

[![](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416113550.jpg)](https://www.baishitou.cn/wp-content/uploads/2019/04/null20190416113550.jpg)

然后输入YOUTUBE的网址,成功。