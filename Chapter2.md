# 第二章 变量和简单数据类型

## 2.2 变量

```python
#变量赋值，可以随时修改
message = "Hello Python world!"
print(message)
```  

### 2.2.1 变量的命名和使用

* 只能包含字母、数字和下划线  
* 不能包含空格，可用下划线分隔  
* 不要用关键字和函数名  
* 简短且具有描述性  
* 慎用小写字母l和大写字母O，易混淆  

## 2.3 字符串

用引号括起来的都是字符串，可以单引号，也可以双引号。  
但不要混着用。  
单（双）引号开头，单（双）引号结尾，  
单引号中间可以插入双引号。
不可以单引号开头，双引号结尾。  
```python
'This is a string.'
"This is also a string."
```

### 2.3.1 使用方法修改字符串的大小写

```python
name = 'sheldon cooper'

#首字母大写
print(name.title())

#全大写
print(name.upper())

#全小写
print(name.lower())
```  

### 2.3.2 合并（拼接）字符串

用加号（+）来拼接字符串。  
```python
first_name = 'sheldon'
last_name = 'cooper'
full_name = first_name + ' ' + last_name
print("Hello, " + full_name.title() + "!")
```  

### 2.3.3 使用制表符或换行符来添加空白

制表符：\t  
换行符：\n  
```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
```

### 2.3.4 删除空白

```python
language = '  python '

#删除前面空白（左边left）
print(language.lstrip())

#删除后面空白（右边right）
print(language.rstrip())

#删除两边的空白
print(language.strip())

#注意这几个方法不会改变变量的值
#要改变值的话，需要重新赋值

```

## 2.4 数字

### 2.4.1 整数

加+，减-，乘*，除/，乘方**，  
可以用小括号()改变运算次序。  

### 2.4.2 浮点数

python中，浮点数可以直接与整数进行运算

### 2.4.3 使用函数str()避免类型错误

函数str()可以将数字转换为字符串。  
```python
age = 23
message = "Happy " + str(age) + "rd Birthday!"
print(message)
```

## 2.5 注释

* 单行注释：在这一行前加一个#；  
* 多行注释：用三个引号括起来；  
```python
#注释
'''
注释1
注释2
注释3
'''
```