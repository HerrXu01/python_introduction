# 第八章 函数

## 8.1 定义函数
下例是一个打印问候语的简单函数。
```python
def greet_user():
    print("Hello!")
    
greet_user()
'''
输出结果为：
Hello!
'''
```  
关键字def用于定义函数，指出函数名，还有可能在括号内指出函数所需要的信息（这里的greet_user()不需要任何信息）。最后，定义以冒号结尾。  
紧跟在冒号后面所有缩进行构成了函数体。  

### 8.1.1 向函数传递信息
对上例函数就可以显示用户姓名。  
```python
def greet_user(username):
    print("Hello, " + username.title() + "!")

username = input("What's your name? ")    
greet_user(username)
'''
输出结果为：
What's your name? xzt
Hello, Xzt!
'''
```  

### 8.1.2 实参和形参
在函数的定义中，比如上面定义greet_user()时括号里的username就是形参。  
而在调用该函数时向该函数传递的信息就是实参，在上例中，获取用户输入的username就是实参。  

## 8.2 传递实参

### 8.2.1 位置实参
调用函数时，Python必须将函数调用中的每个实参与定义中的形参相关联。最简单的关联方式就是基于实参的位置，这种关联方式称为**位置实参**。  
下例是一个显示宠物信息的函数，指出宠物属于哪种动物以及名字。  
```python
def describe_pet(animal_type, pet_name):
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")
    
describe_pet('hamster', 'harry')
'''
输出结果为：

I have a hamster.
My hamster's name is Harry.
'''
```  
1. 调用函数多次
可以根据需要调用函数任意次。  
2. 位置实参的顺序很重要
注意实参要与对应的形参顺序一致，否则结果不对。  

### 8.2.2 关键字实参
关键字实参是传递给函数的 名称-值 对。直接在调用的时候将实参和形参关联起来，这样就不会混淆了。  
```python
def describe_pet(animal_type, pet_name):
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet(pet_name = 'harry', animal_type = 'hamster')
'''
输出结果与之前一致
'''
```  
使用关键字实参，顺序不重要，但要注意在调用时形参名以及对应关系要准确。  

### 8.2.3 默认值
在定义函数时，可以给每个或者某几个形参指定默认值。在调用函数时，如果给所有的形参都提供了实参，那么函数将使用提供的实参，否则就使用形参的默认值。  
在定义函数时，如果只给某几个形参指定默认值，其余形参不指定，这时要注意，把未指定默认值的形参放前面，指定了默认值的形参放后面。在调用函数时，如果需要使用默认值，只要提供实参给那些未指定默认值的形参就行了，指定了默认值的形参就可以不再提供实参了。这时，Python将实参依然视为位置实参，所以对于未指定默认值的形参最好放在前面。  
当然，可以使用关键字实参，让指代更加明确。  
```python
def describe_pet(pet_name, animal_type = 'dog'):
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet('willie')

describe_pet('harry', 'hamster')
'''
输出结果为：

I have a dog.
My dog's name is Willie.

I have a hamster.
My hamster's name is Harry.
'''
```  

### 8.2.4 等效的函数调用
位置实参和关键字实参等效。

### 8.2.5 避免实参错误
出现错误，traceback会指出错在哪。  

## 8.3 返回值
函数并不都是直接显示输出，还可以是处理一些数据，然后返回一个或一组值。  
使用return语句。  

### 8.3.1 返回简单值
下面这个函数接受名和姓，并返回整洁的姓名。  
```python
def get_formatted_name(first_name, last_name):
    full_name = first_name + " " + last_name
    return full_name.title()
    
musician = get_formatted_name('jemi', 'hendrix')
print(musician)
'''
输出结果为：
Jemi Hendrix
'''
```  
调用带有返回值的函数时，要提供一个相应的数据类型，用于存储返回的值。  

### 8.3.2 让实参变成可选的
我们对上例进行修改，使其能够处理中间名。  
```python
def get_formatted_name(first_name, middle_name, last_name):
    full_name = first_name + " " + middle_name + " " + last_name
    return full_name.title()

user = get_formatted_name('sheldon', 'lee', 'cooper')
print(user)
'''
输出结果为：
Sheldon Lee Cooper
'''
```  
然而，不是所有人都有中间名，如果调用这个函数只提供了名和姓，会出现错误。现在，我们需要让中间名变成可选的。  
可以给middle_name指定一个默认值，一个空字符串。  
```python
def get_formatted_name(first_name, last_name, middle_name = ''):
    if middle_name:
        full_name = first_name + " " + middle_name + " " + last_name
    else:
        full_name = first_name + " " + last_name
    return full_name.title()

user = get_formatted_name('sheldon', 'cooper', 'lee')
print(user)

musician = get_formatted_name('jimi', 'hendrix')
print(musician)
'''
输出结果为：
Sheldon Lee Cooper
Jimi Hendrix
'''
```

