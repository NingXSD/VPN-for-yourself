#VPN-for-yourself 
本篇将如何创建属于自己的高速VPN，非免费但是廉价安全！
# 一、科学上网
通过科学上网，意思就是通过VPN技术，绕过一些网络限制，访问到常用的一些外网网站，比如通过谷歌查询一些技术文献就比较方便了。
全部搭建完成后最后可达成的效果为日本服务器60-100ms延迟，下载速度在20Mb/s根据网络波动和使用时间段有关
## v2ray个人搭建教程前言

也许你需要查阅一手技术资料进行学习，也许你想要在互联网中真正的畅游全世界，也许你希望你的网上请求都经过加密处理...

这，你需要一个代理工具，让它来帮你实现科学上网，跨过墙，市面上有一些第三方的代理工具，但并不一定安全稳定，最好的方式自己搭建一个完全属于自己的代理工具。

而 [V2ray](https://github.com/v2fly/v2ray-core) 就是一种相对稳定、安全、跨平台的代理工具。

你完全可以自行搭建好，而且很简单，下文会详细说明。

在此之前，你需要拥有一台墙外的服务器，然后在里面安装并配置好 v2ray。
# 二、购买属于自己墙外VPS（云服务器）
## vultr墙外服务器购买流程

推荐的购买服务器网址：
https://vultr.com/

理由：可以用国内邮箱注册，新用户重置10美金赠送100美金，而我们使用的VPS最低每月6美金，可以支持18个月不关机连续使用，如果能做到使用时才启动VPS，可想而知能用多久。

进去之后你可以看到这个页面，说明你已经通过 vultr  获得了 100 美元赠送的资格：

现在你只要选择支付宝充值 10 美元以上，就可以获得额外赠送的 100 美元。

接下来就可以在这个平台选购云服务器了。

切换成旧版

选择Cloud Compute - Shared CPU--->服务器位置选择在tokyo（根据自己的需求和位置来选择）--->Ubuntu25.10  x64--->最便宜的6/month--->取消自动备份，勾选IPv6--->deploynow

这时候你就拥有了自己的一台云服务器了：

<img width="1261" alt="VPN搭建教程" src="https://user-images.githubusercontent.com/84239400/119021075-86068180-b98e-11eb-82a9-71edb9934f23.png">


点击 Cloud Instance ，可以看到你服务器的 IP 地址和密码：

<img width="1308" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119021183-a20a2300-b98e-11eb-8ff4-7f18d3e3bb80.png">


## 连接到你的服务器

### windows 系统连接到 vultr 服务器

windows 可以下载[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)工具。

打开之后选择 session，将你在 vultr 网上得到的服务器 ip 复制过来，输入到这里：

![](https://user-images.githubusercontent.com/84239400/119023900-037fc100-b992-11eb-85ea-525a61a69657.png)

Port 默认 22，Connection Type 选择 SSH，接着点击 Open，连接进去之后输入你云服务器的密码。

### Linux 和 MacOS 连接到 vultr 服务器

Linux 和 MacOS 可以打开终端，使用如下命令连接：

```
ssh root@xx.xx.xxx.xx
```

`xx.xx.xxx.xx`就是你的服务器上的 IP 地址。

连接进去之后输入 yes 后按回车，接着输入你云服务器的密码，即可使用云服务器。

<img width="772" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119024049-32963280-b992-11eb-8c05-db6df1f7fbfa.png">

OK，现在你已经准备完毕，接下来开始搭建，很快就能搞定！

## 配置服务端

在服务器终端输入

bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)

原安装命令网址在：https://github.com/vaxilu/x-ui

更新后会要求你设置名称如admin和密码如123456，端口号如54321，（全部随便设置就行）

关闭防火墙：

ufw disable

安装完成后访问ui面板

你的服务器ip地址:设置的端口号(英文冒号）
例如167.179.98.152:54321

输入账号密码登录（你自己设置的）

观察xray的内核是否正常工作

如果显示error

在服务器执行 x-ui update

正常工作进入入站列表，备注自定义，协议vless，端口8443，传输协议ws，点击添加

创建成功后点击查看，然后点击复制，粘贴到v2ray里，就可以正常使用
## 配置客户端

https://github.com/v2fly/v2ray-core/releases

windows和linux不同操作系统请在该网址自行下载V2ray
