# 第九章 类

## 9.1 创建和使用类
以下示例是一个表示小狗的简单类Dog，它表示的不是特定的小狗，而是任何小狗。  
对于大多数小狗，我们知道它们有名字和年龄，大多数小狗会蹲下和打滚。由于大多数小狗具备上述两项信息（名字、年龄）和两种行为（蹲下、打滚），我们创建的Dog类将包含它们。  

### 9.1.1 创建Dog类
```python
class Dog():
    '''一次模拟小狗的简单尝试'''
    
    def __init__(self, name, age):
        '''初始化属性name和age'''
        self.name = name
        self.age = age
        
    def sit(self):
        '''模拟小狗被命令时蹲下'''
        print(self.name.title() + " is now sitting.")
        
    def roll_over(self):
        '''模拟小狗被命令时打滚'''
        print(self.name.title() + " rolled over!")
        
        
my_dog = Dog('willie', 6)

print("My dog's name is " + my_dog.name.title() + ".")
print("My dog is " + str(my_dog.age) + " years old.")

my_dog.sit()
my_dog.roll_over()
'''
输出结果为：
My dog's name is Willie.
My dog is 6 years old.
Willie is now sitting.
Willie rolled over!
'''
```  
class及之后缩进的部分是创建Dog类的代码。约定在Python中，首字母大写的名称指的是类。  

类中的函数称为**方法**。方法__init__()是一个特殊的方法，每当根据Dog类创建新实例时，Python都会自动运行它。这个方法的名称中，开头和末尾各有**两个**下划线，避免与普通方法发生名称冲突。  

方法__init__()的定义包含三个形参：self, name和age。其中，self是必不可少的，而且必须放在其他形参前面。创建实例时，Python调用这个方法，将自动传入实参self，它是一个指向实例本身的引用，让实例能访问类中的属性和方法。  

我们在创建Dog实例时，Python调用Dog类的__init__()方法，由于self会自动传递，所以我们只需要为后两个形参name和age提供值就行了。  

方法__init__()的函数体中两个变量name和age都有前缀self，以self为前缀的变量可供类中的所有方法使用，还可以通过类的实例来访问这些变量。self.name = name获取存储在形参name中的值，将其存储到变量name中，并关联到当前创建的实例。  

像这样可以通过实例访问的变量称为**属性**。

Dog类还定义了另外两个方法：sit()和roll_over()，这些方法不需要额外的信息比如名字和年龄，所以只有一个形参self。这里的两个方法都只是打印消息，但是可以扩展这些方法以模拟实际情况：如果这个类是控制机器狗的，那么这些方法将引导机器狗做出蹲下和打滚的动作。

### 9.1.2 根据类创建实例
下面这个语句就是创建一个表示特定小狗的实例：
```python
my_dog = Dog('willie', 6)
```  
Python使用实参'willie'和6调用Dog类中的方法__init__()，创建一个表示特定小狗的实例，并用我们提供的值来设置属性name和age。这里方法__init__()没有return语句，但Python会自动返回一个表示这条小狗的实例，存储在变量my_dog中。  
关于命名的约定：通常首字母大写的名称指的是类，小写的名称指的是根据类创建的实例。  
1. 访问属性
使用句点表示法：
```python
my_dog.name
my_dog.age
```  
2. 调用方法
创建实例之后，使用句点表示法来调用类中定义的任何方法：
```python
my_dog.sit()
my_dog.roll_over()
```  
3. 创建多个实例
可按需求根据类创建任意数量的实例。下面又创建了一个名为your_dog的实例：
```python
your_dog = Dog('lucy', 3)
```  

## 9.2 使用类和实例

### 9.2.1 Car类
下面是一个汽车的类，存储有关汽车的信息，还有一个汇总这些信息的方法：
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
my_car = Car('audi', 'rs7', 2021)
print(my_car.get_descriptive_name())
'''
输出结果为：
2021 Audi Rs7
'''
```  

### 9.2.2 给属性指定默认值
接下来我们来给这个Car类添加一个随时间变化的属性，存储汽车的总里程。  
类中的每个属性都必须有初始值，哪怕是0或空字符串。如果要给某个属性设置默认值，直接在方法__init__()内指定初始值，这样的话，定义的时候就无须包含为它提供初始值的形参。  
在下面示例中，我们添加odometer_reading属性，初始值为0。再添加一个read_odometer()的方法，用于读取汽车的里程表。  
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
my_car = Car('audi', 'rs7', 2021)
print(my_car.get_descriptive_name())
my_car.read_odometer()
'''
输出结果为：
2021 Audi Rs7
This car has 0 miles on it.
'''
```  
出售里程数为0的汽车不多，我们需要一个修改该属性的值的途径。  