### 8.3.3 返回字典
函数还可以返回字典或列表。下例的函数接受姓名的组成部分，返回一个表示人的字典。  
```python
def build_person(first_name, last_name):
    person = {'first': first_name, 'last': last_name}
    return person

musician = build_person('jimi', 'hendrix')
print(musician)
'''
输出结果为：
{'first': 'jimi', 'last': 'hendrix'}
'''
```  
还可以对这个函数进行扩展，使其接受可选值，如中间名、年龄、职业等等，将这些数据放入表示这个人的字典中。  

### 8.3.4 结合使用函数和while循环
可以将函数与任何一种结构结合起来，比如和while循环结合。  
```python
def greet(first_name, last_name):
    full_name = first_name + " " + last_name
    print("\nHello, " + full_name.title() + "!\n")

while True:
    print("Please tell me your name:")
    print("(enter 'q' at any time to quit)")
    f_name = input("First name: ")
    if f_name == 'q':
        break
    l_name = input("Last name: ")
    if l_name == 'q':
        break
    greet(f_name, l_name)
'''
输出结果为：
Please tell me your name:
(enter 'q' at any time to quit)
First name: sherlock
Last name: holmes

Hello, Sherlock Holmes!

Please tell me your name:
(enter 'q' at any time to quit)
First name: q
'''
```  

## 8.4 传递列表
将列表传给函数，让函数来处理列表，效率比较高。
比如有一个用户列表，需要问候每一位用户。
```python
def greet_users(names):
    for name in names:
        msg = "Hello, " + name.title() + "!"
        print(msg)

usernames = ['hannah', 'ty', 'margot']
greet_users(usernames)
'''
输出结果为：
Hello, Hannah!
Hello, Ty!
Hello, Margot!
'''
```  

### 8.4.1 在函数中修改列表
来看一个例子，将使用两种方法实现，第一种是不使用函数。  
一家公司为用户的设计制作3D打印模型，需要打印的设计存在一个列表中，打印好了之后移到另一个列表中。  
```python
unprinted_designs = ['iphone case', 'robot pendant', 'dodecahedron']
completed_models = []

#模拟打印设计的过程
while unprinted_designs:
    current_model = unprinted_designs.pop()
    
    print("Printing model: " + current_model)
    completed_models.append(current_model)
    
print("\nThe following models have been printed:")
for model in completed_models:
    print(model)
'''
输出结果为：
Printing model: dodecahedron
Printing model: robot pendant
Printing model: iphone case

The following models have been printed:
dodecahedron
robot pendant
iphone case
'''
```  
下面是使用函数的代码：
```python
def print_models(unprinted_designs, completed_models):
    while unprinted_designs:
        current_model = unprinted_designs.pop()
        print("Printing model: " + current_model)
        completed_models.append(current_model)

def show_completed_models(completed_models):
    print("\nThe following models have been printed:")
    for model in completed_models:
        print(model)
        
unprinted_designs = ['iphone case', 'robot pendant', 'dodecahedron']
completed_models = []

print_models(unprinted_designs, completed_models)
show_completed_models(completed_models)
'''
输出结果与之前一致
'''
```  
虽然这两段代码输出一致，但是使用函数的更容易扩展和维护，比如要修改的话，只要修改函数就行了。  
这个程序还演示了这样的理念，即一个函数只负责一项具体的工作。如果发现一个函数执行的任务太多，要尝试将这些代码分到两个函数中。  
在一个函数中可以调用另外一个函数。  

### 8.4.2 禁止函数修改列表
在前一个示例中，调用了函数print_models()函数之后，unprinted_designs[]列表就空了。可能有时候我们想保留原始的列表以供备案，这时我们可以在调用函数的时候，传递给函数原始列表的切片：
```python
print_models(unprinted_designs[:], completed_models)
```  
这样，函数只会对列表的副本进行修改，原始的列表保存下来了。  
但是必须要有充分的理由才这么做，因为让函数使用现成的列表可以避免花时间和内存创建副本，能提高效率。   

## 8.5 传递任意数量的实参
有时候，预先不知道函数要接受多少个实参，好在Python允许函数从调用语句中收集任意数量的实参。  
```python
def make_pizza(*toppings):
    '''打印顾客点的所有配料'''
    print(toppings)
    
make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
'''
输出结果为：
('pepperoni',)
('mushrooms', 'green peppers', 'extra cheese')
'''
```  
形参名*toppings中的星号让Python创建一个名为toppings的空元组，并将收到的所有值都装进这个元组。  
在函数体中，我们可以对这个元组执行相应的操作。  
```python
def make_pizza(*toppings):
    '''打印顾客点的所有配料'''
    print("\nMaking a pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)
    
make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
'''
输出结果为：

Making a pizza with the following toppings:
- pepperoni

Making a pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
'''
```  

