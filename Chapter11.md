# 第十一章 测试代码

## 11.1 测试函数
首先学习测试函数。下面是一个返回整洁姓名的函数：
```python
def get_formatted_name(first, last):
    '''生成一个整洁的姓名'''
    full_name = first + " " + last
    return full_name.title()
```  
下面是一个使用这个函数的程序：
```python
from name_function import get_formatted_name

print("Enter 'q' at any time to quit.")

while True:
    first = input("\nPlease give me a first name: ")
    if first == 'q':
        break
    last = input("Please give me a last name: ")
    if last == 'q':
        break
    
    formatted_name = get_formatted_name(first, last)
    print("\tNeatly formatted name: " + formatted_name + ".")
'''
Enter 'q' at any time to quit.

Please give me a first name: jonis
Please give me a last name: joplin
        Neatly formatted name: Jonis Joplin.

Please give me a first name: q
'''
```  
现在我们需要对函数get_formatted_name()进行扩展，比如使其能够处理中间名。但是在扩展的过程中，可能会对函数造成一定的破坏，比如可能会破坏函数原先处理只有名和姓这种情况的功能。所以，在对函数扩展之后我们需要对函数进行测试，确保我们新加入的修改没有破坏原先的功能。当然，我们可以使用上述的程序输入jonis joplin这样的姓名进行手动测试，但是这样很麻烦。Python提供了一种自动测试函数输出的高效方式。  

### 11.1.1 单元测试和测试用例
Python标准库中的模块unittest提供了代码测试工具。  
* **单元测试**用于核实函数的某个方面没有问题；
* **测试用例**是一组单元测试，这些单元测试一起核实函数在各种情形下的行为都符合要求；
* **全覆盖式测试用例**包含一整套单元测试，涵盖各种可能的函数使用方式。  

### 11.1.2 可通过的测试
为函数编写测试用例，首先要导入模块unittest和要测试的函数，再创建一个继承unittest.TestCase的类，并编写一系列方法对函数行为的不同方面进行测试。  
下面是只包含一个方法的测试用例，检查函数get_formatted_name()在给定名和姓时能否正确地工作：
```python
import unittest
from name_function import get_formatted_name

class NamesTestCase(unittest.TestCase):
    '''测试name_function.py'''
    
    def test_first_last_name(self):
        '''能正确处理像Janis Joplin这样的名字吗'''
        
        formatted_name = get_formatted_name('janis', 'joplin')
        self.assertEqual(formatted_name, 'Janis Joplin')
        
unittest.main()
```  
我们创建了一个名为NamesTestCase的类，用于包含一系列要对函数get_formatted_name()进行的单元测试的方法。给其命名时最好让其看上去与被测试函数相关，并包含Test字样。这个类必须继承unittest.TestCase类。  

在这里，NamesTestCase类只包含了一个方法test_first_last_name()，用于测试get_formatted_name()的一个方面。当我们运行这个程序时，所有以test_打头的方法都将自动运行。  

assertEqual()是一个**断言方法**，这是unittest类最有用的功能之一。断言方法用来核实得到的结果是否与期望的结果一致。在这里，我们调用了get_formatted_name()这个函数，向其传递了'janis', 'joplin'两个实参，并将返回值存入了formatted_name这个变量。formatted_name是函数运行的结果，而'Janis Joplin'是我们期望得到的结果。代码
```python
self.assertEqual(formatted_name, 'Janis Joplin')
```  
就是将二者进行比较。输出如下：
```python
'''
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
'''
```  
第一行的句点表示有一个测试通过了，接下来的一行指出Python运行了一个测试，耗时不到0.001秒。最后的OK表明该测试用例中的所有单元测试都通过了。  

### 11.1.3 不能通过的测试
现在我们对函数get_formatted_name()进行扩展，使其能够处理中间名：
```python
def get_formatted_name(first, middle, last):
    '''生成一个整洁的姓名'''
    full_name = first + " " + middle + " " + last
    return full_name.title()
```  
然后我们用之前的程序来测试这个添加了修改的函数，得到下面的结果：
```python
'''
E
======================================================================
ERROR: test_first_last_name (__main__.NamesTestCase)
能正确处理像Janis Joplin这样的名字吗
----------------------------------------------------------------------
Traceback (most recent call last):
  File "E:\masterpre\pywork\test_name_function.py", line 10, in test_first_last_name
    formatted_name = get_formatted_name('janis', 'joplin')
TypeError: get_formatted_name() missing 1 required positional argument: 'last'

----------------------------------------------------------------------
Ran 1 test in 0.001s

FAILED (errors=1)
'''
```  
第一行的字母E指出测试用例中有一个单元测试导致了错误；  

