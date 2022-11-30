---
marp: true
theme: ngi-theme
paginate: false
header: '_08.12.2022_'
footer: '![width:90 height:40](figures/logo/NGI/NGI_logo_transparent.gif)'

---

<!-- _class: title --> 
# "Free" tricks for good software 


## 

####

#### Sunniva Indrehus
#### Norwegian Geotechnical Institute

---



<!-- _class: title --> 
# "Free" tricks for good enough software 

## 

####

#### Sunniva Indrehus
#### Norwegian Geotechnical Institute

---

A little bit about my background 



--- 

Give credit, tricks that are useful for me does not need to be so for others


--- 


<!-- paginate: true -->

<!-- _footer: "![width:90 height:40](figures/logo/NGI/NGI_logo_transparent.gif)  *Figure credit: [Ali Bati](http://www.alibati.com/horse)* " -->

# What is a good *enough* model?


- Use something simplified to learn about the real world 


 
![bg right w:400 h:350](figures/illustrations/horse.png) 



--- 

<!-- paginate: true -->

<!-- _footer: "![width:90 height:40](figures/logo/NGI/NGI_logo_transparent.gif)  *Figure credit: [Ali Bati](http://www.alibati.com/horse)* " -->


# What is a good *enough* model?


- Use something simplified to learn about the real world 


 
![bg right w:400 h:350](figures/illustrations/horse.png) 

# What is a good *enough* code? 

--- 




# What is good (enough)?

<!-- _class: split-text-image -->

<div class=ldiv>





</div>

<div class=rdiv>

![w:550 h:450](figures/illustrations/wtf.png) 
 


</div>




---




# What is good (enough)?

<!-- _class: split-text-image -->

<!-- _footer: "&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; [1] Neural Information Processing Systems: [The Machine Learning Reproducibility Checklist](https://www.cs.mcgill.ca/~jpineau/ReproducibilityChecklist.pdf), retrieved: 11.29, 25th of Febrauary 2022.<br/>
![width:90 height:40](figures/logo/NGI/NGI_logo_transparent.gif)  [2] Common estimate: annually spending 20% of the development time for maintenance work" -->

<div class=ldiv>

## My personal thoughts 

- Something that works 
- Standardized 
- Understandable 
- Reproducable<sup>[1]</sup> 
- Maintainable<sup>[2]</sup> 

</div>

<div class=rdiv>

![w:550 h:450](figures/illustrations/wtf.png) 
 


</div>


--- 



# How to get good enough software ? 

- Spend a lot of time and money? 

--- 



# REference to good enough software speed and time graph 




---


## Good news: you can get a lot for free :smiley: 


personal preferences here 





---

# General advice: automate as much as possible 



--- 

You can do it in the cloud, but there are a lot of things you can do locally also 

# Enforce hooks with git, 

post and pre 

- Automatically think about secrets ? 

--- 


Show screenshots of the pre-commit folder changing color 


--- 


```powershell
Python 3.10.7 (tags/v3.10.7:6cc6b13, Sep  5 2022, 14:08:36) [MSC v.1933 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import this
The Zen of Python, by Tim Peter
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
>>>
```
<!-- 
| ![zen](../figures/the-zen-of-python.png) |
|:--:|
| Figure: A cartoon guide *Credit: FILL INN AUTHOR*| -->


<!-- If you choose to break one of these rules you should have a good reason for it. There exist a lot of tools that can help you to follow the standards efficiently.  -->


--- 

# Pythoninc advices: 


> Know the rules so you know how to break them efficiently - Daila Lama



