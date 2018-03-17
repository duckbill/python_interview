# chap7 编程数据结构和算法
## Q1:
描述如下：斐波契纳数列1，2，3，5，8，13，21.......根据这样的规律，编程求出400万以内最大的婓波契纳数，并求出它是第几个婓波契纳数。
代码如下：

``` python
#!/usr/bin/python
# -*- coding: utf-8 -*-
first = 1
second = 2
third = 0
target = 0
number = 2

while True:
	third = first + second
	number = number + 1
	print "第 " + str(number) + "个数是：" + "third is " + str(third)

	if third>=4000000 and second<= 4000000:
		target = second
		number = number -1
		break

	first = second
	second = third

print number
print target
```
## Q2:
描述如下：上机编程实现以下功能：
dicta = {"a":1,"b":2,"c":3,"d":4,"f":"hello"}
dictb = {"b":3,"d":5,"e":7,"m":9,"k":"word"}
要求写一段代码，实现两个字典的相加，不同的key对应的值保留，相同的key对应相加后保留，如果是字符串就拼接，如上示例得到结果为：
dict = {“a”:1,"b":5,"c":3,"d":9,"e":7,"m":9,"f":"hello","k":"word"}
代码如下：

``` python
#!/usr/bin/python

dicta = {"a":1,"b":2,"c":3,"d":4,"f":"hello"}
dictb = {"b":3,"d":5,"e":7,"m":9,"k":"word"}

for dicta_key in dicta.keys():
	for dictb_key in dictb.keys():
		if dicta_key == dictb_key:
			dicta[dicta_key] = dicta[dicta_key] + dictb[dictb_key]
			dictb.pop(dicta_key)
for dictb_key, dictb_value in dictb.iteritems():
	dicta[dictb_key] = dictb_value

print dicta
```
**注意**：python字典在迭代的时候不能改变字典的大小，所以如果代码中

## Q3:
描述如下：
海滩上有一堆桃子，五个猴子来分，第一只猴子把这堆桃子平均分成无份，多了一个，这只猴子把最多的一个扔到海里，拿走一份，第二只猴子把剩下的四堆桃子合在一起，又平均分成五份，又多了一个，它同样把多的一个扔到海里，拿走了一份，第三只，第四只，第五只都这样做的，问海滩原来多少个桃子。
