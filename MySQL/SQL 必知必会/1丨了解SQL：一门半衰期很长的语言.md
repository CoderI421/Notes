# 1丨了解SQL：一门半衰期很长的语言

> 全专栏的 Xmind:https://github.com/cystanford/SQL-XMind

在我们的日常工作中，使用的是类似 MySQL、Oracle 这种的数据库管理系统，实际上这些数据库管理系统都遵循 SQL 语言，这就意味着，我们在使用这些数据库的时候，都是通过 SQL 语言与它们打交道。所以对于从事编程或者互联网行业的人来说，最具有中台能力的语言便是 SQL 语言。自从 SQL 加入了 TIOBE 编程语言排行榜，就一直保持在 Top 10。

1. SQL 语言无处不在，它对于不同职位的人来说都有价值。SQL 已经不仅仅是技术人员需要掌握的技能，产品经理、运营人员也同样需要掌握 SQL。
2. SQL 语言从诞生到现在，很少变化。这就意味着一旦你掌握了它，就可以一劳永逸，至少在你的职业生涯中，它都可以发挥作用。
3. SQL 入门并不难。

## 一、半衰期很长的 SQL

可以说在整个数字化的世界中，最重要而且最通用的元基础就是数据，而直接与数据打交道的语言就是 SQL 语言。很多人忽视了 SQL 语言的重要性，认为它不就是 SELECT 语句吗，掌握它应该是数据分析师的事。事实上在实际工作中，你不应该低估 SQL 的作用。如今互联网的很多业务处理离不开 SQL，因为它们都需要与数据打交道。

SQL 在各种技术和业务中无处不在，它的情况又是怎样的呢？45 年前，也就是 1974 年，IBM 研究员发布了一篇揭开数据库技术的论文《SEQUEL：一门结构化的英语查询语言》，直到今天这门结构化的查询语言并没有太大的变化，相比于其他语言，SQL 的半衰期可以说是非常长了。

**SQL 有两个重要的标准，分别是 SQL92 和 SQL99，它们分别代表了 92 年和 99 年颁布的 SQL 标准，我们今天使用的 SQL 语言依然遵循这些标准**。要知道 92 年是 Windows3.1 发布的时间，如今还有多少人记得它，但如果你从事数据分析，或者和数据相关的工作，依然会用到 SQL 语言。

作为技术和互联网行业的从业人员，我们总是希望能找到一个通用性强，变化相对少，上手相对容易的语言，SQL 正是为数不多的，可以满足这三个条件的语言。

## 二、入门 SQL 并不难

SQL 功能这么强大，那么学起来会很难吗？一点也不。SQL 不需要像其他语言那样，学习起来需要大量的程序语言基础，SQL 更像是一门英语，有一些简单的英语单词，当你使用它的时候，就好像在用英语与数据库进行对话。

我们可以**把 SQL 语言按照功能划分成以下的 4 个部分：**

1. **DDL，英文叫做 Data Definition Language，也就是数据定义语言，它用来定义我们的数据库对象，包括数据库、数据表和列。通过使用 DDL，我们可以创建，删除和修改数据库和表结构。**
2. **DML，英文叫做 Data Manipulation Language，数据操作语言，我们用它操作和数据库相关的记录，比如增加、删除、修改数据表中的记录。**
3. **DCL，英文叫做 Data Control Language，数据控制语言，我们用它来定义访问权限和安全级别。**
4. **DQL，英文叫做 Data Query Language，数据查询语言，我们用它查询想要的记录，它是 SQL 语言的重中之重。在实际的业务中，我们绝大多数情况下都是在和查询打交道，因此学会编写正确且高效的查询语句，是学习的重点。**

学习 SQL 就像学习英文语法一样。SQL 是为数不多的声明性语言，这种语言的特点就是，你只需要告诉计算机，你想从原始数据中获取什么样的数据结果即可。比如我想找主要角色定位是战士的英雄，以及他们的英雄名和最大生命值，就可以输入下面的语言：

```mysql
SELECT name, hp_max FROM heros WHERE role_main = '战士'
```

这里我定义了 heros 数据表，包括了 name、hp_max、role_main 等字段，具体的数据表我会在后面的课程中作为示例讲解，这里只是做个简单的说明。

你能从这段代码看出，我并没有告诉计算机该如何执行才能得到结果，这也是声明性语言最大的便捷性。我们不需要指定具体的执行步骤，比如先执行哪一步，再执行哪一步，在执行前是否要检查是否满足条件 A 等等这些传统的编程思维。

SQL 语言定义了我们的需求，而不同的 DBMS（数据库管理系统）则会按照指定的 SQL 帮我们提取想要的结果，这样是不是很棒！

## 三、开启 SQL 之旅

**SQL 是我们与 DBMS 交流的语言**，我们在创建 DBMS 之前，还需要对它进行设计，**对于 RDBMS 来说采用的是 ER 图（Entity Relationship Diagram），即实体 - 关系图的方式进行设计。**

**ER 图评审通过后，我们再用 SQL 语句或者可视化管理工具（如 Navicat）创建数据表。**

实体 - 关系图有什么用呢？它是我们用来描述现实世界的概念模型，在这个模型中有 3 个要素：实体、属性、关系。

**实体就是我们要管理的对象，属性是标识每个实体的属性，关系则是对象之间的关系**。比如我们创建了“英雄”这个实体，那么它下面的属性包括了姓名、职业、最大生命值、初始生命值、最大魔法值、初始魔法值和攻击范围等。同时，我们还有“用户”这个实体，它下面的属性包括用户 ID、登录名、密码、性别和头像等。

