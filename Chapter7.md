# 第七章 用户输入和while循环

## 7.1 函数input()的工作原理
函数input()让程序暂停运行，等待用户输入一些文本，获取之后再继续。  
```python
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```  

### 7.1.1 编写清晰的程序
当使用函数input()时，要说明清楚要让用户输入什么信息。  
如果提示超过一行，可以先将提示存在一个变量里，然后将该变量传给函数input()。  

### 7.1.2 使用int来获取数值输入
使用函数input()时，Python将用户的输入解读为字符串，（即使用户输入的是数字）。  
可以使用函数int()将字符串转换为数字。
```python
age = int(input("How old are you? "))
print(age > 18)

'''
输出结果为：
How old are you? 23
True
'''
```  

### 7.1.3 求模运算符
求模运算符%求两个数相除的余数。  
如果整除，则返回余数为0。  
```python
print(4 % 3)
print(5 % 3)

'''
输出结果为：
1
2
'''
```  
下例为判断一个数是奇数还是偶数：  
```python
message = "Enter an integer,"
message += " and I will tell you if it's even or odd: "

integer = int(input(message))
if integer % 2 == 0:
    print("It's even.")
else:
    print("It's odd.")

'''
输出结果为：
Enter an integer, and I will tell you if it's even or odd: 15
It's odd.
'''
```  

## 7.2 while循环简介
while循环不断运行，直到指定的条件不满足为止。  

### 7.2.1 使用while循环  
可以使用while循环来数数。  
```python
number = 1
while number <= 5:
    print(number)
    number += 1

'''
输出结果为：
1
2
3
4
5
'''
```  

### 7.2.2 让用户选择何时退出
下例中，当用户输入quit会退出程序，否则程序将一直运行。  
```python
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
    message = input(prompt)
    if message != 'quit':
        print(message)

'''
输出结果为：

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. hello
hello

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. quit
'''
```  

### 7.2.3 使用标志
有些程序会要求满足多个条件才能继续运行，可以定义一个变量，用于判断整个程序是否处于活动状态，这个变量被称为标志。可以让程序在标志为True时继续运行，任何事件导致标志为False时停止运行。  
```python
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
    message = input(prompt)
    
    if message == 'quit':
        active = False
    else:
        print(message)
#输出结果与之前一致
```  
如果需要再加一件导致终止运行的条件的话，只要在if语句中再加一句elif就行了。  
比如，如果用户输入'exit'程序也终止的话，那就加一句elif，当message为'exit'时，将标志active也置为False就行了。  

### 7.2.4 使用break退出循环
break语句可以用来退出循环，不只是while循环，for循环也可以用break来退出。  
下例让用户输入去过的城市，输入quit时退出。  
```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' to when you are finished.) "

while True:
    city = input(prompt)
    
    if city == 'quit':
        break
    else:
        print(city.title())
```  

### 7.2.5 在循环中使用continue
在循环中使用continue，跳过循环中余下的代码，返回到循环的开头。  
```python
number = 0

while number < 10:
    number += 1
    if number % 2 == 0:
        continue
    print(number)

'''
输出结果为：
1
3
5
7
9
'''
```  

### 7.2.6 避免无限循环
每个while循环必须有停止运行的途径。  
比如在7.2.5的例子中，不能少了number += 1这一句，否则将无限循环。  

## 7.3 使用while循环来处理列表和字典

### 7.3.1 在列表之间移动元素
有一个列表，包含新注册但未验证的用户，验证这些用户之后，要将他们移动到另一个已验证的列表中。  
```python
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)
    
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())

'''
输出结果为：
Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
'''
```  

### 7.3.2 删除包含特定值的所有列表元素
之前介绍过方法remove()是用来根据值删除列表中的元素，但是当列表中要删除的元素有重复时，此方法只能删除第一个出现的值，不能删除所有的。以下示例是用while循环来解决这个问题。  
```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
    pets.remove('cat')
    
print(pets)

'''
输出结果为：
['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
'''
```  

### 7.3.3 使用用户输入来填充字典
可以使用while循环提示用户输入任意数量的信息。  
```python
responses = {}

polling_active = True

while polling_active:
    name = input("\nWhat is your name? ")
    response = input("Which mountain would you like to climb someday? ")
    
    responses[name] = response
    
    repeat = input("Would you like to let another person to respond? " + 
                        "(yes/no) ")
    if repeat == 'no':
        polling_active = False
    
print("\n---Poll Results---")
for name, response in responses.items():
    print(name.title() + " would like to climb " + response.title() +".")
'''
输出结果为：

What is your name? xzt
Which mountain would you like to climb someday? yellow mountain
Would you like to let another person to respond? (yes/no) yes

What is your name? lbl
Which mountain would you like to climb someday? tai mountain
Would you like to let another person to respond? (yes/no) yes

What is your name? lmz
Which mountain would you like to climb someday? changbai mountain
Would you like to let another person to respond? (yes/no) no

---Poll Results---
Xzt would like to climb Yellow Mountain.
Lbl would like to climb Tai Mountain.
Lmz would like to climb Changbai Mountain.
'''
```