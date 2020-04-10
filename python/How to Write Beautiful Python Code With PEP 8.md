# 如何用PEP 8编写优雅的Python代码

## 1. Naming Conventions

### 1.1 Naming Styles

| 类型 | 命名规则                                       | Example                 |
| ---- | ---------------------------------------------- | ----------------------- |
| 函数 | 采用小写单词，中间采用下划线连接               | function,my_funtion     |
| 变量 | 使用小写的字母，词，或者多个词，采用下划线连接 | x,var,my_variable       |
| 类   | 大写字母开头，采用Camel Case                   | Model, MyClass          |
| 方法 | 使用小写词，或者多个词，中间采用下划线分割     | class_method,method     |
| 常量 | 使用大写的字母，单词，或者多词，采用下划线     | CONSTANT,MY_CONSTANT    |
| 模块 | 采用短，小写的词或者多词，采用下划线分割       | module.py, my_modyle.py |
|      | 采用短，小写词或者多词，不使用下划线           | package,mypackage       |

### 1.2 How to Choose Names
在编写代码时，你应该在命名选择中加入相当多的思考，因为这样可以使代码更具可读性。在Python中为对象命名的最佳方法是使用描述性名称来清楚表明对象所代表的内容。
同样的理念适用于Python中的所有其他数据类型和对象，尽量一直使用最简洁且最具描述性的名称。

## 2. Code Layout

### 2.1 Blank Lines

垂直空格或空行可以极大地提高代码的可读性，聚集在一起的代码可能是压倒性的且难以阅读，同样，代码中的空行太多会使其看起来非常稀疏，读者可能需要进行没必要的滚动，以下是关于如何使用垂直空白的三个关键指南。

#####  用两个空行包围顶级函数和类
用两个空行包围顶级函数和类，顶级函数和类应该是完全自包含的，并处理单独的功能，在它们周围放置额外的垂直空间是有意义的，因此很明显它们是分开的：

```python
class MyFirstClass:
    pass


class MySecondClass:
    pass


def top_level_function():
    return None
```
##### 用一个空行包围类中的方法定义
用一个空行包围类中的方法定义，在一个类中，函数都彼此有联系，最好只在它们之间留一行：

```python
class MyClass:
    def first_method(self):
        return None

    def second_method(self):
        return None
```
##### 在函数内部谨慎地使用空行
在函数内部谨慎地使用空行，以显示清晰的步骤，有时候一个复杂的函数必须在return语句之前完成好几个步骤，为了帮助阅读者理解函数里面的逻辑，在每个步骤之间留一个空行会很有帮助。

在下面的示例中，有一个计算列表方差的函数，这个问题可以分为两个步骤，所以我在每个步骤之间留下了一个空行，在return语句之前还有一个空行。这有助于读者清楚地看到返回的内容：
```python
def calculate_variance(number_list):
    sum_list = 0
    for number in number_list:
        sum_list = sum_list + number
    mean = sum_list / len(number_list)

    sum_squares = 0
    for number in number_list:
        sum_squares = sum_squares + number**2
    mean_squares = sum_squares / len(number_list)

    return mean_squares - mean**2
```

### 2.2 Maximum Line Length and Line Breaking

PEP 8建议每行代码限制在79个字符以内，这是因为它允许多个文件并排打开，同时也避免了换行，当然，将语句保持在79个字符以内并不总是可行的。PEP 8概述了允许语句在多行上运行的方法。
如果代码包含在括号、方括号或大括号中，Python将会认为代码是一行的：

```python
def function(arg_one, arg_two,
             arg_three, arg_four):
    return arg_one
```

如果不能用上述的方式进行每行代码延续，那么可以使用反斜杠代替换行：
```python
from mypkg import example1, \
    example2, example3
```
但是，如果可以使用第一个方案，那么就应该尽量这样做。

### 2.3 Indentation

PEP 8制定的关键缩进规则如下：

- 使用4个连续的空格来表示缩进。
- 选择空格而不是制表符(Tab)。

