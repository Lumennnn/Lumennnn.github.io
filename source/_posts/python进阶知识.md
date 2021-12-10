---
title: python进阶知识
date: 2021-08-06 21:41:37
index_img: https://resource.liangzai.online/resource/python.png
categories:
  - 计算机学习
tags:
  - pythoh
---


## 进阶知识

<!-- more -->

**Python 中函数带括号和不带括号的区别**：
>
> 1. 不带括号时，调用的是这个函数本身，是整个函数体，是一个函数对象，不需要等待该函数执行完成
> 2. 带括号（此时必须传入需要的参数），调用的函数的return结果，需要等待函数执行完成的结果
> 3. 如果函数本身带有参数的时候，带括号就必须带参数，同理，函数本身不带参数，带括号就不能带参数

范例：

```python
def a(x)
    print("!")
    return x
print(a)
print(a(10))
```

输出结果：

```cmd
<function a at 0x>
10
```

**函数参数**：
![python参数](python参数.jpg)

### 函数参数

#### 形式参数

形参即在定义函数时，括号内声明的参数。本质上是一个变量名，用来接受外部传来的值

#### 实际参数

实参即调用函数时，括号内传入的值，值可以是常量、变量、表达式或三者的组合

#### 形参与实参的具体使用

1. 位置参数

   在定义函数时，按照从左到右的顺序依次定义形参，称为位置形参，凡是按照这种形式定义的形参都必须被传值

   在调用函数时，按照从左到右的顺序依次定义实参，称为位置实参，凡是按照这种形式定义的实参会按照从左到右的我顺序与形参一一对应

2. 关键字参数

   在调用函数时，实参可以是 key=value 的形式，称为关键字参数，凡是按照这种形式定义的实参，可以完全不按照从左到右的顺序定义，但仍能为指定的形参赋值

   需要注意在调用函数时，实参也可以是按位置或按关键字的混合使用，但必须保证关键字参数在位置参数后面，且不可以对一个形参重复赋值

3. 默认参数

   在定义函数时，就已经为形参赋值，这类形参称之为默认参数，当函数有多个参数时，需要将值经常改变的参数定义成位置参数，而将值改变较少的参数定义成默认参数。

    > 默认参数必须在位置参数之后
    > 默认参数的值仅在函数定义阶段被赋值一次

4. 可变长参数

   + 可变长度的位置参数

      如果在最后一个形参名前加\*号，那么在调用函数时，溢出的位置实参，都会被接收，以*元组*的形式保存下来赋值给该形参

      如果我们事先生成了一个列表，仍然是可以传值给 \*args 的
      如果形参为常规参数（位置或默认），实参仍可以是 \* 的形式
      注意：如果在传入 L 时没有加 *, 那 L 就只是一个普通的位置参数

   + 可变长度的关键字参数

      如果在最后一个形参名前加\*\*号，那么在调用函数时，溢出的关键字参数，都会被接收，以*字典*的形式保存下来赋值给该形参

      如果我们事先生成了一个字典，仍然是可以传值给 \*\*kwargs的
      如果形参为常规参数（位置或默认），实参仍可以是 \*\* 的形式
      注意：如果在传入 dic 时没有加 \*\*, 那 dic 就只是一个普通的位置参数了

5. 命名关键字参数

   想要限定函数的调用者必须以 key=value 的形式传值，Python3 提供了专门的语法：需要在定义形参时，用\*作为一个分隔符号，\*号之后的形参称为命名关键字参数。对于这类参数，在函数调用时，必须按照 key=value 的形式为其传值，且必须被传值

   命名关键字参数也可以有默认值，从而简化调用

   如果形参中已经有一个\*args 了，命名关键字参数就不再需要一个单独的 \*作为分隔符号了

6. 组合使用

   所有参数可任意组合使用，但定义顺序必须是：位置参数、默认参数、args、命名关键字参数、\*kwargs

   可变参数\*args 与关键字参数\*\*kwargs 通常是组合在一起使用的，如果一个函数的形参为\*args与\*\*kwargs，那么代表该函数可以接收任何形式、任意长度的参数

   在该函数内部还可以把接收到的参数传给另外一个函数

   ```python
   def func(x, y, z):
      print(x, y)

   def wrapper(*args, **kwargs):
      func(*args, **kwargs)

   wrapper(1, z=3, y=2)
   ```

   输出：

   ```bash
   1 2 3
   ```

**装饰器**：

### 在代码运行期间动态增加功能的方式，称之为 “装饰器”（Decorator）

函数也是对象，它有__name__等属性，但经过decorator装饰之后的函数，它们的__name__已经改变为装饰器中的函数名，所以需要把原始函数的__name__等属性复制到装饰器中的函数中，否则，有些依赖函数签名的代码执行就会出错。不需要编写 wrapper.__name__ = func.__name__这样的代码，Python 内置functools.wraps 就是干这个事的，所以，一个完整的 decorator 的写法如下：

```python
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('{} {}():'.format(text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

### @property

@property 装饰器来创建只读属性，@property 装饰器会将方法转换为相同名称的只读属性 , 可以与所定义的属性配合使用，这样可以防止属性被修改。

1. 修饰方法，是方法可以像属性一样访问

   ```python
   class DataSet(object):
     @property
     def method_with_property(self): # 含有@property
         return 15
     def method_without_property(self): # 不含@property
         return 15

   l = DataSet()
   print(l.method_with_property) # 加了@property后，可以用调用属性的形式来调用方法,后面不需要加（）。
   print(l.method_without_property())  # 没有加@property , 必须使用正常的调用方法的形式，即在后面加()
   # 两个都输出为 15
   ```

2. 与所定义的属性配合使用，这样可以防止属性被修改。

   由于 python 进行属性的定义时，没办法设置私有属性，因此要通过 @property 的方法来进行设置。这样可以隐藏属性名，让用户进行使用的时候无法随意修改。

   ```python
   class DataSet(object):
      def __init__(self):
         self._images = 1
         self._labels = 2 #定义属性的名称
      @property
      def images(self): #方法加入@property后，这个方法相当于一个属性，这个属性可以让用户进行使用，而且用户有没办法随意修改。
         return self._images
      @property
      def labels(self):
         return self._labels
      l = DataSet()
   #用户进行属性调用的时候，直接调用images即可，而不用知道属性名_images，因此用户无法更改属性，从而保护了类的属性。
      print(l.images) # 加了@property后，可以用调用属性的形式来调用方法,后面不需要加（）。
   ```

**魔法函数**：
