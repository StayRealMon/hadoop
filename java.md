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

## 位运算 ##
> 运算对象为数字的补码，而不是二进制码。当补码的符号位为1时，说明该补码对应的是负数，所以根据补码求原码的时候遵循负数的原则，补码取反加一。如果符号位为0时，则该补码对应的原码与其相同。
> -3：
> 1000 0011 （原码）
> 1111 1100 （反码）
> 1111 1101 （补码）（这是-3在计算机中的表示形式）
> ~（-3）：
> 0000 0010 （补码）（~（-3）在计算机中的表示形式）
> 所以~（-3）=4
>  
> 1：
> 0000 0001 （原码，反码，补码）
> ~1：
> 1111 1110 （补码）（~1在计算机中的表示形式）
> 1000 0010 （原码）
> ~1=-2


## ArrayList 、 LinkedList 、 HashMap ##
HashMap实现Map接口，它允许任何类型的键和值对象，并允许将null用作键或值
ArrayList和LinkedList均实现了List接口
ArrayList的访问速度比LinkedList快

Hashtable不允许 null 值(key 和 value 都不可以)，HashMap允许 null 值(key和value都可以)。 ArrayList和LinkedList均实现了List接口
ArrayList基于数组实现，随机访问更快
LinkedList基于链表实现，添加和删除更快

A、HashMap实现了Map接口的，它的Key和Value都可以是null，但是Hashtable种，Key和Value都不能是null。
B、ArrayList与LinkedList都实现了List接口，继承了AbstractList类。ArrayList是数组方式存储，也就是顺序存储，LinkedList是链式存储。LinkedList方便删除添加，ArrayList方便查找
C、ArrayList底层是动态数组是实现，随机位置添加和删除，都需要移动数组的数据，而LinkedList底层是双向链表，只需要修改Node节点的引用。
D、随机访问数组要比链表块
![](https://uploadfiles.nowcoder.com/images/20180705/3807435_1530799430432_DBD7499309F7A0C283CA6E755CC5E6DA)