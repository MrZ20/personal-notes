## 课程（python）

### 编程语言知识与应用

#### 计算机基础

##### <u>计算机的组成</u>

**1. 硬件系统 (Hardware System)**

硬件是计算机的**物理实体**部分，看得见摸得着。它通常包括：

- **中央处理器 (CPU)：**

  - 被誉为计算机的“大脑”，负责**执行指令**和**进行运算**。
  - 包括**控制器**（Control Unit）和**运算器**（Arithmetic Logic Unit, ALU）。

- **存储器 (Memory)：**

  - 用于**存储数据和程序**。
  - 主要分为**内存**（主存储器，如 RAM 和 ROM）和**外存**（辅助存储器，如硬盘、固态硬盘、光盘等）。

- **输入设备 (Input Devices)：**

  - 用于向计算机**输入数据和命令**。
  - 例如：**键盘**、**鼠标**、扫描仪、麦克风等。

- **输出设备 (Output Devices)：**

  - 用于将计算机**处理结果显示或输出**。
  - 例如：**显示器**、**打印机**、音箱等。

- **总线 (Bus)：**

  - 连接所有硬件部件的**通信线路**，用于数据、地址和控制信息的传输。

  

**2. 软件系统 (Software System)**

软件是**程序、数据及相关文档**的集合，指挥硬件完成特定任务。它通常分为：

- **系统软件 (System Software)：**
  - 负责**管理和控制**计算机硬件和软件资源的软件。
  - 主要包括：
    - **操作系统 (OS)**：如 Windows、macOS、Linux、Android 等。
    - **语言处理程序**：如编译器、解释器。
    - **数据库管理系统** (DBMS) 等。
- **应用软件 (Application Software)：**
  - 为了**解决特定应用领域问题**而开发的软件。
  - 例如：文字处理软件（如 Word）、电子表格软件（如 Excel）、浏览器、游戏、绘图软件等。



##### <u>计算机的使用</u>

软件不是所有功能都对用户开放，用户需要调用软件提供的接口（Interface 交互界面）来操作计算机

用户界面分成两种：TUI（文本交互界面），GUI（图形化交互界面）



##### <u>环境变量</u>

environment variable

修改环境变量，来对计算机进行配置，主要用来配置一些路径



**Linux** 的环境变量通常分为**临时**（只在当前 Shell 会话有效）和**永久**（写入配置文件并在每次启动时加载）。

| **操作**             | **命令**                                                     | **说明**                                                     | **持续性**          |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------- |
| **查看所有**         | `env` 或 `printenv`                                          | 显示所有环境变量。                                           | -                   |
| **查看单个**         | `echo $VARIABLE_NAME`                                        | 显示特定环境变量的值。                                       | -                   |
| **添加/修改 (临时)** | `export VAR_NAME="value"`                                    | 在当前会话中设置或修改变量。                                 | **当前会话有效**    |
| **添加/修改 (永久)** | `vim ~/.bashrc` 或 `~/.zshrc`   然后添加 `export VAR_NAME="value"` | 将变量写入用户配置文件。**重启 Shell 或运行 `source` 后生效。** | **永久** (用户级别) |
| **生效配置**         | `source ~/.bashrc`   或 `source ~/.zshrc`                    | 使修改后的配置文件立即生效，无需重启 Shell。                 | -                   |
| **删除 (临时)**      | `unset VAR_NAME`                                             | 删除当前 Shell 会话中的变量。                                | **当前会话有效**    |
| **删除 (永久)**      | 手动从配置文件中删除对应的 `export` 行，然后 `source` 使其生效。 | -                                                            | -                   |
| **PATH 变量**        | `export PATH=$PATH:/new/path/to/bin`                         | **追加**新路径到现有的 PATH 变量。                           | 临时或永久          |



**Windows** 的环境变量分为**用户变量**（只对当前用户有效）和**系统变量**（对所有用户和系统有效）。

**1. 图形用户界面 (GUI) 操作 (永久)**

这是最常用且影响**永久**的方式：

1. 在 Windows 搜索框中输入 "**环境变量**" 或 "**Edit the system environment variables**" (编辑系统环境变量)。
2. 点击 "**环境变量**" 按钮。
3. 在弹出的对话框中：
   - **添加/修改：** 在 "**用户变量**" 或 "**系统变量**" 框中，点击 "**新建**" 或选择现有变量点击 "**编辑**"。
   - **删除：** 选择变量后点击 "**删除**"。
4. 点击 "**确定**" 保存更改。
5. **注意：** 更改后，需要**打开一个新的命令行窗口**（CMD 或 PowerShell）才能使更改生效。



 **2. 命令行 (CMD) 操作 (临时/永久)**

| **操作**             | **命令**                          | **说明**                                                     | **持续性**       |
| -------------------- | --------------------------------- | ------------------------------------------------------------ | ---------------- |
| **查看所有**         | `set`                             | 显示所有当前可用的环境变量。                                 | -                |
| **查看单个**         | `echo %VARIABLE_NAME%`            | 显示特定环境变量的值。                                       | -                |
| **添加/修改 (临时)** | `set VAR_NAME=value`              | 在当前 CMD 会话中设置或修改变量。                            | **当前会话有效** |
| **添加/修改 (永久)** | `setx VAR_NAME "value" [/M]`      | 永久设置变量。`/M` 用于系统变量，不加则为用户变量。**新窗口生效** | **永久**         |
| **删除 (临时)**      | `set VAR_NAME=` (将值设置为空)    | 删除当前 CMD 会话中的变量。                                  | **当前会话有效** |
| **删除 (永久)**      | `setx VAR_NAME ""` 或图形界面操作 | `setx` 无法直接删除，通常通过设置为**空字符串**或使用 GUI。  | **永久**         |
| **PATH 变量**        | `set PATH=%PATH%;C:\new\path`     | **追加**新路径到现有的 PATH 变量 (临时)。                    | 临时             |
| **PATH 变量 (永久)** | `setx PATH "%PATH%;C:\new\path"`  | **追加**新路径到现有的 PATH 变量 (永久)。                    | 永久             |



##### <u>编译型和解释型语言</u>

**1. 编译型语言 (Compiled Languages)**

编译型语言是指使用**编译器**将高级语言源代码**一次性**转换成目标机器码（机器语言）的程序。这个过程在程序**运行之前**完成。

**工作流程**

1. **编译 (Compile)：** 源代码通过**编译器**转换为机器码 (可执行文件，如 `.exe`, `.out`)
2. **运行 (Execute)：** 直接运行生成的机器码

**核心特点**

- **运行速度快：** 一次性编译成机器码，执行效率高。
- **跨平台性差：** 编译后的机器码通常只能在特定操作系统和硬件架构上运行（如 Windows 上的 `.exe` 不能直接在 Linux 上运行）。
- **调试难度高：** 编译过程长，且程序错误通常在运行前（编译时）或运行时以复杂的形式出现。

**典型代表**

C、C++、Rust、Go



**2. 解释型语言 (Interpreted Languages)**

解释型语言是指使用**解释器**逐条读取并执行源代码的程序。这个过程在程序**运行时**动态进行。

**工作流程**

1. **运行 (Execute)：** 源代码通过**解释器**转换成机器码/操作

**核心特点**

- **运行速度慢：** 每次执行时都需要解释器进行转换，效率相对较低。
- **跨平台性好：** 只要有对应的解释器，源代码可以在不同的操作系统上运行（"一次编写，到处运行"）。
- **调试方便：** 程序错误容易定位到具体的代码行，修改后无需重新编译即可运行。

**典型代表**

Python、JavaScript (通常在浏览器或 Node.js 环境下解释执行)、Shell 脚本 (Bash, Zsh)、Ruby



**3. 混合型语言（JIT 或字节码）**

![image-20251031164023407](C:\Users\57108\AppData\Roaming\Typora\typora-user-images\image-20251031164023407.png)



#### python简介

### 对象

#### 继承

##### <u>MRO</u>

**核心定义**

MRO 是一个**线性的列表**，它定义了当你在一个实例或类上调用一个方法或访问一个属性时，Python 解释器应该沿着哪个路径去查找这个方法或属性。

- **目的：** 解决在多重继承中，如果多个父类拥有同名方法，到底应该调用哪一个的问题。
- **如何查找：** 当调用一个方法时，Python 会沿着这个 MRO 列表**从左到右**依次查找。一旦找到匹配的方法，就停止查找并执行该方法。

**查看 MRO**

任何类都有 MRO 列表，你可以通过以下两种方式查看：

1. **魔术属性：** `ClassName.__mro__`
2. **内置函数：** `help(ClassName)`

