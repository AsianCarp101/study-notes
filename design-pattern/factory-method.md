###工厂方法模式

>整理自：[《java与模式》之工厂方法模式](http://www.cnblogs.com/java-my-life/archive/2012/03/25/2416227.html)

在阎宏博士的《JAVA与模式》一书中开头是这样描述工厂方法模式的：

**工厂方法模式是类的创建模式，又叫做虚拟构造子(Virtual Constructor)模式或者多态性工厂（Polymorphic Factory）模式。**

**工厂方法模式的用意是定义一个创建产品对象的工厂接口，将实际创建工作推迟到子类中。**

那么 **工厂方法模式** 是在什么场景下使用呢，下面就以本人的理解举例说明:

	相信很多人都做过导入导出功能，就拿导出功能来说。有这么一个需求：XX系统需要支持对数据库中的员工薪资进行导出，并且支持多种格式如：HTML、CSV、PDF等，每种格式导出的结构有所不同，比如：财务跟其他人对导出薪资的HTML格式要求可能会不一样，因为财务可能需要特定的格式方便核算或其他用途。

　　如果使用简单工厂模式，则工厂类必定过于臃肿。因为简单工厂模式只有一个工厂类，它需要处理所有的创建的逻辑。假如以上需求暂时只支持3种导出的格式以及2种导出的结构，那工厂类则需要6个if else来创建6种不同的类型。如果日后需求不断增加，则后果不堪设想。

　　这时候就需要工厂方法模式来处理以上需求。在工厂方法模式中，核心的工厂类不再负责所有的对象的创建，而是将具体创建的工作交给子类去做。这个核心类则摇身一变，成为了一个抽象工厂角色，仅负责给出具体工厂子类必须实现的接口，而不接触哪一个类应当被实例化这种细节。

　　这种进一步抽象化的结果，使这种工厂方法模式可以用来允许系统在不修改具体工厂角色的情况下引进新的产品，这一特点无疑使得工厂方法模式具有超过简单工厂模式的优越性。下面就针对以上需求设计UML图：

![](http://imglf.nosdn.127.net/img/SU9HaFdjTlNlVmJBRmJoQnB0M3lDcThobDkyR0dQdGdZRTlZSnZlU29rOG5wTENUcU1BdWxRPT0.png?imageView&thumbnail=500x0&quality=96&stripmeta=0&type=jpg)

从上图可以看出，这个使用的工厂方法模式的系统涉及到以下角色：

　　**抽象工厂（ExportFactory）角色：**担任这个角色的是工厂方法模式的核心，任何在模式中创建对象的工厂类必须实现这个接口。在实际的系统中，这个角色也常常使用抽象类实现。

　　**具体工厂（ExportHtmlFactory、ExportPdfFactory）角色：**担任这个角色的是实现了抽象工厂接口的具体JAVA类。具体工厂角色含有与业务密切相关的逻辑，并且受到使用者的调用以创建导出类（如：ExportStandardHtmlFile）。

　　**抽象导出（ExportFile）角色：**工厂方法模式所创建的对象的超类，也就是所有导出类的共同父类或共同拥有的接口。在实际的系统中，这个角色也常常使用抽象类实现。

　　**具体导出（ExportStandardHtmlFile等）角色：**这个角色实现了抽象导出（ExportFile）角色所声明的接口，工厂方法模式所创建的每一个对象都是某个具体导出角色的实例。

**源代码**

　　首先是抽象工厂角色源代码。它声明了一个工厂方法，要求所有的具体工厂角色都实现这个工厂方法。参数type表示导出的格式是哪一种结构，如：导出HTML格式有两种结构，一种是标准结构，一种是财务需要的结构。

```java
public interface ExportFactory {
    public ExportFile factory(String type);
}
```

具体工厂角色类源代码：

```java
public class ExportHtmlFactory implements ExportFactory{

    @Override
    public ExportFile factory(String type) {
        // TODO Auto-generated method stub
        if("standard".equals(type)){
            
            return new ExportStandardHtmlFile();
            
        }else if("financial".equals(type)){
            
            return new ExportFinancialHtmlFile();
            
        }else{
            throw new RuntimeException("没有找到对象");
        }
    }

}
```

```java
public class ExportPdfFactory implements ExportFactory {

    @Override
    public ExportFile factory(String type) {
        // TODO Auto-generated method stub
        if("standard".equals(type)){
            
            return new ExportStandardPdfFile();
            
        }else if("financial".equals(type)){
            
            return new ExportFinancialPdfFile();
            
        }else{
            throw new RuntimeException("没有找到对象");
        }
    }

}
```

　抽象导出角色类源代码：


