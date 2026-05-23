---
title: shell基础运用
published: 2026-05-23
pinned: false
description: shell基础运用
tags:
  - shell
draft: false
category: 教程
---
# shell的基础运用
linux基础后要会使用shell脚本来快速运维
## shell命令与注释
### shell的开头
文件开头写【#/bin/bash】表示程序默认使用bash解释器执行命令，使用时先【chmod +x 文件名】给文件执行权限，然后【./文件名】执行脚本运行。默认文件名为【文件名.sh】以标识这是一个shell文件。
### shell注释
```bash
#  单行注释
```


```bash
: <<'COMMENT'  
这是多行注释，里面的内容全部忽略
COMMENT
```
## echo命令
echo 是 Shell 脚本中非常常用的命令，它用于向终端输出文本、变量的值，或者将输出内容重定向到文件。了解 echo 的各种用法，可以帮助你更好地调试脚本、展示结果或保存数据。
### 基本语法
```bash
echo [选项] [字符串]
```
选项：用于修改 echo 命令的行为（如是否输出换行符、是否支持转义字符等）。
字符串：是你想要输出的文本、变量等内容。
-n：不输出换行符
默认情况下，echo 会输出换行符，如果你不想要换行符，可以使用 -n 选项。
代码
```bash
echo -n "Hello, World!"
echo "This is on the same line."
```
输出
```bash
Hello, World!This is on the same line.
```

-e：启用转义字符
默认情况下，echo 不会解析一些特殊的转义字符，如 \n、\t 等。使用 -e 选项后，echo 会解析这些转义字符。
```bash
echo -e "Hello\nWorld"
echo -e "Name\tAge"
```
输出
```bash
Hello
World
Name    Age
```
-E：禁用转义字符
如果你不想让 echo 解析转义字符，可以使用 -E 选项。
```bash
echo -E "Hello\nWorld"
```
输出
```bash
Hello\nWorld
```
### 输出变量的值
echo 很常用于输出变量的值：
```bash
name="Alice"
echo "Hello, $name!"
```
输出
```bash
Hello, Alice!
```
你也可以使用大括号来明确变量范围，特别是在变量名后面跟着其他字符时：
```bash
name="Alice"
echo "Hello, ${name}123!"
```
输出
```bash
Hello, Alice123!
```
### 输出文本到文件
你还可以将 echo 的输出重定向到文件中：
```bash
echo "This is a test." > test.txt
```
使用 > 会将内容写入文件并覆盖原有内容。
使用 >> 会将内容追加到文件末尾。
```bash
echo "This is another test." >> test.txt
```
### 输出文本到文件
在 Shell 脚本中，echo 常常用于输出调试信息或者展示用户输入的结果：
```bash
#!/bin/bash
echo "Please enter your name:"
read name
echo "Hello, $name!"
```
运行后，脚本会提示用户输入名字并输出问候语：
```bash
Please enter your name:
Alice
Hello, Alice!
```
### 总结


|   用法   |           示例            |    说明     |
| :----: | :---------------------: | :-------: |
|  输出文本  |   echo "Hello, World"   |  输出指定的文本  |
| 不换行输出  |     echo -n "Hello"     |    不换行    |
| 启用转义字符 | echo -e "Hello\nWorld"  |  启用转义字符   |
| 输出变量值  |   echo "Hello, $name"   |  输出变量的值   |
| 输出到文件  | echo "Text" > file.txt  | 输出内容并覆盖文件 |
| 追加到文件  | echo "Text" >> file.txt | 追加内容到文件末尾 |
## Shell 变量类型
### 系统环境变量
![515665904bc74d66b08e6f44963b383d.png](https://tu.2644536256.date/file/blog/wengzhang/1779521743826_515665904bc74d66b08e6f44963b383d.png)

这些变量由系统定义，用于控制 Shell 的运行环境。常见的系统环境变量包括：

|               变量名                | 含义说明 |
| :------------------------------: | :--: |
|         PATH	|可执行文件的搜索路径|
|         HOME	|当前用户的主目录路径|
| SHELL	|使用的 Shell 类型（如 /bin/bash)|
|           USER	|当前用户名|             
|           PWD	|当前工作目录|
|          LANG	|语言与地区设置|     

