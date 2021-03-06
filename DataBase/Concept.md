数据库（Database）是按照数据结构来**组织、存储和管理数据的仓库**，它产生于距今六十多年前，随着信息技术和市场的发展，特别是二十世纪九十年代以后，数据管理不再仅仅是存储和管理数据，而转变成用户所需要的各种数据管理的方式。

数据库有很多种类型，从最简单的存储有各种数据的表格到能够进行海量数据存储的大型数据库系统都在各个方面得到了广泛的应用。

# 关系数据库

关系数据库由表的集合构成，每个表有唯一的名字。表中一行代表了一组值之间的一种联系。

在关系模型的术语中，关系(relation)用来指代表，而元组(tuple)用来指代行，属性(attribute)指表中的列。关系实例(relation instance)表示一个关系的特定实例，也就是所包含的一组特定的行。对于关系的每个属性，都存在一个允许取值的范围，称为该属性的域(domain)。

数据库模式(database schema)：数据库的逻辑设计，数据库实例(database instance)：给定时刻数据库中数据的一个快照。

## 码

一个关系中没有两个元组在所有属性上的值相同，因此一个元组的属性值必须要能够唯一区分元组。

`超码`（super key）是一个或者多个属性的集合，这些属性的集合能够唯一地标识一个关系中的一个元组。超码中可以包含无关紧要的属性，如果 k 是一个超码，那么 k 的任意超集也是超码。

`候选码`（candidate key）：任意真子集都不能成为超码的超码，也即最小超码。有可能有多个不同的属性集都可以做候选码。

`主码`（primary key）：被数据库设计者选中的，主要用来在一个关系中区分不同元组的候选码。主码的选择必须慎重，应该选择那些值从来不变或者极少变化的属性。

码是整个关系的一种性质，而不是单个元组的性质。码的指定代表了被建模的事物在现实世界中的约束。

此外，一个关系模式（如r1）可能在它的属性中包括另一个关系模式（如r2）的主码，这个属性在r1上称作参照r2的`外码`（foreign key）。

## 关系代数

关系代数是一种过程化查询语言，包括一个运算的集合。这些运算以一个或者两个关系作为输入，产生一个新的关系作为结果。关系代数的基本运算有：选择、投影、并、集合差、笛卡尔积和更名。在基本运算外，还有一些其它运算，即集合交、自然连接和赋值。

### 基本关系代数运算

| 基本关系运算 |          解释       |
|------------|--------------------|
|  选择 σ   | 从关系的水平方向进行运算，选择满足给定条件的元组组成新的关系  | 
|  投影 π   | 从关系的垂直方向开始运算，选择关系中的若干列组成新的列          |
|    并    | R,S 具有相同的关系模式，RUS 为属于R或者S的元组|
|  集合差  | R,S 具有相同的关系模式，R-S为属于R但不属于S的元组 |
|  笛卡儿积 | 从两个输入关系中输出所有的元组对（无论它们在共同属性上的取值是否相同）  |
| 更名 ρ  | 将更名运算运用于关系 r，得到一个具有新名字的相同关系 |

### 附加关系代数运算

通过定义一些附加的运算，虽然不能增强关系代数的表达能力，却可以简化一些常用的查询。

|附加关系运算 |          解释       |
|------------|--------------------|
|集合交运算   | R,S具有相同的关系模式，R∩S=R-(R-S) |
|自然连接 ⋈  |  R⋈S 的结果是在R和S中的在它们的公共属性名字上相等的所有元组的组合。 |
| 赋值运算 ←| 类似程序语言中的赋值，将 ← 右侧的表达式的结果赋给左侧的关系变量，该关系变量可以在后续的表达式中使用  |
| 左外链接 ⟕ | R ⟕ S，包含R中所有元组，对每个元组，若在S中有在公共属性名字上相等的元组，则正常连接，若在S中没有在公共属性名字上相等的元组，则依旧保留此元组，并将对应其他列设为NULL |
| 右外链接 ⟖ | R ⟖ S，外连接的结果包含S中所有元组，对每个元组，若在R中有在公共属性名字上相等的元组，则正常连接，若在R中没有在公共属性名字上相等的元组，则依旧保留此元组，并将对应其他列设为NULL。 |
| 全外链接 ⟗ | R ⟗ S，全外连接的结果包含R与S中所有元组，对每个元组，若在另一关系上中有在公共属性名字上相等的元组，则正常连接，若在另一关系上中没有在公共属性名字上相等的元组，则依旧保留此元组，并将对应其他列设为NULL。|

# No-SQL 数据库

传统的关系数据库具有不错的性能，高稳定型，久经历史考验，而且使用简单，功能强大，同时也积累了大量的成功案例。在互联网领域，MySQL成为了绝对靠前的王者，毫不夸张的说，MySQL为互联网的发展做出了卓越的贡献。

在90年代，一个网站的访问量一般都不大，用单个数据库完全可以轻松应付。在那个时候，更多的都是静态网页，动态交互类型的网站不多。到了最近10年，网站开始快速发展。火爆的论坛、博客、sns、微博逐渐引领web领域的潮流。随着访问量的上升，几乎大部分使用MySQL架构的网站在数据库上都开始出现了性能问题，web程序不再仅仅专注在功能上，同时也在追求性能。

所以出现了 NoSQL数据库，NoSQL最常见的解释是“non-relational”，“Not Only SQL”也被很多人接受。NoSQL被我们用得最多的当数key-value存储，当然还有其他的文档型的、列存储、图型数据库、xml数据库等。

NoSQL无需事先为要存储的数据建立字段，随时可以存储自定义的数据格式。而在关系数据库里，增删字段是一件非常麻烦的事情。如果是非常大数据量的表，增加字段简直就是一个噩梦。这点在大数据量的web2.0时代尤其明显。

# 更多阅读

[NoSQL开篇——为什么要使用NoSQL](http://www.infoq.com/cn/news/2011/01/nosql-why)  



