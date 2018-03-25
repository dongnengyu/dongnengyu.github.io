---
title: 将javaBean对象转化成Map
---

#码农
```java
package com.dongnengyu.mybatis_test2.service;

/**
 * 董能宇 (dongnengyu@gmail.com)
 * 2018/3/25
 */

import org.apache.commons.beanutils.PropertyUtilsBean;
import java.beans.PropertyDescriptor;
import java.util.HashMap;
import java.util.Map;

public class JavaBeanUtil {

    //将javaBean对象转化成Map
    public Map<String, Object> beanToMap(Object obj) {
        Map<String, Object> params = new HashMap<String, Object>(0);
        try {
            PropertyUtilsBean propertyUtilsBean = new PropertyUtilsBean();
            PropertyDescriptor[] descriptors = propertyUtilsBean.getPropertyDescriptors(obj);
            for (int i = 0; i < descriptors.length; i++) {
                String name = descriptors[i].getName();
                if (!"class".equals(name)) {
                    params.put(name, propertyUtilsBean.getNestedProperty(obj, name));
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        return params;
    }
}
```