### 2.4 Tabs vs. Spaces
如同上述所说，当你进行缩进的时候，你最好用空格代替制表符，你可以直接对文本编辑器的设置进行调整，当你按Tab的时候转换为4个空格的输出

如果你使用的是Python 2并且混合使用了制表符和空格来缩进代码，当你运行的时候可能不会看见错误。为了帮助你检查一致性，可以在从命令行运行Python 2代码时添加-t标志。当你不一致地使用制表符和空格时，解释器将会发出警告：

```shell
python2 -t code.py
code.py: inconsistent use of tabs and spaces in indentation
```
相反，如果你使用-tt标志，解释器将发出错误而不是警告，使用此方法的好处是解释器会告诉你缩进不一致的位置在哪里：

```shell
python2 -tt code.py
File "code.py", line 3
    print(i, j)
             ^
TabError: inconsistent use of tabs and spaces in indentation
```
Python 3不允许制表符和空格混合使用，因此，如果你使用的是Python3，解释器将会自动报错：

```shell
python3 code.py
File "code.py", line 3
    print(i, j)
              ^
TabError: inconsistent use of tabs and spaces in indentation
```


### 2.5 Indentation Following Line Breaks
两种缩进风格供你选择。
第一个是将缩进块与开始的分隔符对齐:
```shell
def function(arg_one, arg_two,
             arg_three, arg_four):
    return arg_one
```

有时你会发现只需要4个空格就可以与开口分隔符对齐，这种情况经常发生在 if 语句中，如果跨多行的if+ +(构成4个字符，那么就会发生这种情况，在这种情况下，很难确定 if 语句中嵌套的代码块从哪里开始.在这种情况下，PEP 8提供了两种替代方案来帮助你提高代码可读性：


在最后的条件后添加注释，由于大多数编辑器中有语法高亮显示，这可以将条件与嵌套代码分开：
```shell
x = 5
if (x > 3 and
    x < 10):
    # Both conditions satisfied
    print(x)
```
在换行中添加额外的缩进：
```shell
x = 5
if (x > 3 and
        x < 10):
    print(x)
```
::Note：当你正在使用hanging indent时，第一行不得有任何参数。

```shell
def function(
        arg_one, arg_two,
        arg_three, arg_four):
    return arg_one
```
当你编写遵循PEP 8规范代码的时候，每行字符在79之内的规则使你必须强制换行，为了提高可读性，你应该缩进一行，以表明它是一个连续的行。做到这一点有两种方法，第一种是将缩进的块与开始的分隔符对齐，第二种是使用悬挂缩进，在换行之后，你可以自由选择使用哪种方法进行缩进。

### 2.6 Where to Put the Closing Brace

一行代码的换行操作允许你在括号、方括号或大括号后面断开一行，这会造成一个问题，就是很容易忘记关闭括号，但重要的是要把它放在合理的地方，否则，它会使读者感到困惑，Pep 8为隐含的行延续中的结束括号的位置提供了两个选项:

使用前一行的第一个非空白字符排列右括号：

```python
list_of_numbers = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
    ]
```

将结束括号与声明行的第一个字符对齐:

```python
list_of_numbers = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
]
```

你可以自由地选择任何一种方式，但是，和之前说的一样，一致性是关键，所以之后的代码就要坚持使用你选择的某一个方案以保持代码一致性。

你可以自由地选择任何一种方式，但是，和之前说的一样，一致性是关键，所以之后的代码就要坚持使用你选择的某一个方案以保持代码一致性。

将结束括号与声明行的第一个字符对齐:
list_of_numbers = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
]
你可以自由地选择任何一种方式，但是，和之前说的一样，一致性是关键，所以之后的代码就要坚持使用你选择的某一个方案以保持代码一致性。

## 3. Comments

如果你无法向人描述你的方案，那肯定不是一个好方案；反之亦然

你应该使用注释来说明编写的代码，这对记录你的代码非常重要，这样你的任何协作者都可以理解它。当你或者其他人阅读代码注释，他们应该能够很容易地理解注释所应用的代码，以及它如何与代码的其余部分相匹配。

