---
title: python的自动化运维（二、函数）
published: 2026-06-03
pinned: false
description: python的自动化运维（二、函数）
tags:
  - python
draft: false
category: 教程
---
# python函数
主要是为了代码的复用，让代码更加简洁
## 函数调用
int():转换为整数
input():添加输入信息返回字符串型
abs():绝对值
max():寻找最大值
min();寻找最小值
float():字符串和整型转换为浮点数
str():转换成字符串
bool():0、空、None都是false，其他都是true
hex():整数转换十六进制
函数名其实是指向一个函数对象的引用，可以把函数赋值给变量相当于起别名
## 普通函数
def 函数名（参数）：
	函数体
	return 返回值（可有可无）
# 空函数
def 函数名（参数）：
	pass
## 函数参数
函数定义的时候可以在（）里面写参数称为**形参**，使用函数传递进去的参数叫**实参**几个形参对应几个实参
```python
def calcSum(beg,end):
	sum = 0
	for i in range(beg,end+1): #range左开右闭,现在这个=[beg，end]
		sum+=i
	print(sum)
calcSum(1,100)
calcSum(300,400)
calcSum(1,1000)
```
## 默认参数

```python
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
这里n=2，就是n被设置成默认参数2，此时
```plain
>>> power(5)
25
```
只需要输入5就可以，n为默认值，但是n如果不是2的时候就需要重写参数
```plain
>>> power(5, 3)
125
```
重新给n赋值

## 可变参数
```python
def num(*number):  
    s=0  
    for i in number:  
        s=s+i  
    return s  
  
  
print(num(1,2,3,4,5))
```
number前面增加\*号就是可以参数就变，下面调用这个函数的时候填入了五个参数可以正常运行

## 关键字参数
```python
def kwages(**other):  
    name = other.get("name")  
    age = other.get("age")  
    address = other.get("address","ningbo")  
    print(name,age,address)  
  
  
kwages(name="clj", age=12)
```
其实关键字参数本质是可以传入键值对参数，在传入参数后自动组装成一个字典，可以传入多个字典，当然也可以先创建一个字典然后把这个字典全部导入

```python
ex = {"name":"qjl","age":13,"address":"anhui"}  
  
def add(**ex):  
    name = ex.get("name")  
    age = ex.get("age")  
    address = ex.get("address","ningbo")  
    print(name,age,address)  
  
add(**ex)
```

## 多个返回值
```python
def kwages(**other):  
    name = other.get("name")  
    age = other.get("age")  
    address = other.get("address","ningbo")  
    # print(name,age,address)  
    return name,age,address  
  
  
# print(kwages(name="clj", age=12))  
print(kwages(name="clj",age=12))
```
返回值需要调用者来打印
同时需要屏蔽一个参数可以使用_来屏蔽
```python
def kwages(**other):  
    name = other.get("name")  
    age = other.get("age")  
    address = other.get("address","ningbo")  
    # print(name,age,address)  
    return name,age,address  
  
  
# print(kwages(name="clj", age=12))  
a,b,c=kwages(name="clj",age=12)  
print(a,b,c)
```
改为
```python
def kwages(**other):  
    name = other.get("name")  
    age = other.get("age")  
    address = other.get("address","ningbo")  
    # print(name,age,address)  
    return name,age,address  
  
  
# print(kwages(name="clj", age=12))  
_,b,c=kwages(name="clj",age=12)  
print(b,c)
```
这样代码不会报错同时可以获取到后面两个值

# 参数拓展
## 引用函数参数
```python
def greet():  
    print("hello")  
  
def call_greet(func):  
    func()  
  
  
call_greet(greet)
```
这里的func()其实是因为greet函数作为call_greet的实参引入，把整个函数赋值给func所以才能写func(),如果greet不是函数或者方法之类的，就不能这么写，认真写return或者print

```python
def add(x,y):  
    return x+y  
def mul(x,y):  
    return x*y  
  
func_list=[add,mul]  
print(func_list[0](1, 2))  
print(func_list[1](3, 4))
```

也可以把函数作为列表中的数据引入，然后读取列表数据输入参数也可以执行代码