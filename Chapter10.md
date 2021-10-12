# 第十章 文件和异常

## 10.1 从文件中读取数据
文本文件可以存储很多信息，要使用其中的信息，首先要将信息读取到内存中。为此，可以一次性读取全部内容，也可以每次一行的方式逐步读取。  

### 10.1.1 读取整个文件
我们有一个小数点后30位的圆周率值，现在尝试读取并打印出来。  
```python
with open('pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents.rstrip())
'''
输出结果为：
3.1415926535
  8979323846
  2643383279
'''
```  
首先，要访问一个文件，必须先打开它。函数open()接受一个参数：要打开文件的名称。Python在当前执行文件所在的目录找到这个文件，返回一个表示文件的对象。  
关键字with在不再需要访问文件后将其关闭。这里，我们只调用了open()，没有调用close()。当然，我们可以自己调用open()和close()函数来打开和关闭文件，但如果程序出现bug，导致close()语句未执行，文件未关闭，可能会导致数据丢失或受损。使用with之后，Python会在合适的时候自动将其关闭。  
有了文件对象之后，使用方法read()，读取文件的全部内容，并将其作为一个长字符串存储到变量contents中，然后打印这个变量就能显示出来了。多的空行是由于read()到达文件末尾会返回一个空的字符串，显示出来就是一个空行，要删除的话，就用rstrip()。  

### 10.1.2 文件路径
如果要读取的文件不在当前执行文件所在的目录，则需要提供文件路径。  
如果要读取的文件在当前执行文件所在文件夹的子文件夹下，可以使用相对文件路径。比如，我在Python代码文件所在的文件夹下新建了一个text_files文件夹，用于存储txt文件，文件路径如下，用反斜杠\：
```python
with open('text_files\pi_30_digits.txt') as file_object:
    contents = file_object.read()
    print(contents.rstrip())
'''
输出正确
'''
```  
还可以使用绝对路径，这样就不用关心当前程序存在什么地方了。
```python
file_path = 'E:\\masterpre\\pywork\\text_files\\pi_30_digits.txt'
with open(file_path) as file_object:
    contents = file_object.read()
    print(contents)
'''
输出正确
'''
```  

### 10.1.3 逐行读取
读取文件时，可能会要检查其中的每一行，可以对文件对象使用for循环：  
```python
with open('text_files\pi_30_digits.txt') as file_object:
    for line in file_object:
        print(line.rstrip())
'''
输出结果为：
3.1415926535
  8979323846
  2643383279
'''
```  
这里如果不使用方法rstrip()，输出每一行下面都会出现空白行。  

### 10.1.4 创建一个包含文件各行内容的列表
使用关键字with时，open()返回的文件对象只在with代码块内可用，如果需要在with代码块之外访问文件内容，可以在with代码块内将文件的各行存储在一个列表中。  
下面示例将文件中的各行存到一个列表中，并在with代码块之外打印：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()
    
for line in lines:
    print(line.rstrip())
'''
输出正确
'''
```  
方法readlines()从文件中每读取一行，就将其存入一个列表内，然后该列表被存入变量lines中。在with代码块之外，仍然可以使用lines这个变量。  

### 10.1.5 使用文件的内容
将文件读取之后，就可以使用这些数据了。下面示例是将pi存进一个字符串中：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()
    
pi_string = ''
for line in lines:
    pi_string += line.strip()

print(pi_string)
print(len(pi_string))
'''
输出结果为：
3.141592653589793238462643383279
32
'''
```  

### 10.1.6 包含一百万位的大型文件
之前的例子都是小文件，Python可以处理大型文件。下面示例是精确到小数点后一百万位的圆周率，我们将其存在字符串里并打印前小数点后50位：
```python
file_path = 'text_files\pi_million_digits.txt'

with open(file_path) as file_object:
    lines = file_object.readlines()
    
pi_string = ''
for line in lines:
    pi_string += line.strip()
    
print(pi_string[:52] + "...")
print(len(pi_string))
'''
输出结果为：
3.14159265358979323846264338327950288419716939937510...
1000002
'''
```  

### 10.1.7 圆周率值中包含你的生日吗
检查圆周率小数点后一百万位是否包含自己的生日：
```python
file_path = 'text_files\pi_million_digits.txt'

with open(file_path) as file_object:
    lines = file_object.readlines()
    
pi_string = ''
for line in lines:
    pi_string += line.strip()

birthday = input("Please enter your birthday: ")

if birthday in pi_string:
    digit = pi_string.index(birthday) - 1
    print("Your birthday appears in the first million digits of pi.")
    print("Your birthday appears in the " + str(digit) + "th place after " + 
    " the decimal point.")
else:
    print("Your birthday doesn't appear in the first million digits of pi.")

'''
输出结果为：
Please enter your birthday: 280998
Your birthday appears in the first million digits of pi.
Your birthday appears in the 473438th place after  the decimal point.
'''
```  

## 10.2 写入文件

### 10.2.1 写入空文件
要将文本写入文件，调用open()时要提供另一个实参。下面是一个简单的例子：
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
    file_object.write("I love programming.")
