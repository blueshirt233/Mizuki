---
title: linux系统学习（后续慢慢补充）
published: 2026-05-19
pinned: false
description: linux系统学习
tags:
  - linux
draft: false
category: 教程
---
# Linux快速入门
## 1.Linux目录结构
linux目录结构，核心思想，万物皆文件，一切从“/”开始
![3c0080b6-df63-44b3-b188-e224455a32.png](https://tu.2644536256.date/file/blog/wengzhang/1779195961763_3c0080b6-df63-44b3-b188-e224455a32.png)
## 2.Linux命令入门
### ls命令
ls：以平铺的形式，列出当前工作目录下的内容
ls 【-a  -l  -h】
-a：列出全部文件包括隐藏文件
-l：以列表的形式，列出当前工作目录下的内容，并展示更多细节
-h：文件大小显示单位
通常使用为ll，ll -a
### cd命令
cd 【linux路径】：切换到指定文件夹下
cd ~  |  cd /  |  cd 【相对路径】  |  cd 【绝对路径】
### pwd命令
pwd：查看当前工作目录
### mkdir命令
mkdir 【-p】【linux路径】：创建文件夹，【-p】自动创建不存在的父文件夹，适用于多层级目录。
### touch命令
touch【linux路径】创建对应路径下的文件
### cat命令
cat【linux路径】：查看文件内容
### more命令
more【linux路径】：查看文件内容，支持翻页操作，空格键翻页
### cp命令
cp【-r】【源文件路径】【目标文件路径】：复制文件，【-r】复制文件夹表示递归
### mv命令
mv【源文件路径】【目标文件路径】：移动文件或文件夹，两个路径相同效果为改名
### rm命令
rm 【-r】【-f】【文件或文件夹路径】：删除文件或文件夹路径，【-r】删除文件夹，【-f】强制删除，【文件或文件夹路径】可以多个用空格隔开
### which命令
which【命令】：查找命令的程序文件在哪里
### find命令
find 【起始路径（从哪个文件夹下开始找）】 -name “被查找的文件名” ：查找文件
\*：表示通配符(包含空格)
test*：表示匹配任意以test开头的文件
*test：：表示匹配任意以test结尾的文件
\*test*：表示匹配任意包含test的文件
find 【起始路径（从哪个文件夹下开始找）】-size 【+或-{单位k、M、G}】：查找对应文件夹下对应大小的文件
fing /【-type f】 -size +50M -size -100M：查找大于50M小于100M的文件【-type f】：仅匹配普通文件（排除目录、设备文件等）。
### wc命令
wc【-c】【-m】【-l】【文件路径】统计文件的行数，单词数量
-c：统计bytes数量 -m：统计字符数量 -l：统计行数 -w：统计单词数量
### echo命令
echo：打印命令  echo `pwd` ：被反引号包围的作为命令执行结果打印出来  echo >和 echo >>分别为覆盖和追加。
### tail命令
tail【-f】【-num】【文件路径】：持续跟踪文件倒数【num】行数的内容，其中【-f】为持续跟踪
### vi编辑器
vi编辑器使用方法：
编辑模式：【i】当前光标位置开始编辑，编辑结束，【esc】后【：wq】保存退出，【：q！】为强制退出，【q】仅退出，【w】仅保存，【set nu】显示行数【set paste】设置粘贴模式
【a】当前光标位置之后开始编辑
【I】当前行的开头开始编辑
【A】当前行的结尾开始编辑
【o】当前光标的下一行开始编辑
【O】当前光标的上一行开始编辑
命令模式：【dd】删除光标所在行的内容
【ndd】n是数字，删除当前光标以下n行的内容
【yy】复制当前行的内容
【nyy】n是数字，复制当前光标以下n行的内容
【p】粘贴复制内容
【u】撤销修改
【ctrl+r】反向撤销
【gg】跳到行首
【G】跳到行尾
【dG】从当前行开始向下全部删除
【dgg】从当前行开始向上全部删除
【dS】从当前光标开始删除到本行结尾
【d0】从光标开始删除到本行开头
### su命令
su 【用户名】切换用户
给普通用户开放sudo命令：切换到root用户下执行visudo。会自动进入编辑 /etc/sudiers 文件， 在文件最后添加【用户】 ALL=(ALL)    NOPASSWD:ALL之后保存，切换回用户使用sudo无需密码
### 用户组
groupadd 【用户组名】创建用户组
groupdel 【用户组名】删除用户组名
### 用户
useradd 【-g，-d】【用户名】：创建用户【-g】指定用户的组（需要已存在的组），不指定，会创建同名组用户自动加入，【-d】指定用户home目录的路径，不指定就默认
userdel 【-r】【用户名】：删除用户【-r】删除用户home目录
id 【用户名】：查看用户所在组
usermod -aG 【用户组】【用户名】：将指定用户加入指定用户组
getent passwd：查看当前系统中有哪些用户
getent group：查看当前系统中有哪些用户组
### 文件控制信息
![de7627e6e84d4ef5b893d4002a01423f.png](https://tu.2644536256.date/file/blog/wengzhang/1779284995806_de7627e6e84d4ef5b893d4002a01423f.png)

### chmod
chmod【-r】 【权限】【文件或文件夹】：修改文件文件夹的权限信息，【-r】对文件夹内全部内容应用权限
### chown
chown 【-r】【用户】：【用户组】【文件或文件夹】：修改文件、文件夹所属用户和用户组，【-r】对文件夹内全部内容应用权限
### 快捷案件
【ctrl+c】：强制停止
【ctrl+d】：强制退出
【history】：搜索历史命令
【！q】：搜索以（q）开头的最后一次执行的历史命令
【ctrl+r】：搜索命令，搜索最后一次只想的相关命令
【ctrl+a】：跳到命令开头
【ctrl+e】：跳到命令结尾
【ctrl+键盘左键】：向左跳一个单词
【ctrl+键盘右键】：向右挑一个单词
### systemctl
systemctl 【参数】【服务名】
参数：
start、restart、disable、enable、stop
### ln软链接
ln -s 【被链接的文件或文件夹】【目的位置】：-s：创建软链接
### date命令
date【-d】【+格式化字符串】：【-d】按照给定的格式化字符串来显示日期，一般用于日期计算
date -d “+1 day”  ：结果为明天，加一天
date -d “-1 day”：结果为昨天，减一天
格式化字符串：
%Y    年
%y    年份后两位数字
%m    月份
%d     日
%H    小时
%M    分钟
%S    秒
%s    从1970-01-01 00：00：00 UTC 到现在的秒数
ntp服务需要下载，dnf install ntp 然后启动服务start和enable
ntpdate -u 时间服务器网址：手动跟时间服务器校准时间
修改时区：
rm -f /etc/localtime 删除本地时间
sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 用软链接把上海市区重新给本地时区
### 修改ip和主机名
hostname 主机名 ： 修改主机名
vi /etc/NetworkManager/system-connections/网卡名 ：修改ip改为固定ip，其中auto改为manual，ipaddress：x.x.x.x/24/x.x.x.x,dns=x.x.x.x
### 下载
wget 【-b】 url：文件下载器 【-b】为后台下载，同时写入日志 
curl 【-O】url ：发起网络请求，【-O】用于下载
### 端口
nmap需要安装，nmap+ip扫描ip下有几个端口暴露
netstat可能需要安装 dnf install net-tools 
netstat -anp | gerp 6000：查看本机6000端口占用情况
### 进程
ps 【-e -f】：查看系统进程【-e】显示出全部进程【-f】 完全格式化的形式展示信息，一般是ps -ef来用
kill 【-9】进程ID：关闭进程【-9】为强制关闭
### 环境变量
使用evn命令来查看当前环境变量，这个具体再shell中详细描述
### 解压压缩
tar 【-c -v- x- f- z- C】解压文件
-c；创建压缩文件
-v：显示压缩解压过程
-x：解压模式
-f：要创建或解压的文件，这个要在多选中排最后
-z：gzip模式，不适用就是tarball格式
-C：解压到哪里，用于解压
zip 【-r】文件：zip压缩文件【-r】：被压缩的文件包含文件夹的时候使用
unzip 【-d】 文件：解压zip文件【-d】：指定解压要去的位置
# linux运维命令
## 基础运维命令
### top命令
![1470684-20180918100416703-87744477.png](https://tu.2644536256.date/file/blog/wengzhang/1779370619947_1470684-20180918100416703-87744477.png)