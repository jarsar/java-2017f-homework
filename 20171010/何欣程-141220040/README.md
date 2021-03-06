# 工程说明

在完成葫芦娃作业的过程中，我主要从两个方面来考虑实现问题，一个应该如何将整个葫芦娃大战妖怪的整个事件抽象出来，第二是该怎样将项目划分成各部分，更有条理地实现。

## 一 抽象
![2](https://github.com/njuhxc/java-2017f-homework/blob/master/20171010/何欣程-141220040/jpg/2.png)

整个世界都可以作为一个存在(Being)，存在分为生物(Creature)和非生物的二维空间(Position)，Creature有五个子类，葫芦娃，人，蛇，蝎子，小兵。这样，就形成了完整的父类和子类的关系。

从属性来讲：
生物拥有属性：CREATURE_TYPE  type，String name，int position_x，int position_y。即属于哪种生物，名字叫什么，在二位空间坐标是多少，这是所有生物都具有的特征。
葫芦娃在生物的基础上，拥有颜色，在兄弟中排行等特殊属性。
小兵在生物基础上，拥有在小兵中排行的特殊属性。
非生物二维空间中一个position则拥有属性：CREATURE_TYPE  type，int id，bool is_empty，int x,int y
即这个位置具体是哪个坐标，是否为空，不空的话在这个位置上的是什么人等。

从行为来讲：
生物均拥有改变位置的行为，即走进一个位置，走出一个位置，其中————
爷爷，蛇精都拥有加油这一行为，但具体加油的内容不同，故选择用接口实现。
葫芦娃，蝎子精，小兵拥有切换队形的行为。
位置position拥有：让某一个生物走进位置，让一个生物走出位置，展现目前在自己位置上生物是谁的行为。

通过以上分析，大体可以写出各类的各项属性与成员函数。
其中，为了保证数据的完整性，所有成员变量均为protected/private，对外传递均使用成员函数进行传递。


## 二 代码结构
![1](https://github.com/njuhxc/java-2017f-homework/blob/master/20171010/%E4%BD%95%E6%AC%A3%E7%A8%8B-141220040/jpg/1.png)

由上图，可以清晰地看出代码结构。本项目由三大部分组成：
BaseDefine: Action.java,Being.java,Creature.java,Position.java
以上四个文件定义了各父类，子类的属性以及本身具有的行为。
RealDefine:WarRole.java 具体地定义了一场战争的规则，想让定义出来的这些对象做什么，怎么做，这个工程的执行顺序是什么。
RunGame:WarStart.java 封装好的对外接口，用户所拿到的只有warRole.war_start()这一个用户接口。

## 三 好处
通过一层层的封装和抽象，我深刻地体会到了抽象机制的必要性。
一，结构清晰分明，让人一目了然。
二，保护数据完整性和私密性。
三，对外接口清晰，便于程序的维护和扩展。
