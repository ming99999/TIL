
## ABC와 Abstract method

추상 클래스를 상속받는 하위 클래스가 반드시 해당 메소드를 구현하도록 해준다.


```python
from abc import *

class Flyable(metaclass = ABCMeta):    #creating new ABC
    name = "Unknown"
        
    def myname(self):
        pass
    
    @abstractmethod                    #decorator for abstract method
    def flying(self):
        pass
```


```python
# sub classes of abc 'Flyable'

class Duck(Flyable):
    def __init__(self, name):
        self.name = name
        
    def myname(self):
        print("my name is {}".format(self.name))
        
    def flying(self):
        print("{} can fly!".format(self.name))

        
class Airplane(Flyable):
    def __init__(self, name):
        self.name = name
        
    def flying(self):
        print("{} can fly!".format(self.name))

        
class Chicken(Flyable):
    def __init__(self, name):
        self.name = name
        
    def myname(self):
        print("my name is {}".format(self.name))
```

하위 클래스의 인스턴스를 만들어보자


```python
boo = Duck("Duck")
boo.myname()
boo.flying()
```

    my name is Duck
    Duck can fly!


하위 클래스가 상위 클래스의 메소드를 구현하지 않았을 경우, 상위 클래스의 메소드를 그대로 사용한다 


```python
foo = Airplane("Airplane")
foo.myname()                          #Not implemented
foo.flying()
```

    Airplane can fly!


하지만 상위 클래스의 abstract method를 구현하지 않았다면, 하위 클래스의 인스턴스 생성시 에러가 발생한다 


```python
qoo = Chicken("Chicken")
qoo.myname()
qoo.flying()                          #Not implemented
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-17-f9ed9bb6a2aa> in <module>
    ----> 1 qoo = Chicken("Chicken")
          2 qoo.myname()
          3 qoo.flying()


    TypeError: Can't instantiate abstract class Chicken with abstract methods flying


abstract method를 구현하고 다시 인스턴스를 생성하면 잘 작동한다.


```python
class Chicken(Flyable):
    def __init__(self, name):
        self.name = name
        
    def myname(self):
        print("my name is {}".format(self.name))
        
    def flying(self):
        print("I wanna fly")
```


```python
qoo = Chicken("Chicken")
qoo.myname()
qoo.flying()
```

    my name is Chicken
    I wanna fly

