# 第六章 字典

## 6.1 一个简单的字典
以下是一个字典，存储了有关外星人的信息。
```python
alien_0 = {'color': 'green', 'points': 5}

print(alien_0['color'])
print(alien_0['points'])
```  
输出结果为：
green  
5  

## 6.2 使用字典
字典是一系列 键-值 对。每一个键都与值相关联。与键相关联的值可以是数字、字符串、列表乃至字典。  
字典用放在花括号{}中的一系列键-值对来表示。  
键和值之间用冒号分隔，键-值对用逗号分隔。

### 6.2.1 访问字典中的值
依次指定字典名和放在方括号内的键，如6.1中的代码所示。

### 6.2.2 添加键-值对
要添加键-值对，可依次指定字典名、用方括号括起的键和相关联的值。  
```python
alien_0 = {'color': 'green', 'points': 5}

alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)
```  
输出结果为：  
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 25}  
输出键值对的排列顺序可能会与添加顺序不同，Python不关心键值对的添加顺序，只关心键和值的联系。  

### 6.2.3 先创建一个空字典
使用字典来存储用户提供的数据或在编写能够自动生成大量键值对代码时，通常需要先定义一个空字典，然后添加键值对。  
使用一对空的花括号定义一个空字典。  
```python
alien_0 = {}
```  

### 6.2.4 修改字典中的值
直接赋值。  
依次指定字典名、方括号括起的键以及与该键相关联的新值。
```python
alien_0 = {'color': 'green'}

alien_0['color'] = 'yellow'
```  

### 6.2.5 删除键-值对
使用del语句，指定要删除的字典名和相应的键。  
```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

del alien_0['points']
print(alien_0)
```  
输出结果为：  
{'color': 'green', 'points': 5}  
{'color': 'green'}  

### 6.2.6 由类似对象组成的字典
在之前的示例中，字典存储的时一个对象（一个外星人）的多种信息。字典也可以用来存储多个对象的同一种信息，例如不同人喜欢的编程语言。  
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("Sarah's favorite language is " + 
    favorite_languages['sarah'].title() + 
    ".")
```  
注意这里，当字典内容较多时，应使用多行来定义字典。  
输入左花括号后回车，缩进四个空格，然后指定一个键值对，逗号，再换行指定第二个键值对，这时第二个键值对会自动对齐缩进，这样直到最后。  
可以在最后一个键值对后面加上一个逗号，为之后添加键值对做好准备。  
输出较长的print语句时，也应当分行，用+号连接，换行要缩进四个空格。  

## 6.3 遍历字典
字典可存储大量数据，Python支持对字典遍历。  
遍历的方式：键-值对、键或值。  

### 6.3.1 遍历所有的键-值对
使用for循环遍历  
下面例子中的字典用于存储一名用户的用户名、名和姓。  
```python
user_0 = {
    'username': 'efermi',
    'first': 'enrico',
    'last': 'fermi',
    }

for key, value in user_0.items():
    print("\nkey: " + key)
    print("value: " + value)
```  
输出结果为：
  
key: username  
value: efermi  
  
key: first  
value: enrico  
  
key: last  
value: fermi  
方法items()的作用是返回一个键-值对列表，for循环将每个键-值对存储到所声明的两个变量中：key和value，然后再打印出来。  

### 6.3.2 遍历字典中的所有键
当只需要遍历键的时候，用方法keys()。
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

for name in favorite_languages.keys():
    print(name.title())
```  
输出结果为：  
Jen  
Sarah  
Edward  
Phil  
如果这里不用方法keys()，输出结果也不会改变，因为默认遍历所有键，但是最好用方法keys()，这样便于理解。  

### 6.3.3 按顺序遍历字典中的所有键
之前提到过获取字典元素的顺序是不确定的，但是要想按特定顺序获取元素，可以调用函数sorted()。  
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

for name in sorted(favorite_languages.keys()):
    print(name.title())
```  
输出结果为：  
Edward  
Jen  
Phil  
Sarah  
与之前对比可以看到键按顺序排列了。  

### 6.3.4 遍历字典中的所有值
如果只要遍历值，可以使用方法values()，返回一个值列表。   
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("The following languages have been mentioned:")
for language in favorite_languages.values():
    print(language.title())
```  
输出结果为：  
The following languages have been mentioned:  
Python  
C  
Ruby  
Python  
可以看到，输出会有重复的情况。如果想没有重复的元素，可以对包含重复元素的列表调用集合set()函数，结果是一个没有重复项的列表。  
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("The following languages have been mentioned:")
for language in set(favorite_languages.values()):
    print(language.title())
```  
输出结果为：  
The following languages have been mentioned:  
Python  
C  
Ruby  

## 6.4 嵌套
列表中嵌套字典，字典中嵌套列表，字典中嵌套字典。  

### 6.4.1 字典列表
列表中的每个元素都是一个字典。  
以下例子是包含三个字典的列表。  
```python
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2]

for alien in aliens:
    print(alien)
```  
实际情形更多是用代码自动生成外星人字典。  
```python
aliens = []

for alien_number in range(30):
    new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
    aliens.append(new_alien)
    
#显示前5个外星人
for alien in aliens[:5]:
    print(alien)

print("...")

#显示创建了多少外星人
print("Total number of aliens: " + str(len(aliens)))
```  
输出结果为：  
{'color': 'green', 'points': 5, 'speed': 'slow'}  
{'color': 'green', 'points': 5, 'speed': 'slow'}  
{'color': 'green', 'points': 5, 'speed': 'slow'}  
{'color': 'green', 'points': 5, 'speed': 'slow'}  
{'color': 'green', 'points': 5, 'speed': 'slow'}  
...  
Total number of aliens: 30  
如有需要，可以再对其进行修改。  

### 6.4.2 在字典中存储列表
每当在字典中一个键要关联多个值时，可以再字典中嵌套列表。  
比如之前显示每个人喜欢的编程语言的例子，如果有人喜欢的编程语言大于一种，这时可以将列表存储在字典中。  
```python
favorite_languages = {
    'jen': ['python', 'ruby'],
    'sarah': ['c'],
    'edward': ['ruby', 'go'],
    'phil': ['python', 'c++'],
    }
    
for name, languages in favorite_languages.items():
    if len(languages) == 1:
        print("\n" + name.title() + "'s favorite language is: " + 
            "\n\t" + languages[0].title())
    else:
        print("\n" + name.title() + "'s favorite languages are: ")
        for language in languages:
            print("\t" + language.title())
```  
输出结果为：  
   
Jen's favorite languages are:  
        Python  
        Ruby  
  
Sarah's favorite language is:  
        C  

Edward's favorite languages are:  
        Ruby  
        Go  

Phil's favorite languages are:  
        Python  
        C++  

### 6.4.3 在字典中存储字典
比如要存储一个网站的多个用户的多项信息，可以将用户名作为键，值是相应的字典，存储该用户的不同信息。  
```python
users = {
    'aeinstein': {
        'first': 'albert',
        'last': 'einstein',
        'location': 'princeton',
        },
        
    'mcurie': {
        'first': 'marie',
        'last': 'curie',
        'location': 'paris',
        },
        
    }

for username, user_info in users.items():
    print("\nUsername: " + username)
    full_name = user_info['first'] + " " + user_info['last']
    location = user_info['location']
    
    print("\tFull name: " + full_name.title())
    print("\tLocation: " + location.title())

'''
输出结果为：  
  
Username: aeinstein  
        Full name: Albert Einstein  
        Location: Princeton  
  
Username: mcurie  
        Full name: Marie Curie  
        Location: Paris 
'''
```  
