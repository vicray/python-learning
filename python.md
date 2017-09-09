# Python

### 1. 元类
参见文档 [Python 元类(metaclass)](https://www.evernote.com/shard/s328/sh/eb4255e2-b51a-4b73-8adb-45de5cdede8a/f008b01551abc87e7b3f5d12cc60c32d)
		
### 2. Python 自省
编译时不能确定对象的某个字段或者方法名，而是在运行时由对象告知，这种 **在运行时获取未知对象信息** 的手段叫 **自省** (或 **反射** )




### 3. Python函数参数
1. *参数：表示参数存储为一个元祖（tuple）

		def function_with_one_star(*t):
			print (t, type(t))
	
		function_with_one_start(1, 2, 3)
		# 输出结果：{1, 2, 3} <class 'tuple'>
		
2. **参数：表示参数存储的是一个字典(dict)

		def cuntion_with_two_star(**d):
			print (d, type(d))
	
		function_with_two_star(a=1, b=2, c=3)
		# 输出结果： {'a': 1, 'b': 2, 'c': 3} <class 'dict'>	

**注意：** 由于参数的不确定性，带\*或\**的参数必须放在最后：
		
	def funcD(a, b, *c):
		print a
		print b
		print "length of c is:  %d" % len(c)
		print (c, type(c))
	
	funcD(1, 2, 3, 4, 5, 6)
	# 运行结果：
	#  1
	#  2
	#  length of c is 4
	#  (3, 4, 5, 6) <class 'tuple'>


### 4. Python lambda
用来简化单行函数定义
实际上lambda表达式是一个叫简化的函数定义

	g = lambda x: x+1   # g表示一个函数，函数入口参数x， x+1表示函数体
	g(1)  # 输出：2 （1 + 1）
	g(2)  # 输出：3 （2 + 1）
	
	
### 5.  Python中的self，cls
Python中有两种方法：普通方法，类方法(由@classmethod装饰)
1. 普通方法：第一个参数需要self, 表示一个具体的实例
2. classmethod方法：第一个参数是cls，表示类本身

		class A(object):
			def foo1(self):
				print 'Hello ', self
			
			@staticmethod
			def foo2():
				print 'hello staticmethod'
			
			@classmethod
			def foo3(cls):
				print 'hello, 'cls

		a = A()
		a.foo1()       # 输出： Hello <__main__.A object at 0x9f6abec>
		A.foo1(a)     # 输出： Hello <__main__.A object at 0x9f6abec>
		A.foo2()       # 输出：hello staticmethod 
		A.foo3()       # 类方法，第一个参数必须为类本身，输出： hello <class '__main__.A'>
		A                 # 输出：<class '__main__.A'
	

### 6. Python yield
一个带有 yield 的函数就是一个 generator，它和普通函数不同，生成一个 generator 看起来像函数调用，但不会执行任何函数代码，直到对其调用 next()（在 for 循环中会自动调用 next()）才开始执行。虽然执行流程仍按函数的流程执行，但每执行到一个 yield 语句就会中断，并返回一个迭代值，下次执行时从 yield 的下一个语句继续执行。看起来就好像一个函数在正常执行的过程中被 yield 中断了数次，每次中断都会通过 yield 返回当前的迭代值。
yield 的好处是显而易见的，把一个函数改写为一个 generator 就获得了迭代能力，比起用类的实例保存状态来计算下一个 next() 的值，不仅代码简洁，而且执行流程异常清晰。