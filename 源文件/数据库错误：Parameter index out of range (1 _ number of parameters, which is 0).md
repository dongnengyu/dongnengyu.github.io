---
title: 数据库错误：Parameter index out of range (1 > number of parameters, which is 0). 
date: 2018-02-27 21:49:11
tags:
---

错误发生原因其实很简单😏，就是当设置参数时，没有相应的问号与之匹配（或者根本就没有？号）.
如果是：Parameter   index   out   of   range   (26   >   number   of   parameters,  which   is   25). 
翻译为：找到了25个问号，却插入了26个值，导致参数越界（根据得到的信息打印将很容易判断数据是否与数据库字段匹配等小问题）。
 
与sql语句有关的原因如下：
1.？号被单引号包围。
（如setString(1,"slkdjfkd");时sql语句为：insert into table1 (c1,c2) values ('?','?')）。
此时？会被作为参数传入，而不会再传入 setString里面的值。
 
2.sql语句中没有？号，在后面用到了set语句。（如：select * from table）；
此时无需传值。传值就会出错。
 
3.初学者很常见的错误：?---？
这两个问号是不同了，因为一个是中文，一个是英文，如果在sql语句中写入的是英文，将无法识别。
 
 
其他原因：
1.连接已经关闭。 
 如果与其他操作语句一起公用conn时，如果上一操作已经关闭连接，则会报错。表现为：时而能够进行操作，时而不能。
2.pstm没有初始化，无驱动包，得到连接出错等基础问题……