```python
class A: pass
class B(A): pass

# B 的 MRO: (B, A, object)
```

**MRO 的计算：C3 线性化算法**

从 Python 2.3 开始，所有新式类都使用 **C3 线性化算法**来计算 MRO。C3 算法保证了 MRO 具有以下两个关键特性：

**1. 局部优先原则 (Local Precedence)**

子类永远优先于父类被搜索。在一个类的继承列表中，列在前面的父类优先于列在后面的父类被搜索。

- 如果 `class Child(Parent1, Parent2):`
  - 那么 `Parent1` 必须在 MRO 中排在 `Parent2` 之前。

**2. 单调性原则 (Monotonicity)**

一旦确定了一个类的 MRO，那么在任何继承自该类的子类中，**父类之间的相对顺序不能被颠倒**。

- 如果在一个类X的 MRO 中P_1在P_2之前，那么在X的所有子类Y的MRO中，只要P_1和 P_2都存在，它们依然保持P_1在P_2之前的顺序。
- 这个原则避免了复杂的、易错的继承结构。



#### 类中的属性和方法

##### <u>类属性 (Class Attributes)</u>

- **定义位置：** 直接在类体中定义，但在任何方法之外。
- **归属/存储：** 属于类本身，存储在类的字典中。
- **共享性：** **所有**实例共享**同一个**类属性。
- **访问方式：**
  - 通过**类名**访问和修改：`ClassName.class_attribute`
  - 通过**实例名**访问（但不推荐通过实例直接修改，因为这可能会创建一个同名的实例属性来“覆盖”它）。

```python
class Dog:
    # 这是一个类属性
    species = "Canis familiaris" 
    
    def __init__(self, name):
        self.name = name

# 通过类名访问
print(Dog.species) # 输出: Canis familiaris 

my_dog = Dog("Buddy")
# 通过实例名访问
print(my_dog.species) # 输出: Canis familiaris
```

##### <u>实例属性 (Instance Attributes)</u>

- **定义位置：** 通常在 `__init__` 构造方法中使用 `self.attribute_name` 来定义。
- **归属/存储：** 属于特定的实例对象，存储在实例的字典中。
- **独立性：** 每个实例都有自己独立的实例属性，彼此不共享。
- **访问方式：** 只能通过**实例名**访问和修改：`instance_name.instance_attribute`

##### <u>类方法 (Class Methods)</u>

- **装饰器：** 必须使用 `@classmethod` 装饰器。
- **第一个参数：** 必须是 `cls` (Class 的缩写)，它代表方法被调用时所操作的**类本身**。
- **作用：** 主要用于操作类属性，或创建类的工厂方法（根据不同的输入返回类的实例）。
- **调用方式：** 可以通过**类名**或**实例对象**调用，但通常推荐使用**类名**调用：`ClassName.class_method()`

```python
class Dog:
    breed = "Unknown" # 类属性
    
    @classmethod
    def change_breed(cls, new_breed):
        # 它可以访问和修改类属性 cls.breed
        cls.breed = new_breed
        return f"Breed is now {cls.breed}"
    
print(Dog.breed) # 输出: Unknown
print(Dog.change_breed("Golden Retriever")) # 输出:Breed is now Golden Retriever
print(Dog.breed) # 输出: Golden Retriever
```

##### <u>实例方法 (Instance Methods)</u>

- **装饰器：** 不需要装饰器（默认就是实例方法）。
- **第一个参数：** 必须是 `self`，它代表方法被调用时所操作的**实例对象**本身。
- **作用：** 最常用的方法类型，用于操作实例属性，或执行需要访问实例特定数据的任务。
- **调用方式：** 必须通过**实例对象**来调用：`instance_name.method()`

##### <u>静态方法 (Static Methods)</u>

- **装饰器：** 必须使用 `@staticmethod` 装饰器。
- **参数：** **不需要**默认的第一个参数 (`self` 或 `cls`)。
- **作用：** 它们是逻辑上属于类，但在功能上**与类或实例数据无关**的工具函数。它们只是被放置在类命名空间中以实现更好的组织性。
- **调用方式：** 可以通过**类名**或**实例对象**调用：`ClassName.static_method()`



### 编程规范理解与应用



### 软件测试

unittest

mock

pytest

doctest

覆盖率

测试原则-FIRST

Fast、Isolated、Repeatable、Self-Validating、Timely（Test-Driven Development）

### 调试与定位

#### pdb调试器

