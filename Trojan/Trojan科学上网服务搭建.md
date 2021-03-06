# trojan-go搭建

## 一、简介

Trojan是近两年兴起的网络工具，项目官网https://github.com/trojan-gfw。

与强调加密和混淆的SS/SSR等工具不同，trojan将通信流量伪装成互联网上最常见的https流量，从而有效防止流量被检测和干扰。在敏感时期，基本上只有trojan和V2Ray伪装能提供稳如狗的体验。

V2Ray和Trojan有如下区别及特点：

1. v2ray是一个网络框架，功能齐全；trojan只是一个绕过防火墙的工具，轻量级、功能简单；都使用TLS加密的情况下，理论上trojan比V2ray性能更好；
2. v2ray和trojan都能实现https流量伪装；
3. v2ray内核用go语言开发，trojan是c++实现；
4. v2ray名气大，使用的人多，客户端很好用；trojan关注和使用的人少，官方客户端简陋，生态完善度不高。

## 二、准备

- 国内可连接的国外VPS一台、域名一个。

## 三、Trojan搭建

#### 3.1 解析域名

首先，为了国内操作方便，我们可以将域名托管到阿里云，或者直接在阿里云购买一个域名也可以。只是解析IP地址工信部是不会管的。具体步骤如下：

- 访问阿里云官网：https://www.aliyun.com/，完成登录后点击右上角的控制台，然后按照下例图示访问域名控制面板。

![3.1-1](./img/3.1-1.png)

- 在弹出的页面中找到全部域名，其中就有已购买（或已托管）的域名，点击该域名操作部分的解析进入解析页面。

![3.1-2](./img/3.1-2.png)

- 点击添加记录。

![3.1-3](./img/3.1-3.png)

- 
- 
- 可以采用 `ping 域名` 的方式检测解析是否成功。

#### 3.2 配置BBR内核加速

- 执行一键脚本进行安装。

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

- 选择2安装 BBRplus版内核。

```bash
 TCP加速 一键安装管理脚本 [v1.3.2]
  -- 就是爱生活 | 94ish.me --

  0. 升级脚本
     ————————————内核管理————————————
  1. 安装 BBR/BBR魔改版内核
  2. 安装 BBRplus版内核
  3. 安装 Lotserver(锐速)内核
     ————————————加速管理————————————
  4. 使用BBR加速
  5. 使用BBR魔改版加速
  6. 使用暴力BBR魔改版加速(不支持部分系统)
  7. 使用BBRplus版加速
  8. 使用Lotserver(锐速)加速
     ————————————杂项管理————————————
  9. 卸载全部加速
  10. 系统配置优化
  11. 退出脚本
      ————————————————————————————————

 当前状态: 已安装 BBRplus 加速内核 , BBRplus启动成功

 请输入数字 [0-11]:2
```

- 选择7使用BBRplus版加速。

```bash
 TCP加速 一键安装管理脚本 [v1.3.2]
  -- 就是爱生活 | 94ish.me --

  0. 升级脚本
     ————————————内核管理————————————
  1. 安装 BBR/BBR魔改版内核
  2. 安装 BBRplus版内核
  3. 安装 Lotserver(锐速)内核
     ————————————加速管理————————————
  4. 使用BBR加速
  5. 使用BBR魔改版加速
  6. 使用暴力BBR魔改版加速(不支持部分系统)
  7. 使用BBRplus版加速
  8. 使用Lotserver(锐速)加速
     ————————————杂项管理————————————
  9. 卸载全部加速
  10. 系统配置优化
  11. 退出脚本
      ————————————————————————————————

 当前状态: 已安装 BBRplus 加速内核 , BBRplus启动成功

 请输入数字 [0-11]:2
```

#### 3.3 安装Trojan

- 在服务器上执行一键安装脚本

```shell
source <(curl -sL https://git.io/trojan-install)
```



