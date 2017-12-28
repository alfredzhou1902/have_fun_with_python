#### 标准文档中使用BNF来解释expression，下面是相关的内容

### BNF定义
[维基百科](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form)
> In computer science, Backus–Naur form or Backus normal form (BNF) is a 
notation technique for context-free grammars, often used to describe the
syntax of languages used in computing, such as computer programming 
languages, document formats, instruction sets and communication protocols. 

### python官方文档中的BNF
[3.6.4官方文档 6-Expressions](https://docs.python.org/3/reference/expressions.html#grammar-token-expression)

1. and or表达式
```
or_test  ::=  and_test | or_test "or" and_test
and_test ::=  not_test | and_test "and" not_test
not_test ::=  comparison | "not" not_test

comparison ::=  or_expr ( comp_operator or_expr )*
comp_operator ::=  "<" | ">" | "==" | ">=" | "<=" | "!="| "is" ["not"] | ["not"] "in"
                   
and_expr ::=  shift_expr | and_expr "&" shift_expr
xor_expr ::=  and_expr | xor_expr "^" and_expr
or_expr  ::=  xor_expr | or_expr "|" xor_expr
```
>In the context of Boolean operations, and also when expressions are used by control flow statements, 
the following values are interpreted as false: **False**, **None**, numeric **zero** of all types, and empty strings 
and containers (including strings, tuples, lists, dictionaries, sets and frozensets). All other values are 
interpreted as true. User-defined objects can customize their truth value by providing a __bool__() method.

>The operator *not* yields True if its argument is false, False otherwise.

>The expression x *and* y first evaluates x; if x is false, its value is returned; 
otherwise, y is evaluated and the resulting value is returned.

>The expression x *or* y first evaluates x; if x is true, its value is returned; 
otherwise, y is evaluated and the resulting value is returned.

#### 做一些测试，不过不是用条件语句
```python

def andTest(a=0,b=1):
  return a and b
  
def orTest(a=0,b=1):
  return a or b

print(andTest())
#return is 0

print(andTest(a=True))
#return is 1

print(andTest(a=True,b=None))
#return is None

print(andTest(a=True,b='Helloworld!'))
#return is 'Helloworld!'

print(orTest())
#return is 1

print(orTest(a='HelloAgain!',b=True))
#return is 'HelloAgain!'

print(orTest(a=None,b=[]))
#return is []

```
#### return的这个性质之前没有注意。经过上述测试，用return可以得到一些有趣的结果，例子灵感来自狗书作者（@Miguel Grinberg）的代码。
附上狗书作者的2017年最新的教程视频[地址](https://www.youtube.com/watch?v=mLOaSBP0X4Q)
2. etc.