```  
调用open()时，第一个实参是要打开的文件名称，第二个实参'w'是告诉Python我们要以写入模式打开这个文件，还有其他模式：
* 读取模式 'r'
* 写入模式 'w'
* 附加模式 'a'
* 读取和写入模式 'r+'
如果不加模式实参，则默认以只读模式打开。  
如果要写入的文件不存在，函数open()会自动创建。  
**注意：以写入模式'w'打开文件时，如果指定的文件已经存在，Python将在返回文件对象前清空该文件。**  

### 10.2.2 写入多行
函数write()不会在你写入文本的末尾添加换行符。需要的话自己在写入的时候手动添加换行符。  

### 10.2.3 附加到文件
如果要给文件添加内容，而不是覆盖原有内容，可以用附加模式打开文件。  
```python
filename = 'programming.txt'

with open(filename, 'a') as file_object:
    file_object.write("I also love finding meaning in large datasets.\n")
    file_object.write("I love creating apps that can run in a browser.\n")
```  
文件原来的内容没有被删除。  

## 10.3 异常
Python使用名为异常的特殊对象来管理程序运行期间发生的错误。如果编写了处理异常的代码，程序将继续运行，如果没有对异常进行处理，程序会停止，并显示traceback。  
异常是使用try-except代码块处理的，告诉Python发生异常时怎么办。  

### 10.3.1 - 10.3.4 处理ZeroDivisionError异常
我们知道数字除法中，除数不能为0，如果让Python计算比如5/0，就会显示ZeroDivisionError。首先，我们来看一个执行除法的程序：
```python
print("Give me two integers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("First number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    if second_number == 'q':
        break
    answer = int(first_number) / int(second_number)
    print(answer)
    print("\n")
'''
输出结果测试：
Give me two integers, and I'll divide them.
Enter 'q' to quit.
First number: 7
Second number: 2
3.5


First number: 6
Second number: 3
2.0


First number: 5
Second number: 0
Traceback (most recent call last):
  File "E:\masterpre\pywork\ss10.3.1_division.py", line 11, in <module>
    answer = int(first_number) / int(second_number)
ZeroDivisionError: division by zero
'''
```  
我们可以看到，如果除数不为0的话，则一切正常，如果第二个数被用户输入0，则程序停止运行并报错。让用户看到traceback不好，不懂技术的人会被搞糊涂，训练有素的攻击者可以根据这些信息判断出可对代码发起什么样的攻击。  
所以，需要使用try-except代码块对异常进行处理，从而提高程序抵御错误的能力。  
```python
print("Give me two integers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("First number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    if second_number == 'q':
        break
    
    try:
        answer = int(first_number) / int(second_number)
    except ZeroDivisionError:
        print("You can't divide by 0!\n")
    else:
        print(answer)
        print("\n")
'''
输出测试：
Give me two integers, and I'll divide them.
Enter 'q' to quit.
First number: 7
Second number: 2
3.5


First number: 6
Second number: 3
2.0


First number: 5
Second number: 0
You can't divide by 0!

First number: q
'''
```  
try代码块只包含可能导致错误的代码块，在这里也就是执行除法运算的代码。依赖于try代码块成功执行的代码放在else代码块中，在这里，如果除法运算成功，我们就使用else代码块来打印结果。except代码块告诉Python出现ZeroDivisionError异常时该怎么办，在这里，我们打印一条信息告诉用户除数不能为0。这样，程序会继续运行，用户不会看到traceback。  

### 10.3.5 - 10.3.7 处理FileNotFoundError异常
使用文件时，一种常见的问题是找不到文件：可能要找的文件在其他地方、可能文件名不对或者文件不存在。这种情况下，Python会报告FileNotFoundError异常。可以使用try-except代码块来处理。  
比如，我们要打开一个不存在的文件：
```python
filename = 'alice.txt'

with open(filename) as f_obj:
    contents = f_obj.read()
'''
Traceback (most recent call last):
  File "E:\masterpre\pywork\ss10.3.5_alice.py", line 3, in <module>
    with open(filename) as f_obj:
FileNotFoundError: [Errno 2] No such file or directory: 'alice.txt'
'''
```  
果然，报告异常。我们添加try-except代码块：
```python
filename = 'alice.txt'

try:
    with open(filename) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    msg = "Sorry, the file " + filename + " does not exist."
    print(msg)
    
'''
输出：
Sorry, the file alice.txt does not exist.
'''
```  
不再显示traceback，但是这里报告异常之后程序什么都没做，体现不出错误处理代码的意义。看下面的例子。  
我们想要对文本进行分析，看看文本大致包含多少单词。我们首先将整个文本作为一个很长的字符串存储到一个变量中，然后对字符串使用方法split()。这个方法的作用是以空格为分隔符将字符串拆成多个部分，然后将这些部分存储到一个列表中，结果就是一个包含字符串中所有单词的列表（有些单词会带有标点符号）。最后求列表包含多少元素就能确定原来的文本大致包含多少单词。  
```python
filename = 'alice.txt'
filepath = 'text_files\\' + filename 

try:
    with open(filepath) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    msg = "Sorry, the file " + filename + " does not exist."
    print(msg)
else:
    words = contents.split()
    num_words = len(words)
    print("The file " + filename + " has about " + str(num_words) + " words.")
'''
The file alice.txt has about 29461 words.
'''
```  
程序运行正常，现在我们要用这个程序分析多个文件。我们可以将这段代码写成一个函数，然后向函数传递文件名，来计算文件所含单词数。  
```python
def count_words(filename):
    '''计算text_files文件夹下一个文件大致包含多少单词'''
    filepath = "text_files\\" + filename
    try:
        with open(filepath) as f_obj:
            contents = f_obj.read()
    except FileNotFoundError:
        msg = "Sorry, the file " + filename + " does not exist."
        print(msg)
    else:
        words = contents.split()
        num_words = len(words)
        print("The file " + filename + " has about " + str(num_words) 
                + " words.")
                
filenames = [
            'alice.txt', 'siddhartha.txt', 
            'moby_dict.txt', 'little_women.txt',
            ]
for filename in filenames:
    count_words(filename)
'''
The file alice.txt has about 29461 words.
The file siddhartha.txt has about 42172 words.
The file moby_dict.txt has about 215136 words.
The file little_women.txt has about 189079 words.
'''
```  
我们看到输出正常。这时，我们任意删除一个文件，比如我们删除siddhartha.txt，再一次运行程序，输出如下：
```python
'''
The file alice.txt has about 29461 words.
Sorry, the file siddhartha.txt does not exist.
The file moby_dict.txt has about 215136 words.
The file little_women.txt has about 189079 words.
'''
```  
我们可以看到第二个文件不存在不影响对其他文件的分析。如果我们没有对异常进行处理，那么程序在循环到siddhartha.txt这个文件时，就会停下显示traceback报错，剩下的两个文件也不会接着分析。  

### 10.3.8 失败时一声不吭
在前一个例子中，我们告诉用户有一个文件找不到。但有些时候，我们可能会希望程序在发生异常时一声不吭，就像什么都没发生一样。我们只需要在except代码块写一个pass就行了。  

## 10.4 存储数据
有时候需要将用户提供的信息保存下来，即使在程序关闭之后。一种简单的方式是使用模块json来存储数据。模块json能够将简单的Python数据结构转储到文件中，并在程序再次运行时加载该文件中的数据。还可以使用json在不同程序甚至不同语言的程序之间共享数据。  

### 10.4.1 使用json.dump()和json.load()
我们来编写两个程序。第一个程序使用json.dump()来存储一个数字列表，第二个程序使用json.load()加载这个数字列表。  
函数json.dump()接受两个实参：要存储的数据以及用于存储数据的文件对象。  
```python
import json

numbers = [2, 3, 5, 7, 11, 13]

filename = 'numbers.json'

with open(filename, 'w') as f_obj:
    json.dump(numbers, f_obj)
```  
使用文件扩展名.json来指出文件存储的数据为JSON格式。  
再编写下一个程序，使用json.load()将这个列表读取到内存中：
```python
import json

filename = 'numbers.json'

with open(filename) as f_obj:
    numbers = json.load(f_obj)
    
print(numbers)
'''
[2, 3, 5, 7, 11, 13]
'''
```  
这是一种在程序之间共享数据的简单方式。  

### 10.4.2 保存和读取用户生成的数据
对于用户生成的数据，使用json保存它们大有裨益。如果不以某种方式进行存储，程序停止运行时，用户的信息将丢失。来看一个例子：用户首次运行程序时被提示输入自己的名字，这样再次运行程序时就记住他了：
```python
import json

#如果以前存储了用户名，就加载它
#否则，就提示用户输入用户名并存储它

filename = 'username.json'

try:
    with open(filename) as f_obj:
        username = json.load(f_obj)
except FileNotFoundError:
    username = input("What is your name? ")
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
        print("We'll remember you when you come back, " + username + "!")
else:
    print("Welcome back, " + username + "!")
'''
第一次运行：
What is your name? xzt
We'll remember you when you come back, xzt!
再一次运行：
Welcome back, xzt!
'''
```  

### 10.4.3 重构
经常会遇到这样的情况：代码能正确运行，但是可以进一步改进——将代码划分为一系列完成具体工作的函数。这样的过程被称为重构，让代码更清晰、易于理解和扩展。  
接下来，我们对上面的例子进行重构。当然重构不一定是一步到位完成的，而是一步步将函数简化细分，最终使得每个函数只完成一项具体工作。这里我们直接给出最后的结果：
```python
import json

def get_stored_username():
    '''如果存储了用户名，就获取它'''
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        return None
    else:
        return username
        
def get_new_username():
    '''提示用户输入用户名'''
    username = input("What is your name? ")
    filename = 'username.json'
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
        return username
        
def greet_user():
    '''问候用户，并指出其名字'''
    username = get_stored_username()
    if username:
        print("Welcome back, " + username + "!")
    else:
        username = get_new_username()
        print("We'll remember you when you come back, " + username + "!")
        
greet_user()
'''
输出与之前一致
'''
```