### 9.2.3 修改属性的值
有三种方法：
1. 直接修改属性的值
通过实例直接访问该属性并修改。
```python
my_car.odometer_reading = 23
my_car.read_odometer()
'''
输出结果为：
This car has 23 miles on it.
'''
```  
2. 通过方法修改属性的值
可以添加一个方法，将值传递给这个方法，让方法来修改属性的值。  
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        self.odometer_reading = mileage
        
my_car = Car('audi', 'rs7', 2021)
print(my_car.get_descriptive_name())
#my_car.odometer_reading = 23
my_car.update_odometer(23)
my_car.read_odometer()
'''
输出结果与之前一致
'''
```  
我们还可以对方法进行扩展，禁止任何人将里程数回调，这里只展示函数：
```python
def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
```  
3. 通过方法对属性的值进行递增
有时候需要将属性值递增特定的量，而不是将其设置为特定的值。比如买了一辆二手车，从购买到登记期间增加了100英里的里程：
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
            
    def increment_odometer(self, miles):
        '''将里程表读数增加指定的量'''
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back an odometer!")
            
my_used_car = Car('mclaren', 'p1', '2020')
print(my_used_car.get_descriptive_name())

my_used_car.update_odometer(23500)
my_used_car.read_odometer()

my_used_car.increment_odometer(100)
my_used_car.read_odometer()
'''
输出结果为：
2020 Mclaren P1
This car has 23500 miles on it.
This car has 23600 miles on it.
'''
```  

## 9.3 继承
编写类时，不一定是从空白开始的，可以是一个现成类的特殊版本，可以使用**继承**。一个类继承另一个类时，将自动获得另一个类的所有属性和方法，原类称为父类，新类称为子类。子类还可以定义自己的属性和方法。  

### 9.3.1 子类的方法__init__()
子类的方法__init__()需要父类施以援手。  
我们来看一个例子，模拟电动汽车，电动汽车时汽车的一种，可以在Car类的基础上创建新类ElectricCar，这样我们只需要为电动汽车编写特有的属性和行为。这是一个简单的ElectricCar类版本，具有Car类所有功能。  
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
            
    def increment_odometer(self, miles):
        '''将里程表读数增加指定的量'''
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back an odometer!")
            
class ElectricCar(Car):
    '''电动汽车的独特之处'''
    
    def __init__(self, make, model, year):
        '''初始化父类属性'''
        super().__init__(make, model, year)
        

my_tesla = ElectricCar('tesla', 'model s', '2020')
print(my_tesla.get_descriptive_name())
'''
输出结果为：
2020 Tesla Model S
'''
```  
* 创建子类时，父类必须包含在当前文件中，且位于子类前面；
* 定义子类时，必须在括号内指定父类名称；
* 方法__init__()接受创建Car实例所需的信息；
* super()是一个特殊的函数，将父类和子类关联起来。父类也称超类（superclass），所以用super()。该行代码让Python调用ElectricCar的父类的方法__init__()，让ElectricCar实例包含父类的所有属性。  

### 9.3.3 给子类定义属性和方法
子类可以添加新的属性和方法。  
还是上面电动汽车的例子，我们添加电动汽车特有的属性电瓶容量，以及一个描述该属性的方法。这里只展示子类代码。  
```python
class ElectricCar(Car):
    '''电动汽车的独特之处'''
    
    def __init__(self, make, model, year):
        '''初始化父类属性'''
        super().__init__(make, model, year)
        self.battery_size = 70
        
    def describe_battery(self):
        '''描述电瓶容量'''
        print("This car has a " + str(self.battery_size) + "-kWh battery.")