下面是一些你为你代码作注释时候需要注意的关键点：

- 将注释和文档字符串的行长限制为72个字符
- 使用完整的句子，以大写字母开头
- 注释随着代码的更新而更新

### 3.1 Block Comments

这是一个解释for循环功能的块注释，请注意，句子为了每行保留79个字符行限制进行了换行：

```python
for i in range(0, 10):
    # Loop over i ten times and print out the value of i, followed by a
    # new line character
    print(i, '\n')
```


有时，如果代码技术性较强，那么有必要在块注释中使用多个段落：

```python
def quadratic(a, b, c, x):
    # Calculate the solution to a quadratic equation using the quadratic
    # formula.
    #
    # There are always two solutions to a quadratic equation, x_1 and x_2.
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)
    return x_1, x_2
```


如果你不确定什么样的注释类型是合适的，那么块注释通常是正确的选择。请尽量在你的代码中添加注释，一旦你对代码进行了更新也请务必对注释进行更新！

### 3.2 Inline Comments

行内注释对单个语句中的一段代码进行了解释，这有助于提醒你或者其他人为什么某行代码是必须的，以下是 `PEP 8`对他们的评价:

- 谨慎使用行内注释
- 在与它们引用的语句相同的行上写入行内注释
- 从语句中用两个或多个空格分隔行内注释
- 像块注释那样，用#加上一个空格开始每一行的注释
- 不要用它们来解释明显的问题

下面是一个行内注释的例子：

```python
x = 5  # This is an inline comment
```

行内注释比块注释更具体，并且容易在非必要时候添加它们，这会导致代码混乱。除非你确定需要行内注释，不然使用块注释避免代码混乱的问题比较好，坚持使用块注释，可以让你的代码更加符合PEP8的标准。

### 3.3 Documentation Strings
Documentation strings 或者说docstrings， 是用双引号（”””）或单引号（’’’）括起来的字符串，它们出现在任何函数，类，方法或模块的第一行，你可以使用它们来解释和记录特定的代码块。这里有一个对应的PEP，见PEP 257，但你可以从本节阅读总结的经验：

使用文档字符串的重要规则如下：

- 文档字符串两边都有三个双引号环绕，比如："""This is a docstring"""
- 为所有公共模块，函数，类和方法编写docstrings
- 使用单行"""结束多行docstring

```python
def quadratic(a, b, c, x):
    """Solve quadratic equation via the quadratic formula.

    A quadratic equation has the following form:
    ax**2 + bx + c = 0

    There always two solutions to a quadratic equation: x_1 & x_2.
"""
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)

    return x_1, x_2
```
对于单行docstrings，保持"""在同一行：
```python
def quadratic(a, b, c, x):
    """Use the quadratic formula"""
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)

    return x_1, x_2
```
想要了解更多，请阅读Documenting Python Code: A Complete Guide – Real Python

## 4. Whitespace in Expressions and Statements
正确使用空格在表达式和语句中非常有用，如果代码中没有足够的空格，那么代码应该很难阅读，因为他们都凑在一起，如果空格太多，又会难以在视觉上将完整的语句联系出来。

### 4. 1 Whitespace Around Binary Operators
在进行以下二元操作的时候，应该在其两边加上空格：

- 分配操作（=, +=, -=, 等等）
- 比较（==, !=, >, <. >=, <=）和 （is, is not, in, not in）
- 布尔（and, not, or）
::Note：当=是为一个函数的参数赋值时候就不用在两边加空格::
```python
# Recommended
def function(default_parameter=5):
    # ...


# Not recommended
def function(default_parameter = 5):
    # ...

```

