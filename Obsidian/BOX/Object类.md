#input #CS #programming_language 
# 5. Object 类
## 1. Object

Object是Java默认提供的一个类。Java里面除了Object类，所有的类都是存在继承关系的。默认会继承Object父 类。即所有类的对象都可以使用Object的引用进行接收。

例如：使用Object接收所有类的对象

```java
class Person{}
class Student{}
public class Test {
    public static void main(String[] args) {
        function(new Person());
        function(new Student());
    }
    public static void function(Object obj) {
        System.out.println(obj);
    }
}
//执行结果：
//Person@1b6d3586
//Student@4554617c
```

所以在开发之中，Object类是参数的最高统一类型。但是Object类也存在有定义好的一些方法.

先熟悉三个方法：toString()方法，equals()方法，hashcode()方法



## 2. 获取对象信息

如果要打印对象中的内容，可以直接重写Object类中的toString()方法。

查看前面的笔记。



## 3. 对选哪个比较equals方法

在Java中，==进行比较时：

1. 如果==左右两侧是基本类型变量，比较的是变量中值是否相
2. 如果==左右两侧是引用类型变量，比较的是引用变量地址是否相同
3. 如果要比较对象中内容，**必须重写Object中的equals方法**，因为equals方法默认也是按照地址比较的

```java
//Object类中的equals方法
public boolean equals(Object obj){
    return(this == obj);//使用引用中的地址直接来进行比较
}
```



```java
class Person{
    private String name ;
    private int age ;
    public Person(String name, int age) {
        this.age = age ;
        this.name = name ;
    }
}
public class Test {
    public static void main(String[] args) {
        Person p1 = new Person("gaobo", 20) ;
        Person p2 = new Person("gaobo", 20) ;
        int a = 10;
        int b = 10;
        System.out.println(a == b); // 输出true
        System.out.println(p1 == p2); // 输出false
        System.out.println(p1.equals(p2)); // 输出false
    }
}
```

Person类重写equals方法后，然后比较：

```java
class Person{
...
    @Override
    public boolean equals(Object obj) {
        if (obj == null) {
            return false ;
        }
        if(this == obj) {
            return true ;
        }
// 不是Person类对象
        if (!(obj instanceof Person)) {
            return false ;
        }
        Person person = (Person) obj ; // 向下转型，比较属性值
        return this.name.equals(person.name) && this.age==person.age ;
    }
}
```



## 4. hashcode方法

hashcode方法源码：

```java
public native int hashCode();
```

该方法是一个native方法，底层是由C/C++代码写的。我们看不到。

我们认为两个名字相同，年龄相同的对象，将存储在同一个位置，如果不重写hashcode()方法，我们可以来看示例 代码：

```java
class Person {
    public String name;
    public int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
public class TestDemo4 {
    public static void main(String[] args) {
        Person per1 = new Person("gaobo", 20) ;
        Person per2 = new Person("gaobo", 20) ;
        System.out.println(per1.hashCode());
        System.out.println(per2.hashCode());
    }
}
//执行结果
460141958 
1163157884
```

两个对象的hash值不一样。

重写hashcode()方法:

```java
class Person {
    public String name;
    public int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
public class TestDemo4 {
    public static void main(String[] args) {
        Person per1 = new Person("gaobo", 20) ;
        Person per2 = new Person("gaobo", 20) ;
        System.out.println(per1.hashCode());
        System.out.println(per2.hashCode());
    }
}
//执行结果
460141958 
460141958
```

hash值一样。

结论：

1. hashcode方法用来确定对象在内存中存储的位置是否相同
2. 事实上hashCode() 在散列表中才有用，在其它情况下没用。在散列表中hashCode() 的作用是获取对象的 散列码，进而确定该对象在散列表中的位置。
