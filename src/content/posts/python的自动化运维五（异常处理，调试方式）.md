---
title: python的自动化运维五（异常处理）
published: 2026-06-16
pinned: false
description: python的自动化运维五（异常处理）
tags:
  - python
draft: false
category: 教程
---
# try...except...else...finall
```python
try:  
    i=input("number:")  
    r=10/i  
    print(r)  
except ZeroDivisionError as e:  
    print(e)  
except TypeError as e:  
    print(e)  
except BaseException as e:  
    print(e)  
else:  
    print("程序没有异常")  
finally:  
    print("程序结束")
```
以上是异常处理的结构体
基础的类型或常用的就是
```python
try:  
    i=input("number:")  
    r=10/i  
    print(r)  
except ZeroDivisionError as e:  
    print(e)  
except TypeError as e:  
    print(e)  
except BaseException as e:  
    print(e)  
```
这种类型try区域写代码或者是main的主题代码，except写异常类型，分为上部分呢写细分，下部分写总，最后没有异常可以写一个else来输出没有异常，提示程序结束可以写一个finally，else和finally可写可不写，看使用情况而定
最终可以写成
```python
def n():  
    i=input("number:")  
    return i  
  
def pro():  
    r=10/n()  
    return r  
  
def func():  
    print(pro())  
  
def main():  
    print(func())  
  
try:  
    if __name__ == "__main__":  
        main()  
except ZeroDivisionError as e:  
    print(e)  
except TypeError as e:  
    print(e)  
except BaseException as e:  
    print(e)  
else:  
    print("best")  
finally:  
    print("exit")
```
只要最后执行的程序拦截到异常就行，不需要内部程序写具体内容