如果语句中有多个运算符，则在每个运算符前后添加单个空格可能会让人感到困惑，相反，最好只在优先级最低的运算符周围添加空格，尤其是在执行数学运算时。以下是几个例子：
```python
    # Recommended
    y = x**2 + 5
    z = (x+y) * (x-y)
    
    # Not Recommended
    y = x ** 2 + 5
    z = (x + y) * (x - y)
```
还可以将此应用于有多个条件的if语句：
```python
    # Recommended
    if x>5 and x%2==0:
        print('x is larger than 5 and divisible by 2!')
```

### 4. 2 When to Avoid Adding Whitespace
在某些情况下，添加空格可能会使代码难以阅读，太多的空格会使代码过于稀疏而难以理解。 PEP 8概述了一些非常明显的例子应当不使用空格

在一行的末尾避免添加空格是最重要的地方，这称为trailing whitespace，它是不可见的，可能产生难以追踪的错误。

以下列表概述了一些应避免添加空格的情况：

- 直接放在括号、方括号或大括号内:
```python
# Recommended
my_list = [1, 2, 3]

# Not recommended
my_list = [ 1, 2, 3, ]
```
- 在逗号，分号或冒号之前：
```python
x = 5
y = 6

# Recommended
print(x, y)

# Not recommended
print(x , y)
```
- 在打开函数调用的参数列表的开括号之前：
```python
def double(x):
    return x * 2

# Recommended
double(3)

# Not recommended
double (3)
```
- 在开始索引或切片的开括号之前:
```python
# Recommended
list[3]

# Not recommended
list [3]
```
- 在尾随逗号和右括号之间：
```python
# Recommended
tuple = (1,)

# Not recommended
tuple = (1, )
```
- 对齐赋值运算符：
```python
# Recommended
var1 = 5
var2 = 6
some_long_var = 7

# Not recommended
var1          = 5
var2          = 6
some_long_var = 7
```
确保你的代码中没有尾随空格。 在其他情况下，PEP 8不鼓励添加额外的空格，例如立直接放在括号、方括号或大括号内，以及逗号和冒号之前。 为了对齐操作符，也不应该添加额外的空格。

### 5. Programming Recommendations

- 不要使用等价运算符将布尔值与True或False进行比较，你经常需要检查布尔值是True还是False，当这样操作时，请使用如下所示的语句直观地执行此操作：
```python
# Recommended
if my_bool:
    return '6 is bigger than 5'
```

- 在if语句中判断列表是否为空，当你希望确定列表是否为空时，你通常会判断列表的长度，如果列表为空，那么长度为0，在if语句中使用时等于False. 在Python中，任何空列表，字符串或元组都可以当为False的。因此，我们可以提出一个更简单的替代方案：
```python
# Recommended
my_list = []
if not my_list:
```

- 在if语句中，使用 is not 比 no ... is in 好，当你需要确定一个变量是否被赋值，这里有两种方法，第一种是评估if语句中的x是不是为非None，如下所示：
```python
# Recommended
if x is not None:
    return 'x exists!'
```

- 当你想表达if x is not None时，不要使用if x，有时候，你可能拥有一个函数带有默认值为None的参数，当对参数arg检查是否带有不同的值的时候经常会犯下面这样的错误：
```python
# Not Recommended
if arg:
    # Do something with arg...
```
此代码检查的是arg是否为真，但相对的你要的是检查是否为None，所以下面这样写比较好：
```python
# Recommended
if arg is not None:
    # Do something with arg...
```
上面的错误会使得判断是否为真和not None相等，你可以设置arg = []，如上所述，空列表在Python中被认为是False，因此，尽管参数被声明为[]，但条件并没有满足，因此函数里面的代码if声明并不能被执行。
- 用.startswith() 和.endswith()代替切片，如果你想检查一段字符串的前缀或者后缀是否带有字符串cat，这看起来使用列表切片似乎比较明智，但是，列表切片容易出错，您必须对前缀或后缀中的字符数进行硬编码，对于那些不太熟悉Python列表切片的人来说很难看清楚你想要实现的目的：
```python
# Not recommended
if word[:3] == 'cat':
    print('The word starts with "cat"')

# Recommended
if word.startswith('cat'):
    print('The word starts with "cat"')
```