“英雄”和“用户”这两个实体之间就是多对多的关系，也就是说一个英雄可以从属多个用户，而一个用户也可以拥有多个英雄。

除了多对多之外，也有一对一和一对多的关系。

创建完数据表之后，我们就可以用 SQL 操作了。你能看到很多 SQL 语句的大小写不统一，虽然大小写不会影响 SQL 的执行，不过我还是推荐你采用统一的书写规范，因为好的代码规范是提高效率的关键。

**关于 SQL 大小写的问题，我总结了下面两点：**

1. **表名、表别名、字段名、字段别名等都小写；**
2. **SQL 保留字、函数名、绑定变量等都大写。**

比如下面这个 SQL 语句：

```mysql
SELECT name, hp_max FROM heros WHERE role_main = '战士'
```

你能看到 SELECT、FROM、WHERE 这些常用的 SQL 保留字都采用了大写，而 name、hp_max、role_main 这些字段名，表名都采用了小写。此外在数据表的字段名推荐采用下划线命名，比如 role_main 这种。

## 总结

今天我带你初步了解了 SQL 语言，当然，SQL 再简单，也还是需要你一步一步，从点滴做起，先掌握基本的 DDL、DML、DCL 和 DQL 语法，再了解不同的 DBMS 中的 SQL 语法差异，然后再来看如何优化，提升 SQL 的效率。要想写出高性能的 SQL，首先要了解它的原理，其次就是做大量的练习。

SQL 的价值在于通用性强（市场需求普遍），半衰期长（一次学习终身受用），入门不难。实际上，很多事情的价值都可以按照这三点来进行判断，比如一个产品的市场价值。如果你是一名产品经理，你是喜欢通用性更强的产品，还是喜欢更个性的产品。今天的文章只是简单预热，你可能也会有一些感悟，不妨说说你对一个产品或者语言的市场价值的理解。

![image-20220906234033830](1%E4%B8%A8%E4%BA%86%E8%A7%A3SQL%EF%BC%9A%E4%B8%80%E9%97%A8%E5%8D%8A%E8%A1%B0%E6%9C%9F%E5%BE%88%E9%95%BF%E7%9A%84%E8%AF%AD%E8%A8%80.resource/image-20220906234033830.png)

欢迎你在评论区写下你的心得，也欢迎把这篇文章分享给你的朋友或者同事，让更多人了解 SQL 这门语言。

## 精选留言

- 对于大小写问题，不同的数据库系统规范不一样吧？

  作者回复: 不太一样
  MySQL在Windows下都不区分大小写。
  Oracle中，SQL语句是不区分大小写，如果查询中有字符，是区分大小写的
  比如 SELECT * FROM heros WHERE name = 'guanyu'
  和 SELECT * FROM heros WHERE name = 'GUANYU'
  在Oracle中会认为是不同的查询，而在MySQL中是相同的查询
  同时，我们可以通过修改系统参数来进行配置，比如在MySQL可以通过参数lower_case_table_names来配置
  数据库和数据表的大小写敏感性
  
- 作者的回复有误吧：MYSQL是否区分大小写是可以设置的，我前几天刚装了套-默认是区分大小写；我同事的代码就报错。5.6开始的版本基本上都是大小写敏感的，除非设置成不区分大小写。
  不同数据库的sql特性不同：各家对T-SQL的支持/保留不一样吧；sql server保留的最好-其实当时从它的名字也可以发现这点，其次是sybase,后面是mysql【注：5.5后的版本有太多oracle的东西继承了】oracle只保留了大概60-70%左右的T-SQL。
  其实mysql默认安装是区分大小写的：尤其是表名和数据库名；除非参数设置进行修改；尤其是5.6开始。各家对关键字的保留还不一样：这是数据库用多了最大的问题，总是会记岔了关键字。

  展开**

  作者回复: **MySQL是否区分大小写是可以通过参数设置的。**
  **同时MySQL在默认情况下是否区分大小写，也和操作系统有关。比如在Linux下，MySQL对表名和数据库名是区分大小写的。而在Windows下，MySQL默认情况是不区分大小写的**
  
- 老师日常 画ER图都是用什么工具啊？

  作者回复: Navicat本身也有ER图，你可以在左侧面板中选择一个数据库，然后再从上面导航条中选择“查看”=>"ER图表”就可以显示出来
  另外你也可以使用PowerDesigner来设计ER图

  

- 老师，请问学习SQL是不就是学习数据库呢？这两者是个什么关系

  作者回复: SQL是结构化查询语言，是有相应标准的，就类似英语语法一样，只不过是操作数据库的语言。
  而数据库软件则是实现SQL的数据库管理系统，你可以把它理解是个软件，不同家软件的特点不同，也同时在SQL的标准上有自己独特的部分。比如MySQL有存储引擎，Oracle有共享池等。虽然不同的数据库软件有所差异，但是SQL都是他们的基本语言。
  
- 老师，请问数据库管理系统和数据库是一回事吗？如果不是的话，他们是什么关系？

  作者回复: 这个我在后面会讲到：
数据库管理系统，DataBase Management System，简称DBMS，实际上它可以对多个数据库进行管理，所以你可以理解为DBMS = 多个数据库（DB） + 管理程序。
  数据库，DataBase。数据库是存储数据的集合，你可以把它理解为多个数据表。
数据库系统，DataBase System。它是更大的概念，包括了数据库、数据库管理系统以及数据库管理人员DBA。