接下来的一段指出是方法test_first_last_name()导致了错误；  

第三段是一个traceback，指出错误是由于调用函数get_formatted_name()时少了一个必须要有的位置实参；  

最后一段指出整个测试用例未通过，因为发生了一个错误。  

### 11.1.4 测试未通过时怎么办
如果检查条件没错的话，测试没通过就是函数代码有问题。这时，需要检查对函数添加的修改，找出导致函数行为不符合预期的修改。  

在这个例子中，原来的get_formatted_name()只接受两个实参，就是名和姓，但现在要求三个实参：名、中间名和姓。修改的办法就是让中间名变成可选的：
```python
def get_formatted_name(first, last, middle=''):
    '''生成一个整洁的姓名'''
    if middle:
        full_name = first + " " + middle + " " + last
    else:
        full_name = first + " " + last
    return full_name.title()
```  
再次运行测试程序，得到如下结果：
```python
'''
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
'''
```  
测试通过了。这样我们就知道我们对函数新添加的修改没有破坏函数原来的行为了。  

### 11.1.5 添加新测试
我们还需要再添加一个测试，用于测试函数是否能够正确处理有中间名的情况。为此，我们需要在NameTestCase类中再添加一个方法，注意方法名必须是test_打头的！
```python
import unittest
from name_function import get_formatted_name

class NamesTestCase(unittest.TestCase):
    '''测试name_function.py'''
    
    def test_first_last_name(self):
        '''能正确处理像Janis Joplin这样的名字吗'''
        
        formatted_name = get_formatted_name('janis', 'joplin')
        self.assertEqual(formatted_name, 'Janis Joplin')
        
    def test_first_middle_last_name(self):
        '''能正确处理像Wolfgang Amadeus Mozart这样的名字吗'''
        
        formatted_name = get_formatted_name('wolfgang', 'mozart', 'amadeus')
        self.assertEqual(formatted_name, 'Wolfgang Amadeus Mozart')
        
unittest.main()
```  
我们给这个方法命名为test_first_middle_last_name()，方法名必须是描述性的。方法名很长也是允许的。  
测试结果如下：
```python
..
----------------------------------------------------------------------
Ran 2 tests in 0.001s

OK
```  
两个测试都通过了。  

## 11.2 测试类
下面学习针对类的测试。  

### 11.2.1 各种断言方法
之前说过，断言方法检查你认为应该满足的条件是否确实满足。下表时6个常用的断言方法，只能在继承unittest.TestCase的类中使用这些方法。  
| 方法 | 用途 |
| ---- | ---- |
| assertEqual(a, b) | 核实a == b |
| assertNotEqual(a, b) | 核实a != b |
| assertTrue(x) | 核实x为True |
| assertFalse(x) | 核实x为False |
| assertIn(item, list) | 核实item在list中 |
| assertNotIn(item, list) | 核实item不在list中 |

### 11.2.2 一个要测试的类
首先，我们要有一个类。来看一个帮助管理匿名调查的类：
```python
class AnonymousSurvey():
    '''收集匿名调查问卷的答案'''
    
    def __init__(self, question):
        '''存储一个问题，并为存储答案做准备'''
        self.question = question
        self.responses = []
        
    def show_question(self):
        '''显示调查问卷'''
        print(self.question)
        
    def store_response(self, new_response):
        '''存储单份调查问卷'''
        self.responses.append(new_response)
        
    def show_results(self):
        '''显示收集到的所有答案'''
        print("Survey results:")
        for response in self.responses:
            print("- " + response)
```  
下面是一个使用上面类的程序：
```python
from survey import AnonymousSurvey

#定义一个问题，并创建一个表示调查的AnonymousSurvey对象
question = "What language did you first learn to speak?"
my_survey = AnonymousSurvey(question)

#显示问题并存储答案
my_survey.show_question()
print("Enter 'q' at any time to quit.\n")
while True:
    response = input("Language: ")
    if response == 'q':
        break
    my_survey.store_response(response)
    
#显示调查结果
print("\nThank you to everyone who participated in the survey!")
my_survey.show_results()
'''
运行结果：
What language did you first learn to speak?
Enter 'q' at any time to quit.

Language: Chinese
Language: English
Language: German
Language: q

Thank you to everyone who participated in the survey!
Survey results:
- Chinese
- English
- German
'''
```  
如果我们想对类进行改进，就可能会存在风险，影响AnonymousSurvey类的当前行为。所以需要编写一个针对这个类的测试。  

