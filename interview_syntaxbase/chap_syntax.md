

# chap1 python语言特性

## 1 python的函数参数传递

>例子1：

```python
a = 1
def fun(a):
	a = 2
	print id(a)

fun(a)
print a
print id(a)
```
输出结果：

```sh
140586339311568
1
140586339311592
```
*tag：全局变量，局部变量*


>例子2

```python
a = []
def fun(a):
	a.append(1)
	print id(a)
fun(a)
print a
print id(a)
```
输出结果：

```sh
4363431880
[1]
4363431880
```

总结：
- 所有的变量都可以理解是内存中一个对象的“引用”，或者，也可以看似c中void*的感觉。
- 有人说当数字超过255时候会出现这么一个概念“小整数对象池”：python在执行的时候，为了节约空间，帮我们创建好了小整数对象池，[-5~256]，都是固定的地址，不管你用不用，都会存在。a=1000,b=1000,这时会给a一个地址，也会给b一个地址，但他们都不相等。也有人说在python3.0中，python中缓存了0到255的数字，所以在这范围内的字面值的变量的地址都一样 。但是我在在线python3中测试超过255结果id也是一样的。
*参考《python源码剖析》*
- 通过`id`来看引用`a`的内存地址
这里记住的是类型是属于对象的，而不是变量。而对象有两种,**“可更改”**（mutable）与“不可更改”（immutable）对象。**在python中，strings, tuples, 和numbers是不可更改的对象，而 list, dict, set 等则是可以修改的对象。**(这就是这个问题的重点)

当一个引用传递给函数的时候,函数自动复制一份引用,这个函数里的引用和外边的引用没有半毛关系了.所以第一个例子里函数把引用指向了一个不可变对象,当函数返回的时候,外面的引用没半毛感觉.而第二个例子就不一样了,函数内的引用指向的是可变对象,对它的操作就和定位了指针地址一样,在内存里进行修改.

如果还不明白的话,这里有更好的解释: http://stackoverflow.com/questions/986006/how-do-i-pass-a-variable-by-reference

*参考*[python变量和内存](http://blog.csdn.net/msdnwolaile/article/details/50371991)Python 存储变量的方法跟其他 OOP 语言不同。它与其说是把值赋给变量，不如说是给变量建立了一个到具体值的 reference。

## 2 详解python相对引入和绝对引入

>前言：我记得我第一次接触绝对和相对的概念时是大学的时候学习html时候提到的『绝对路径』和『相对路径』。其实这里的绝对引入和相对引入是相对于『包内引入』而言的。
> 『包内导入』：包内部模块导入包内的模块。好比一个家庭里你没有手机你借你哥哥的手机玩。而不是去邻居家借你的好伙伴的手机玩一样。

 ----

### 2.1 为什么需要import
代码重复利用，分层设计，结构更加清晰。类似C里面`include<>`
### 2.2 需要知道的名词
**模块:** 模块通常是个文件，可以作为mnodule的文件类型：“.py”、“.pyo”、“.pyd”、“.so”、“.dll”
**包：** 通常是个文件夹，随便一个文件夹可不是包哦，约定文件夹中含有`__init__.py`的才算。如果文件里的子文件夹也有`__init__.py`那么这个文件可作为一个子包。

### 2.3 python import的搜索路径
- 在当前目录下搜索该模块
- 在环境变量PYTHONPATH中指定路径列表以此搜索
- 在Python安装路径的lib库中搜索

### 2.3 python import步骤
python所有加载的模块信息都存放在`sys.modules`结构中，当import一个
> #### 参考：[python import详解]()

## 3 Python中的元类(metaclass)
这个非常的不常用,但是像ORM这种复杂的结构还是会需要的，具体参考[https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python](https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python)

## 4 python浅copy和深copy
