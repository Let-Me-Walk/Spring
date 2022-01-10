# Spring

框架怎么学习？框架是其他人写好的软件
1）知道框架能做什么，mybatis--访问数据库，对表中的数据执行增删查改
2）框架的语法，框架要完成一个功能，需要一定的步骤来支持的，
3）学习框架的内部实现，原理是什么
4）通过学习，实现一个自己的自定义框架

第一章 IOC-Inversion of Control

1.IOC概念
1）IOC-控制反转，是一种理论，是一个思想，描述的是把对象的创建，赋值、管理都交给代码之外的容器（Container）实现。也就是说对象的创建由其他的外部资源来完成
2）控制：创建对象，对象属性的赋值，对象之间的关系管理
3）反转：把原来开发人员管理创建对象的权限转移给代码之外的容器实现。由容器代替开发人员管理对象，创建对象、给对象赋值
4）正转：由开发人员在代码中使用new 构造方法创建对象，开发人员主动管理对象（自己决定对象）
5）容器：可以是一个服务器软件，可以说一个框架（如spring）
6）使用IOC的优点：做到最少对代码的改动也能实现不同的功能（少做多得），实现解耦合，降低代码之间依赖程度

2.java中创建对象方式
1）构造方法：new student（）；
2）反射：
3）序列化
4）克隆
5）IOC：容器创建对象


3.IOC的技术实现
1）DI（Dependency Injection）依赖注入：是IOC的技术实现
只需要在程序中提供要使用的对象名称即可，这个对象在容器中如何创建、赋值、查找都由容器内部实现 
spring使用ID实现了IOC功能，底层使用的是Java反射机制




第二章：AOP-Aspect Orient Programming

1.动态代理（面试常问）：
  实现方式：JDK动态代理，使用JDK中的Proxy，Method，InvocationHandler创建代理对象，JDK动态代理要求目标类必须实现接口
           CJLIB动态代理，第三方的工具库，创建代理对象，原理是继承。通过继承目标类，创建其子类，子类就是代理对象，要求目标类不能是final的，其中方法也不能是final
           
2.动态代理的作用（面试常问）：
1）在目标类源代码不变，不需要重新编译的情况下，增加功能
2）减少代码的重复，提高复用率
3）专注业务逻辑代码
4）解耦合，让业务功能和日志、事务等非业务能封离

3.AOP：面向切面编程
  Aspect：切面，给你的目标类（业务类）增加的新功能，就是切面，如例子，增加的时间、事务等功能都叫切面
          切面的特点：一般都是非业务方法，独立使用的
          
  Orient：面向，对着
  
  Programming：编程
  
  oop：面向对象编程
  oip：面向接口编程
  
4.怎么理解面向切面编程？（面试常问）
1）.需要在分析项目功能时，找出切面（难点所在）
2）.合理的安排切面的执行时间（在目标方法前面执行、还是后面执行）
3）.合理的安排切面的位置，在哪个类、哪个方法增加增强功能

5.术语
1）Aspect：切面，表示增强的功能，就是一堆代码，完成某一个非业务功能，常见的有日志，事务，统计信息，参数检查，权限验证
2）JoinPoint：连接点，连接业务方法和切面的位置。就是某个目标类中的业务方法
3）Pointcut:切入点，指多个连接方法的集合，多个方法，一般用于表示切面执行的位置
4）目标对象：给哪个类的方法增加功能，这个类就是目标对象
5）Advice：通知，通知表示切面功能执行的时间

一个切面有三个关键因素：
1）切面的功能代码，切面干什么-----Aspect
2）切面的执行位置，使用Pointcut表示切面执行的位置
3）切面的执行时间，使用Advice表示时间，在目标方法之前还是之后
           
6.aop的实现：aop是一个规范，是动态代理的一个规范化，是一个标准
 aop技术实现的框架：
 1）spring：在spring内部实现了aop规范，能做aop的构造；
            我们在项目中很少使用spring的aop实现，因为spring的aop比较笨重
            spring主要在做事务处理时用aop
            
 2）aspectJ：一个开源的专门做aop的框架，spring框架中集成了aspectJ框架，通过spring就能使用aspectJ的功能
             aspectJ框架实现aop有两种方式：
             1.使用xml的配置文件，配置全局事务
             2.使用注解，我们在项目中一般都用注解实现aop，aspecJ有5个注解
               1）Before
               2）AfterReturning
               3）AfterThrowing
               4）Around
               5）After
               
 
 
 
 ====================================================================================================================================
 第三章：spring整合mybatis
 
 to be continue..........
 
 
 ====================================================================================================================================
 第四章：spring事务处理
 
 一.处理事务需要做什么？怎么做？
 spring处理事务的的模型，使用的步骤都是固定的。把事务使用的信息提供给spring就可以了
 
 1. 事务内部 提交、回滚使用的是事务管理器对象，代替你完成commit，rollback
    
    1)事务管理器：是一个接口和接口的众多实现类组成的。
    
    2)接口：platformTranscationManager，定义了事务处理的重要方法-commit()、rollback().
    
    3)实现类：spring把每一种数据库访问技术对应的事务处理类都封装创建好了。
           mybatis访问数据库——spring创建好的是DataSourceTranscationManager
           hibernate访问数据库——spring创建好的是HibernateTranscationManager
          
    4)怎么使用：你需要告诉spring需要用的是哪种数据库访问技术
    5)如何告诉：在spring配置文件中使用<bean>标签声明使用的数据库访问技术对应的实现类就可以了
            如，使用mybatis访问数据库技术：<bean id="xxx" class="...DataSourceTranscationManager">
                使用Hibernate访问数据库技术：<bean id="xxx" class="...HibernateTranscationManager">
  
 2.你的业务方法需要什么样的事务，向spring说明需要事务的类型
   事务类型由三部分组成：事务隔离级别、事务传播行为、事务超时时间
   1）事务隔离级别：一共四个级别，若不选择则采用默认级别（Default）。mysql 默认级别为REPEATABLE_READ，Oracle默认级别为READ_COMMITTED
      READ_UNCOMMITTED：读未提交，未解决任何并发问题
      READ_COMMITTED：读已提交，解决脏读问题，存在不可重复读与幻读问题
      REPEATABLE_READ:可重复读，解决脏读、不可重复读、幻读问题
      SERIALIZABLE:串行化，无并发问题
  
   2)事务传播行为：控制业务方法是否有事务，是怎么样的事务的，一共有7个传播行为，表示业务方法调用时，事务在方法间是怎么样使用的
     PROPAGATION_REQUIRED
     PROPAGATION_REQUIRED_NEW
     PROPAGATION SUPPORTS
     以上三个为常用重要的
     PROPAGATION_MANDATORY
     PROPAGATION_NESTED
     PROPAGATION_NEVER
     PROPGATION_NOT_SUPPORTED
  
  3）事务的超时时间：表示一个方法最长允许的执行时间，如果方法执行超过了时间，事务就回滚，单位是秒，整数值，默认为-1，一般不做改动
  
 3.事务commit、rollback的时机：
   1）当业务方法执行成功，没有异常抛出，则当方法执行完毕，spring在方法执行完成后提交事务，调用事务管理器的commit
   2）当业务方法抛出运行时异常或error是，spring执行回滚操作，调用事务管理器的rollback
      运行时异常定义：RunTimeException，它与它的子类都为运行时异常，如NullPointException、NumberFormatException等
   3）当你的方法抛出非运行时异常，主要是受控异常时，提交事务，调用事务管理器的commit
      受控异常：代码中必须处理的异常，如IOException、SQLException 