[pdb --- Python 的调试器 — Python 3.14.0 文档](https://docs.python.org/zh-cn/3.14/library/pdb.html)



## python高阶

### 装饰器

两个基本原则

- 不能修改被装饰函数的源码

- 不能修改被装饰函数的调用方式

装饰器 = 高阶函数 + 嵌套函数

#### 前置

##### <u>函数即变量</u>

函数既可以直接被调用，也可以作为变量赋值

```python
# 相当于变量，保存在一个内存地址
# 函数定义中调用其他函数，并不会立即调用函数
def boo():
	print("in boo")
    foo()

def foo():
	print("in foo")

a = foo  # 指向函数的内存地址
a()
# 虽然foo在boo下方，但程序并不会报错，因为定义函数值分配内存，不会调用函数到cpu上执行
boo()
```

##### <u>高阶函数</u>

符合下列条件：

- 接受函数名作为形参
- 返回值中包含函数名

```python
import time
def boo():
    time.sleep(3)
	print("in boo")

def gf(func):
    start_time = time.time()  # 运行函数前附加的功能语句
    func()
    end_time = time.time()  # 运行函数前附加的功能语句
    print(f"运行时间是{end_time-start_time}s")  # 运行函数前附加的功能语句

gf(boo)  # 改变了boo的调用方式，不满足装饰器的条件
```

##### <u>嵌套函数</u>

定义：在函数里面定义函数，调用函数不算

```python
import time

def boo():
    time.sleep(3)
	print("in boo")

def gf(func):
    start_time = time.time()
    return func
    end_time = time.time()  # 无法运行
    print(f"运行时间是{end_time-start_time}s")  # 无法运行

boo = gf(boo)
boo()

# ===========修改后===============
def timer(func):
    def gf():
        start_time = time.time()
        func()
        end_time = time.time()
        print(f"运行时间是{end_time-start_time}s")
    return gf

# 方法1
def boo():
    time.sleep(3)
	print("in boo")
boo = gf(boo)
boo()

# 方法2
@timer  # boo = timer(boo)
def boo():
    time.sleep(3)
	print("in boo")
boo()
```

#### 被装饰器带参数

```python
import time

def timer(func):
    def gf(*arg, **kwargs):  # 避免参数不确定
        start_time = time.time()
        func(*arg, **kwargs)
        end_time = time.time()
        print(f"运行时间是{end_time-start_time}s")
    return gf

@timer  # boo = timer(boo) ==> boo = gf ==> boo(name) == gf(name)
def boo(name, age):
    time.sleep(3)
	print("in boo", name, age)

boo("Lisi", 11)
```

#### 装饰器带参数

```python
import time

def timer(timer_type):
    print(timer_type)
    def outer(func):
        def inner(*arg, **kwargs):  # 避免参数不确定
            start_time = time.time()
            func(*arg, **kwargs)
            end_time = time.time()
            print(f"运行时间是{end_time-start_time}s")
        return inner
    return outer

@timer(timer_type='minutes')  # boo = timer(timer_type='minute')(boo)
def boo(name, age):
    time.sleep(3)
	print("in boo", name, age)

boo("Lisi", 11)  # inner(*arg, **kwargs)
```

#### 被装饰函数带返回值

```python
import time

def timer(timer_type):
    print(timer_type)
    def outer(func):
        def inner(*arg, **kwargs):  # 避免参数不确定
            start_time = time.time()
            res = func(*arg, **kwargs)
            end_time = time.time()
            print(f"运行时间是{end_time-start_time}s")
            return res
        return inner
    return outer

@timer(timer_type='minutes')  # boo = timer(timer_type='minute')(boo)
def boo(name, age):
    time.sleep(3)
	print("in boo", name, age)
    return name

print(boo("Lisi", 11) ) # inner(*arg, **kwargs)
```

#### 装饰器执行顺序

```python
# 原始代码
@timer(timer_type='minutes')
def boo(name, age):
    # ...

# 解释器的实际处理顺序
# 1. 函数声明完成：定义了原始 boo
def boo(name, age):
    # ...
    
# 2. 装饰器执行：相当于执行了两个执行语句（赋值语句）

# 第一步执行： timer(timer_type='minutes')
_decorator_func = timer(timer_type='minutes') # 得到 outer 函数

# 第二步执行： outer(boo) 并重新赋值给 boo
boo = _decorator_func(boo) # 注意，这里的 boo 是在步骤 1 中刚声明的！
```

#### 闭包

所有装饰器都是闭包

```python
func_list = []
# 情况1
for i in range(3):
    def myfunc(a):
        return i+a  # 此时i是公有变量，我理解是实参，调用函数的时候i已经是2了
    func_list.append(myfunc)  # 这里是作为变量赋值

# 情况2
for i in range(3):
    def deco(i):
        def myfunc(a):
            return i+a  # 此时的i是私有变量，我理解是形参
        return myfunc
    func_list.append(deco(i))
    
for f in func_list:
    print(f(1))
```



#### 总结

```python
# (1)被装饰器函数带有参数或不带参数
def deco(func):
    def inner(*args, **kwargs):
        # 包含所有要附加的功能
        func(*args, **kwargs)
    return inner

# (2)装饰器本身带参数
def deco(parma):
    def outer(func):
        def inner(*args, **kwargs):
            # 包含所有要附加的功能
            func(*args, **kwargs)
    	return inner
	return outer

# (3)被装饰器有返回值
def deco(parma):
    def outer(func):
        def inner(*args, **kwargs):
            # 包含所有要附加的功能
            res = func(*args, **kwargs)
            return res
    	return inner
    return outer
```

### 多线程

#### 进程、线程、并行并发

##### <u>进程(Process)</u>

一个进程是**程序在计算机上的一次执行活动**。

- **定义：** 它是操作系统进行资源分配（如内存空间、文件句柄等）的基本单位。
- **资源：** 每个进程都有自己独立的**内存地址空间**。一个进程中的数据和代码对其他进程是**隔离**的，互不干扰。
- **开销：** 创建、销毁或切换进程的**开销较大**，因为需要分配和回收大量资源。
- **类比：** 想象一个进程就是一个**独立的车间**。车间里有自己的机器、原材料和工人，与其他车间完全隔离。

##### <u>线程(Thread)</u>

线程是**进程内的一个执行单元**，也被称为**轻量级进程**。

- **定义：** 它是操作系统进行**CPU调度**和执行的基本单位。
- **资源：** **同一进程内**的所有线程**共享**该进程的资源，如内存地址空间、文件句柄等；每个进程至少有一个主线程。
- **独立性：** 线程拥有自己独立的**程序计数器**、**栈**和**寄存器**等上下文信息。
- **开销：** 创建、销毁或切换线程的**开销较小**，因为它不涉及独立的资源分配。
- **类比：** 进程是车间，线程就是**车间里的工人**。工人们共享车间的资源（机器、原材料），但每个人执行自己的具体任务。

##### <u>并行(Concurrency)</u>

并发的重点在于**如何处理（Deal with）**多个任务，让它们看起来像在同时进行。

- **定义：** 指的是在**同一时间段内**，系统能够处理**多个任务**的能力。它通过在任务之间**快速切换**（时间片轮转）来实现，使每个任务都有机会向前推进。
- **硬件要求：** 可以在**单核 CPU** 上实现。
- **微观状态：** **同一时刻**，只有一个任务真正在执行。
- **宏观状态：** 多个任务交替执行，给人以“同时进行”的错觉。
- **目标：** 提高系统的**响应速度**和**效率**，尤其是在处理 I/O 密集型任务（如等待网络响应、读写文件）时，可以利用等待时间去执行其他任务。

##### <u>并发(Parallelism)</u>

并行的重点在于**如何真正执行（Execute）**多个任务，实现同时运行。

- **定义：** 指的是在**同一时刻**，**多个任务**在**多个执行单元**（如多核 CPU）上**真正地同时运行**。
- **硬件要求：** **必须**有**多核/多处理器**的硬件支持。
- **微观状态：** **同一时刻**，多个任务都在独立执行。
- **宏观状态：** 多个任务在物理上同时完成工作。
- **目标：** 提高系统的**处理能力**和**计算速度**，尤其是在处理 CPU 密集型任务（如复杂的数学计算、图形渲染）时。

#### threading库

##### <u>核心线程管理</u>

**`threading.Thread`类**（线程对象）：用于表示一个独立的执行进程

| **方法/属性**            | **描述**                                                     | **用法示例**                                        |
| ------------------------ | ------------------------------------------------------------ | --------------------------------------------------- |
| **`__init__(...)`**      | 构造函数，用于创建线程实例。                                 | `t = threading.Thread(target=my_func, args=(1, 2))` |
| **`target`**             | **必需**。线程启动时要执行的函数或可调用对象。               |                                                     |
| **`args`**               | 传递给 `target` 函数的位置参数（元组）。                     |                                                     |
| **`kwargs`**             | 传递给 `target` 函数的关键字参数（字典）。                   |                                                     |
| **`name`**               | 线程的名称。                                                 |                                                     |
| **`start()`**            | **启动线程**。调用后，线程开始运行 `target` 指定的函数。     | `t.start()`                                         |
| **`join(timeout=None)`** | **等待线程结束**。调用此方法的线程会阻塞，直到被调用的线程执行完毕或达到 `timeout` 时间。 | `t.join()`                                          |
| **`run()`**              | 线程执行体。通常通过继承 `Thread` 类并重写此方法来实现自定义线程逻辑，但对于简单任务直接使用 `target` 更常见。 |                                                     |
| **`name`**               | 获取或设置线程的名称。                                       | `print(t.name)`                                     |
| **`is_alive()`**         | 判断线程是否仍在执行（存活）。                               | `if t.is_alive(): ...`                              |

**模块级函数**

| **函数**                         | **描述**                                           |
| -------------------------------- | -------------------------------------------------- |
| **`threading.current_thread()`** | 返回当前执行的 **Thread 对象**。                   |
| **`threading.main_thread()`**    | 返回主线程对象（即启动 Python 解释器的那个线程）。 |
| **`threading.active_count()`**   | 返回当前存活的 **Thread 对象**的数量。             |
| **`threading.enumerate()`**      | 返回一个包含所有存活 **Thread 对象**的列表。       |

##### <u>线程同步原语</u>

当多个线程访问或修改共享数据时，可能会导致数据竞争和错误。同步原语用于协调线程的执行顺序，确保数据安全。

**1. 锁 (Lock)**

GIL = 全局解释器锁，python伪并行

GIL什么时候释放：

- 当前的执行线程在执行I/O操作时，会主动放弃GIL锁

- 当前执行的线程执行100条字节码的时候，会自动释放GIL锁

```python
import threading

num = 0
# GIL是粗粒度的锁，必须配合线程模块中的锁才能对每个原子操作进行锁定
# 如果没有Lock，数据量过大，还没操作完，就自动释放GIL，造成数据混乱
lock = threading.Lock()
def deposit():
    for i in range(1000000):
        lock.acquire()  # 主动获取锁
        global num
        num += 1
        lock.release()  # 主动释放锁
def withdraw():
    for i in range(1000000):
        with lock:  # 自动获取释放锁
            global num
            num -= 1
        
if __name__ == '__main__':
    # 主线程
    t1 = threading.Thread(target=deposit)
    t2 = threading.Thread(target=withdraw)
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print(num)
```

最基本的同步机制，用于保护共享资源。

| **方法/属性**                | **描述**                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| **`threading.Lock()`**       | 创建一个**互斥锁**对象（Mutex）。                            |
| **`acquire(blocking=True)`** | 获取锁。如果锁已被占用，线程将被阻塞（默认行为），直到锁被释放。 |
| **`release()`**              | 释放锁。必须在线程获取锁之后才能释放。                       |

推荐使用 `with` 语句来管理锁的获取和释放，确保即使发生异常，锁也能被正确释放。

```python
lock = threading.Lock()
with lock:
    # 访问共享资源的代码块
    pass # 离开 with 块时，锁自动释放
```

**2. 递归锁 (RLock)**

允许**同一个线程**多次获取它已经持有的锁，只有当获取和释放次数匹配时，锁才真正释放。

| **方法/属性**                 | **描述**                                 |
| ----------------------------- | ---------------------------------------- |
| **`threading.RLock()`**       | 创建一个递归锁。                         |
| **`acquire()` / `release()`** | 与 `Lock` 类似，但支持同一线程多次调用。 |

**3. 信号量 (Semaphore)**

用于控制对共享资源的访问数量，而不是仅限于一个。

| **方法/属性**                    | **描述**                                           |
| -------------------------------- | -------------------------------------------------- |
| **`threading.Semaphore(value)`** | 创建一个信号量，`value` 为最大访问计数（许可数）。 |
| **`acquire()`**                  | 获取一个许可。如果许可数为零，则阻塞。             |
| **`release()`**                  | 释放一个许可，使许可数加一。                       |

```python
import threading
import time

class HtmlSpider(threading.Thread):
    def __init__(self, url, sem):
        super().__init__()
        self.url = url
        self.sem = sem
        
    def run(self):
        time.sleep(2)
        print(f"获取网页内容成功: {self.url}")
        self.sem.release()  # 爬取完毕释放锁资源
        
class UrlProducer(threading.Thread):
    def __init__(self, sem):
        super().__init__()
        self.sem = sem
        
    def run(self):
        for i in range(20):
            self.sem.acquire()  # 先获取锁再执行线程
            html_thread = HtmlSpider(f"http://www.baidu.com/{i}", self.sem)
            html_thread.start()

if __name__ == '__main__':
    sem = threading.Semaphore(value=3)
    url_producer = UrlProducer(sem)
    url_producer.start()

```

**4. 条件变量 (Condition)**

用于线程间的复杂通信。一个线程可以等待某个条件成立，而另一个线程可以通知等待的线程条件已成立。

| **方法/属性**                        | **描述**                               |
| ------------------------------------ | -------------------------------------- |
| **`threading.Condition(lock=None)`** | 创建一个条件变量，通常内部自带一个锁。 |
| **`wait()`**                         | 释放内部锁并阻塞，直到被通知（唤醒）。 |
| **`notify(n=1)`**                    | 唤醒最多 `n` 个正在等待的线程。        |
| **`notify_all()`**                   | 唤醒所有正在等待的线程。               |

##### <u>代码</u>

```python
# 通过Thread类构造器创建新线程
import threading

def get_web(url):  # 子线程
    pass

if __name__ == '__main__':
    # 主线程
    t1 = threading.Thread(target=get_web, args=('<url_1>',))
    t2 = threading.Thread(target=get_web, args=('<url_2>',))
    t1.start()
    t2.start()
    t1.join()  # 让子线程阻塞主线程的执行过程，等待子线程结束后再往下执行
    t2.join()
    print("Finished！")  # 没有join，会先打印这句
```

```python
# 通过继承于Thread类来创建新线程
import threading

class MyThread(threading.Thread):
    def __init__(self, url):
        super.__init__()
        self.url = url
        
    def run(self): # 重写父类的run方法，定义在新的线程类里面要完成的task
        pass  # def get_web(url)里面的内容
    
if __name__ == '__main__':
    # 主线程
    t1 = MyThread("线程1","<url_1>")
    t2 = MyThread("线程2","<url_2>")
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print("Finished！")
```



#### 线程间通讯机制

##### <u>消息队列 (Message Queue) - `queue.Queue`</u>

消息队列是线程间通信的**首选和最安全**的方式，它实现了生产者-消费者模式，通过**间接数据传输**来避免直接共享数据带来的复杂性。主要用于不同线程间任意类型数据的共享。

**核心概念**

- **FIFO (先进先出):** 默认情况下，消息按照放入的顺序取出。
- **线程安全:** `queue.Queue` 内建了锁和条件变量，所有操作（`put` 和 `get`）都是原子性的，这意味着您无需额外加锁即可安全地在多个线程中使用它。
- **缓冲与阻塞:** 队列有容量限制（可选），并在存取时提供阻塞机制。

**常用方法**

| **方法**               | **描述**                                                     | **应用场景**                 |
| ---------------------- | ------------------------------------------------------------ | ---------------------------- |
| **`Queue(maxsize=0)`** | 创建队列，默认为0，即不受限制                                |                              |
| **`put(item)`**        | 将数据项放入队列。如果队列已满，默认会阻塞，直到有空间。     | **生产者线程**用来发送数据。 |
| **`get(timeout=1)`**   | 从队列中取出并移除一个数据项。如果队列为空，默认会阻塞，直到有数据。 | **消费者线程**用来接收数据。 |
| **`qsize()`**          | 返回队列中当前的数据项数量。                                 | 调试或监控。                 |
| **`join()`**           | 阻塞，直到队列中的所有项都被取出并处理完毕。                 | 确保所有任务都被完成。       |

**优势**

- **安全:** 极大地简化了线程安全问题，开发者无需手动管理锁。
- **解耦:** 生产者和消费者之间只依赖队列接口，彼此不需要知道对方的存在。
- **流量控制:** 队列的大小可以限制内存使用，阻塞机制可以调节生产和消费速度。

**代码**

```python
from queue import Queue
import threading
import time

def product(q):
    kind = ('1', '2', '3')
    for i in range(3):
        print(threading.current_thread().name, 'start')
        time.sleep(1)
        q.put(kind[i%3])
        print(threading.current_thread().name, 'end')

def consumer(q):
    while True:
        print(threading.current_thread().name, 'ready')
        time.sleep(1)
        t = q.get()
        print('{} finish'.format(t))

if __name__ == '__main__':
    q = Queue(maxsize = 1)
    # start product
    threading.Thread(target=product, args=(q,)).start()
    threading.Thread(target=product, args=(q,)).start()
    # start consumer
    threading.Thread(target=consumer, args=(q,)).start()
```



##### <u>事件对象 (Event Object) - `threading.Event`</u>

`Event` 对象是用于**简单线程信号通知**的同步原语。它像一个“旗帜”或“红绿灯”，用于一个线程通知其他线程发生了某个事件。主要用于通过事件通知机制实现线程的大规模并发。

**核心概念**

- **二元状态:** `Event` 只有两种状态：**设置 (True)** 和 **未设置 (False)**。
- **广播唤醒:** 当旗帜被设置为 True 时，所有正在等待的线程都会被同时唤醒。

**常用方法**

| **方法**                 | **描述**                                                     |
| ------------------------ | ------------------------------------------------------------ |
| **`Event()`**            | 创建                                                         |
| **`set()`**              | 将事件状态设置为 True。这会**立即唤醒**所有正在 `wait()` 的线程。 |
| **`clear()`**            | 将事件状态重置为 False。                                     |
| **`wait(timeout=None)`** | 阻塞当前线程，直到事件状态被设置为 True。如果事件已经是 True，则立即返回。 |
| **`is_set()`**           | 返回事件的当前状态 (True/False)。                            |

**应用场景**

- **启动控制:** 主线程等待所有子线程就绪后，通过 `set()` 发出“开始”信号。
- **全局停止:** 在程序需要紧急退出时，通过 `set()` 向所有工作线程发送“停止”信号。

**代码**

```python
import threading
import time

class MyThread(threading.Thread):
    def __init__(self, event):
        super().__init__()
        self.event = event
    
    def run(self):
        print(f"线程{self.name}已经初始化完成，随时准备启动...")
        self.event.wait()
        print(f"{self.name}开始执行...")

if __name__ == "__main__":
    event = threading.Event()
    threads = []
    [threads.append(MyThread(event)) for i in range(1,11)]

    event.clear()
    [t.start() for t in threads]
    time.sleep(2)
    event.set()
    [t.join() for t in threads]
```



##### <u>条件对象 (Condition Object) - `threading.Condition`</u>

`Condition` 对象是一种更复杂的同步机制，它允许线程在**特定条件满足**时进行**有针对性的通信和等待**。它总是与一个锁（Lock 或 RLock）绑定，用于保护共享数据。主要用于多个线程间轮流交替执行任务。

**核心概念**

- **条件等待:** 线程可以在**持有锁**时进入等待状态，并**暂时释放**锁。
- **精确通知:** 线程可以在修改共享数据后，通知**特定**或**全部**等待该条件的线程。

**核心方法（配合锁使用）**

| **方法**                    | **描述**                                                     | **内部操作**                             |
| --------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| **`acquire()`/`release()`** | 获得/释放内部关联的锁。                                      | 确保对共享数据的检查和修改是原子性的。   |
| **`wait(timeout=None)`**    | **释放内部锁**，并阻塞等待通知。被唤醒后，它会**重新获取**锁，然后返回。 | 用于线程：**等待**某个条件满足。         |
| **`notify(n=1)`**           | 唤醒最多 n 个正在等待的线程。                                | 用于线程：**通知**等待者条件可能已满足。 |
| **`notify_all()`**          | 唤醒所有正在等待的线程。                                     | 用于线程：**通知**所有等待者。           |

**应用场景**

- **高级生产者-消费者:** 当使用 `queue.Queue` 不足以满足需求时（例如，需要等待一个自定义数据结构中的特定条件，如“列表长度大于 5”）。
- **资源分配:** 一个线程等待某个资源可用，只有在资源被释放或创建时，才会被唤醒。

**代码**

```python
import threading
import time

cond = threading.Condition()  # 公用，不是每个线程调用

class person1(threading.Thread):
    def __init__(self, cond, name):
        threading.Thread.__init__(self, name=name)
        self.cond = cond

    def run(self):
        self.cond.acquire()  # 获取锁
        print(f"{threading.current_thread().name}:An arrow piercing through the clouds")
        self.cond.notify()  # 唤醒其他wait状态的线程
        self.cond.wait()  # 进入wait线程挂起状态等待notify通知

        print(f"{threading.current_thread().name}:Mountains without edges, heaven and earth merge, but I dare to sever ties with you")
        self.cond.notify()  # 唤醒其他wait状态的线程
        self.cond.release()  # 结束后释放锁

class person2(threading.Thread):
    def __init__(self, cond, name):
        threading.Thread.__init__(self, name=name)
        self.cond = cond

    def run(self):
        self.cond.acquire()  # 获取锁
        self.cond.wait()  # 等待指令
        print(f"{threading.current_thread().name}:Thousands of troops and horses come to meet")
        self.cond.notify()  # 唤醒其他wait状态的线程
        self.cond.wait()  # 进入wait线程挂起状态等待notify通知

        print(f"{threading.current_thread().name}:The sea may wither, the rocks may rot, and passion never fades")
        self.cond.notify()  # 唤醒其他wait状态的线程
        self.cond.release()  # 结束后释放锁

if __name__ == "__main__":
    man = person1(cond, "man")
    woman = person2(cond, "woman")
    # man先说话，但不能先启动
    # 因为man启动后，发出notify指令，而woman可能还未启动，无法接受notify指令
    woman.start()
    man.start()
```

#### 线程间消息隔离机制

```python
import threading

local_data = threading.local()
local_data.name = "local_data"

class MyThread(threading.Thread):
    def run(self):
        print("赋值前-子进程", threading.current_thread(), local_data.__dict__)
        local_data.name = threading.current_thread().name
        print("赋值后-子进程", threading.current_thread(), local_data.__dict__)

if __name__ == "__main__":
    print("开始-主进程", local_data.__dict__)

    t1 = MyThread()
    t1.start()
    t1.join()

    t2 = MyThread()
    t2.start()
    t2.join()

    print("结束-主进程", local_data.__dict__)
```

#### 线程池

线程池管理着一组工作线程，它维护着一个任务队列。当有新任务到来时，线程池从池中分配一个空闲线程来执行任务，任务完成后线程返回池中等待下一个任务。

**为什么需要线程池？**

| 优势             | 说明                                             |
| :--------------- | :----------------------------------------------- |
| **减少开销**     | 避免频繁创建和销毁线程的系统开销                 |
| **提高响应速度** | 任务到达时可以直接使用现有线程，无需等待线程创建 |
| **资源管理**     | 可以控制并发线程数量，防止系统资源耗尽           |
| **任务管理**     | 提供任务排队、调度和拒绝策略                     |

```python
from concurrent.futures import ThreadPoolExecutor
import time

executor = ThreadPoolExecutor(max_workers=3)

def get_html(times):
    print(f"获取网页信息{times}开始")
    time.sleep(times)
    print(f"获取网页信息{times}完毕")
    return times

# 通过submit方法提交执行的函数到线程中，submit函数会立即返回，不会阻塞主线程
task1 = executor.submit(get_html, 1)
task2 = executor.submit(get_html, 2)
task3 = executor.submit(get_html, 3)
task4 = executor.submit(get_html, 4)
print(task1.done())  # 检查任务是否完成，并返回结果，因为submit不阻塞主进程，为False
print(task4.cancel())  # 任务4被阻塞，可以取消，为True
print(task3.result())  # 拿到任务执行的结果，该方法是一个阻塞方法
print('end')

```

**常用方法**

| 函数           | 返回顺序 | 异常处理 | 适用场景     | 特点             |
| :------------- | :------- | :------- | :----------- | :--------------- |
| `as_completed` | 完成顺序 | 逐个处理 | 实时进度更新 | 谁先完成先处理谁 |
| `map`          | 提交顺序 | 统一处理 | 批量数据处理 | 保持原始顺序     |
| `wait`         | 自定义   | 灵活控制 | 复杂任务协调 | 多种等待策略     |

在Python的`concurrent.futures`模块中，`wait`函数用于控制主线程等待一组异步任务完成的方式。下面是其核心参数和一个对比表格，可以帮助你快速了解它们的作用：

| 参数              | 说明                                                         | 可选值及影响                                                |
| :---------------- | :----------------------------------------------------------- | :---------------------------------------------------------- |
| **`fs`**          | **Future对象序列**：需要等待的任务集合。                     | -                                                           |
| **`timeout`**     | **超时时间(秒)**：等待任务的最大时长，超时则返回。若为`None`(默认)，则无限期等待。 | -                                                           |
| **`return_when`** | **返回条件**：决定函数何时返回。                             | `ALL_COMPLETED`(默认), `FIRST_COMPLETED`, `FIRST_EXCEPTION` |

#### 创建多个进程

##### <u>以指定函数作为参数创建进程</u>

```python
import multiprocessing

def get_web(url):
    pass

if __name__ == '__main__':
    p1 = multiprocessing.Process(target=get_web, agrs=('<url_1>',))
    p2 = multiprocessing.Process(target=get_web, agrs=('<url_2>',))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print('Finish!')
```

##### <u>继承Process类创建进程</u>

```python
import multiprocessing

class MyProcess(multiprocessing.Process):
    def __init__(self, url):
        super.__init__()
        self.url = url
        
    def run(self): # 重写父类的run方法，定义在新的线程类里面要完成的task
        pass  # def get_web(url)里面的内容
    
if __name__ == '__main__':
    # 主线程
    t1 = MyProcess("子进程1","<url_1>")
    t2 = MyProcess("子进程2","<url_2>")
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print("Finished！")
```

##### <u>多线程间的通讯(消息队列)</u>

```python
import multiprocessing
import time

def product(q):
    kind = ('1', '2', '3')
    for i in range(3):
        print(multiprocessing.current_process().name, 'start')
        time.sleep(1)
        q.put(kind[i%3])
        print(multiprocessing.current_process().name, 'end')

def consumer(q):
    while True:
        print(multiprocessing.current_process().name, 'ready')
        time.sleep(1)
        t = q.get()
        print('{} finish'.format(t))

if __name__ == '__main__':
    q = multiprocessing.Queue(maxsize = 1)
    # start product
    multiprocessing.Process(target=product, args=(q,)).start()
    multiprocessing.Process(target=product, args=(q,)).start()
    # start consumer
    threading.Process(target=consumer, args=(q,)).start()
```

##### <u>进程池</u>



### 生成器及协程

#### 可迭代对象

**什么是可迭代对象？**

在python的任意对象中，定义了可以返回一个迭代器的`__iter__`方法，或者定义了可以支持下标索引的`__getitem__`方法，简单来说，就是可以被for循环遍历的对象。`dir(对象)`查看一个对象里面有什么。

**如何判断一个对象是否是可迭代对象？**

```python
# method 1:isinstance + iterable
from collections import abc

# 列表是可迭代对象
my_list = [1, 2, 3]
print(isinstance(my_list, abc.Iterable))  # 输出：True

# 整数不是可迭代对象
my_int = 100
print(isinstance(my_int, abc.Iterable))   # 输出：False

# method 2:hasattr + __getitem__
# 不全面： 很多现代的可迭代对象（如集合 set、生成器、文件对象）只实现了 __iter__，并没有实现 __getitem__。它们无法通过这个检查
```

**如何创建可迭代对象？**

```python
class Employee:
    def __init__(self, employee):
        self.employee = employee

    def __getitem__(self, item):
        # item是解释器帮我们维护的索引值，当在for循环中时，自动从0开始计数
        return self.employee[item]

emp = Employee(['a', 'b', 'c'])
for i in emp:
    print(i)
```

#### 迭代器

**什么是迭代器对象？**

如果你把 **可迭代对象 (Iterable)** 想象成一个装满商品的**货架（例如列表 `list`）**，那么 **迭代器 (Iterator)** 就是在货架前推着的**购物车**。

迭代器对象是一个**有状态**的对象，它专门用来做两件事：

1. **记录位置 (State):** 它知道当前迭代进行到哪个元素了。
2. **获取下一个元素:** 它定义了如何获取序列中的下一个元素。

在技术层面，一个对象只要实现了以下两个特殊方法，它就是一个迭代器：

| **方法名称** | **职责**                     | **当没有更多元素时...**         |
| ------------ | ---------------------------- | ------------------------------- |
| `__iter__`   | 返回迭代器本身。             | N/A                             |
| `__next__`   | 返回序列中的**下一个**元素。 | 必须抛出 `StopIteration` 异常。 |

**为什么要有迭代器？**

迭代器的存在，主要是为了解决三个核心问题：

**1. 统一性 (Universal Protocol)**

迭代器提供了一个**统一的接口**（`__iter__` 和 `__next__`），让 **所有** Python 对象都能用 **同一种方式**（即 `for item in container:`）被遍历。

- **没有迭代器：** `for` 循环需要学习如何遍历列表（用索引）、如何遍历集合（用哈希表）、如何遍历文件（用读取方法）。
- **有了迭代器：** `for` 循环只需要做一件事——**不断调用 `next()` 直到遇到 `StopIteration`**。它不需要知道底层数据结构是什么。

**2. 内存效率 (Lazy Evaluation)**

迭代器实现了**惰性求值**（或叫**延迟加载**）。

- 当你在处理一个**巨大的文件**、一个**无限的序列**（比如斐波那契数列）或者一个**数据库查询结果**时，你不能把所有数据一次性加载到内存中。
- 迭代器通过 `__next__` 方法**按需生成并返回下一个数据**，每次只处理一个元素，极大地节省了内存。**生成器 (Generator)** 就是迭代器这种特性的最佳体现。

**3. 支持非序列 (Non-Sequence)**

我们之前提到过 **集合 (Set)**。像集合、字典、文件对象这些**没有索引、没有固定顺序**的对象，完全无法依赖 `__getitem__(index)` 来遍历。

- 迭代器通过保存**当前遍历到的位置状态**，成功地为这些非序列类型提供了可遍历的能力。

```python
from itertools import count
from collections import abc

counter = count(start=10)
print(type(counter))  # 查看counter类型
print(dir(counter))  # 查看counter有哪些属性
print(isinstance(counter, abc.Iterator))  # 判断是否为迭代器
print(len(counter))  # 报错，迭代器没有len属性

for i in range(100):
    print(next(counter))

# for c in counter:  # 等价
#     print(c)
    
a = [1, 2, 3]
a_iter = iter(a)  # 转换为迭代器
for item in a_iter:  # next，自动拿出迭代器元素，内部不会再有元素
    print(item)
print(next(a_iter))  # 报错：StopIteration
```

##### <u>**可迭代对象和迭代器**</u>

- 迭代器迭代时会拿出元素，不可再次迭代

- 可迭代对象可以重复迭代

**这些对象本身不是迭代器，但它们可以创建迭代器。它们是容器或序列。**

| **类型**       | **示例**                                       | **备注**                   |
| -------------- | ---------------------------------------------- | -------------------------- |
| **内置序列**   | `list` (列表)                                  | `[1, 2, 3]`                |
|                | `tuple` (元组)                                 | `(1, 2, 3)`                |
|                | `str` (字符串)                                 | `"hello"`                  |
| **内置集合**   | `dict` (字典)                                  | 键、值或项是可迭代的。     |
|                | `set` (集合)                                   | `{1, 2, 3}`                |
| **范围/映射**  | `range`                                        | 内存高效的数字序列。       |
|                | `map` (注意：`map` 既是可迭代对象，也是迭代器) | `map(func, iterable)`      |
| **文件对象**   | 文件句柄                                       | `open('file').readlines()` |
| **用户自定义** | 实现了 `__iter__` 方法的任何类。               | 例如您代码中的 `class Z:`  |



**这些对象是“有状态”的，跟踪当前位置，通常通过 `next()` 函数或 `for` 循环内部机制驱动。**

| **类型**       | **示例**                                   | **备注**                             |
| -------------- | ------------------------------------------ | ------------------------------------ |
| **显式创建**   | `iter([1, 2, 3])`                          | 通过对列表调用 `iter()` 得到。       |
| **生成器**     | `(x**2 for x in range(5))`                 | 生成器表达式或生成器函数返回的对象。 |
| **内置工具**   | `zip`                                      | `zip(a, b)`                          |
|                | `enumerate`                                | `enumerate(iterable)`                |
|                | `filter`                                   | `filter(func, iterable)`             |
| **用户自定义** | 实现了 `__iter__` **和** `__next__` 的类。 | 例如您代码中的 `class Y:`            |

**既是可迭代对象又是迭代器:**某些对象，如 `map`、`filter`、`enumerate` 的返回结果



#### 生成器

**定义：**一种特殊的迭代器，不需要写`__iter__`和`__next__`方法，只需要`yield`关键字，就相当于定义了生成器

**核心优势**：是惰性求值（Lazy Evaluation）和内存效率：

- **常规函数**执行完毕后会 `return` 一个值并结束。
- **生成器函数**遇到 `yield` 关键字时，会**暂停**执行，并把 `yield` 后面的值返回给调用者。当需要下一个值时，它会从上次暂停的地方**继续**执行，直到遇到下一个 `yield`

**调用生成器(next, send)**

```python
def demo():
    t = yield 5  # return 5，同时send通过yield传递参数给t
    print(t)
    yield 6

print(type(demo))  # 输出生成器
print(dir(demo))  # 有__next__

# ========================================================
c = demo()  # 调用demo()，创建一个暂停在起跑线上的迭代器
# 第一次调用时为预激活，用send只能用c.send(None)
print(next(c))  # next方法，停留在t = yield 5
c.send("test")  # send方法，t = "test"，同时寻找下一个yield，没有则隐式报错StopIteration

# =========================================================
for x in c:  # 调用一次，直接预激活，且结束时不会抛出隐式错误StopIteration
    print(x)  # x是第一次yield的返回值5
    y = c.send("test")  # y是第二次yield的返回值6
    print(y)

# ==========================================================
a=(i for i in range(10))  # generator
for item in a:
    print(item)
print(a)  # <generator object <genexpr> at 0x0000024780085F00>

a=[i for i in range(10)]
for item in a:
    print(item)
print(a)  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### 协程

##### <u>概念</u>

**1. 微线程/纤程 (Microthread/Fiber):**

- 协程可以理解为一种**用户级的轻量级线程**。
- 与操作系统级别的多线程不同，协程的切换和调度是在**用户态（User Space）**进行的，而不是操作系统内核。
- 协程有自己的寄存器上下文和栈。

**2. 协作式多任务处理 (Cooperative Multitasking):**

- 协程的核心特点是**协作**。一个协程在执行过程中，必须**主动**让出（挂起/暂停）控制权，事件循环（Event Loop）才能去执行其他的协程。
- 在一个线程中，不同的子程序之间可以中断去执行其他的子程序，并且在中断回来后，可以从中断的地方继续执行。
- 这意味着在一个线程内，**同一时间只有一个协程在运行**。这与多线程的**抢占式**调度（操作系统随时可能中断一个线程）是不同的。

**3. 无阻塞 I/O (Non-blocking I/O) 的高效处理:**

- 协程的主要优势在于处理 **I/O 密集型**任务（如网络请求、文件读写）。
- 当一个协程遇到 I/O 操作需要等待时，它会使用 `await` 关键字**挂起**自身，将控制权交给事件循环。
- 事件循环会趁这段等待时间去运行其他准备就绪的协程，而不是傻傻地等待 I/O 完成，从而提高了单个线程的**资源利用率和吞吐量**。

```python
def consumer():
    r = ''
    while True:
        n = yield r
        if not n:
            return
        print('[Consumer] Consuming %s' % n)
        r = '200 OK'
def producer(c):
    c.send(None)
    n = 0
    while n < 5:
        n = n + 1
        print('[Producer] Producing %s' % n)
        r = c.send(n)
        print('[Producer] Consumer return %s' % r)

c = consumer()
producer(c)
```

#### `asyncio`框架

 同步IO和异步IO：同步IO是指操作开始后，线程必须等待IO操作结束后拿到结果，异步则等IO操作结束后由系统通知，再回来拿到结果，无需等待

`asyncio`框架存在的意义：框架可以将很多重复的，复杂度高的工作提交完成，我们在写代码时只需要专注于业务代码的实现

##### <u>`@asyncio.corotutine`装饰器定义协程</u>

```python
import asyncio
from collections import Generator, Coroutine

"""
使用装饰器方式定义协程，只是将这个函数对象
【标记】为协程对象。实际上，它的本质还是一个生成器
但是标记后，可以当成一个协程来使用
"""
@asyncio.coroutines
def hello():
    pass

coro = hello()
print(isinstance(coro, Coroutine))  # False
print(isinstance(coro, Generator))  # True
```

##### <u>`asyncio`原生协程定义</u>

```python
import asyncio
from collections import Generator, Coroutine

async def hello():
    print('hello')

coro = hello()  # 生成协程对象，但不会运行函数内的代码打印hello
print(isinstance(coro, Coroutine))  # True
```

##### <u>几个重要概念</u>

**事件循环`event_loop`**

`asyncio`中开启的一个无限的事件循环，`asyncio`会自动在满足条件时去调用相应的协程对象，我们只需要将协程对象注册到该事件循环上即可

**协程对象`corotutine`**

一个用`async`来定义的函数，在调用时不会立即执行，而是返回一个协程对象，协程对象需要注册到事件循环，有事件循环进行调用

**`future`对象**

代表将来执行或没有执行的任务的结果

**`task`对象**

一个协程对象就是一个原生可以挂起的函数，而任务则是对协程的进一步封装，其中包含任务的各种状态，`task`对象是`future`对象的子类，它可以将`corotutine`和`future`联系在一起，将`corotutine`封装成一个`future`对象

**`async`/`await`**

定义协程的关键字，`async`定义一个协程，`await`用于挂起阻塞的异步调用接口，作用类似于`yield`

##### <u>协程的工作流程</u>

- 定义/创建协程对象
- 定义事件循环对象容器
- 将协程转为task任务
- 将task扔进事件循环对象中触发

```python
import asyncio

# 1.定义协程对象--相当于构建任务模版
async def hello(name):
    print('hello', name)
    
# 2.创建协程对象--相当于构建具体任务
coro = hello('world')
# 3.获取事件循环对象容器--相当于构建负责完成操作的机器
loop = asyncio.get_event_loop()
# 4.将协程对象转化为task--相当于给机器发布任务
task = loop.create_task(coro)
# 5.将task任务扔进事件循环对象中触发--相当于按下开关，让任务开始执行
loop.run_until_complete(task)

# 现在更简洁写法
import asyncio

async def hello(name):
    print('hello', name)

async def main():
    await hello('world')
    
# 自动完成创建事件循环、创建Task、运行直到完成、清理资源
asyncio.run(main())
```

##### <u>获取协程对象返回值</u>

```python
import asyncio

async def hello(x):
    await asyncio.sleep(x)
    return x

# 1.直接 await
async def main():
    # 直接 await 协程对象获取返回值
    result = await hello(2)
    print(f"返回值: {result}")  # 返回值: 2

asyncio.run(main())

# 2.通过 Task 对象获取
async def main():
    # 创建任务
    task = asyncio.create_task(hello(3))
    # 等待任务完成
    await task
    # 通过 task.result() 获取返回值
    result = task.result()
    print(f"任务返回值: {result}")  # 任务返回值: 3

asyncio.run(main())

# 3.在回调函数中获取
def callback(future):
    # 在回调中通过 future.result() 获取返回值
    result = future.result()
    print(f"回调中获取返回值: {result}")

async def main():
    task = asyncio.create_task(hello(1))
    task.add_done_callback(callback)
    
    await task  # 等待任务完成，回调会自动执行

asyncio.run(main())
```

##### <u>协程的并发</u>

获取多个协程对象的结果

```python
import asyncio

async def do_some_work(x):
    print(f'wait {x}')
    await asyncio.sleep(x)
    return f'wait: {x}'

# 1.使用 asyncio.gather()
async def main():
    coro1 = do_some_work(1)
    coro2 = do_some_work(2)
    coro3 = do_some_work(3)
    
    # 使用 asyncio.gather 获取所有结果
    results = await asyncio.gather(coro1, coro2, coro3)
    print("所有结果:", results)

asyncio.run(main())

# 2.使用 asyncio.wait()
async def main():
    coro1 = do_some_work(1)
    coro2 = do_some_work(2)
    coro3 = do_some_work(3)
    
    # 创建任务
    tasks = [asyncio.create_task(coro1), 
             asyncio.create_task(coro2), 
             asyncio.create_task(coro3)]
    
    # 使用 asyncio.wait 等待所有任务完成
    done, pending = await asyncio.wait(tasks)
    
    # 从完成的任务中提取结果
    results = [task.result() for task in done]
    print("所有结果:", results)

asyncio.run(main())

# 3.使用 asyncio.as_completed()（按完成顺序）
async def main():
    coro1 = do_some_work(3)
    coro2 = do_some_work(1)
    coro3 = do_some_work(2)
    
    tasks = [asyncio.create_task(coro1), 
             asyncio.create_task(coro2), 
             asyncio.create_task(coro3)]
    
    print("按完成顺序获取结果:")
    # as_completed 按完成顺序返回任务
    for completed_task in asyncio.as_completed(tasks):
        result = await completed_task
        print(f"  完成: {result}")

asyncio.run(main())
```

##### <u>利用协程和多线程的方式生成10000个txt文件</u>

```python
# 多线程
import threading
import time

def write_file(path, x):
    print(f"generating {x} files")
    with open(path, 'w') as f:
        f.write(f"this is file{x}")

if __name__ == '__main__':
    start = time.time()

    threads = []
    for i in range(1,10001):
        t = threading.Thread(target=write_file, args=('d:/demo/file'+str(i)+'.txt', i))
        threads.append(t)
        t.start()
    
    [t.join() for t in threads]

    end = time.time()
    print(f"time:{end-start}s")

```

```python
# 协程
import asyncio
import time

# 实质上with open是同步操作，会造成堵塞
async def write_file(path, x):
    print(f"generating {x} files")
    with open(path, 'w') as f:
        f.write(f"this is file{x}")

async def main():
    start = time.time()
    
    for i in range(1, 10001):
        task = asyncio.create_task(write_file(f'd:/demo/file{i}.txt', i))
        tasks.append(task)

    # 使用 asyncio.gather 并发执行所有任务
    await asyncio.gather(*tasks)
    
    end = time.time()
    print(f"time: {end - start}s")

if __name__ == '__main__':
    asyncio.run(main())
```



## 真题

```python
"""
Decimal 解决浮点数精度问题，会保留有效位数（加减取最长，乘相加，除法:整除-max(被除数-除数, 非0小数位);不整除-需要设置精度(default 28)）
"""
Decimal(′1.30′)×Decimal(′1.20′) == Decimal(′1.5600′) # True
Decimal(′1.30′)×Decimal(′1.20′) == Decimal(′1.56′)  # False

Decimal(0.1) + Decimal(0.2) == Decimal(0.3)  # False

```

```python
"""
asyncio是一种基于单线程协作的并发模型（即协程）
它通过在等待I/O时让出控制权来实现并发，而不是像threading那样通过操作系统创建和切换线程来实现并发
"""
import threading
import asyncio

async def hello(thread_id):
    current_thread = threading.current_thread()
    if thread_id == current_thread:
        print('the same thread')
    else:
        print('not the same thread')

async def main():
    main_thread = threading.current_thread()
    hello1 = asyncio.create_task(hello(main_thread))

    await hello(main_thread)
    await hello1

asyncio.run(main())

```

```python
"""
跳过列表开头符合条件的数，直到遇到第一个不符合的数。
"""
import itertools

data = [0, 0, 0, 5, 6, 0, 4, 0, 7]
# predicate 函数：判断元素是否等于 0
result = itertools.dropwhile(lambda x: x == 0, data)
print(list(result))
# 输出: [5, 6, 0, 4, 0, 7]
```

```
对于必填的关键配置（如数据库密码），请使用 os.environ['KEY']，让程序在变量缺失时立即报错。

对于可选配置或需要提供默认值的配置，请使用 os.getenv('KEY', default_value) (或 os.environ.get('KEY', default_value))，使程序具有更高的容错性。
```

```python
"""
Python 的 multiprocessing 模块通过创建进程（Process）来实现并发。与线程不同，进程之间是相互独立的，它们在操作系统层面拥有独立的内存空间。

当您启动一个新进程时（如 a1 和 a2），它会复制父进程（if __name__ == '__main__': 块）的内存空间。

全局变量 nums = [11, 22]：这个列表在主进程中初始化。当子进程 a1 和 a2 启动时，它们各自会得到一个 nums 列表的独立副本，初始值都是 [11, 22]
"""
from multiprocessing import Process

nums = [11, 22]
def p1():
    for i in range(3):
        nums.append(i)
def p2():
    for i in range(3):
        nums.append(i)
    print(nums)
    
if __name__ == '__main__':
    a1 = Process(target=p1)
    a2 = Process(target=p2)
    a1.start()
    a1.join()
    a2.start()
    a2.join()
```

```
pdb 的核心要求是：有一个能够运行它的 Python 解释器，并且解释器的标准库中必须包含 pdb 模块
```

```python
"""
返回值问题： B.__new__ 方法没有 return 语句，所以它隐式地返回了 None。
创建失败： Python 的对象创建流程规定，如果 __new__ 没有返回一个当前类（B）的实例，那么 __init__ 方法就不会被调用。
结果： obj1 被赋值为 None，并且 'Bi' 没有被打印
"""
class A:
    def __new__(cls):
        print('An')
        return object.__new__(cls)
    
    def __init__(self):
        print('Ai')
    
class B:
    def __new__(cls):
        print('Bn')
    
    def __init__(self):
        print('Bi')

obj1 = B() # Bn
obj2 = A() # An Ai
```

```
在 Python 中定义函数时，参数必须按照严格的顺序排列。基本顺序是：
具体的参数类型和顺序如下：
    位置或关键字参数 (Positional or Keyword Arguments)
    默认参数 (Default Arguments)
    可变位置参数 (*args，即打包所有额外的位置参数)
    仅关键字参数 (Keyword-Only Arguments)
    可变关键字参数 (**kwargs，即打包所有额外的关键字参数)
```

```python
class AE(Exception):
    def __str__(self):
        return "A"
class BE(AE):
    def __str__(self):
        return "B"
    
try:
    try:
        raise BE         # 1. 抛出 BE 异常
    except AE:           # 2. BE 是 AE 的子类，所以这里成功捕获了 BE 异常。
        raise            # 3. 再次把刚刚捕获的 BE 异常扔出去！
except Exception as exc: # 4. 外部捕获所有异常（接住了 BE 异常），并命名为 exc。
    print(str(exc))      # 5. 打印 exc 异常对象（这里触发了 BE 类中的 __str__ 方法）
```

```python
# b开头，字节串字面量，不可变的字节序列，存储原始字节值
l = b"China"
print(l)  # b'China'
print(type(l))  # <class 'bytes'>
print(str(l))
print(type(str(l)))
```

```python
"""
__iter__(self): 返回 self。根据迭代器协议，迭代器必须返回自身。这使 Y 实例成为一个已耗尽自身的迭代器（通常不推荐这种模式，因为它只能迭代一次）

Z类实现了可迭代对象协议，__iter__(self)，它返回一个新的Y实例：return Y(self.n)。
每次请求迭代时（如每次调用 list(z) 时），Z 都会创建一个全新的 Y 迭代器，并从头 (i=0) 开始计数。
"""
class Y:
    def __init__(self, n):
        self.i = 0
        self.n = n

    def __iter__(self):
        return self
    
    def __next__(self):
        if self.i<self.n:
            i = self.i
            self.i += 1
            return i
        else:
            raise StopIteration()

class Z:
    def __init__(self, n):
        self.n = n
    
    def __iter__(self):
        return Y(self.n)

z = Z(5)
print(list(z))  # [0, 1, 2, 3, 4]
print(list(z))  # [0, 1, 2, 3, 4]
```

```python
两个对象的 id() 相等，意味着它们是同一个对象。这主要发生在以下几种情况：
1.将一个变量赋值给另一个变量时，它们会指向内存中的同一个对象
2.CPython 为了优化性能和内存使用，会对某些不可变 (Immutable) 的小对象进行缓存或驻留
	-5到256之间的整数
    简短、不含空格和特殊字符的字符串
3.某些魔术方法或操作会返回对象本身（例如某些链式操作），此时id也会相等

两个对象的值（==）相等，它们的 id 也可能不相等，这意味着它们是两个独立的对象，只是内容相同
1.list、dict、set 等可变对象，即使内容相同，也会在内存中创建独立的副本
2.超出小整数范围的数字，通常会创建新的对象
```

```python
# set(iterable), 只能接受一个可迭代对象作为输入
x = set('abc')  # True,当传入一个字符串时，它会将其视为一个由单个字符组成的序列进行迭代
x = set(['a','b','c'])  # True
x = set(('a','b','c'))  # True
x = set('a','b','c')  # TypeError
```

```python
"""
整数除法 (//) 的结果是向下取整 (floor division)
取模运算的结果符号总是与除数（即 % 右边的数）的符号相同。它满足以下数学关系：a = q \ b + r
a是被除数（左边的数，dividend）
b是除数（右边的数，divisor）
q是整数商（a // b）
r是余数（a % b）
"""
print(10//3)
print(-10//3)
print(2%-3)
print(2%3)
```

```python
如果子类没有定义__init__，会直接调用父类的
如果子类有定义__init__，会覆盖父类的，可以用super().__init__()继承
如果函数需要调用self.x
    先从自身的__init__
    再从父类的__init__（如果有super或者子类未定义）
    再从子类的类变量中创建一个独立的实例变量，不改变类变量
    再从父类的类变量中创建一个独立的实例变量，不改变类变量
```

```python
"""
自定义的异常类形成了清晰的继承链：D-C-B-Exception,这意味着D是C的子类，C是B的子类。因此，如果抛出D异常，它也是一个C异常，也是一个B异常

当一个异常被抛出时，Python 会从上到下依次检查 except 块，并执行第一个匹配到的捕获块
由于except B: 放在最前面，并且C和D都是B的子类，所以except B:会捕获所有这三种异常
"""
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

e = []
for l in [B,C,D]:
    try:
        raise l()
    except B:
        e.append('B')
    except C:
        e.append('C')
    except D:
        e.append('D')

print(e) # BBB

```

```
使用 obj1 == obj2 进行比较时，Python 解释器在底层会自动调用 obj1.__eq__(obj2)
```

```
<< 运算符操作的对象是位模式 (bit patterns)，因此它只能对 整数类型 (int) 进行操作
右操作数（移动的位数）必须是非负整数（即≥0）
```

```
正常情况下，Python 的每个类实例都有一个内置的字典属性 __dict__，用来存储实例的所有变量。这个字典非常灵活，但会占用额外的内存空间（对于每个实例来说，通常是几十到几百个字节）。

通过在类中定义 __slots__，你可以禁用这个 __dict__ 字典，强制实例只存储在 __slots__ 中列出的属性，从而显著减少每个实例的内存开销。
```

```python
"""
Pipe() 创建了一个管道，用于两个进程之间的通信。它返回两个连接对象：
pa (Parent/父进程连接)：用于主进程接收数据。
ch (Child/子进程连接)：用于子进程发送数据。
通信方向： 虽然 Pipe 是全双工的（双向可读写），但在这个例子中，ch 负责发送（send），pa 负责接收（recv）

recv() 是一个阻塞操作，它会一直等待直到管道中有数据可用
"""
from multiprocessing import Process, Pipe

def f(n):
    n.send('a')
    n.send('b')

if __name__ == "__main__":
    pa, ch = Pipe()
    p = Process(target=f,args=(ch,))
    p.start()
    m = pa.recv()
    p.join()
    print(m)  # a
```

```python
def func():
    yield (x for x in range(3))

for x in func():  # func()为一个生成器
    print(tuple(x))  # x为生成器，tuple调用__next__完成转换

# (0, 1, 2)
```

```
Python的模块搜索顺序是：当前脚本目录 ==> PYTHONPATH目录 ==> 标准库/site-packages目录
```

```
括号内填写的内容：
    super():确定MRO搜索起点
    __init__():传递初始化数据
```

```
12_00 是一种整数 (int) 数据类型。
下划线 _ 在 Python 的数字字面量中没有任何数值意义，它只用作视觉分隔符，目的是提高数字的可读性。
```

```
Python 中的布尔运算符（and, or）不一定返回 True 或 False，它们返回的是参与运算的表达式的值（或称为“短路求值”）。

1. and 运算规则
A and B
如果 A 是假值（Falsy，如 0, False, None, ""），返回 A。
如果 A 是真值（Truthy，如非空字符串、非零数字），返回 B。

2. or 运算规则
A or B
如果 A 是真值，返回 A（短路）。
如果 A 是假值，返回 B。
```

假设 `name = "Alice's book"`：

| **格式化方式**               | **代码**      | **实际调用** | **输出**          | **用途**                                                     |
| ---------------------------- | ------------- | ------------ | ----------------- | ------------------------------------------------------------ |
| **默认（隐式调用 `str()`）** | `f"{name}"`   | `str(name)`  | `Alice's book`    | 用于用户界面的**可读输出**。                                 |
| **`!r` 转换**                | `f"{name!r}"` | `repr(name)` | `'Alice\'s book'` | 用于**调试**、**日志记录**、**表示数据结构**，清楚地显示数据的边界和类型。 |
