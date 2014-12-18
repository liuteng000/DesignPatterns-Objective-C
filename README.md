# DesignPatterns

用Objective-C实现《大话设计模式》书中的例子，并用一些Objective-C的特性对例子的实现加以优化，希望能对初学设计模式的iOS开发者有所帮助。

## 前言

在某些人看来学习设计模式没有什么意义，因为在实际工作中基本用不上，因此没有什么学习的必要。但是在我看来，学习设计模式非常有必要，暂且不论在实际工作中能否用得上，理解了设计模式的原理和其中所蕴含的大智慧后可以帮助我们写出结构更合理、风格更优雅、更容易复用的代码。

## 设计模式的基本原则

设计模式的基本原则非常重要，只要真正深入地理解了设计原则，很多设计模式其实就是原则的应用而已，或许在不知不觉中就在使用设计模式了：
* **单一职责原则（SRP）**，就一个类而言，应该仅有一个引起它变化的原因。
* **开放-封闭原则（OCP）**，是说软件实体（类、模块、函数等等）应该可以拓展，但是不可修改。
* **依赖倒转原则（DIP）**，A.高层模块不应该依赖低层模块，两个都应该依赖抽象。B.抽象不应该依赖细节，细节应该依赖抽象。
* **里氏代换原则（LSP）**，子类型必须能够替换掉它们的父类型。
* **迪米特法则（LoD）**，如果两个类不必彼此直接通信，那么这两个类就不应当发生直接的相互作用。如果其中一个类需要调用另一个类的某一个方法的话，可以通过第三者转发这个调用。
* **合成/聚合复用原则（CARP）**，尽量使用合成/聚合，尽量不要使用类继承。

注：SRP-Single Responsibility Principle，OCP-Open-Closed Principle，DIP-Dependency Inversion Principle，LSP-Liskov Subsitution Principle，LoD-Law of Demeter，CARP-Composition/Aggregation Principle。

## 常用的23种设计模式

不管是.NET中的C#语言，还是Java、VB.NET、C++或Objective-C语言，面向对象语言在设计模式的层面上都是相通的，只不过在设计模式的具体实现上语法稍有差异罢了：
 1. **策略模式（Strategy）**，它定义了算法家族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化，不会影响到使用算法的客户。
 2. **装饰模式（Decorator）**，动态地给一个对象添加一些额外的职责，就增加功能来说，装饰模式比生成子类更为灵活。
 3. **代理模式（Proxy）**，为其他对象提供一种代理以控制对这个对象的访问。
 4. **工厂方法模式（Factory Method）**，定义一个用于创建对象的接口，让子类决定实例化哪一个类。工厂方法使一个类的实例化延迟到其子类。
 5. **原型模式（Prototype）**，用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。
 6. **模板方法模式（Template Method）**，定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。
 7. **外观模式（Facade）**，为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。
 8. **建造者模式（Builder）**，将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。
 9. **观察者模式（Observer）**，定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态发生变化时，会通知所有观察者对象，使它们能够自动更新自己。
 10. **抽象工厂模式（Abstract Factory）**，提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。
 11. **状态模式（State）**，当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类。
 12. **适配器模式（Adapter）**，将一个类的接口转换成客户希望的另外一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。
 13. **备忘录模式（Memento）**，在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可将该对象恢复到原先保存的状态。
 14. **组合模式（Composite）**，将对象组合成树形结构以表示‘部分-整体’的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性。
 15. **迭代器模式（Iterator）**，提供一种方法顺序访问一个聚合对象中各个元素，而又不暴露该对象的内部表示。
 16. **单例模式（Singleton）**，保证一个类仅有一个实例，并提供一个访问它的全局访问点。
 17. **桥接模式（Bridge）**，将抽象部分与它的实现部分分离，使它们都可以独立地变化。
 18. **命令模式（Command）**，将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求排队或记录请求日志，以及支持可撤销的操作。
 19. **职责链模式（Chain of Responsibility）**，使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。将这个对象连成一条链，并沿着这条链传递该请求，直到有一个对象处理它为止。
 20. **中介者模式（Mediator）**，用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。
 21. **享元模式（Flyweight）**，运用共享技术有效地支持大量细粒度的对象。
 22. **解释器模式（Interpreter）**，给定一个语言，定义它的文法的一种表示，并定义一个解释器，这个解释器使用该表示来解释语言中的句子。
 23. **访问者模式（Visitor）**，表示一个作用于某对象结构中的各元素的操作。它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

## 已实现的设计模式

说明：由于平时工作较忙，空闲时间比较有限，因此本仓库将采用不定期的方式进行更新，目前已经实现的设计模式有：
* 第1章 代码无错就是优?——简单工厂模式
* 第2章 商场促销——策略模式
* 第7章 为别人做嫁衣——代理模式
* 第8章 雷锋依然在人间——工厂方法模式
* 第10章 考题抄错会做也白搭——模板方法模式
* 第12章 牛市股票还会亏钱?——外观模式
* 第13章 好菜每回味不同——建造者模式
* 第15章 就不能不换DB吗?——抽象工厂模式
* 第16章 无尽加班何时休——状态模式
* 第21章 有些类也需计划生育——单例模式
* 第22章 手机软件何时统一——桥接模式

## License

DesignPatterns is available under the MIT license. See the [LICENSE](LICENSE) file for more info.
