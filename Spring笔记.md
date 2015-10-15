这篇笔记是在看慕课网上《Spring入门篇》时做的笔记。
由于在实际项目中使用过IOC方面的东西，所以对于课程里IOC内容理解的很好。由于没有使用过AOP，所以对课程里的AOP的使用和内容理解不足。对于这方面内容只是作为了解，对于后面的AspectJ的方面的也只是了解一下，__在用到的时候再来学习__。

重要：__对于本文没有详细说明的内容，需要详细了解读者希望可以去查找Spring官方文档__。

注：在正文中 __加粗__是引起注意，_斜体_表示不知道那句话对不对。

目录：
==========


[TOC]



## 1-1 课程简介
SpringFramework中的IOC和AOP只是Spring里面基础的东西，SpringFramework还包括其他的东西：Spring Expression Language, Spring Integration, __Spring Web Flow__, __Spring Security__, Spring Data, Spring Batch。

<br/>
## 1-2 Spring概况
Spring是一个开源框架，为了解决开发过程的复杂性而创建的。__控制反转(IOC)和面向切面(AOP)是容器框架__。通过IOC技术达到松耦合的目的，AOP技术可以分离应用的业务逻辑和系统级服务进行内聚性的开发。__Spring管理并应用对象的配置和生命周期__，这个意义上算是一种容器。__Spring支持将简单的组件组合成复杂的应用__，这个意义上是一个框架。__Spring作用__：是一种容器；并提供多种技术的支持；AOP(应用在事务管理、日志等)提供了方便的辅助类；主流应用框架的支持。

<br/>
## 1-3 框架
__框架__的特点：是一个半成品，封装了特定的处理流程和控制逻辑，更专注于某一个领域。

<br/>
## 2-1 IOC及Bean容器
__接口__就是类似于函数的声明。__面向接口编程__：在结构设计中不同的层次之间依赖于接口而不是接口的实现，接口实现的变动不影响各层之间的调用。
**IOC：**控制反转；控制权的转移，应用程序本身不负责依赖对象的创建和维护，而是由外部容器创建和维护，__由IOC容器(Spring容器)负责创建并管理对象__。**DI(依赖注入)**是一种实现的方式。IOC目的是创建对象和组装对象之间的关系。例如：如果类A依赖类B，在实例化的时候，IOC容器实例化A和B并把B赋值给A。__什么被反转了__：获得依赖对象的过程被反转了，获得依赖对象的过程由自身管理变成了由IOC容器主动注入。所谓的__依赖注入__就是由IOC容器在运行期间，动态的将某中依赖关系注入到对象之中。__过程__：先找到IOC容器，容器返回需要的对象，然后开始使用对象。
Spring的Bean配置：class是Bean的具体的类。classpath中的信息加载到Spring的上下文中去。
__Bean初始化：BeanFactory提供配置结构和基本功能，加载并初始化Bean；ApplicationContent保存了Bean的对象并在Spring中被广泛使用__。初始化ApplicationContent方式(扫描xml文件)：本地文件，Classpath，Web应用中依赖servlet和Listener

<br/>
## 2-2 Spring注入方式
Spring注入是指在启动Spring容器加载Bean配置的时候，完成对变量的赋值行为。如：类A依赖类B，在初始化A的时候，IOC就会对A的依赖B进行赋值。
注入方式：__设值注入__(自动的调用set方法)和构造注入(有构造器且__同名__参数)。
``` xml
// 设值注入(自动的调用set方法)
<bean id ="id"  class="com.test">
	<property name="property_name" ref=""/>// 需要在类里面有一个setproperty_name的方法，才可以。具体使用方式可以查资料。
</bean>

// 构造注入(有构造器，有同名参数)
<bean id ="id"  class="com.test">
	<constructor-arg name="para_name" ref=""/>// 需要在类里面有一个构造器的方法且有一个同名参数才可以。具体使用方式可以查资料。
</bean>
```

<br/>
## 3-1 Bean的配置项和作用域
Bean配置项：class必须，其他的可以不写。有许多配置项，请自行查找。
Bean的作用域：__singleton__单例一个Bean容器中只存在一份「_一个上下文(ApplicationContent)对应于一个Bean容器_」；__prototype__：每次请求(每次使用)创建新的实例；request，在request当前中有效；session；global session；

