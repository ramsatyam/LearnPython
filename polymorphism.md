# Polymorphism
Polymorphism means having many form. Poly means many, morphs means forms.
There are four important topics related to polymorphism. 
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
        print('Duck Quacks')


class Human:
    def talk(self):
        print('Human speaks')


class Dog:
    def bark(self):
        print('Dog barks')


def f1(obj):
    if hasattr(obj, 'talk'):
        obj.talk()
    elif hasattr(obj, 'bark'):
        obj.bark()


dk = Duck()
h = Human()
d = Dog()

f1(dk) ==>Ouput: Dog barks
f1(h)  ==>output: Human speaks
f1(d)  ==>output: Dog barks
```

#  2. OverLoading

Overloading ( **using same operator/method/constructor for multiple purposes**) is of three types

    1. Operator Overloading: 
    2. Method Overloading (**Methods having same name but different number of arguments**)
    3. Constructor Overloading 
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

# Method Overriding
print(' # Method Overriding')


class Test10:
    def __init__(self) -> None:
        print('Parent constuctor executed')

    def walk(self):
        print('This is printed by Parent walk Method')

    def speak(self):
        print('This is printed by Parent speak Method')


class Test11(Test10):
    def __init__(self) -> None:
        super().__init__()
        print('Child constructer executed')

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
## 3.1 Method Overriding
```

```