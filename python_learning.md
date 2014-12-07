#《The Python Tutorial》 learning

##Data Struct
###lambda

	# map example
	for d in map(lambda x: x ** 2, range(2, 25)):
		print d
	for d in map(lambda x, y: (x + y) ** 2, range(2, 25), range(2, 25)):
		print d
	
	# filter example
	print filter(lambda x: x % 2 != 0, range(2, 25))
	
	# reduce example (add all)
	print reduce(lambda x,y: x + y, range(1, 5))

###List Comprehensions

	print [x ** 2 for x in range(10)]
	print [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
	
###tuple
在python里面，tuple就像是多个由逗号隔开的数据类型的压缩

	x = 1,2,3
	x1, x2, x3 = x
	
由此，python里面就可以支持所谓的多值返回，print也支持多值。tuple给人的感觉和list很像，但目的和使用场景却不同。tuple就像是一种特殊的list类型

[详细区别](http://stackoverflow.com/questions/626759/whats-the-difference-between-list-and-tuples)

###sets
>Python also includes a data type for sets. A set is an unordered collection with no duplicate elements. Basic uses include membership testing and eliminating duplicate entries. Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.
	
	>>> a = set('abracadabra')
	>>> b = set('alacazam')
	>>> a                                  # unique letters in a
	set(['a', 'r', 'b', 'c', 'd'])
	>>> a - b  

###Dictionaries
>Tuples can be used as keys if they contain only strings, numbers, or tuples; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key. You can’t use lists as keys, since lists can be modified in place using index assignments, slice assignments, or methods like append() and extend().

	>>> tel = {'jack': 4098, 'sape': 4139}
	>>> tel['guido'] = 4127
	>>> tel
	{'sape': 4139, 'guido': 4127, 'jack': 4098}
	>>> tel['jack']
	4098
	>>> del tel['sape']
	>>> tel['irv'] = 4127
	>>> tel
	{'guido': 4127, 'irv': 4127, 'jack': 4098}
	>>> tel.keys()
	['guido', 'irv', 'jack']
	>>> 'guido' in tel
	True

##Module
###6.1.2. The Module Search Path
>When a module named spam is imported, the interpreter first searches for a built-in module with that name. If not found, it then searches for a file named spam.py in a list of directories given by the variable sys.path. sys.path is initialized from these locations:
	the directory containing the input script (or the current directory).
	PYTHONPATH (a list of directory names, with the same syntax as the shell variable PATH).
	the installation-dependent default.
After initialization, Python programs can modify sys.path. The directory containing the script being run is placed at the beginning of the search path, ahead of the standard library path. This means that scripts in that directory will be loaded instead of modules of the same name in the library directory.

##Input and Output

##Errors and Exceptions
	import sys

	class MyError(Exception):
		def __init__(self, value):
			self.value = value
	try:
		if True:
			raise MyError(1)
	except MyError as e:
		print 'cccc'

##class