<br/>
## 3-2 Bean生命周期
Bean初始化：一种实现org.springframework.beans.factory.InitializingBean接口，并覆盖afterPropertiesSet方法；另一种：__配置`init-method=""`__，在对应的类里面实现指定的初始化方法。
Bean销毁：一种实现org.springframeword.beans.factory.DisposableBean接口，覆盖destroy方法；实现配置__`destroy-method=""`__，在对应的类里面实现指定的销毁方法。
全局默认初始化和销毁方法，配置：`default-init-method="" default-destroy-method=""` 「_这个方法好象是需要在每一个类里面都需要实现_」。如果Bean里面没有指定的全局初始化和销毁方法也可以。
如果实现了多个初始化和销毁方法，那么__实现接口的要先于自己配置的__，但是不会执行全局默认的初始化和销毁方法。
注：配置的使用方式更常见。

<br/>
## 3-3 Aware接口
Spring提供了一些以Aware结尾的接口，实现了Aware接口的Bean在被初始化后，可以获取相关的资源。并可以对相关的资源进行操作，但是要慎重，因为可能获取的是IOC容器的核心资源。没有了解太多，需要的时候自己去网上找。


<br/>
## 3-4 自动装配
Bean的自动装配(Autowiring)方式(在全局属性里进行配置default-autowire="")：no不做任何操作(_应该就是没有注解的方式_)；__byname__根据属性名(id)自动装配，查找IOC容器所有内容根据名字查找与属性完全一致的bean，进行自动装配。__bytype__查找类型(class)完全一样的bean，如果存在多个匹配的bean则会抛出异常；如果没有找到符合的则什么也不做。Constructor与bytype类似，不同之处在于它应用于构造器参数，如果容器中没用找到与参数类型一致bean则抛出异常。

## 3-5 Resources
Resources:针对资源文件的接口。包括：UrlResource，ClassPathResource，FileSystemResource，ServeltContextResource，InputStreamResource，ByteArrayResource。
ResourceLoader加载资源文件，参数类型(前缀)：classpath，file，http，(none)「_依赖于classpath_」。

<br/>
## 4-1 Bean的定义和作用域的注解实现
Classpath扫描与组件管理。__@Component__是一个通用的注解，可用于注解任意的bean。__@Repository__通常用于注解DAO类，即持久类；__@Service__通常用于注解Service类，即服务层；__@Controller__通常用于注解Controller类，即控制层(MVC)；元注解，可以自己定义注解，这个目前没有接触，需要时上网查资料。
Spring可以自动检测所有的类并注册Bean到ApplicationContext中。注解可注解到类名上或者是方法名上或是成员变量上。
基于在XML的Spring配置如下标签`<context:annotation-config />`「需要包含上下文命名空间」，此标签仅会查找在同一个ApplicationContext中的Bean注解。这个功能是在Bean注册完成之后，扫面已经注册类的基于方法或者变量的注解。一般使用后面的就不使用这个配置。
为了能够自动检测这些类并注册相应的Bean，需要包含如下内容__`<context:component-scan base-package="org.example"/>`__，设置需要扫描的包名。此配置包含了前面的配置，所以使用了这个就不使用前面的配置。
使用过滤器进行自定义的扫描，在上面的配置中加上条件配置`<context：include-filter />`和`<context:exclude-filter />`就可以实现自定义的扫描。具体的使用方法自行查资料。
默认情况下，类被自动发现并注册Bean的条件是：使用__@Component，@Repository，@Service，@Controller__。
定义Bean：扫描过程中组件被自动检测，Bean的名字由BeanNameGenerator生成，规则是类名的第一个字母小写作为Bean的id使用「我们可以自定义bean命名策略实现BeanNameGenerator接口，需要包含一个无参的构造器」。同样我们可以利用上面4个注解的name属性可以显式的指定Bean的名字。如：__`@Service("your_id")`__。
Bean作用域注解：@Scope「指定方式：@Scope("prototype")」，同样可以自定义实现ScopeMetadataResolver接口，提供一个无参构造器。
代理方式：scoped-proxy。没详细了解。

