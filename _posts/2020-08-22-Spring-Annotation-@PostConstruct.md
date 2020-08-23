---
layout: post
title: Spring Annotation - @PostConstruct 
date: 2020-08-22 23:51:49.000000000 +10:00

---

> Executing specific methon in initialization

#### Annotation explanation

Spring annotated @PostConstruct annotation on a method, means the method is executed immediately after this Java Bean is instantiated by Spring before instantiating other Beans. @PostConstruct could also be used for annotating multiple methods in a single Bean.



#### Example code:

```java
package com.example.demo.service;


import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;

import javax.annotation.PostConstruct;

@Service("BeanA")
public class BeanA {
    private static final Logger LOGGER = LoggerFactory.getLogger(BeanA.class);

    public BeanA() {
        LOGGER.info("Bean A constructed in -> {} ", System.currentTimeMillis());
    }

    @PostConstruct
    public void start() {
        LOGGER.info("Bean A started in -> {}, calling Bean B", System.currentTimeMillis());
        BeanB.uniqueInstance().print();
    }

    @PostConstruct
    public void print() {
        LOGGER.info("Bean A running a private function -> {} ", System.currentTimeMillis());
    }
}

```



```java
package com.example.demo.service;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;

import javax.annotation.PostConstruct;

@Service("BeanB")
public class BeanB {
    private static final Logger LOGGER = LoggerFactory.getLogger(BeanB.class);

    public BeanB() {
        LOGGER.info("Bean B constructed in -> {} ", System.currentTimeMillis());
    }

    private static BeanB instance = uniqueInstance();

    public static BeanB uniqueInstance() {
        if (instance == null ) {
            instance = new BeanB();
        }
        return instance;
    }

    @PostConstruct
    public void start() {
        LOGGER.info("Bean B started in -> {} ", System.currentTimeMillis());
    }

    @PostConstruct
    public void print() {
        LOGGER.info("Bean B running a private function -> {} ", System.currentTimeMillis());
    }
}

```



```java
package com.example.demo.service;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;


@Service("BeanC")
public class BeanC {
    private static final Logger LOGGER = LoggerFactory.getLogger(BeanC.class);

    public BeanC() {
        LOGGER.info("Bean C constructed in -> {} ", System.currentTimeMillis());
    }
}

```



#### Execucation result:

```
2020-08-23 10:53:00.761  INFO 49785 --- [           main] com.example.demo.service.BeanA           : Bean A constructed in -> 1598143980761 
2020-08-23 10:53:00.762  INFO 49785 --- [           main] com.example.demo.service.BeanA           : Bean A started in -> 1598143980762, calling Bean B
2020-08-23 10:53:00.762  INFO 49785 --- [           main] com.example.demo.service.BeanB           : Bean B constructed in -> 1598143980762 
2020-08-23 10:53:00.762  INFO 49785 --- [           main] com.example.demo.service.BeanB           : Bean B running a private function -> 1598143980762 
2020-08-23 10:53:00.762  INFO 49785 --- [           main] com.example.demo.service.BeanA           : Bean A running a private function -> 1598143980762 
2020-08-23 10:53:00.762  INFO 49785 --- [           main] com.example.demo.service.BeanB           : Bean B constructed in -> 1598143980762 
2020-08-23 10:53:00.763  INFO 49785 --- [           main] com.example.demo.service.BeanB           : Bean B started in -> 1598143980763 
2020-08-23 10:53:00.763  INFO 49785 --- [           main] com.example.demo.service.BeanB           : Bean B running a private function -> 1598143980763 
2020-08-23 10:53:00.763  INFO 49785 --- [           main] com.example.demo.service.BeanC           : Bean C constructed in -> 1598143980763 
```



#### Add up:

`Constructor >> @Autowired >> @PostConstruct`