
# Inheritance 
Inheritance allows us to define a class that inherits all the methods and properties from another class.<br>
<a href="https://www.scientecheasy.com/2023/09/types-of-inheritance-in-python.html/">Types of inheritance</a>
1. Single Inheritance
2. Multiple Inheritance
3. Multilevel Inheritance
4. Hierarchical Inheritance
5. Hybrid Inheritance
<br></br>
<img src ="https://www.scientecheasy.com/wp-content/uploads/2023/09/types-of-inheritance-in-python-768x553.png">

# Polymorphism
The word <a href="https://www.w3schools.com/PYTHON/python_polymorphism.asp"> Polymorphism </a> means many forms, and in programming it refers to methods/functions/operators with the same name that can be executed on many objects or classes.
There are important topics related to polymorphism. 
1. Duck Typing
2. Overloading
    1. Operator Overloading
    2. Method Overloading
    3. Constructor Overloading
3. Overriding
    1. Method Overriding
    2. Constructor Overriding
## 1. Duck Typing
In python type cannot be specified explicityly, depending on the provided value at runtime the type is automatically considered.
```
class Duck:
    def talk(self):
        print('Talking from duck class')


class Human:
    def talk(self):
        print('Talking from human class')


class Dog:
    def bark(self):
        print('Talking from dog class')


def f1(obj):
    if hasattr(obj, 'talk'):
        obj.talk()
    elif hasattr(obj, 'bark'):
        obj.bark()


dk = Duck()
h = Human()
d = Dog()

f1(dk) ==>Ouput: Talking from duck class
f1(h)  ==>output: Talking from human class
f1(d)  ==>output: Talking from dog class
```

#  2. OverLoading

Overloading ( <strong>using same operator/method/constructor for multiple purposes</strong>) is of three types.
1. Operator Overloading: 
2. Method Overloading (<i>Methods having same name but different number of arguments</i>)
3. Constructor Overloading 
<br>
* Method and constructor overloading is not possible. If we try to declare multiple methods with same name and different number of arguments then **python will always consider only last method/constructor**.
* If method with variable number of arguments required then we can handle with **default arguments or with variable number of argument methods**.
* Similarly, we can declare constructor **with default arguments or variable number of arguments**.

### 2.1 Operator Overloading

```
class Book:
    def __init__(self, pages) -> None:
        self.pages = pages

    def __add__(self, other):
        return self.pages + other.pages

    def __mul__(self, other):
        return self.pages * other.pages


b1 = Book(10)
b2 = Book(20)

print(b1+b2)
print(b1 * b2)
```
### 2.2 Method Overloading

```
class Test:
    def m1(self, a=None, b=None):
        print('No arg Method')
    # def m1(self, a):
    #     print('One arg method')
    # def m1(self, a, b):
    #     print('Two arg method')


t1 = Test()
t1.m1()


class Test01:
    def __init__(self, *a):
        for i in a:
            print(i)
        return None


t2 = Test01(3, 2, 1)
t3 = Test01('a', 'b', 'c', 'd')
# t2.m1(3,2,1)
```
### 2.3 Constructor Overloading
```

class Test02:
    def __init__(self, *a) -> None:
        for i in a:
            print(i)


t3 = Test02(30, 20, 10)
```
### 3.1 Method Overriding
In Python, the <a href="https://realpython.com/python-super/">super()</a> function is used to refer to the parent class or superclass <i>(gives you access to methods in a superclass from the subclass that inherits from it)</i>
```
class Test10:

    def walk(self):
        print('This is printed by Parent walk Method')

    def speak(self):
        print('This is printed by Parent speak Method')


class Test11(Test10):

    def walk(self):
        super().walk()
        print('This is printed by Child speak Method')


print('-------Parent class--------')
v10 = Test10()
v10.walk()
v10.speak()
print('--------Child class---------')
v11 = Test11()
v11.speak()
v11.walk()
```
### 3. Constructor Overriding
```
class Test20:
    """Docstring to be provided"""

    def __init__(self):
        print('Parent Test20 constuctor executed')

    def check_print(self):
        print("Printing to check super method")


class Test21(Test20):
    """Docstring to be provided"""

    def __init__(self) -> None:
        print('Child Test21 constructer executed')


class Test22(Test20):
    """Docstring to be provided"""

    def __init__(self) -> None:
        print('Child Test22 constructer executed')
        super().__init__()
        super().check_print()


v20 = Test20()
v21 = Test21()
v22 = Test22()
```