---
layout:     post
title:      React Native iOS 开发踩坑
subtitle:   尝试通过 React Native 进行 iOS Android 双平台开发
date:       2019-10-22
author:     KinsoZHENG
header-img: img/post_background.jpg
catalog: true
tags:
    - React Native
    - Restaurant Order System
---
>Today is 2019-10-22. <br>
 Trying to develop the Restaurant Order System by React Native on iOS and 
  Android. <br>
 



# 前言

近期, 遇到了一个针对单个餐厅的餐厅系统开发的需求，对于其具体所需要开发的功能仍处于待商讨阶段。考虑到或许需要在
 iOS 和 Android 系统上的运行，决定尝试使用 React Native 进行开发，以满足双平台运行的需要。<br>
 
 
此篇 Blog 以及其后续，将会逐一记录 React Native 开发环境的配置，遇到的Bug 问题以及解决方案。包括开发工程中，
对App开发的思路，代码展示。<br>

当前开发环境:

- MacBook Pro 2017
- OS: MacOS Mojave (Version 10.14.6)


# 正文

**环境配置参考于[**React Native**](https://reactnative.cn/docs/getting-started.html)**

## 安装依赖

```shell
brew install node
brew install watchman
```

## Yarn、React Native 的命令行工具（react-native-cli）
```shell
npm install -g yarn react-native-cli
```

在 npm 安装的工程中， 我遇到了如下问题。

```npm
npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules
npm ERR! path /usr/local/lib/node_modules
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access
npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
npm ERR!  { [Error: EACCES: permission denied, access '/usr/local/lib/node_modules']
npm ERR!   stack:
npm ERR!    'Error: EACCES: permission denied, access \'/usr/local/lib/node_modules\'',
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/local/lib/node_modules' }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator (though this is not recommended).

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/zhengqingshuo/.npm/_logs/2019-10-22T20_35_54_864Z-debug.log
```

此处根据**WARN** 和 **ERR** 的Feedback来看是缺少相关的写入权限

解决办法<br>
使用sudo 提升相关权限。在安装命令前加上sudo,输入用户的登陆密码, 并对npm 进行升级。

```shell
# 更新npm
sudo npm i -g npm

```

再次进行
```shell
sudo npm install -g yarn react-native-cli
```
安装成功
```shell
zhengqihuodeMBP:~ zhengqingshuo$ sudo npm install -g yarn react-native-cli
Password:
/usr/local/bin/react-native -> /usr/local/lib/node_modules/react-native-cli/index.js
/usr/local/bin/yarn -> /usr/local/lib/node_modules/yarn/bin/yarn.js
/usr/local/bin/yarnpkg -> /usr/local/lib/node_modules/yarn/bin/yarn.js
+ react-native-cli@2.0.1
+ yarn@1.19.1
updated 2 packages in 12.047s
```

在运行GitHub上往年开源项目时，遇到了版本问题造成 **BUILD FAIL**<br>
解决方案：
在项目下的："node_modules/react-native/local-cli/runIOS/findMatchingSimulator.js" 文件中修改<br>
分别将第30行和第36行修改为
```js
if (!version.includes("iOS"))
```
```js
if (simulator.availability !== '(available)' && simulator.isAvailable !== true) 
```



# *** Continue...***


