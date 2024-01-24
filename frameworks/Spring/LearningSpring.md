# Spring Framework

#### INDEX
* [What is Spring FrameWork](#what-is-spring-framework)
* [Dependency Injection](#dependency-injection)
    * [Working of Dependency Injection](#working-of-dependency-injection)
    * [Java2EE Layers](#java2ee-layers)
* [Spring Modules](#spring-modules)
* [Spring IoC Container](#spring-ioc-inversion-of-control-container)
    * [ApplicationContext](#applicationcontext)

### What is Spring FrameWork ?
* Spring is a Dependency Injection framework to make java application loosely coupled. Spring framework is also called as **FRAMEWORK OF FRAMEWORKS**.
* Spring framework makes the development of JavaEE application easy.
* It was developed by **ROD JOHNSON** in 2003.

### Dependency Injection
* It is a design pattern.
* Inversion Of Control(IOC):- Jab humlog object creation ka control apne haath se hataker spring ko dedete hai phir spring un dependencies ka object dynamically runtime pe create karke inject kar deta hai. This is called Inversion Of Control(IOC).

### Working of Dependency Injection
![Dependency Injection](/frameworks/Spring/images/DependencyInjection_IOC.png)

### Java2EE Layers
![Java2EE Layers](/frameworks/Spring/images/java2EE_Layers.png)

### Spring Modules
![Spring Modules](/frameworks/Spring/images/Spring_Module.png)

### Spring IoC (Inversion Of Control) Container
* It is a predefine program.
* It is a component of spring framework so basically it comes with spring framework.
* Working of IoC :- 
    * Creating objects.
    * Holding objects in memory.
    * Injecting one object into another object as required i.e Dependency Injection.
    * It basically maintains the life cycle of an object i.e from creation till destruction of an object.
* We need to tell the spring container that which bean or pojo class it has maintain or manage.
* We have to provide the information of our config(xml) file. We do this so that spring container could understand that which bean is dependent. Now spring container after analying the config(xml) file, it will create the object of dependent beans.

![IOC](/frameworks/Spring/images/IOC.png)

### ApplicationContext
* It reprensent Spring IoC container or context.
* It already contains bean factory since it extends bean factory.
* It is an interface. 
* Since it is an interface we can not create it's object but we can create object of it's subclasses which are as follows:- 
    * **ClasspathXMLApplicationContext**:- It searches for XML Config file in Java's classpath.
    * **AnnotationConfigApplicationContext**:- It searches for those beans in which we have used annotation.
    * **FileSystemXMLApplicationContext**:- It searches for XML Config file in File System.

![ApplicationContext](/frameworks/Spring/images/ApplicationContext.png)














