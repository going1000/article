#python import note

###Import
一般写php的一定知道，文件一般都需要手动包含进来的。但是python是自动包含的。
python包含的方式
    
    import filename
    # 这种方式的引用，需要加上全名
    class1Obj = filename.class1()
    function1Result = filename.function1()
    
    from filename import class1, class2, function1
    # 这种方式，不需要加全名
    class1Obj = class1()
    function1Result = function1()
    
包含的时候，会在sys.path里找相应的filename已经下面的module。我将sys.path输出

    ['/Volumes/development_env/g1ksTips/python', '/Library/Python/2.7/site-packages/pip-1.5.5-py2.7.egg', '/Library/Python/2.7/site-packages/django_evolution-0.6.9-py2.7.egg', '/Library/Python/2.7/site-packages/MySQL_python-1.2.5-py2.7-macosx-10.9-intel.egg', '/Library/Python/2.7/site-packages/image-1.3.1-py2.7.egg', '/Library/Python/2.7/site-packages/Pillow-2.4.0-py2.7-macosx-10.9-intel.egg', '/Library/Python/2.7/site-packages/RBTools-0.6.1-py2.7.egg', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python27.zip', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-darwin', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac/lib-scriptpackages', '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-tk', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-old', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-dynload', '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/PyObjC', '/Library/Python/2.7/site-packages']

第一个目录是我的文件所在目录，而加载顺序是自前往后遍历目录查找，遇到第一个匹配就结束。

>After initialization, Python programs can modify sys.path. The directory containing the script being run is placed at the beginning of the search path, ahead of the standard library path. This means that scripts in that directory will be loaded instead of modules of the same name in the library directory. This is an error unless the replacement is intended. See section Standard Modules for more information.

###Packages
细心的人会发现，假如我的当前路径里面有个文件夹 libs，sys.path 里是找不到的。即**子文件夹不会被自动加载**。这个时候，就需要使用到python中的package概念。

>Packages are a way of structuring Python’s module namespace by using “dotted module names”. For example, the module name A.B designates a submodule named B in a package named A. Just like the use of modules saves the authors of different modules from having to worry about each other’s global variable names, the use of dotted module names saves the authors of multi-module packages like NumPy or the Python Imaging Library from having to worry about each other’s module names.


>When importing the package, Python searches through the directories on sys.path looking for the package subdirectory.

>The __init__.py files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name, such as string, from unintentionally hiding valid modules that occur later on the module search path. In the simplest case, __init__.py can just be an empty file, but it can also execute initialization code for the package or set the __all__ variable, described later.

说得简单点，python里的pachage就是要引入整个文件夹。如何初始化package呢？需要在目录下建一个 \_\_init__.py 文件。如下

    going1000@osx libs $  (master) ls
    __init__.py	__init__.pyc	mail.py		mail.pyc	mysqlClass.py

Note:如果想要加载多层子目录，只能从上至下每个文件夹都建一个 \_\_init__.py 文件。估计包含的伪代码类似于

	importFolder(folder):
		if !find(__init__.py)
			return
		for item in folderItemList:
			if is_folder(item):
				importFolder(item):
			else:
				include item

###Importing * From a Package
一般而言，\_\_init\_\_.py 只需要是个空文件就可以了。但是如果想使用 Import * 这种语句，就需要设置下 \_\_init\_\_.py 中的 \_\_all__ 属性:

	__all__ = ["mail"]

如此，当你 import * 的时候，就会引入其中的 mail module

###sys.path.append
当然，还有其他方式来添加加载的文件夹

    import sys
    # 使用 sys.path.append 添加文件夹
	sys.path.append('/Volumes/development_env/g1ksTips/python/lib_test')
	import datetime
	import libs.mail

	print sys.path
	print sys.modules

###dir()
python的每个module都有独立的变量表，而dir()函数用来查看 __main__ module变量表中 import的 module 和变量的关系
比如

	print dir(sys)
	# output
	['__displayhook__', '__doc__', '__egginsert', '__excepthook__', '__name__', '__package__', '__plen', '__stderr__', '__stdin__', '__stdout__', '_clear_type_cache', '_current_frames', '_getframe', '_mercurial', 'api_version', 'argv', 'builtin_module_names', 'byteorder', 'call_tracing', 'callstats', 'copyright', 'displayhook', 'dont_write_bytecode', 'exc_clear', 'exc_info', 'exc_type', 'excepthook', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info', 'float_repr_style', 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags', 'getfilesystemencoding', 'getprofile', 'getrecursionlimit', 'getrefcount', 'getsizeof', 'gettrace', 'hexversion', 'long_info', 'maxint', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'py3kwarning', 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit', 'settrace', 'stderr', 'stdin', 'stdout', 'subversion', 'version', 'version_info', 'warnoptions']


这时候你会发现，内建的函数无法打印出来，比如open()，这时候，可以 import __builtin__ 

	import __builtin__ as b
	print dir(b)
	#output
	['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException', 'BufferError', 'BytesWarning', 'DeprecationWarning', 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False', 'FloatingPointError', 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError', 'ImportWarning', 'IndentationError', 'IndexError', 'KeyError', 'KeyboardInterrupt', 'LookupError', 'MemoryError', 'NameError', 'None', 'NotImplemented', 'NotImplementedError', 'OSError', 'OverflowError', 'PendingDeprecationWarning', 'ReferenceError', 'RuntimeError', 'RuntimeWarning', 'StandardError', 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError', 'SystemExit', 'TabError', 'True', 'TypeError', 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError', 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning', 'ValueError', 'Warning', 'ZeroDivisionError', '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs', 'all', 'any', 'apply', 'basestring', 'bin', 'bool', 'buffer', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod', 'cmp', 'coerce', 'compile', 'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'execfile', 'exit', 'file', 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'intern', 'isinstance', 'issubclass', 'iter', 'len', 'license', 'list', 'locals', 'long', 'map', 'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property', 'quit', 'range', 'raw_input', 'reduce', 'reload', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'unichr', 'unicode', 'vars', 'xrange', 'zip']
	
	
========================================================
扩展阅读

>https://docs.python.org/2/tutorial/modules.html
>https://docs.python.org/3/reference/import.html