<br/>
## 4-2 Autowired注解说明-1
@Required注解适用于bean属性的set方法，仅仅表示受影响的属性必须在配置时被填充，说明是必须要的，不常用。
__@Autowired__可以用于变量、构造器、set方法，常用的注解。可以通过`@Autowired(required=false)`用于在set方法中的Autowired，如果找不到合适的Bean可以避免Autowired抛出异常。__这个通常注解到成员变量上__。

<br/>
## 4-3 Autowired注解说明-2
可以使用Autowired注解众所周知的解析依赖性的接口，如：在一个类中通过注解`private ApplicationContext context`来获得应用上下文信息，在这个类里面就可以应用了。
还可以__注解相应的数组变量或者set方法__来提供ApplicationContext中所有特定类型的Bean。如注解到某个类中成员属性`private List<bean_type_name> name;` 则可以得到此时ApplicationContext中所以Bean_name类型以及它的子类的Bean。同时可以注解到Map上`private Map<string, bean_type_name> name;`其中key得到的是Bean的id，value是Bean的对象。可以使用@Order是数组的对象有序，在类上使用此注解。如`@Order(1)`，1代表的是它的顺序。

<br/>
## 4-4 Autowired注解说明-3
按类型装配有多个bean实例的情况，可以使用__@Qualifier__缩小范围(或者指定唯一`@Qualifier("id")`)，也可以用于指定单独的构造器参数或方法参数(`public void func(@Qualifiter("id")type_a a, type_b b)`，此时type_a有多个满足的Bean，此方法已被Autowired注解了)。可以用于注解集合。
如果通过名字进行注解，就不使用Autowired进行注解，则使用@Resource注解，通过名称来定义识别特定的目标(是一个与声明的类型无关的匹配过程)，_这个不太理解，使用方式不太懂_。Resource适用于成员变量，只有一个参数的set方法，所以目标是构造器或者是多参数的方法时，最好使用Qualitier。可以自己定义方式。

<br/>
## 4-5 基于Java的容器注解说明——@Bean
@Bean标识一个配置和初始化使用SpringIOC容器管理的新对象的方法，类似于XML配置文件中的`<Bean/>`。 用@Component注解类使用@Bean注解任何方法，在方法里面创建对象并返回进而让SpringIOC容器管理返回的对象，但是通常是@Configuration和@Bean一起搭配使用。同时可以自定义一些方法，如`@Bean(initMethod="init") @Bean(destoryMethod="destory")`，也可以自定义Bean的name：`@Bean(name="my_id")`。这些方法都是在Bean类里面定义和实现的。如果没有指定Bean的id，默认是方法名。

<br/>
## 4-6 基于Java的容器注解说明——@ImportResource和@Value
利用`<context:property-placeholder  location="classpath:"/>`__适用于加载数据库的资源文件__。
利用@ImportResource引入一些资源，并利用@Value注解取出值注入变量中。详细的可以看这个视频。这个一般使用XML配置，清晰一些。

<br/>
## 4-7 基于Java的容器注解说明——@Bean和@Scope
利用@Scope指定Bean的作用域，如：@Scope("prototype")。同时可以指定代理方式：`@Scope(proxyMode="")`，具体网上查找。

<br/>
## 4-8 基于Java的容器注解说明——基于泛型的自动装配
这是在Spring4里面新增的内容。
可以自定义CustomAutowireConfigurer，使用的情况不多，详细的可以看视频。

<br/>
## 4-9 Spring对JSR支持的说明
@Resouce通常用于成员变量或set方法上。通常是在Java EE5以上的通用模式。@Resource有name属性，Spring使用该值作为Bean的名称。如果不指定，则使用成员变量名或者set方法中得出。类似Autowired。
@PostConstruct和@PreDestroy初始化Bean和销毁Bean的注解方法。
@Inject等效与@Autowired，可以用于类、属性、方法、构造器。
有多个Bean匹配但是想使用特定名称的Bean注入就使用@Named，与@Component等效。

<br/>
## 5-1 AOP基本概念及特点
AOP：Aspect Oriented Programming。AOP实现方式2种：预编译方式(AspectJ)和运行期动态代理(SpringAOP、JbossAOP)。实现程序功能的统一维护。主要的功能：日志记录、性能统计、安全控制、事务处理、异常处理等等。
__AOP相关概念__：

