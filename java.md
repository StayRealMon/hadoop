## 面向对象的基本原则 ##
> s( Single-Resposibility Principle ): 单一职责原则
> o( Open-Closed principle ): 开放封闭原则
> l( Liskov-Substituion Principle ): 里氏原则
> i( Interface-Segregation Principle ): 接口隔离原则
> d( Dependecy-Inversion Principle ): 依赖倒置原则
> 一个单词：立方体(solid)
> 
> **单一职责**原则（Single-Resposibility Principle）：一个类，最好只做一件事，只有一个引起它的变化。单一职责原则可以看做是低耦合、高内聚在面向对象原则上的引申，将职责定义为引起变化的原因，以提高内聚性来减少引起变化的原因。 
> **开放封闭**原则（Open-Closed principle）：软件实体应该是可扩展的，而不可修改的。也就是，对扩展开放，对修改封闭的。 
> **Liskov替换**原则（Liskov-Substituion Principle）：子类必须能够替换其基类。这一思想体现为对继承机制的约束规范，只有子类能够替换基类时，才能保证系统在运行期内识别子类，这是保证继承复用的基础。 
> **接口隔离**原则（Interface-Segregation Principle）：使用多个小的专门的接口，而不要使用一个大的总接口
> **依赖倒置**原则（Dependecy-Inversion Principle）：依赖于抽象。具体而言就是高层模块不依赖于底层模块，二者都同依赖于抽象；抽象不依赖于具体，具体依赖于抽象。 

## 线程同步 ##
> **喂，SHE**：喂（Vector）S（Stack）H（hashtable）E（enumeration）
> 线程安全的同步的类：
> **vector**：就比arraylist多了个同步化机制（线程安全），因为效率较低，现在已经不太建议使用。在web应用中，特别是前台页面，往往效率（页面响应速度）是优先考虑的。
> **statck**：堆栈类，先进后出
> **hashtable**：就比hashmap多了个线程安全
> **enumeration**：枚举，相当于迭代器
> 除了这些之外，其他的都是非线程安全的类和接口。

## ThreadLocal ##
> 1. ThreadLocal的类声明：public class ThreadLocal<T>。可以看出ThreadLocal并没有继承自Thread，也没有实现Runnable接口。
> 2. ThreadLocal类为每一个线程都维护了自己独有的**变量拷贝**。每个线程都拥有了自己独立的一个变量。所以ThreadLocal重要作用并不在于多线程间的数据共享，而是**数据的独立**。由于每个线程在访问该变量时，读取和修改的，都是自己独有的那一份变量拷贝，不会被其他线程访问，变量被彻底封闭在每个访问的线程中。
> 3. ThreadLocal中定义了一个哈希表用于为每个线程都提供一个变量的副本
> 
> ThreadLocal继承Object，相当于没继承任何特殊的。
> ThreadLocal没有实现任何接口。
> ThreadLocal并不是一个Thread，而是Thread的局部变量。