## 6. When to Ignore PEP 8
如果你严格遵循 PEP 8，就可以保证您拥有干净、专业和可读的代码。 这对你以及合作者和潜在雇主都有好处。

但是，PEP 8中的一些指导方针在以下实例中不适用：

- 如果遵守PEP 8将破坏与现有软件的兼容性
- 如果你正在从事的工作的代码与 PEP 8不一致
- 如果代码需要与旧版本的Python版本保持兼容

## 7. Tips and Tricks to Help Ensure Your Code Follows PEP 8
想要你的代码兼容PEP 8，那你得记住不少规范，在开发代码时，记住所有这些规则可能是一项艰巨的任务。特别是对老项目进行更新以兼容PEP 8时，幸运的是，有些工具可以帮助你加快这一过程，这里有两个工具可以帮你强制兼容PEP 8规范：linters和autoformatters。

### 7.1 Linters
Linters是分析代码和标记错误的程序，他们可以为你如何修复错误提供建议，在作为文本编辑器的扩展安装时，Linters特别有用，因为它们标记了你编程时的错误和格式问题。在本节中，您将看到Linters程序是如何工作的大纲，最后还有文本编辑器扩展的链接。

对于Python代码，最好的linters如下：

- [pycodestyle](pycodestyle · PyPI)是一个根据PEP 8中的某些风格约定来检查Python代码的工具
```shell
# 使用pip安装pycodestyle
pip install pycodestyle
```

使用以下命令在终端中使用pycodestyle：
```shell
pycodestyle code.py
code.py:1:17: E231 missing whitespace after ','
code.py:2:21: E231 missing whitespace after ','
code.py:6:19: E711 comparison to None should be 'if cond is None:'
```

- flake8是一个结合了调试器，pyflakes和pycodestyle的工具
```shell

# 使用pip安装flake8
pip install flake8
```

使用以下命令在终端中使用pycodestyle：

```shell
flake8 code.py
code.py:1:17: E231 missing whitespace after ','
code.py:2:21: E231 missing whitespace after ','
code.py:3:17: E999 SyntaxError: invalid syntax
code.py:6:19: E711 comparison to None should be 'if cond is None:'

```
这些也可用作Atom，Sublime Text，Visual Studio Code和VIM的扩展。您还可以找到有关为Python开发设置Sublime Text和VIM的指南，以及Real Python中一些流行的文本编辑器的概述。

### 7.2 Autoformatters
Autoformatters可以重构你的代码以使其符合PEP 8规范，像black程序就可以根据PEP 8规范重新格式化你的代码，一个很大的区别是它将行长度限制为88个字符，而不是79个字符。但是，您可以通过添加命令行标志来覆盖它，如下面的示例所示。

可以使用pip安装black，它需要Python 3.6+：
```shell
pip install black
```

如果你想要更改行长度限制，则可以使用—line-length标志：
```shell
black --line-length=79 code.py
reformatted code.py
All done!
```
另外两个autoformatters分别为autopep8和yapf，它们和black操作类似。

另一个Real Python教程，由Alexander van Tol编写的Python Code Quality: Tools & Best Practices详细解释了如何使用这些工具。

## 8. Conclusion
你现在已经知道如何使用PEP 8中的指南编写高质量，可读高的Python代码，虽然指南看起来很迂腐，但遵循它们可以真正改善你的代码，特别是在与潜在雇主或合作者共享代码时。

在本教程中你了解到：

- 什么是PEP 8以及其存在的原因
- 为什么你应该编写符合PEP 8标准的代码
- 如何编写符合PEP 8的代码
- 除此之外，您还了解了如何使用linters和autoformatters根据PEP 8指南检查代码。

如果你想了解更多，可以阅读[full documentation](PEP 8 — Style Guide for Python Code | Python.org)或者浏览pep8.org，这些教程不仅提供了类似的信息同时也提供了很好的格式让你阅读，在这些文档中，您将找到本教程未涉及的其余PEP 8指南。



