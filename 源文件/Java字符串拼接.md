---
title: Java字符串拼接
date: 2018-02-26 19:37:05
tags:
---


1. plus方式

当左右两个量其中有一个为String类型时，用plus方式可将两个量转成字符串并拼接。

`String a="";`
`int b=0xb;`
`String c=a+b;`

2. concat方式

当两个量都为String类型且值不为null时，可以用concat方式。

`String a="a";`
`String b="b";`
`String c= a.concat(b);`

理论上，此时拼接效率应该最高，因为已经假定两个量都为字符串，做底层优化不需要额外判断或转换，而其他方式无论如何优化，都要先走到这一步。

3. append方式

当需要拼接至少三个量的时候，可以考虑使用StringBuffer#append()以避免临时字符串的产生

`StringBuffer buf=new StringBuffer()`
`buf.append("a");`
`if(someCondition){`
`    buf.append("b");`
`}`
`buf.append("c");`
`String d=buf.toString();`

当a,b,c拼接起来会很长时，可以给在构造器中传入一个合适的预估容量以减少因扩展缓冲空间而带来的性能开销。

`StringBuffer buf=new StringBuffer(a.length()+b.length()+c.length());`

JDK对外提供的一些涉及可append CharSequence的参数或返回值类型往往是StringBuffer类型，毕竟安全第一，而StringBuffer大多数情况(包括append操作)线程安全。

若不会出现多线程同时对一实例并发进行append操作，建议使用非线程安全的StringBuilder以获得更好性能

4. 其他

若需拼接至少三个量，只用一个连续拼接的语句就可完成时，从使代码简洁角度考虑，用plus方式。

`String a="a";`
`String b="b";`
`String c="c";`
`String d=a+b+c;`

此时，第4句经JDK编译后其字节码(或)会自动优化为等效于下列代码编译后的字节码。

`String d=new StringBuilder().append(a).append(b).append(c).toString();`

若采用模板+参数来替换占位符的方式或需同时对要拼接日期/数字进行格式化，可以用String.format()来实现

`String c=String.format("a %s!","b");`

此方式资源占用/耗时相对会稍多，毕竟首先要解析模板。当用方法封装并进行format条件调用时，整体效率也不算差。
