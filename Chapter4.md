# 第四章 操作列表  

## 4.1 遍历整个列表  
用for循环
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician)
```  
列表中的元素会被一一打印出来。

### 4.1.1 深入研究循环  
使用for循环时，每一个元素都会被执行循环指定的操作。
在使用for循环时，可以使用单复数来区分变量和列表，例如：
```python
for dog in dogs:

for cat in cats:

```  
### 4.1.2 在for循环中执行更多的操作
在for下面，每个缩进的代码行都是循环的一部分。  
```python
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("Goodbye, " + magician.title() + ".\n")
```  
### 4.1.3 在for循环结束后执行一些操作
在for循环的后面，遇到没有缩进的代码，该for循环就结束了。
没有缩进的代码只会执行一次。
```python
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("Goodbye, " + magician.title() + ".\n")
print("Thank you!")
```  

## 4.2 避免缩进错误  
python对缩进敏感。
**只在必要情况下缩进，不必要缩进时就不要缩进！**  

## 4.3 创建数值列表  

### 4.3.1 函数range()  
函数range()可以生成一系列数字。
```python
for value in range(2,6):
    print(value)
```
输出的结果为：
2
3
4
5
range()函数不包含所指定的第二个数，到所指定的第二个数的前一个数为止。  

### 4.3.2 使用range()创建数字列表
* 使用函数list()将range()的结果直接转换为列表，
将range()作为list()的参数。
```python
numbers = list(range(1,6))
print(numbers)
```  
输出的结果为：
[1, 2, 3, 4, 5]  

* 使用函数range()还可以指定步长。
```python
even_numbers = list(range(2,11,2))
print(even_numbers)
```
输出结果为：
[2, 4, 6, 8, 10]  

* 使用range()可以创建任意想要的数字集  
例如创建1~10的平方的列表：
```python
squares = []
for value in range(1,11):
    squares.append(value**2)
print(squares)
```  
输出结果为：
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]  

### 4.3.3 对数字列表执行简单的统计计算  
几个函数：
最大值：max()
最小值：min()
总和：sum()
```python
digits = list(range(0,10))
print(min(digits))
print(max(digits))
print(sum(digits))
```  
输出结果为：
0
9
45  

### 4.3.4 列表解析
前面创建1~10平方数列表用了3行代码，其实只需要一行。
列表解析将for循环和创建新元素的代码合并成一行，并自动附加新元素。  
```python
squares2 = [value**2 for value in range(1,11)]
print(squares2)
```  

## 4.4 使用列表的一部分

### 4.4.1 切片
切片就是列表的部分元素。
要创建切片，需要指定两个索引值。
用[]括起来，用冒号:隔开。
切片从第一个索引值指定的元素开始，
到第二个索引值的前一个元素结束。
```python
letters = ['a', 'b', 'c', 'd', 'e']
print(letters[1:3])
```  
输出结果为：
['b', 'c']  

可以不指定起始和终止索引：
* 没有起始索引：默认从列表开头开始提取；
* 没有终止索引：默认直到列表最后；
* 支持负数起止索引；  

### 4.4.2 遍历切片
如果要便利列表中的部分元素，可以在for循环中使用切片。
```python
letters = ['a', 'b', 'c', 'd', 'e']
for letter in letters[1:4]:
    print(letter)
```  
输出结果为：
b
c
d  

### 4.4.3 复制列表
我们可能会想要对一个列表进行复制然后再进行不同的操作，
但是复制列表不能简单地使用列表名称进行赋值！！
比如下面这种是错的！
```python
#numbers1列表包含1，2，3，
#我们需要对这个列表复制，放到numbers2里，
#然后numbers1列表添加数字4，
#numbers2列表添加数字5
#我们期望输出结果为numbers1是1234，numbers2是1235
numbers1 = [1, 2, 3]
numbers2 = numbers1

numbers1.append(4)
numbers2.append(5)

print(numbers1)
print(numbers2)
```  
输出结果为：
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5]  
与期望不一致，原因在于复制的方式不对。
numbers2 = numbers1  
这个语句相当于将指向[1, 2, 3]这个列表起始的指针赋值给了numbers2，
这时numbers1和numbers2是两个指向同样列表[1, 2, 3]的指针。
所以后面看上去是在对两个列表进行不同的操作，实际上是对同一个列表进行了所有的操作。  

正确的方式如下：
要复制列表，就要创建一个包含整个列表的切片，省略起始和终止索引。
```python
numbers1 = [1, 2, 3]
numbers3 = numbers1[:]
numbers1.append(4)
numbers3.append(5)
print(numbers1)
print(numbers3)
```  
输出结果为：
[1, 2, 3, 4]
[1, 2, 3, 5]
与预期一致。  

## 4.5 元组
列表是在程序运行中是可以不断变化的，但有时候我们可能希望列表的元素不可改变，而不可变的列表称为**元组**。

### 4.5.1 定义元组
元组使用圆括号而不是方括号来标识。定义元组后，就可以访问其元素，就像访问列表元素一样。访问元素的时候，索引用方括号。
```python
numbers = (1, 2, 3)
print(numbers[0])
```  
如果尝试修改元组的元素，程序会报错。
### 4.5.2 遍历元组中的所有值
可以使用for循环。
```python
numbers = (1, 2, 3)
for number in numbers:
    print(number)
```  
输出结果为：
1
2
3  
### 4.5.3 修改元组变量
虽然不能修改元组的元素，但是可以存储元组的变量赋值，即重新定义整个元组。
```python
numbers = (1, 2, 3)
print(numbers)
numbers = (7, 8, 9)
print(numbers)
```  
这种情况下，程序不会报错。