* Aspect(切面)：关注点的模块化，这个关注点可能会横切多个对象。
* Jointpoint(连接点)：程序执行过程中的某个特定的点。
* Advice(处理逻辑,通知)：在切面某个特定的连接点执行的动作。advice是我们切面功能的实现，它通知程序新的额外的行为。
* Pointcut(切点)：匹配连接点的断言，就是找到需要的连接点方法。pointcut可以控制你把哪些advice应用于jointpoint上去。
* Introduction(引入)：在不改变类代码的前提下，向类添加新的方法和属性。
* Target(目标类)：被一个或者多个切面所通知的对象。指那些将使用advice的类。
* AOP Proxy(代理类)：使用了proxy的模式。AOP框架创造的对象，用来实现切面契约(aspect contract)。
* Weaving(插入)：是指应用aspects到一个target对象创建proxy对象的过程：complie time，classload time，runtime。把切面和对象关联起来，创建一个被通知的对象。

__Advice的类型__：

+ Before advice(前置通知)：在执行连接点之前执行通知。
+ After returning advice(返回后通知)：在连接点正常执行后执行通知。
+ After throwing advice(抛出异常后通知)：在方法抛出异常退出时执行通知，
+ After(finally) advice(后通知)：在连接点退出时执行通知(不论是正常退出或是异常推出)。
+ Around advice(环绕通知)：包围一个连接点的通知，在其之前和之后都可以执行通知的代码。

Spring框架中AOP的用途：提供了声明式的企业服务；允许用户定义自己的Aspect。
SpringAOP的实现：纯java的实现，不需要特殊的编译过程，不需要控制类加载器的层次，但是AspectJ提综合全面的AOP解决方案。
有接口和无接口Spring AOP实现。

<br/>
## 5-2 配置切面Aspect
Schema-based AOP。Spring所有的切面和通知器都必须放在一个`<aop:config>`内(可以配置包含多个此标签)，每一个`<aop:config>`可以包含pointcut，advisor和aspect元素(但是__必须按照顺序进行声明__)，这种配置使用了Spring的自动代理机制。
``` xml
<aop:config>
	<aop:aspect id="id" ref="orther_bean_name">
		...
	</aop:aspect>
</aop:config>
```

<br/>
## 5-3 配置切入点Pointcut
__execution()__里面配置切入点的设置，如执行public方法时，某个类里面的方法，某个包下的方法等，这个属性是Spring AOP和AspectJ都支持的。whithin()和this()只在Spring AOP中支持，还有许多其他的方式。需要时自行在网上查找相关资料。
``` xml
<aop:config>
	<aop:aspect id="id" ref="orther_bean_name">
		// expression语法可上网查。
		<aop:pointcut id="id" expression="execution()" />
	</aop:aspect>
</aop:config>
```

<br/>
## 5-4 Advice应用(上)
Before Advice的两种方式：
``` xml
<aop:aspect id="id" ref="orther_bean_id">
	// 引用其他的切入点
	<aop:before 
		pointcut-ref="orther_pointcut_id"
		method="some_funtion"  />//这个函数要在引用的Bean中实现
	
	// 这个是自己实现切入点
	<aop:before
		pointcut="execution()"
		method="some_function"/>
</aop:aspect>
```
在aspect里引用的其他的Bean，这个Bean就是专门处理aop中的事务的函数集合。在这个Bean里面，只有和aop功能相关的函数实现。
一个配置例子：
``` xml
<aop:config>
	<aop:aspect id="id" ref="orther_bean_name">
		<aop:pointcut id="pointcut_id" expression="execution()" />

		<aop:before pointcut-ref="pointcut_id" method="some_funtion" />

		// 这里面还有其他的东西可以设置，需要时自行查找
		<aop:after-returning pointcut-ref="pointcut_id" method="some_funtion" />

		// 这里面还有其他的东西可以设置，需要时自行查找
		<aop:after-throwing pointcut-ref="pointcut_id" method="some_funtion" />
		
		<aop:after pointcut-ref="pointcut_id" method="some_funtion" />

		// 下面一节课(5-5)中的代码，
		<aop:around pointcut-ref="pointcut_id" method="some_funtion" />
		
	</aop:aspect>
</aop:config>
```