*[The zen of Python Illustrated](https://hacktoon.com/posts/2016/the-zen-of-python-illustrated/)* 



--- 


# A language problem 


--- 

Python is a high level programming language that ueses dynamic typing (in contrast to C/C++/Fortran where the variables are static) you do not need to declare types of variables, parameters, and return values from a function upfront. The return types can be any type and the types of the variables can change during run time. Dynamic typing leads to bugs that can be very difficult to debug. 

[PEP 484 - type hints ](https://peps.python.org/pep-0484/) (already suggested from 2014) suggests using annotation for types and return values from functions. Type hints were introduced as a new feature in Python 3.5. 

[mypy](https://mypy.readthedocs.io/en/stable/) is a static type checker for Python 3 that helps us to run type checks and catch bugs. 

--- 


# Type hints (help with static checks)


```python
# this file is named factorial.py
def factorial(n):
    if n < 2:
        return 1
    return n * factorial(n - 1)
 
my_int = 4 
print(f"value is: {factorial(my_int)}")

my_string = "4"
print(f"value is: {factorial(my_string)}")
```


```python
value is: 24
Traceback (most recent call last):
  File "C:\Users\SuI\test-factorial\type_hint_example\type_hint_example\factorial.py", line 13, in <module>
    print(f"value is: {factorial(my_string)}")
  File "C:\Users\SuI\test-factorial\type_hint_example\type_hint_example\factorial.py", line 2, in factorial
    if n < 2:
TypeError: '<' not supported between instances of 'str' and 'int'
```

--- 


## Adding type hints 


```python 
# this file is named factorial_int.py
def factorial_int(n: int ) -> int:
    if n < 2:
        return 1
    return n * factorial_int(n - 1)

print(f"value is: {factorial_int(4)}")
 

print(f"value is: {factorial_int(4.5)}")
```

Output 

```powershell
(type-hint-example-py3.10) python .\type_hint_example\factorial_int.py
value is: 24
value is: 39.375
```
--- 



## Is this pythonically correct? 

```powershell
(type-hint-example-py3.10) mypy .\type_hint_example\factorial_int.py
type_hint_example\factorial_int.py:12: error: Argument 1 to "factorial_int" has incompatible type "float"; expected "int"
Found 1 error in 1 file (checked 1 source file)
```

My error is catched 


--- 


## Other cool tools for model validation 

By updating the code to use `float` instead of `int` I will have a code that uses the correct types. 

```python 
# this file is named factorial_float.py
def factorial_float(n: float) -> float:
    if n < 2:
        return 1
    return n * factorial_float(n - 1)
```


--- 
Running the code still provides the same answer,

```powershell 
(type-hint-example-py3.10) python .\type_hint_example\factorial_float.py
value is: 24
value is: 39.375
```
but now the code is also statically valid 

```powershell 
(type-hint-example-py3.10) mypy .\type_hint_example\factorial_float.py
Success: no issues found in 1 source file
```


:scream: what about data and type hints<sup>[1]</sup>?

<!-- _footer: "&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; [1] Actually agreeable [Pydantic](https://pydantic-docs.helpmanual.io/), [Pandera](https://pandera.readthedocs.io/en/stable/), retrieved: 15.11, 30th of November 2022 :heart_eyes: <br/>
![width:90 height:40](figures/logo/NGI/NGI_logo_transparent.gif)" -->



--- 




## Follow the python style guide  

> Readability counts  

[PEP 8](https://peps.python.org/pep-0008/) gives general guidelines for your code style like whitespace expressions, comments, naming, etc. 

#### Examples from the official documentation

**Indentation**
```python 
# Correct: aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Wrong: arguments on first line forbidden when not using vertical alignment.
foo = long_function_name(var_one, var_two,
    var_three, var_four)
```

**Names to avoid** 
> Never use the characters ‘l’ (lowercase letter el), ‘O’ (uppercase letter > oh), or ‘I’ (uppercase letter eye) as single character variable names.
> In some fonts, these characters are indistinguishable from the numerals one and zero. When tempted to use ‘l’, use ‘L’ instead.
> 

```python 
l : string = "my_string"
1 : float = 4.5
```

Why does this matter? Because you are working on making things more standardized. Getting all these things right seems difficult. They are only tools that can help you achieve *good code* (whatever you define as good code). Luckily python has an excellent ensemble of available tools to help you spend less time following these rules and more time on focus on implementation. Black will help you to reformat your code, and flake8 can check for coding style and errors against PEP8.  


---

#### Example with black 
The following code can run correctly, but is not correctly formatted according to PEP8 because of the extra indents. 

```python 
# this file is named factorial_float.py
def factorial_float(
    n: float) -> float:
    if n <          2:
        return 1
    return n * factorial_float(n - 1)
```
By running black from the terminal 
```powershell 
(type-hint-example-py3.10) black .\type_hint_example\factorial_float.py
reformatted type_hint_example\factorial_float.py

All done! ✨ 🍰 ✨
1 file reformatted.
```
the code is automatically formatted to 

```python 
# this file is named factorial_float.py
def factorial_float(n: float) -> float:
    if n < 2:
        return 1
    return n * factorial_float(n - 1)
```
 
--- 


#### Example with flake8 
The following code can run correctly, but is not correctly formatted according to PEP8 because of the unnecesseary import of the unsed `math` library. 

```python 
# this file is named factorial_float.py
import math 

def factorial_float(n: float) -> float:
    if n < 2:
        return 1
    return n * factorial_float(n - 1)

```

By running flake8 from the terminal 
```powershell 
(type-hint-example-py3.10) flake8 .\type_hint_example\factorial_float.py
.\type_hint_example\factorial_float.py:1:1: F401 'math' imported but unused
.\type_hint_example\factorial_float.py:8:1: E741 ambiguous variable name 'l'
```
The developer needs to manually remove this import. 


---



# Summary 

:boom: Pydantic let's you focus on your algorithm and not data model validation :boom:

## Other cool tools for model validation 
- [Pandera](https://pandera.readthedocs.io/en/stable/), for data-validation on dataframe-like objects 
  GitHub :star: 1.7k (currently, 18.10.22)

--- 

# [Demo repository](https://github.com/sunnivin/demo-make-model-validation-sexy-again) 

