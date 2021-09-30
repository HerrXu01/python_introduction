# 第五章 if语句

## 5.1 一个简单示例
有一个汽车列表，我们想要打印出来。
对于bmw，需要全大写，其他的只要首字母大写即可。
```python
cars = ['audi', 'bmw', 'porsche', 'benz']

for car in cars:
    if car == 'bmw':
        print(car.upper())
    else:
        print(car.title())
```  
输出结果：
Audi
BMW
Porsche
Benz  

## 5.2 条件测试
每条if语句的核心都是一个值为True或False的表达式，这种表达式被称为条件测试。
如果条件测试的值为True，Python就会执行if语句后面的代码；
如果为False，if语句后面的代码被忽略。  

### 5.2.1 检查是否相等
一个等号=是赋值，
两个等号==是比较。
==两边的值若相等，返回True，不等则返回False。

### 5.2.2 大小写
Python检查是否相等时会区分大小写。
如果不想区分大小写，可以将变量转为小写再比较。  

### 5.2.3 检查是否不相等
用 != 符号，如果两边的值不相等，则返回True，
若相等，则返回False。  

### 5.2.4 比较数字
是否相等 ==  
是否不等 !=  
大于 >
小于 <
大于等于 >=  
小于等于 <=  

### 5.2.5 检查多个条件
1. 使用and  
每个测试都为True才能返回True，有一个为False就返回False。
2. 使用or  
只要一个测试为True就返回True，全都为False时才返回False。  

### 5.2.6 检查特定值是否包含在列表中
用关键字 in 来检查某特定值是否在列表中。  
```python
numbers = list(range(1,9))
print(9 in numbers)
print(8 in numbers)
```  
输出结果为：
False
True  

### 5.2.7 检查特定值是否不包含在列表中
用关键字 not in  
```python
numbers = list(range(1,9))
print(9 not in numbers)
print(8 not in numbers)
```  
输出结果为：
True
False  

## 5.3 if语句

### 5.3.1 简单的if语句
最简单的if语句只有一个测试，一个操作。
```python
age = 19
if age >= 18:
    print("You are old enough to vote!")
    print("Have you register to vote yet?")
```  
如果条件测试为True，则执行所有紧跟在if语句后面缩进的代码块，
若结果为False，Python会忽略后面缩进的代码块。  

### 5.3.2 if-else 语句
条件测试通过时执行一个操作，没通过时执行另一个操作。
```python
age = 17
if age >= 18:
    print("You are old enough to vote!")
    print("Have you register to vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 18.")
```  
输出结果为：
Sorry, you are too young to vote.
Please register to vote as soon as you turn 18.  
条件测试通过的话，执行紧跟在if语句后面缩进的代码块，
没通过的话，执行紧跟在else语句后面缩进的代码块。  
这种情况是只有两种情形：符合条件或者不符合条件。  

### 5.3.3 if-elif-else结构
需要检查超过两种情形时用此结构。
例如：游乐场根据年龄收费：
4岁以下免费，
4-18岁收费5元，
18岁（含）以上收费10元。
```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10

print("Your cost is " + str(price) + ".")
```  
Python只会执行其中的一个代码块。
Python首先依次检查每个条件测试，直到遇到通过的条件测试，然后执行紧跟在它后面缩进的代码块，然后跳过余下的测试。  

### 5.3.4 使用多个elif代码块
elif代码块可以不止一个。
比如在上述游乐园门票的例子中，再加一项>=65岁可以打折，门票5元。
```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
else:
    price = 5

print("Your cost is " + str(price) + ".")
```  

### 5.3.5 省略else代码块
并不强制一定要有else代码块。
如果有else的话，若之前的条件测试均不通过的话，就直接执行else代码块的命令；
如果没有else的话，若if和所有的elif条件测试均不通过的话，则不执行任何命令。  

### 5.3.6 测试多个条件
if-elif-else结构只会执行一个代码块，要想执行多个代码块的话，需要使用一系列独立的if语句。  

## 5.4 使用if语句处理列表

### 5.4.1 检查特殊元素
开头5.1 一个简单示例 就是检查特殊元素bmw。

### 5.4.2 确定列表不是空的
在程序中，列表有可能是空的，需要确认。
if后面直接加列表名称，若列表非空，返回True，若为空，返回False。
```python
numbers = []

if numbers:
    for number in numbers:
        print(number)
else:
    print("This is an empty list.")
```  
输出结果为：
This is an empty list.  

### 5.4.3 使用多个列表
可能会需要使用到多个列表。
比如我有一些数字的卡片，别人需要一些数字的卡片。
```python
my_numbers = [6, 7, 8, 9]
need_numbers = [2, 4, 6, 8]

for number in need_numbers:
    if number in my_numbers:
        print("I have the number: " + str(number) + ".")
    else:
        print("I don't have the number: " + str(number) + ".")
```  
运行结果为：
I don't have the number: 2.
I don't have the number: 4.
I have the number: 6.
I have the number: 8.  

## 5.5 设置if语句的格式
最好在运算符的两端各添加一个空格。