<br/>
## 5-5 Advice应用(下)
配置代码写在上面了，__注意__：处理的around函数的__第一个参数必须是ProceedingJoinPoint类型__的。此类型有一个__proceed方法__，执行此方法就代表执行当前具体业务的方法，并会有返回值不论是否是void类型。__在这句前面添加的功能就是执行前的功能，在这句之后就是函数执行后的功能代码__。
``` java
public Object function(ProceedingJoinPoint pjp){
	
	// 在下面的一句之前添加执行之前的处理函数。
	Object obj = pjp.proceed(); // 这句就相当于执行了，obj就是返回值。
	// 在上面一句以后添加执行之后的处理函数。
	
	return obj;
}
```
Advice同时可以使用参数匹配来进行切入点的设置。具体的设置是在pointcut中的expression中设置。

<br/>
## 5-6 Introductions应用
>允许一个切面声明一个实现指定接口的通知对象，并提供一个接口的实现类来代表这些对象。

可以使用一个新类来代表匹配到的对象。这个新类就是声明的父类。
>由`<aop:declare-parents>`元素声明，该元素用于声明所匹配到的类型拥有一个新的parent。

这句话有点不好理解，看完视频的代码实例，大概的意思就是可以把通过AOP匹配到Bean，通过这种方式再添加一个父类，这个父类是在元素中声明的。

下面是相关的代码：
``` xml
// types-matching里面是匹配的表达式参考execution
// implement-interface是新parent的父类的声明
// default-impl 是父类的实现
<aop:declare-parents types-matching="execution(...)"
	implement-interface=""
	default-impl="" />
```

__schema-defined aspects(所有基于配置的AOP的aspect)只支持singleton model(单例模式)__。

<br/>
## 5-7 Advisors
_advisor就像一个小的自包含的方面，只有一个advice_。切面自身通过一个Bean表示，并且必须实现某个advice接口(advisor可以很好的利用AspectJ的切入点表达式)。
Spring通过文件配置中`<aop:advisor>`元素支持advisor的使用，大多数会和__transactional advise(事务) __配合使用。
``` xml
<aop:config>
	<aop:aspect id="id" ref="orther_bean_name">
		<aop:pointcut id="pointcut_id" expression="execution()" />

		<aop:advisor pointcut-ref="pointcut_id" advice-ref="advice_id"/>
	</aop:aspect>
</aop:config>

<tx:advice id="advice_id">
	...   // 一些配置
</tx:advice>
```
看完视频，我觉得视频的例子和这个并不相关 > < 。
__环绕通知应用在一个方法的调用次数的统计__。

<br/>
## 6-1 Spring AOP API的Pointcut、advice概念及应用
__Spring AOP API是基础__。这里只是了解一下，具体的可以参考Spring的官方文档。
这里就是介绍了自己实现了相应的接口内容。大概的了解了一下。
__这视频里面并没有代理相关的课程。代理方面根本听不懂。__

<br/>
## 6-2 ProxyFactoryBean及相关内容（上）
这节课讲的就是代理的知识，和AOP相关的内容。接触的AOP应用少，就稍微了解了一下。

<br/>
## 6-3 ProxyFactoryBean及相关内容（下）
这节课讲的就是代理的知识，和AOP相关的内容。接触的AOP应用少，就稍微了解了一下。

<br/>
## 7-1 AspectJ介绍及Pointcut注解应用
@AspectJ类似java注解的普通java类。配置可以用XML或者注解方式。
@Aspect注解，不能通过类路径自动发现，需要配合@Component一起使用，或者通过在XML中配置类的方式。这个注解表示为一个切面类。
@Pointcut注解一个切入点，此方法的返回值必须是void类型。

<br/>
## 7-2 Advice定义及实例
使用注解的方式，如：Before Advice使用@Before注解并写明pointcut条件就好。里面介绍了关于AOP方面注解的信息和使用。

<br/>
## 7-3 Advice扩展
Advice的一些扩展的应用。如给advice传递参数，泛型参数额传递。
切面实例化模型：通过__perthis__指定切面的有效期。

总结：看完教程详细的了解了IOC的知识，但是对于AOP方面了解的不多。