### 8.5.1 结合使用位置实参和任意数量实参
使用任意数量实参的函数通常接受同种类型的参数放入元组，如果要让函数接受不同类型的实参，必须在函数定义中，将接纳任意数量实参的形参放在最后。Python先匹配位置实参和关键字实参，再将余下的实参都收集到最后一个形参中。  
比如，在上个例子中，再加入一个表示pizza尺寸的实参：
```python
def make_pizza(size, *toppings):
    '''打印顾客点的所有配料'''
    print("\nMaking a " + str(size) + "-inch" + 
            "pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)
    
make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
'''
输出结果为：

Making a 16-inchpizza with the following toppings:
- pepperoni

Making a 12-inchpizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
'''
```  

### 8.5.2 使用任意数量的关键字实参
有时候，需要接受任意数量的实参，但预先不知道传递给函数的会是什么样的信息。这时，可以将函数编写成能接受任意数量的键-值对。  
一个示例创建用户简介：
```python
def build_profile(first, last, **user_info):
    profile = {}
    profile['first name'] = first
    profile['last name'] = last
    for key, value in user_info.items():
        profile[key] = value
    return profile
    
user_profile = build_profile('albert', 'einstein',
                                location = 'princeton',
                                field = 'physics')
print(user_profile)
'''
输出结果为：
{'first name': 'albert', 'last name': 'einstein', 'location': 'princeton', 'field': 'physics'}
'''
```  
形参**user_info中的两个星号让Python创建一个名为user_info的空字典，并将所有收到的名称-值对（即关键字实参）都封装到这个字典中。

## 8.6 将函数存储在模块中
函数的优点之一就是可以将代码块与主程序分离。还可以更进一步，将函数存储在被称为**模块**的独立文件中，再将模块导入到主程序中，使用import语句。  
导入模块的方法有多种。

### 8.6.1 导入整个模块
要让函数是可导入的，得先创建模块。模块是扩展名为.py的文件，包含要导入到程序中的代码。以下为一个简单示例：
我们先创建一个pizza.py文件，里面是8.5.1中用到的make_pizza函数，只保留函数部分，没有其他代码。  
```python
def make_pizza(size, *toppings):
    '''打印顾客点的所有配料'''
    print("\nMaking a " + str(size) + "-inch" + 
            " pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)
```  
在pizza.py所在的目录中创建另一个making_pizzas.py的文件，导入刚创建的模块，调用make_pizza()函数。  
```python
import pizza

pizza.make_pizza(16, 'pepperoni')
pizza.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
'''
输出结果与8.5.1中的一致
'''
```  
代码import pizza让Python打开pizza.py文件，将其中的所有函数复制到这个程序中，这样，就可以在当前程序中使用pizza.py中定义的所有函数。  
调用的时候，要指定导入的模块名称pizza和函数名make_pizza()，并用句点分隔，如下：
```python
module_name.function_name()
```  

### 8.6.2 导入特定的函数
可以导入模块中特定的函数。语法如下：
```python
from module_name import function_name
```  
这里函数名后面不用加括号。  
可以导入模块中任意数量的函数，用逗号分隔：
```python
from module_name import function_0, function_1, function_2
```  
在这种情况下，调用函数时，就不用再指定模块名了，只要指定函数名称就行了。  

### 8.6.3 使用as给函数指定别名
要导入的函数名称可能会与程序中现有的名称冲突，或者函数名称太长，可以给函数指定一个简短而独一无二的别名，类似于外号。这样调用函数只要指定函数的别名就行了。  
```python
from pizza import make_pizza as mp

mp(16, 'pepperoni')
mp(12, 'mushrooms', 'green peppers', 'extra cheese')
```  

### 8.6.4 使用as给模块指定别名
还可以给模块指定别名，比如给模块pizza指定别名p。  
```python
import pizza as p

p.make_pizza(16, 'pepperoni')
p.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```  
这样，函数名称没变，模块名简化了，因为对于理解代码而言，函数名更加重要。  

### 8.6.5 导入模块中的所有函数
使用星号（*）运算符可以导入模块中的所有函数，这个方法与导入整个模块的区别在于在调用函数时不用指定模块名称了，直接指定函数名称就行了。  
```python
from pizza import *

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```  
**注意**：如果使用非自己编写的大型模块时，最好不要用这种方法，因为导入的模块中可能有与当前程序重复的函数名。  

## 8.7 函数编写指南
* 给函数指定描述性名称，并只使用小写字母和下划线；
* 函数应包含描述其功能的注释，跟在定义后面，三引号括起来；
* 给形参指定默认值，以及调用函数使用关键字实参时，等号两边不要有空格；
* 定义函数时，如果形参过多，超过了那条线，可以在输入左括号后回车，再按两次tab键，与只缩进一层的函数体区分开来；
* 如果程序或模块包含多个函数，应将相邻两个函数空两行分开；
* 所有import语句放在文件开头；