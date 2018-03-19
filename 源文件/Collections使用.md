---
title: Collections使用
---

#码农
### util.Collection与java.util.Collections区别
* util.Collection 是一个集合接口。它提供了对集合对象进行基本操作的通用接口方法。Collection接口在Java 类库中有很多具体的实现。Collection接口的意义是为各种具体的集合提供了最大化的统一操作方式。
* java.util.Collections 是一个包装类。它包含有各种有关集合操作的静态多态方法。此类不能实例化，就像一个工具类，服务于Java的Collection框架。
```java
/**
 * xiaomu (dongnengyu@gmail.com)
 * 2018/3/18
 */

import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class Test {

    public static void main(String[] args) {

        List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);

        //查找最小值
        System.out.println(Collections.min(intList));

        // 查找最大值
        System.out.println(Collections.max(intList));

        //使集合乱序
        Collections.shuffle(intList);
        System.out.println(intList);

        //该方法用于返回一个不可变列表组成的n个拷贝的指定对象。
        // 生成一个由10个100组成的整数列表
        List<Integer> nCopiesList = Collections.nCopies(10, 100);
        //[100, 100, 100, 100, 100, 100, 100, 100, 100, 100]
        System.out.println(nCopiesList);

        //对集合排序，从小到大
        Collections.sort(intList);
        System.out.println(intList);

        //对集合排序，从大到小，需要重写，以后再填坑
        Collections.sort(intList);
        System.out.println(intList);

        //binarySearch
        System.out.println(Collections.binarySearch(intList, 18));

        //copy
        //用两个参数，一个目标 List 和一个源 List, 将源的元素拷贝到目标，并覆盖它的内容。目标 List至少与源一样长。
        List<String> listOne = Arrays.asList("A", "B", "C", "D");
        List<String> listTwo = Arrays.asList("X", "Y", "Z");
        //listOne 是目标List,所以他的元素会被listTwo（源List）覆盖
        Collections.copy(listOne, listTwo);
        System.out.println(listOne);// [X, Y, Z, D]
        System.out.println(listTwo);//[X, Y, Z]

        //disJoint
        //用于检查两个集合有无相同的元素，如果没有则返回true。
        List<String> list3 = Arrays.asList("A", "B", "C", "D");
        List<String> list4 = Arrays.asList("A", "Y", "Z");
        boolean disJoint = Collections.disjoint(list3, list4);
        // 返回false，因为两个集合都有A
        System.out.println(disJoint);


        //未完待续




    }
}
```