### 11.2.3 测试AnonymousSurvey类
下面来编写一个测试，对AnonymousSurvey类的行为的一个方面进行验证：如果用户面对调查只提供了一个答案，那么这个答案也能被妥善地存储。这里，我们将使用断言方法assertIn()来核实答案是否被保存在列表中了：
```python
import unittest
from survey import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
    '''针对AnonymousSurvey类的测试'''
    
    def test_store_single_response(self):
        '''测试单个答案会被妥善存储'''
        question = "What language did you first learn to speak?"
        my_survey = AnonymousSurvey(question)
        my_survey.store_response('Chinese')
        
        self.assertIn('Chinese', my_survey.responses)
        
unittest.main()
'''
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
'''
```  
测试通过。但是这里我们检查的是只收集一种答案的情况。下面来核实当用户提供了三个答案时，也会被妥善保存。我们需要在TestAnonymousSurvey类中新增一个方法：
```python
import unittest
from survey import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
    '''针对AnonymousSurvey类的测试'''
    
    def test_store_single_response(self):
        '''测试单个答案会被妥善存储'''
        question = "What language did you first learn to speak?"
        my_survey = AnonymousSurvey(question)
        my_survey.store_response('Chinese')
        
        self.assertIn('Chinese', my_survey.responses)
        
    def test_store_three_responses(self):
        '''测试三个答案会被妥善保存'''
        question = "What language did you first learn to speak?"
        my_survey = AnonymousSurvey(question)
        responses = ['Chinese', 'English', 'German']
        for response in responses:
            my_survey.store_response(response)
        
        for response in responses:
            self.assertIn(response, my_survey.responses)
        
unittest.main()
'''
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
'''
```  
两个测试都通过。但是我们注意到测试单个答案和三个答案的这两个方法中，代码有重复的地方：在两个方法中，都创建了AnonymousSurvey实例以及一些答案。我们可以使用下一小节unittest的另一项功能来提高效率。  

### 11.2.4 方法setUp()
unittest.TestCase类包含方法setUp()。如果在TestCase类中包含了方法setUp()，Python将先运行它，然后再运行各个以test_打头的方法。所以我们可以在setUp()内创建所需的对象一次，然后之后就可以在后面的每个测试方法中使用它们了。   
下面使用setUp()来创建一个AnonymousSurvey对象以及一组答案，供方法test_store_single_response()和test_store_three_responses()使用：
```python
import unittest
from survey import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
    '''针对AnonymousSurvey类的测试'''
    
    def setUp(self):
        '''创建一个调查对象以及一组答案，供之后的测试方法使用'''
        question = "What language did you firsr learn to speak?"
        self.my_survey = AnonymousSurvey(question)
        self.responses = ['Chinese', 'English', 'German']
        
    def test_store_single_response(self):
        '''测试单个答案会被妥善存储'''
        self.my_survey.store_response(self.responses[0])
        self.assertIn(self.responses[0], self.my_survey.responses)
        
    def test_store_three_responses(self):
        '''测试三个答案会被妥善存储'''
        for response in self.responses:
            self.my_survey.store_response(response)
        
        for response in self.responses:
            self.assertIn(response, self.my_survey.responses)
            
unittest.main()
'''
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
'''
```  
两个测试都通过了。  
方法setUp()做了两件事：创建了一个AnonymousSurvey调查对象，创建了一个答案列表。存储这二者的变量前有前缀self（即存在属性中），所以这两个可以在这个类的任何地方使用。这样就不用在之后的测试方法中再各自创建对象和答案了。  

注意：运行测试用例时，每完成一个单元测试，Python都会打印一个字符：
* 测试通过时打印一个句点；
* 测试引发错误时打印一个E；
* 测试导致断言失败时打印一个F。