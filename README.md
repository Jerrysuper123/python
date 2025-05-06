# python

You're encountering this error because **Voila or Jupyter is running with a Python kernel that isn't pointing to your `.venv`**, even though you've activated the environment in your terminal. That’s why it can’t find `pandas`.

### 🔥 Key Clues from the Logs:

* Python version shown: **3.9.6**
* Your virtualenv is using **Python 3.13**

  ```
  /.../.venv/lib/python3.13/site-packages/...
  ```
* This mismatch means: **Voila is launching a different kernel than your `.venv`**, and `pandas` isn't installed there.

---

### ✅ Fix: Force Jupyter/Voila to Use Your `.venv` Kernel

#### 1. **Activate Your Environment in Terminal**

```bash
source .venv/bin/activate
```

#### 2. **Install `ipykernel` and Register Your Kernel**

Run this *inside the activated environment*:

```bash
pip install ipykernel
python -m ipykernel install --user --name user-behaviour-env --display-name "Python (user-behaviour)"
```

This registers your `.venv` environment with Jupyter.

#### 3. **Install Voila Inside the Virtual Environment**

To avoid version mismatches, do:

```bash
pip install voila
```

Then start Voila **from within the environment**:

```bash
voila your_notebook.ipynb
```

This ensures Voila uses the correct Python interpreter.

#### 4. **(Optional) Remove Broken Kernel**

You may have old/broken Jupyter kernels. List them:

```bash
jupyter kernelspec list
```

Remove any outdated ones (e.g., `python3`):

//we might have uninstall the old kernel to resolve the issue

```bash
jupyter kernelspec uninstall old-kernel-name
```

Replace `old-kernel-name` with the actual name you want to remove.

---

### ✅ Final Check

After all this, running:

```bash
which python
```

Should show:

```
/your/project/.venv/bin/python
```

And in the notebook interface, the kernel you use should be named:

```
Python (user-behaviour)
```

---



The relationship between **kernel**, **Python environment**, and **underlying libraries** is central to how a Jupyter Notebook or Python script runs. Here's a breakdown of how they interconnect:

### 1. **Kernel**

* A **kernel** is the computational engine that runs your code.
* In Jupyter Notebooks, the kernel executes the Python code in each cell and returns the result.
* Each kernel is tied to a specific **Python interpreter** (such as one from a virtual environment, system Python, or conda environment).
* When you change the kernel in Jupyter or VS Code, you're telling it which **Python environment** it should use to run the code.

### 2. **Python Environment**

* A **Python environment** refers to a specific **Python interpreter** along with its installed packages. This can be:

  * **System-wide Python** (default Python installed on your OS).
  * **Virtual Environments** (`.venv`, `venv`, `conda`, etc.), where you isolate specific packages for a project.
  * **Conda environments** (`conda create`), where you create and manage isolated environments with specific Python versions and dependencies.
* The **Python environment** ensures that your project uses the exact dependencies (such as `pandas`, `numpy`, etc.) you need for the project to run correctly.

### 3. **Underlying Libraries**

* The **underlying libraries** (such as `pandas`, `numpy`, `plotly`, etc.) are the **packages** installed within the **Python environment**.
* Libraries are installed via package managers like `pip` (e.g., `pip install pandas`) or `conda` (for Conda environments).
* The **kernel** communicates with the **Python environment** to access these libraries and execute the code that uses them.

---

### ✅ How They Work Together:

1. **Python Environment**:

   * You create a virtual environment for your project (e.g., `.venv`) to ensure that you have the exact packages you need for that specific project.
   * This environment contains a **specific version of Python** and any libraries you install, such as `pandas`, `numpy`, or `matplotlib`.

2. **Kernel**:

   * You select the **kernel** that is linked to your Python environment. The kernel uses the Python interpreter from that environment to execute the code.
   * If you select a kernel tied to a `.venv` or conda environment, it will use the exact Python interpreter and packages from that environment to run your code.

3. **Libraries**:

   * The libraries you install (e.g., `pandas`) are available for use in that Python environment.
   * If you're running code in a notebook, the kernel will use the packages installed in the environment to execute the notebook's code.

### Example Flow:

* You create a virtual environment (e.g., `.venv`) for your project.
* You install `pandas` and other libraries in that `.venv`.
* When you open a Jupyter notebook, you select the kernel corresponding to that `.venv` environment.
* The kernel executes the code and accesses the libraries installed in that `.venv`.

### Summary:

* **Kernel** is the engine that runs your code.
* **Python Environment** provides the interpreter and libraries.
* **Libraries** are the packages installed within the environment that your code uses.

When there's a **mismatch** between the kernel and the Python environment, or if the kernel can’t find the libraries installed in the current environment, you'll encounter errors like `ModuleNotFoundError`.


# Using UV
https://docs.astral.sh/uv/getting-started/features/

Old way of creating virtual env and start the app
```
1006  mkdir old_way
 1007  cd old_way
 1008  ls
//set up and active the virtual env
 1009  python3 -m venv .venv
 1010  source .venv/bin/activate
 1011  pip install fask requests
 1012  pip install flask requests
 1013  touch main.py
 1014  ls
 1015  ls -la
//create a requirement file, similar to package.json
 1016  pip freeze > requirement.txt
 1017  ls
 1018  cat requirement.txt
```

New way of using UV

```
1019  cd ..
 1020  ls
 1021  uv init new_app
 1022  cd new_app
 1023  ls
 1024  ls
 1025  ls -la
//UV automatically create git, main, readme, and pyproject.toml (similar to package.json), uv.lock (all dependencies tree)
.		.git		.python-version	main.py		README.md
..		.gitignore	.venv		pyproject.toml	uv.lock

//install dependencies
 1033  uv add flask requests
//show lib dependency tree
 1034  uv tree
 1035  deactivate
//even if u deactivate, you can still run the main.py
//even if u deleted .venv, becos of the uv.lock file, uv can install based on all the dependencies.
//u do not have to manage the .venv again
 1036  uv run main.py
```

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
