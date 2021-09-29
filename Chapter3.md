# 第三章 列表简介  

## 3.1 列表是什么  

*列表* 由一系列按特定顺序排列的元素组成。  
用方括号[]表示列表，用逗号分隔元素。  
通常给列表指定一个表示复数的名称，如names, letters等等。  

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
```

### 3.1.1 访问列表元素

指出列表名称，再指出元素索引。  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0].title())
```

### 3.1.2 索引从0而不是1开始

第一个列表元素索引为0。
索引为-1可以返回列表最后一个元素，  
-2返回列表倒数第二个元素，以此类推。  

### 3.1.3 使用列表中的各个值

可以像使用变量一样使用列表中的值。

## 3.2 修改、添加和删除元素

### 3.2.1 修改列表元素

通过索引访问元素直接赋值。  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
bicycles[0] = 'giant'
print(bicycles)
```

### 3.2.2 在列表中添加元素

1. 在列表末尾添加新元素
用方法append()，将新元素添加到列表末尾。  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
bicycles.append('giant')
print(bicycles)
```  
方法append()也可以直接对空列表进行操作。

2. 在列表中插入元素  
用方法insert()，要指定索引和值。  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
bicycles.insert(0, 'giant')
print(bicycles)
```  

### 3.2.3 从列表中删除元素

1. 根据位置，使用del语句删除  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
del bicycles[0]
print(bicycles)
```  
2. 使用方法pop()弹出列表最后一个元素  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
popped_bicycle = bicycles.pop()
#使用过方法pop()之后，最后一个元素'specialized'就被删除了
print(bicycles)
```  
3. 使用方法pop()弹出任意位置处的元素
在方法pop()的括号里指定索引值，可以弹出指定位置的元素
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
popped_bicycle = bicycles.pop(0)
#这里就是第一个元素'trek'被删除了
print(bicycles)
```  
4. 根据值，使用方法remove()删除元素
不知道元素位置，但知道元素值，这种情况下要删除元素，可以使用方法remove()，在括号里指定要删除的元素的值即可。  
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
bicycles.remove('cannondale')
print(bicycles)
#注意：如果要删除的值在列表中出现多次的话，
#方法remove()只能删除第一个指定的值。
```  

## 3.3 组织列表  

### 3.3.1 使用方法sort()对列表进行永久性排序
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)
cars.sort()
print(cars)

#还可以按字母顺序反向排列
#向sort()方法传递参数reverse=True
cars.sort(reverse=True)
print(cars)
```  

### 3.3.2 使用函数sorted()对列表进行临时排序
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']

print("Here is the original list:")
print(cars)

print("\nHere is the sorted list:")
print(sorted(cars))

print("\nHere is the original list again:")
print(cars)

#如果要临时倒着排序的话，也同样传递参数reverse=True
print("\nHere is the reversed list:")
print(sorted(cars, reverse=True))
```  

### 3.3.3 倒着打印列表
要按与原顺序相反的顺序打印列表，可以使用方法reverse()。
这个方法是永久性的，但是要想恢复成原来的顺序的话，只要再用一次此方法就行了。
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)
cars.reverse()
print(cars)
```  

### 3.3.4 确定列表的长度
使用函数len()
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)
print(len(cars))
```  

