# python

# Standard Output (stdout)

In computing, stdout stands for Standard Output. It refers to the default output stream where a program writes its output data. When a program executes, it can produce output in various forms, such as text, images, or audio. Stdout is one of the three standard streams in Unix-like operating systems, along with stdin (Standard Input) and stderr (Standard Error).

How stdout works

When a program runs, it inherits three file descriptors:

0: stdin (input)
1: stdout (output)
2: stderr (error)
By default, stdout is connected to the terminal or console where the program is running. Any output written by the program to stdout is displayed on the screen.

Examples of stdout

A simple echo command in a shell script: echo "Hello World!" outputs "Hello World!" to stdout.
A Python program that uses print(): print("Hello World!") outputs "Hello World!" to stdout.
A Java program that uses System.out.println(): System.out.println("Hello World!"); outputs "Hello World!" to stdout.
Redirecting stdout

Output can be redirected from stdout to a file or another device using redirection operators (>, >>, etc.). For example:

echo "Hello World!" > output.txt redirects the output to a file named output.txt.
echo "Hello World!" >> output.txt appends the output to the end of the existing file output.txt.
In summary, stdout is the primary output stream where programs write their output data, which is usually displayed on the screen or redirected to a file or other device.

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
## python enum, similar to ts and java
```
class CALL_STATUS(Enum):
    EXCEEDED_LIMIT = 1
    UNAVAILABLE = 2

```
