# java inheritance

Java 继承(inheritance)是 Java 面向对象的三大重要特性之一（封装-encapsulation,   继承-inheritance,  多态-polymorphsim)   Java 继承很好的管理了具有相似特征的类之间的关系(主要集中在成员变量、方法),  使程序可扩展、易修改，并且成为java多态的基础。下面将介绍Java继承的基本语法以及特性：



## 1.  使用extends关键字实现类与类之间的继承
``` java
public class parent {

}

public class child extends parent {

}
```
在这段代码中，我们首先声明了一个名叫parent的类。然后声明了一个child类extends parent类作为parent的子类，这时候parent类就被用作了父类(super class)。事实上，任何类都可以被用作父类，只要我们为其声明子类，不管它是否是抽象类(abstract class)。 在我们不重写(overwrite) 或重载(override)父类中的方法、不增添新的方法、不更改原始的成员变量或增加新的变量的情况下，子类将默认保留父类的特性。
## 2.  关于抽象类的继承

对于一个抽象类，如果里面包含有未实现的抽象方法并且我们想创造一个子类继承这个抽象类，这个子类不必重写(overwrite)抽象类中所有未实现的抽象方法，但是必须被定义为抽象类。同理，如果一个类实现一个接口(Interface)，那么它要么重写接口里的所有抽象方法，要么被定义为抽象类。

## 3. 关于父类与子类构造器的调用

父类与子类均为默认构造器：
``` java
public class parent {

}

public class child extends parent {

}
```
在如上代码中，父类与子类均调用super class Object的构造器(constructor)。需要注意的是，当我们使用“new”关键字新建子类child对象时，同时会调用父类parent的构造器并新建一个父类对象(parent对象)


父类与子类均不为默认构造器:
``` java
public class parent{
    public parent (int m) {

    }
}

public class child extends parent {
    public child (int m, String a) {
        super(m);
    }
}
```
在这种情况下，子类必须重写(overwrite)或重载(override)父类的构造函数，同时必须调用父类的构造器(constructor)，因为父类不再有默认的构造器可供调用。


## 4. Java单继承的特性

在java中，一个父类被多个子类继承，但一个子类只能继承一个父类。与接口不同的是，一个类可以实现(implement)多个接口。



## 5. 创建子类或父类的对象

我们看下面这段代码：
``` java
public class demo {
    public static void main (String[] args) {
        parent p = new parent();
        child c = new child();
        parent pc = new child();
    }
}

public class parent {

}

public class child extends parent {

}
```
对于main方法中的前两行，我们可以很容易的看出它新建了一个子类的对象和一个父类的对象，对于第三行这种，叫做父类的引用指向子类的对象，我们下边分别来分析对于三种声明的成员变量和方法的调用。
实例方法(instance method)和实例变量(instance method)的调用：

针对p和c，这个类里面有什么实例方法和实例变量，那么就允许调用什么

针对pc，编译器首先会在父类中进行搜索，如果搜索到，则不会报错，此时再去看子类中有没有重写此方法或改变此变量。如果有，则调用子类的。如果被调用的方法或变量只在子类中有而在父类中没有，那么编译器会报错。

静态方法(static method)和静态变量(static variable)的调用：   

针对p和c，这个类里面有什么实例方法和实例变量，那么就允许调用什么

针对pc，同理，只有在父类中存在，编译器才不会报错。但是，即使子类重写了父类的静态方法，调用时依然会使用父类的静态方法(在理论上，不建议通过objectName.method或objectName.variable的方式调用静态方法或变量，最好使用className.method或className.variable的方法调用)
