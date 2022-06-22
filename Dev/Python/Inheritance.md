---
sort : 1
---

# Inheritance

Is a way of inheriting all the methods and properties from another class.

```python

class Parent:
  def __init__(self, parm1, parm2):
    self.attr1 = parm1
    self.attr2 = parm2

  def method(self):
    print(self.attr1, self.attr2)


class Child(Parent):
    pass


Obj = Child(1, 2)

print(help(Obj))
```

This will print 

```
Help on Child in module __main__ object:

class Child(Parent)
 |  Child(parm1, parm2)
 |  
 |  Method resolution order:
 |      Child
 |      Parent
 |      builtins.object
 |  
 |  Methods inherited from Parent:
 |  
 |  __init__(self, parm1, parm2)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |  
 |  method(self)
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors inherited from Parent:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
```





# Super() 

used to extend a method in the parent class

```python

class Parent:
  def __init__(self, parm1, parm2):
    self.attr1 = parm1
    self.attr2 = parm2

  def method(self):
    print(self.attr1, self.attr2)


class Child(Parent):
    def __init__(self, parm1, parm2, parm3):
        super().__init__(parm1, parm2)          # instead of copying the parent __init__() content, Just call it
        self.attr3 = parm3

    def method(self, New):
        print(New)                              # Overwrite the Parent method


Obj = Child(1, 2, 3)
```