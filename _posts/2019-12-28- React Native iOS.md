---
layout:     post
title:      Pytorch FCN 开发
subtitle:   尝试通过 Pytorch 进行 FCN
date:       2019-12-28
author:     KinsoZHENG
header-img: img/post_background.jpg
catalog: true
tags:
    - FCN
    - Pytorch
---
>Today is 2019-10-22. <br>
 Trying to develop FCN pytorch.<br>
 



# 前言




# 正文


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
在项目下的："node_modules/react-native/local-cli/runIOS/findMatchingSimulator.js"<br>
分别将第30行和第36行修改为
```js
if (!version.includes("iOS"))
```
```js
if (simulator.availability !== '(available)' && simulator.isAvailable !== true) 
```



# *** Continue...***