示例：
```bash
echo $HOME
echo $USER
echo $PATH
```
![f29a0818707e4adeab377c820c1288d9.png](https://tu.2644536256.date/file/blog/wengzhang/1779521971360_f29a0818707e4adeab377c820c1288d9.png)
设置环境变量：
```
export VAR_NAME=value   # 临时设置
```
若想永久生效，可写入 ~/.bashrc 或 ~/.profile 等配置文件。
### 自定义变量
	变量定义规则
       1.变量名称可以有字母,数字和下划线组成,但是不能以数字开头
       ⒉.等号两侧不能有空格
       3.在bash环境中,变量的默认类型都是字符串 类型,无法直接进行数
       4.变量的值如果有空格,必须使用双引号括起来
       5.不能使用Shell的关键字作为变量名称

```bash
name="Tom"
age=20
```
使用变量：
```bash
echo "My name is $name, I am $age years old."
```
注意事项：
=两边不能有空格。
变量名区分大小写。

![6b2b41ecc41b40c9b906471647217863.png](https://tu.2644536256.date/file/blog/wengzhang/1779522127219_6b2b41ecc41b40c9b906471647217863.png)

### 局部变量（函数中）使用 local 关键字：
```bash
myfunc() {
  local temp="hello"
  echo $temp
}
```


### declare 的基本用法
declare：是 Bash 中的一个内建命令，主要用于声明变量并设置其属性，相比于普通的赋值，它可以精细控制变量的类型和行为
```bash
declare [选项] 变量名=值
```
#### 常用选项
|选项|	说明|
| :------------------------------: | :--: |
|-r	|只读变量（readonly）|
|-i	|整数变量，只能执行数学运算|
|-a	|数组变量|
|-A	|关联数组变量（键值对）|
|-x	|导出为环境变量（类似 export）|
|-f	|显示已定义的函数|
|-p	|显示变量定义信息|

#### 示例详解
 声明只读变量
```
 declare -r pi=3.14
pi=3.14159   # 报错：只读变量不能修改
```
![745aa0863980496b9b901bb34937860d.png](https://tu.2644536256.date/file/blog/wengzhang/1779522397037_745aa0863980496b9b901bb34937860d.png)

声明整数变量并进行计算
```
declare -i num=5
num=num+3
echo $num  # 输出：8
```
![a5b1f7b9c7304ee0b6a951b853d89736.png](https://tu.2644536256.date/file/blog/wengzhang/1779522415127_a5b1f7b9c7304ee0b6a951b853d89736.png)

 声明数组变量
```
declare -a fruits=("apple" "banana" "cherry")
echo ${fruits[1]}  # banana
```
![a293496ae8544a18a199dcd25b9d21ba.png](https://tu.2644536256.date/file/blog/wengzhang/1779522441927_a293496ae8544a18a199dcd25b9d21ba.png)

 声明关联数组（Bash 4+）
```
declare -A info
info[name]="Tom"
info[age]=22
echo ${info[name]}  # Tom
```
![90ac0d919afd42189931c4903a77f537.png](https://tu.2644536256.date/file/blog/wengzhang/1779522450979_90ac0d919afd42189931c4903a77f537.png)

查看变量声明信息
```
declare -p fruits
declare -p info
```
![0071d5b0426446588e925acc7d685c7f.png](https://tu.2644536256.date/file/blog/wengzhang/1779522466100_0071d5b0426446588e925acc7d685c7f.png)

将变量声明为环境变量（类似 export）
```
declare -x user="Alice"
```

declare 与 local 的关系
在函数内部，如果你想限制变量作用域为函数内，使用：
```
local var="inside"
```
或者结合 declare：
```
local -i count=0
```
### 小结
|命令|	说明|
| :------------------------------: | :--: |
|declare	|控制变量属性（类型、安全性）|
|declare -i	|整数运算变量|
|declare -r	|设置只读变量|
|declare -a/-A	|声明数组/关联数组|
|declare -x	|类似 export，用于设置环境变量|