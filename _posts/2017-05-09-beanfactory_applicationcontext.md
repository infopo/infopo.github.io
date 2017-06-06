---
layout: post
title: BeanFactory vs ApplicationContext
category: etc
---

**BeanFactory vs ApplicationContext**  
The difference between BeanFactory and ApplicationContext in Spring framework is another frequently asked Spring interview question mostly asked Java programmers with 2 to 4 years experience in Java and Spring. Both BeanFactory and ApplicationContext provides a way to get a bean from Spring IOC container by calling getBean("bean name"), but there is some difference in there working and features provided by them. One difference between bean factory and application context is that former only instantiate bean when you call getBean() method while ApplicationContext instantiates Singleton bean when the container is started,  It doesn't wait for getBean to be called. This interview questions is third on my list of frequently asked spring questions e.g. Setter vs Constructor Injection and  What is default scope of Spring bean. If you are preparing for Java interview and expecting some Spring framework question, It’s worth preparing those questions.  

If you are new in Spring framework and exploring Spring API and classes than you would like check my post on some Spring utility functions e.g. calculating time difference with StopWatch and  escaping XML special characters using Spring HtmlUtils. Coming back to BeanFactory vs ApplicationContext, let’s see some more difference between them in next section.  


*BeanFactory vs ApplicationContext in Spring*  

Before seeing difference between ApplicationContext and BeanFactory, let see some **similarity** between both of them. Spring provides two kinds of IOC container, one is BeanFactory and other is ApplicationContext. Syntactically BeanFactory and ApplicationContext both are Java interfaces and ApplicationContext extends BeanFactory. Both of them are configuration using XML configuration file. In short BeanFactory provides basic IOC and DI features while ApplicationContext provides advanced features.  

Apart from these, Here are few more **difference** between BeanFactory and ApplicationContext which is mostly based upon features supported by them.  

1. BeanFactory doesn't provide support for internationalization i.e. i18n but ApplicationContext provides support for it.

2. Another difference between BeanFactory vs ApplicationContext is ability to publish event to beans that are registered as listener.

3. One of the popular implementation of BeanFactory interface is XMLBeanFactory while one of the popular implementation of ApplicationContext interface is ClassPathXmlApplicationContext. On Java web application we use WebApplicationContext  which extends ApplicationContext interface and adds getServletContext method.

4. If you are using auto wiring and using BeanFactory than you need to register AutoWiredBeanPostProcessor using API which you can configure in XML if you are using  ApplicationContext. In summary BeanFactory is OK for testing and non production use but ApplicationContext is more feature rich container implementation and should be favored over BeanFactory

These were some worth noting difference between BeanFactory and ApplicationContext in Spring framework. In most practical cases you will be using ApplicationContext but knowing about BeanFactory is important to understand fundamental concept of spring framework. I mostly use XML configuration file and ClassPathXmlApplicationContext to quickly run any Spring based Java program from Eclipse  by using following snippet of code :  

```
public static void main(String args[]){
    ApplicationContext ctx =new ClassPathXmlApplicationContext("beans.xml");
    Hello hello =(Hello) ctx.getBean("hello");
    hello.sayHello("John");
}
```    

here beans.xml is your spring configuration file and “hello” is a bean defined in that spring configuration file. Here we have used ClassPathXmlApplicationContext  which is an implementation of ApplicationContext interface in Spring.  

[Read more](http://javarevisited.blogspot.com/2012/11/difference-between-beanfactory-vs-applicationcontext-spring-framework.html#ixzz4S32Aa9Lw){:target="_blank"}  

