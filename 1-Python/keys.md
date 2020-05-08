[toc]

### 1. Python 下划线命名格式     

| 格式                 | 举例      | 含义                                                         |
| -------------------- | --------- | ------------------------------------------------------------ |
| 单前导下划线         | _var      | 命名约定，仅供内部使用。通常不会由python解释器强制执行(通配符导入除外)，只作为对coder的提示。 |
| 单末尾下划线         | var_      | 按约定使用避免与 python 关键字冲突                           |
| 双前导下划线         | __var     | 类中私有变量名。当在类上下文中使用时，触发“名称修饰”，由python解释器强制执行 |
| 双前导和双末尾下划线 | `__var__` | python 语言自己定义的特殊方法                                |
| 单下划线             | `_`       | 用作临时 或无意义变量的名称                                  |


### 2. `__repr__`和 `__str__`

`__repr__`和 `__str__` 这两个方法都是用于显示的，`__str__`是面向用户的，而`__repr__`面向程序员。

打印操作会首先尝试`__str__` 和str内置函数(print运行的内部等价形式)，它通常应该返回一个友好的显示。

`__repr__` 用于所有其他的环境中：用于交互模式下提示回应以及repr函数，如果没有使用`__str__` ，会使用print和str。它通常应该返回一个编码字符串，可以用来重新创建对象，或者给开发者详细的显示。

当我们想所有环境下都统一显示的话，可以重构`__repr__` 方法；当我们想在不同环境下支持不同的显示，例如终端用户显示使用`__str__`，而程序员在开发期间则使用底层的`__repr__`来显示，实际上`__str__`只是覆盖了`__repr__`以得到更友好的用户显示。     

### 3. global、nonlocal关键字       
#### 3.0 python LEGB变量作用域规则      
- L —— Local(function)；函数内的名字空间  
- E —— Enclosing function locals；外部嵌套函数的名字空间(例如closure)  
- G —— Global(module)；函数定义所在模块（文件）的名字空间
- B —— Builtin(Python)；Python内置模块的名字空间
#### 3.1 global关键字    
用来在函数中或局部的作用域中使用全局变量      
```Python
count = 0
def test():
    global count
    count += 1
    print(count)
test()

Output: 1,  count = 1
```   
同时使用global后，全局变量的值也会改变        

#### 3.2 nonlocal关键字          
python3加入的`nonlocal`关键字，在嵌套函数中使用`nonlocal`声明变量时，表示这个变量是外部函数中定义的变量     
