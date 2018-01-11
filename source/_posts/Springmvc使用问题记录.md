---
title: Springmvc使用问题记录
date: 2018-01-11 18:09:35
tags:
    - springmvc
    - json
---

# 使用jackson将json字符串转为java bean时 报错

## 描述
错误为
```
com.fasterxml.jackson.databind.JsonMappingException: No suitable constructor found for type [simple type, class com.findcookie.ssm.entity.User]: can not instantiate from JSON object (missing default constructor or creator, or perhaps need to add/enable type information?)
 at [Source: {"id":28,"userName":"1","password":"8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92","createdAt":1515638029000,"updatedAt":1515638029000}; line: 1, column: 2]
```
大意为json字符串不能被实例化为对象，提示是否遗漏默认构造方法，对！缺少默认构造方法

## 解决方案

为实体加上默认的无参构造方法
```
    public User(){
        super();
    }
```
我猜先new了一个这个Class，但是没有默认的无参的构造方法（已经有其他有参的构造方法了，所以没默认隐式的了），然后再把json中的键值对，通过setKey的方式给到对象。