my_tesla = ElectricCar('tesla', 'model s', '2020')
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
```  
可以根据需要给子类添加任意数量的属性和方法。但如果一个属性或方法是任何汽车都有的，而不是电动汽车特有的，应将其加入Car类。  

### 9.3.4 重写父类的方法
父类中的方法有可能不适合子类，可以在子类中对其进行重写。在子类中定义这个方法，它与要重写的父类方法同名。这样，Python就不会考虑父类中的方法，只关注子类中定义的方法。  
比如Car类中有一个fill_gas_tank()的方法，对电动汽车无意义，可以在ElectricCar类中重写它：
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
            
    def increment_odometer(self, miles):
        '''将里程表读数增加指定的量'''
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back an odometer!")
    
    def fill_gas_tank(self):
        print("The gas tank has been filled.")
            
class ElectricCar(Car):
    '''电动汽车的独特之处'''
    
    def __init__(self, make, model, year):
        '''初始化父类属性'''
        super().__init__(make, model, year)
        self.battery_size = 70
        
    def describe_battery(self):
        '''描述电瓶容量'''
        print("This car has a " + str(self.battery_size) + "-kWh battery.")
        
    def fill_gas_tank(self):
        print("This car doesn't have a gas tank.")

my_tesla = ElectricCar('tesla', 'model s', '2020')
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
my_tesla.fill_gas_tank()
'''
输出结果为：
2020 Tesla Model S
This car has a 70-kWh battery.
This car doesn't have a gas tank.
'''
```  
可以看出，如果有人想对ElectricCar创建的实例调用fill_gas_tank()函数，Python会忽略Car类中的方法。  

### 9.3.5 将实例用作属性
模拟实物时，类中的内容可能会很多，可以将类的一部分作为一个独立的类提取出来。  
例如，不断给ElectricCar类添加细节时，发现其中有很多针对汽车电瓶的属性和方法。这样的话，可以将这些属性和方法提取出来，放到另一个名为Battery的类中，并将一个Battery类的实例用作ElectricCar类的一个属性：
```python
class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
            
    def increment_odometer(self, miles):
        '''将里程表读数增加指定的量'''
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back an odometer!")
    
    def fill_gas_tank(self):
        print("The gas tank has been filled.")
        
class Battery():
    '''模拟电动汽车电瓶'''
    
    def __init__(self, battery_size=70):
        self.battery_size = battery_size
        
    def describe_battery(self):
        print("This car has a " + str(self.battery_size) + "-kWh battery.")
        
class ElectricCar(Car):
    '''模拟电动汽车'''
    
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        self.battery = Battery()
        
my_tesla = ElectricCar('tesla', 'model s', 2020)

print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
'''
输出结果为：
2020 Tesla Model S
This car has a 70-kWh battery.
'''
```  
这里，Battery是一个新类，它没有继承任何类。有一个可选的形参battery_size和方法describe_battery()。  
在ElectricCar类中，我们添加了一个名为self.battery的属性。创建了一个Battery实例存进了这个属性中。  
输出结果与之前一致，虽然看上去麻烦，但是如果要添加更多描述电瓶的细节，就不会让ElectricCar类看上去混乱。  

### 9.3.6 模拟实物
现实世界的建模方法没有对错之分，有些方法效率更高，但要找到效率最高的表示法，需要经过一定的实践。  

## 9.4 导入类
Python允许将类存储在模块中，然后再主程序中导入所需的模块。  

### 9.4.1 导入单个类
创建一个只包含Car类的模块，命名为car.py。
```python
'''一个可用于表示汽车的类'''

class Car():
    '''一次模拟汽车的简单尝试'''
    
    def __init__(self, make, model, year):
        '''初始化描述汽车的属性'''
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
        
    def get_descriptive_name(self):
        '''返回整洁的描述性信息'''
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
        
    def read_odometer(self):
        '''打印一条指出汽车里程的消息'''
        print("This car has " + str(self.odometer_reading) + " miles on it.")
        
    def update_odometer(self, mileage):
        '''将里程表读数置为指定值'''
        if mileage > self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
            
    def increment_odometer(self, miles):
        '''将里程表读数增加指定的量'''
        if miles >= 0:
            self.odometer_reading += miles
        else:
            print("You can't roll back an odometer!")
```  
我们在开头加了简要的描述，这是必要的。  
接着，创建另一个文件my_car.py，导入Car类，并创建其实例：
```python
from car import Car

my_car = Car('mclaren', 'p1', 2021)
print(my_car.get_descriptive_name())

my_car.odometer_reading = 23
my_car.read_odometer()
'''
输出结果为：
2021 Mclaren P1
This car has 23 miles on it.
'''
```  

