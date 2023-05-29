# “Linux 生物信息技术基础”总结报告 2

> 组：G04 <br/>次：2<br/>组长：高大可<br/>执笔：邓昆月<br/>参与人员：高大可、邓昆月、唐明川、吴航锐<br/>时间：2023 年 3 月 12 日，19:30-21:30。 <br/>地点：35 楼 B111

# <strong>主题</strong>

好用的安装指令

好用的子系统介绍

EMBOSS 的安装与用法

# 内容

## Terminal preview 的介绍（W11 自带）

了解基本用法，其可以将多种子系统整合在一起

## conda 常见指令及使用方法

`conda activate 激活环境`

`conda create -n new_env r-base=`<em>4.1.2</em>`r-esstial`

`conda install 安装一些软件包`

<em>其他资源链接：[https://mp.weixin.qq.com/s/vhSpEoIkYP5Hky0lnyGVvQ](https://mp.weixin.qq.com/s/vhSpEoIkYP5Hky0lnyGVvQ)</em>

## apt（advanced package tool）的用法

可使用 apt 命令来安装 emboss：`sudo apt install emboss`

<em>参考文献：[https://blog.csdn.net/m0_46278037/article/details/120232679](https://blog.csdn.net/m0_46278037/article/details/120232679)</em>

## wget 的使用

可使用 wget 源码安装一些软件包，或者在网址上下载数据

`wget 'link'`

## EMBOSS 的安装与使用

dottup、dotmatch 指令的讨论

## 使用 scp 从服务器下载或上传文件

<em>参考网址：[https://blog.csdn.net/zhaozhichenghpu/article/details/80975023](https://blog.csdn.net/zhaozhichenghpu/article/details/80975023) </em>

利用 scp 传输文件,实现从远程服务器下载文件或上传文件到服务器上,本地使用 unix([linux](https://so.csdn.net/so/search?q=linux&spm=1001.2101.3001.7020)/mac)命令行完成操作

### 从远程服务器下载文件到本地

`scp <用户名>@<ssh服务器地址>:<文件> <本地文件路径>`

### 下载文件夹到本机

`scp -r <用户名>@<ssh服务器地址>:<文件夹名> <本地路径>`

### 从本地上传到服务器上

`scp <本地文件名> <用户名>@<ssh服务器地址>:<上传保存路径>`

`scp  -r <本地文件夹名> <用户名>@<ssh服务器地址>:<上传保存路径>`

# 问题

1. EMBOSS 对于当今科研生活中的应用情况，比起其他的软件包有没有独特的优势？
2. 自己安装 EMBOSS 后，用 EMBOSS 指令是用的服务器安装的，还是自己安装的？
3. 有无生物信息实践项目，能够将目前学的知识学以致用？
