---
title: nvm
date: 2020-02-16 11:11:08
tags: 环境
---
最近新换了Mac，公司的项目需要多个版本的node，所以需要安装一个node版本管理，之前的Thinkpad一切顺利，到了Mac居然配置不上环境变量，每次启动终端都需要运行一下环境变量，这怎么能忍，经过了2个小时的安装，配置。
终于解决了这个问题，问题解决之后回顾觉得自己就是个憨批，于是准备把这个问题记录下来。

### 什么是Nvm 
nvm是node版本管理工具
为了解决node各种版本存在不兼容现象
让你可以在一台电脑上安装不同版本的node工具。
### 安装Nvm
安装方式有两种
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```
这里推荐第一种安装方式
github地址：https://github.com/nvm-sh/nvm

运行结果有如下提示，说明安装成功：
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
记得要将上面的代码拷贝下来。
由于网络原因，经常会下载不下来，多试几次即可。
### 配置环境变量
安装nvm成功后，需要配置环境变量，否则每次打开终端输入nvm都会提示command not found nvm。
环境变量需要保存在以下某一个文件内(~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).
也就是``` exprot NVM_DIR ```上面那一段,
```
#此时我们进入到.nvm文件内，通常是隐藏文件夹，通过命令 Command + Shift + . 显示

#一 打开~/.bash_profile文件，把刚刚复制的拷贝进来，然后关闭文件
open ~/.bash_profile

#二 如果提示未找到该文件，需要创建
touch ~/.bash_profile

#三 重新执行步骤一，然后运行环境变量
source ~/.bash_profile

#关闭终端重新打开输入nvm就一切正常了
```

如果上述操作之后依然提示command not found nvm，那么创建 ```.zshrc```文件，我就是一直折腾 ```.bash_profile``` 很久，结果配置 ```.zshrc``` 后一切就正常了,还是要学会变通啊。

## nvm常用命令

```
# nvm常用命令
nvm install stable # 安装最新版
nvm install --lts # 安装长期支持版
nvm ls # 列出所有已安装的版本
nvm use <version> # 使用node版本
nvm current # 当前版本
nvm # 查看命令
nvm uninstall <version> # 卸载node版本
```