### 9.4.2 在一个模块中存储多个类
可根据需要在一个模块中存储任意数量的类。我们将类Battery和类ElectricCar加入模块car.py中。然后新建一个my_electric_car.py的文件，导入ElectricCar类，并创建一辆电动汽车：
```python
class Battery():
    '''模拟电动汽车电瓶'''
    
    def __init__(self, battery_size=70):
        self.battery_size = battery_size
        
    def describe_battery(self):
        print("This car has a " + str(self.battery_size) + "-kWh battery.")
        
    def get_range(self):
        '''打印一条描述电瓶续航里程的消息'''
        
        if self.battery_size == 70:
            range = 240
        elif self.battery_size == 85:
            range = 270
            
        message = "This car can go approximately " + str(range)
        message += " miles on a full charge."
        print(message)
        
class ElectricCar(Car):
    '''模拟电动汽车'''
    
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        self.battery = Battery()
```  
创建电动汽车：
```python
from car import ElectricCar

my_tesla = ElectricCar('tesla', 'model s', 2020)

print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.battery.get_range()
'''
输出结果为：
2020 Tesla Model S
This car has a 70-kWh battery.
This car can go approximately 240 miles on a full charge.
'''
```  

### 9.4.3 从一个模块中导入多个类
可根据需要在程序中导入任意数量的类。  
比如，如果要在一个程序中创建普通汽车和电动汽车时，就将Car类和ElectricCar类都导入：
```python
from car import Car, ElectricCar

my_mclaren = Car('mclaren', 'p1', 2021)
print(my_mclaren.get_descriptive_name())

my_tesla = Car('tesla', 'model s', 2020)
print(my_tesla.get_descriptive_name())
'''
输出结果为：
2021 Mclaren P1
2020 Tesla Model S
'''
```  

### 9.4.4 导入整个模块
可以导入整个模块，再使用句点表示法访问所需要的类。  
```python
import car

my_mclaren = car.Car('mclaren', 'p1', 2021)
print(my_mclaren.get_descriptive_name())
```  

### 9.4.5 导入模块中的所有类
用下面的语法：
```python
from module_name import *
```  
但是不推荐使用这种方式。这种方式没有明确指出使用了哪些类，还有可能导致名称方面的错误。如果要从一个模块中导入很多类时，最好使用上一节的方式导入整个模块。  

### 9.4.6 在一个模块中导入另一个模块
有时候，需要将类分散到多个模块中，以免模块太大。  
例如，我们将Car类存储在一个模块里，Battery类和ElectricCar类存储在另一个模块里。由于ElectricCar类需要访问其父类Car，所以需要将Car类导入这个模块中。当要创建实例时，从每个模块导入所需的类。  

### 9.4.7 自定义工作流程
一开始应让代码结构尽可能简单，先尽量在一个文件中完成所有的工作，确定一切正确运行后，再将类移到独立的模块中。  

## 9.5 Python标准库
Python标准库是一组模块，安装的Python都包含它。现在尝试使用别人编写好的模块，模块collections中的一个类OrderedDict。  
我们之前提到字典只关注键值对，不关注其顺序。如果想要记录顺序的话，可以使用上述这个类。
```python
from collections import OrderedDict

favorite_languages = OrderedDict()

favorite_languages['jen'] = 'python'
favorite_languages['sarah'] = 'c'
favorite_languages['edward'] = 'ruby'
favorite_languages['phil'] = 'python'

for name, language in favorite_languages.items():
    print(name.title() + "'s favorite language is " + 
            language.title() + ".")
'''
输出结果为：
Jen's favorite language is Python.
Sarah's favorite language is C.
Edward's favorite language is Ruby.
Phil's favorite language is Python.
'''
```  

## 9.6 类编码风格
* 类名采用驼峰命名法，即类名的每个单词首字母大写，单词之间不使用下划线，实例名和模块名都小写，单词间加下划线；
* 对于每个类，都应紧跟在定义后面包含一个文档字符串，描述其功能，每个模块也应当在开头对其中的类进行描述；
* 使用空行来组织代码，但不要滥用。在类中，使用一个空行分隔方法，在模块中，使用两个空行分隔类；
* 如果要同时导入标准库的模块和自己编写的模块，先导入标准库的模块，然后空一行，再导入自己编写的模块；