---
title: 蓝牙Wi-Fi助手
date: 2023-11-29 20:59:22
tags:
categories: APP & 小程序
---

# 蓝牙Wi-Fi助手

## Android APP如何和硬件进行通信？

开发板搭配蓝牙模块或者WI-FI模块。

WI-FI模块常用型号：ESP8266
蓝牙模块常用型号：HC08


**esp8266的三种工作模式：**
1. station（客户端模式）：类似于手机，小爱音响等设备（client）
2. AP（接入点模式）：类似于路由器(server)，可以让其他设备访问
3. station+AP（客户端+接入点模式）


**使用手机APP连接WI-FI模块控制单片机硬件的逻辑：**
将WiFi模块设置成了AP模式下的TCP Server模式，就相当于一个路由器，并配置好WiFi模块的IP地址和端口号，就可以通过手机APP连接这个WiFi模块，并相互传输数据，进而就可以控制单片机所连接的硬件设备，实现简易物联网的功能


**使用手机APP连接蓝牙模块控制单片机硬件的逻辑：**
![蓝牙连接逻辑图](https://img-blog.csdnimg.cn/45db4cbceee945de801785b487aeae66.png)


## 逻辑设计
### 主界面
可选**WI-FI**模式和**蓝牙**模式

WI-FI模式下端口号和IP地址输入的审核逻辑：

1. 若端口号和IP地址输入为空，则提示对应异常
2. 输入端口号和IP地址后，开始进行连接，连接成功直接跳转到操作界面；连接失败则停留在主界面，并报错

蓝牙模式下的操作逻辑：
搜索按钮直接显示附近的蓝牙信号源，点击后尝试连接，连接成功直接跳转到操作界面；连接失败则停留在主界面，并报错

### 操作界面
1. 显示当前连接的IP地址/蓝牙名称
2. 提供两个输入框，一个可以直接输入AT指令，一个可以选择单片机操作模型。
3. 返回值显示框

## Android APP WI-FI部分实现

引用：
[AndroidWIFI使用简述](https://blog.csdn.net/qq_38436214/article/details/128786627?ops_request_misc=&request_id=&biz_id=102&utm_term=Android%20APP%E8%BF%9E%E6%8E%A5WI-FI&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-128786627.142^v96^pc_search_result_base5&spm=1018.2226.3001.4187) ----（xml配置比较详细）
[APP和ESP8266进行联网传输](https://blog.csdn.net/qq_45488746/article/details/124730926?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170127665016800227444165%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=170127665016800227444165&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-124730926-null-null.142^v96^pc_search_result_base5&utm_term=Android%20APP%E5%90%91esp8266%E5%8F%91%E9%80%81%E6%95%B0%E6%8D%AE&spm=1018.2226.3001.4187)--(xml只配置了网络)
**配置项目的静态权限**
在 **AndroidManifest.xml** 增加代码
```
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

在Android13大版本更新后，Google 将 Wi-Fi 扫描与位置相关内容分离， Android 13 为管理设备与周围 Wi-Fi 热点连接的应用添加 NEARBY_WIFI_DEVICES 运行时权限 (属于NEARBY_DEVICES权限组)，从而在不需要 ACCESS_FINE_LOCATION 权限的情况下，也可以让应用访问附近的 Wi-Fi 设备。

但为了考虑Android13版本以下的机型，所以项目中仍然需要配置定位权限。
```
        <!--Android 6 ~ 12 使用定位权限-->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"
        tools:ignore="CoarseFineLocation" />

    <!--Android 13及以上使用权限-->
    <uses-permission
        android:name="android.permission.NEARBY_WIFI_DEVICES"
        android:usesPermissionFlags="neverForLocation"
        tools:targetApi="Tiramisu" />

```

## Android Studio安装(mac)

[参考文章](https://blog.csdn.net/ChenYu_2511/article/details/129316950?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170127730316800215062578%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=170127730316800215062578&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-129316950-null-null.142^v96^pc_search_result_base5&utm_term=mac%20M2%E5%AE%89%E8%A3%85Android%20Studio&spm=1018.2226.3001.4187)

[参考文章2](https://blog.csdn.net/qq_38091632/article/details/132174988?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170127730316800215062578%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=170127730316800215062578&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-132174988-null-null.142^v96^pc_search_result_base5&utm_term=mac%20M2%E5%AE%89%E8%A3%85Android%20Studio&spm=1018.2226.3001.4187)



