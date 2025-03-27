# python

## python class compared to java
```
class Character:
    # __init_ is a constructor 
    # self rep the instance created by the class
    def __init__(self, health, damage, speed):
        self.health = health
        self.damage = damage
        self.speed = speed
    
    # we can pass self/instance into the function
    def double_speed(self):
        self.speed *=2


warrior = Character(20,30,40)
ninja = Character(30,50,40)

print(f"warrior speed: {warrior.speed}")
print(f"ninja speed: {ninja.speed}")
ninja.double_speed()
print(f"warrior speed: {warrior.speed}")
print(f"ninja speed: {ninja.speed}")
```
## how to extends to class in python
```
class Character:
    # __init_ is a constructor 
    # self rep the instance created by the class
    def __init__(self, health, damage, speed):
        self.health = health
        self.damage = damage
        self.speed = speed
    
    # we can pass self/instance into the function
    def double_speed(self):
        self.speed *=2

# pass in parameter to extend to class Character
class Teacher(Character):
    def __init__(self, health, damage, speed, intelligence):
        # calling parent contructor
        super().__init__(health, damage, speed)
        self.intelligence = intelligence

warrior = Character(20,30,40)
ninja = Character(30,50,40)
teacher = Teacher(30,40,50,100)

print(f"teach intelligence: {teacher.intelligence}")
```
