> **导航：** 
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")
> 
> **代码：**https://wwmg.lanzouk.com/ictoK135ye2f

**目录**

[一、准备工作](#%E4%BA%8C%E3%80%81%E6%89%8B%E5%86%99Spring%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C%EF%BC%88Ioc%EF%BC%89)

[1.0 项目目录](#%E9%A1%B9%E7%9B%AE%E7%9B%AE%E5%BD%95)

[1.1 Spring包下的类](#Spring%E7%9B%B8%E5%85%B3%E7%B1%BB)

[1.1.1 容器类](#1.%E6%96%B0%E5%BB%BA%E5%AE%B9%E5%99%A8%E7%B1%BB)

[1.1.2 @ComponentScan注解](#3.%E6%96%B0%E5%BB%BA%40ComponentScan%E6%B3%A8%E8%A7%A3)

[1.1.3 @Component注解](#5.%20%E6%96%B0%E5%BB%BA%40Component%E6%B3%A8%E8%A7%A3)

[1.1.4 @Autowired注解](#%40Autowired%E6%B3%A8%E8%A7%A3)

[1.1.5 @Scope注解](#%40Scope%E6%B3%A8%E8%A7%A3)

[1.1.6 Bean的声明类：BeanDefinition](#Bean%E7%9A%84%E5%A3%B0%E6%98%8E%E7%B1%BB%EF%BC%9ABeanDefinition)

[1.1.7 Bean名回调接口：BeanNameAware](#Bean%E5%90%8D%E5%9B%9E%E8%B0%83%E6%8E%A5%E5%8F%A3%EF%BC%9ABeanNameAware)

[1.1.8 初始化接口：InitializingBean](#%E5%88%9D%E5%A7%8B%E5%8C%96%E6%8E%A5%E5%8F%A3%EF%BC%9AInitializingBean)

[1.1.9 Bean后置处理器接口：BeanPostProcessor](#Bean%E5%90%8E%E7%BD%AE%E5%A4%84%E7%90%86%E5%99%A8%E6%8E%A5%E5%8F%A3%EF%BC%9ABeanPostProcessor%C2%A0) 

[1.2 用户业务相关类](#1.2%20%E7%94%A8%E6%88%B7%E4%B8%9A%E5%8A%A1%E7%9B%B8%E5%85%B3%E7%B1%BB%C2%A0%C2%A0) 

[1.2.1 测试类创建容器](#1.2.1%20%E6%B5%8B%E8%AF%95%E7%B1%BB%E5%88%9B%E5%BB%BA%E5%AE%B9%E5%99%A8)

[1.2.2 配置类AppConfig](#4.%E6%96%B0%E5%BB%BA%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)

[1.2.3 UserService](#UserService)

[1.2.4 OrderService，用于依赖注入](#OrderService%EF%BC%8C%E7%94%A8%E4%BA%8E%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5%C2%A0) 

[1.2.5 Bean后置处理器接口实现类：MyBeanPostProcessor](#Bean%E5%90%8E%E7%BD%AE%E5%A4%84%E7%90%86%E5%99%A8%E6%8E%A5%E5%8F%A3%E5%AE%9E%E7%8E%B0%E7%B1%BB%EF%BC%9AMyBeanPostProcessor)

[二、完善容器类：VinceApplicationContext](#%E4%B8%89%E3%80%81%E5%AE%8C%E5%96%84SpringCodeApplicationContext%EF%BC%88Ioc%EF%BC%89)

[2.0 创建Bean流程](#2.0%20%E5%88%9B%E5%BB%BABean%E6%B5%81%E7%A8%8B)

[2.1 代码实现](#2.1%20%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0)

[2.1.1 成员变量](#2.1.1%20%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F%C2%A0) 

[2.1.2 构造方法，参数是配置类](#2.1.2%20%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%EF%BC%8C%E5%8F%82%E6%95%B0%E6%98%AF%E9%85%8D%E7%BD%AE%E7%B1%BB)

[2.1.3 createBean()方法](#2.1.3%C2%A0createBean%28%29%E6%96%B9%E6%B3%95%C2%A0) 

[2.1.4 getBean()方法](#3.1.4%C2%A0getBean%28%29%E6%96%B9%E6%B3%95)

[三、完整代码](#%E4%B8%89%E3%80%81%E6%89%80%E6%9C%89%E4%BB%A3%E7%A0%81)

--

## 一、准备工作

### 1.0 项目目录

![](https://i-blog.csdnimg.cn/blog_migrate/3ecb0196354ccb008b1bcf80146fb701.png)

### 1.1 Spring包下的类

com.vince.spring包下的类：

#### 1.1.1 容器类

>  对比一下创建Spring容器的方式，我们需要模拟的是AnnotationConfigApplicationContext类。
> 
> -   **ClassPathXmlApplicationContext：**是需要传入一个**xml配置文件**，告诉Spring需要按照指定的配置创建一个Spring容器ApplicationContext，创建完之后就可以通过getBean从容器中拿到相应的bean对象
> -   **AnnotationConfigApplicationContext ：**也是一个容器，只是传入的是以**Java配置类**的形式传入。可以在类上加上@ComponentScan定义Spring等下需要扫描的路径。还可以通过@Bean的方法（等于bean标签），通过这种注解的方式，给容器加入一个Bean
> 
> ```java
> public class Test {
> 	public static void main(String[] args) {
> 		ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("spring.xml");
> 		classPathXmlApplicationContext.getBean("user");
> 
> 		AnnotationConfigApplicationContext annotationConfigApplicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
> 		
> 		SpringCodeApplicationContext applicationContext = new SpringCodeApplicationContext(AppConfig.class);
> 	}
> }
> ```
> 
> 参考Spring框架可知，这个容器类需要有构造方法、传入参数、`getBean()`方法

package com.vince.spring; 

```java
//模拟AnnotationConfigApplicationContext
public class VinceApplicationContext{

    private Class configClass;
//构造方法，参数是配置类的字节码文件
	public SpringCodeApplicationContext(Class configClass) {
        //1.赋值配置类成员变量
    	this.configClass = configClass;

		// 2.解析配置类
        // 通过反射，判断配置类字节码有没有注解@ComponentScan
		// 如果有，就根据@ComponentScan传入的扫描路径，扫描那个包下的Bean

        // 3.实例化bean

    }
//容器里拥有getBean()方法，获取Bean
    public Object getBean(String beanName){
		return null;
	}
```

#### 1.1.2 @ComponentScan注解

package com.vince.spring; 

```java
/**
 * 用于扫描指定包路径的Bean
 */
@Retention(RetentionPolicy.RUNTIME)//注解生命周期，不仅被保存到class文件中，jvm加载class文件之后，仍然存在
//@Target用来表示注解作用范围，超过这个作用范围，编译的时候就会报错。
@Target(ElementType.TYPE)//注解范围是：接口、类、枚举、注解
public @interface ComponentScan {

    String value() default "";

}
```

#### 1.1.3 @Component注解

package com.vince.spring; 

```java
/**
 * 注解为Bean
 */
@Retention(RetentionPolicy.RUNTIME)//注解生命周期，不仅被保存到class文件中，jvm加载class文件之后，仍然存在
@Target(ElementType.TYPE)//注解范围是：接口、类、枚举、注解
public @interface Component {

    String value() default "";

}
```

#### 1.1.4 @Autowired注解

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface Autowired {

}
```

#### 1.1.5 @Scope注解

```java
@Retention(RetentionPolicy.RUNTIME)//注解生命周期，不仅被保存到class文件中，jvm加载class文件之后，仍然存在
@Target(ElementType.TYPE)//注解范围是：接口、类、枚举、注解
public @interface Scope {

    String value() default "";

}
```

#### 1.1.6 Bean的声明类：BeanDefinition

> BeanDefinition 定义 Bean 的配置元信息，包含：
> 
> -   Bean 的类名
> -   设置父 bean 名称、是否为 primary、
> -   Bean 行为配置信息，作用域、自动绑定模式、生命周期回调、延迟加载、初始方法、销毁方法等
> -   Bean 之间的依赖设置，dependencies
> -   构造参数、属性设置  

```java
//Bean的声明类，用来描述Bean；里面定义的Bean的类型（Class格式）和作用域
public class BeanDefinition {

    private Class type;
    private String scope;

    @Override
    public String toString() {
        return "BeanDefinition{" +
                "type=" + type +
                ", scope='" + scope + '\'' +
                '}';
    }

    public Class getType() {
        return type;
    }

    public void setType(Class type) {
        this.type = type;
    }

    public String getScope() {
        return scope;
    }

    public void setScope(String scope) {
        this.scope = scope;
    }
}
```

#### 1.1.7 Bean名回调接口：BeanNameAware

```java
//回调接口，主要setter方法给Bean的beanName变量赋值。Aware译为明白的，意识到的。
public interface BeanNameAware {

    public void setBeanName(String beanName);
}
```

#### 1.1.8 初始化接口：InitializingBean

```java
//初始化Bean的接口，有个方法，
public interface InitializingBean {

    //在属性填充后执行
    public void afterPropertiesSet();

}
```

#### 1.1.9 Bean后置处理器接口：BeanPostProcessor 

本接口的两个方法在初始化之前和之后执行，可以通过实现类使用JDK的Proxy 

```java
//Bean后置处理器接口
public interface BeanPostProcessor {

    //在Bean 的初始化方法（如 @PostConstruct 注解的方法）被调用之前被自动调用
    public Object postProcessBeforeInitialization(String beanName,Object bean);

    //在 Bean 的初始化方法被调用之后被自动调用
    public Object postProcessAfterInitialization(String beanName,Object bean);

}
```

### 1.2 用户业务相关类  

com.vince.service包下的类： 

#### 1.2.1 测试类创建容器

package com.vince.spring; 

```java
public class Test {
    public static void main(String[] args){
//模拟AnnotationConfigApplicationContext容器，构造参数传入配置类
        VinceApplicationContext applicationContext = new VinceApplicationContext(AppConfig.class);
        UserInterface userService = (UserInterface)applicationContext.getBean("userService");
        userService.test();
    }
}
```

#### 1.2.2 配置类AppConfig

package com.vince.spring; 

```java
// com/springCode/service/UserService.java
@ComponentScan("com.springCode.service")
public class AppConfig {
}
```

#### 1.2.3 UserService

package com.vince.service; 

```java
public interface UserInterface {

    public void test();

}
```

```java
@Component
//@Scope("prototype") //多例
public class UserService implements BeanNameAware , InitializingBean ,UserInterface{

    @Autowired
    private OrderService orderService;

    private String beanName;

    @Override
    public void test(){
        System.out.println(orderService);
    }

    @Override
    public void setBeanName(String beanName) {
        this.beanName = beanName;
    }

    @Override
    public void afterPropertiesSet() {
        System.out.println("初始化方法");
    }
}
```

#### 1.2.4 OrderService，用于依赖注入 

```java
@Component
//@Scope("prototype") //多例
public class OrderService {
    public void submitOrder(){
        System.out.println("下单。。。");
    }

}
```

#### 1.2.5 Bean后置处理器接口实现类：MyBeanPostProcessor

```java
//Bean后置处理器实现类，两个方法在初始化之前和之后执行，可以通过实现类使用JDK的Proxy.newProxyInstance()；基于反射实现aop。
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(String beanName, Object bean) {
        if ("userService".equals(beanName)) {
            System.out.println("BeanPostProcessor实现类的postProcessBeforeInitialization()方法");
        }
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(String beanName, Object bean) {
        if ("userService".equals(beanName)) {
            //代理对象，通过JDK的Proxy.newProxyInstance()；基于反射实现aop。
            // 第一个参数类加载器，第二个参数接口的class对象，第三个参数重写invoke()的InvocationHandler实现类
            Object proxyInstance = Proxy.newProxyInstance(MyBeanPostProcessor.class.getClassLoader(),
                    bean.getClass().getInterfaces(), new InvocationHandler() {
                @Override
                public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                    System.out.println("切面逻辑，BeanPostProcessor实现类的postProcessAfterInitialization()方法");
                    return method.invoke(bean,args);
                }
            });
            return proxyInstance;
        }
        return bean;
    }
}
```

## 二、完善容器类：VinceApplicationContext

### 2.0 创建Bean流程

注解容器类构造方法创建Bean：

-   **获取Bean扫描路径：**获取配置类的Class对象，基于反射获取@ComponentScan注解里设置的扫描路径；
-   **遍历扫描Bean：**遍历扫描路径里每个类的字节码文件，用类加载器加载成class对象，基于反射判断@Component等注解，有的话这个类就是Bean类。
    -   **BeanPostProcessor实例化后存列表：**如果Bean类是BeanPostProcessor接口的实现类，那么就将这个Bean类实例化并存进成员变量List<BeanPostProcessor>里；
    -   **创建并赋值BeanDefinition对象：**创建BeanDefinition对象并赋值，type变量赋值Bean类的class对象，scope变量赋值作用域（通过反射获取@Scope注解值）。BeanDefinition存储Bean的对象、作用域等元信息。
    -   **beanDefinitionMap添加键值对：**把Bean名和它对应的BeanDefinition对象，以键值对形式添加到容器类成员变量beanDefinitionMap里。beanDefinitionMap线程安全，是ConcurrentHashMap类型。
-   **遍历beanDefinitionMap创建Bean：**遍历beanDefinitionMap的键，调用**createBean()**方法创建Bean。**createBean()方法具体逻辑：**
    -   **实例化：**基于反射，根据Bean类的Class对象推断构造方法、创建实例，如果是单例就存入单例池。实例化这个方法在getBean()时候也会用到，所以抽取成私有方法，这个方法获取Bean先判断作用域，单例的话就优先根据Bean名从单例池取，单例池没有就调用createBean()方法，根据Bean名和对应的BeanDefinition创建Object类型的Bean对象。
    -   **属性填充：**基于反射，根据Bean类的Class对象获取它所有属性，将注解了@Autowired等的属性开启私有成员访问限制，通过getBean(名或类)方法给该属性填充它的Bean对象。**getBean()方法：**判断作用域，如果单例则调用createBean()再放入单例池再返回，如果原型则调用createBean()后直接返回。简化起见这里暂时只考虑一级缓存，二级三级缓存暂时不考虑。
    -   **处理Aware回调：**如果Bean实例实现了BeanNameAware接口（通过instanceof判断），调用Bean重写的setBeanName()方法，给Bean实例的beanName变量赋值。
    -   **执行所有BeanPostProcessor的初始化前方法：**遍历BeanPostProcessor列表，执行每个BeanPostProcessor对象里的postProcessBeforeInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
    -   **初始化：**如果Bean实例实现了InitializingBean接口（通过instanceof判断），调用Bean重写的afterPropertiesSet()方法，处理初始化逻辑。afterPropertiesSet译为“在属性填充之后”
    -   **执行所有BeanPostProcessor的初始化后方法：**遍历BeanPostProcessor列表，执行每个BeanPostProcessor对象里的postProcessAfterInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
    -   **放进单例池：**如果是单例还要把Object类型Bean的代理对象放进单例池singletonObjects。

### 2.1 代码实现

spring包下的VinceApplicationContext类  

#### 2.1.1 成员变量 

```java
    private Class configClass;//配置类的Class对象

    //Bean名和它对应的BeanDefinition键值对；
    private ConcurrentHashMap<String,BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<>();

    //单例池；map存各Bean名所对应的Bean实例
    private ConcurrentHashMap<String,Object> singletonObjects = new ConcurrentHashMap<>();
    //存放扫描包路径下的所有BeanPostProcessor类
    private ArrayList<BeanPostProcessor> beanPostProcessorList = new ArrayList<>();
```

#### 2.1.2 构造方法，参数是配置类

```java
//构造方法，参数是配置类的Class对象
    public VinceApplicationContext(Class configClass) {
        //1.赋值配置类成员变量
        this.configClass = configClass;
        // 2.通过反射，判断配置类Class对象有没有注解@ComponentScan；如果有，就解析ComponentScan对象
        // --->BeanDefinition -->beanDefinitionMap
        if (configClass.isAnnotationPresent(ComponentScan.class)) {
            //解析ComponentScan对象
            ComponentScan componentScanAnnotation = (ComponentScan) configClass.getAnnotation(ComponentScan.class);
//            获取ComponentScan对象的value，也就是用户传入的扫描路径。例如@ComponentScan("com.vince.service")，扫描这个包下的Bean
            String path = componentScanAnnotation.value();// com.vince.service
            // 将包名中的点号替换为斜杠
            path = path.replace(".","/");//com/vince/service
            // 获取容器类的类加载器
            ClassLoader classLoader = VinceApplicationContext.class.getClassLoader();
            // 类加载器获取扫描包的绝对路径
            URL resource = classLoader.getResource(path);//file:/D:/xxx/com/vince/service
            // 把URL绝对路径对象封装成File对象
            File file = new File(resource.getFile());
            // 如果File对象是目录，则遍历判断扫描目录下的文件是不是bean；
            if (file.isDirectory()) {
                File[] files = file.listFiles();
                //遍历“扫描路径”下所有文件中，找到Bean，创建对应BeanDefinition对象，并存到map里；
                // 判断Bean方式：基于反射，判断该字节码文件对应的类有没有@Component注解
                for (File f: files) {
                    String fileName = f.getAbsolutePath();
                    if (fileName.endsWith(".class")) {
                        //将文件名转为类名；D:\xxx\com\vince\service\AppConfig.class ----> AppConfig
                        //这里其实不应该写死成“com”，只是方便起见，其实应该用更复杂的逻辑截取全名为类名
                        String className = fileName.substring(fileName.indexOf("com"), fileName.indexOf(".class"));
                        className = className.replace("\\",".");
                        try {
                            //根据类的全限定名加载类
                            Class<?> clazz = classLoader.loadClass(className);
                            //如果该类有@Component注解
                            if (clazz.isAnnotationPresent(Component.class)) {
                                System.out.println("容器类构造方法里，扫描@ComponentScan('xx')，发现xx路径下这个类是Bean："+clazz.getName());
                                //a.如果@Component("类名")有设置类名，Bean名就是设置的这个类名
                                Component component = clazz.getAnnotation(Component.class);
                                String beanName = component.value();

                                //判断这个Bean类是不是BeanPostProcessor接口的实现类，如果是的话就通过反射创建实例，并放进处理器列表里。
                                //注意不能用instanceof，因为instanceof是实例与类的关系比较，isAssignableFrom是类和接口的关系比较
                                if (BeanPostProcessor.class.isAssignableFrom(clazz)) {
                                    BeanPostProcessor instance = (BeanPostProcessor) clazz.newInstance();
                                    beanPostProcessorList.add(instance);
                                    System.out.println("这个Bean是BeanPostProcessor接口的实现类，需要加入list里，以供所有Bean初始化之前和之后增强");
                                }

                                //b.如果@Component没有设置类名，就将首字母小写后的Bean类名设为Bean名
                                if ("".equals(beanName)) {
                                    beanName = Introspector.decapitalize(clazz.getSimpleName());//工具类将字符串校验后首字母小写
                                }

                                // 创建一个BeanDefinition对象，用来描述Bean，里面赋值这个Bean的类型和作用域
                                BeanDefinition beanDefinition = new BeanDefinition();
                                //反射获取@Scope注解指定的作用域，赋值给BeanDefinition对象的scope变量
                                if (clazz.isAnnotationPresent(Scope.class)) {
                                    Scope scopeAnnotation = clazz.getAnnotation(Scope.class);
                                    beanDefinition.setScope(scopeAnnotation.value());
                                }else{
                                    beanDefinition.setScope("singleton");
                                }
                                //把这个Bean的Class对象赋值给BeanDefinition对象的type变量
                                beanDefinition.setType(clazz);
                                //把所有Bean名和它对应的BeanDefinition对象映射关系，存到map里统一管理
                                beanDefinitionMap.put(beanName,beanDefinition);
                                System.out.println("Bean名："+beanName+"，BeanDefinition对象："+beanDefinition);
                            }
                        } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        }

        // 3.实例化bean，如果作用域是单例，则从单例池中取；取不到就创建新的Bean对象，并存入单例池
        for (String beanName:beanDefinitionMap.keySet()) {
            BeanDefinition beanDefinition = beanDefinitionMap.get(beanName);
            if ("singleton".equals(beanDefinition.getScope())) {
                //实例化Bean
                Object bean = createBean(beanName,beanDefinition);
                singletonObjects.put(beanName,bean);
            }
        }
    }
```

#### 2.1.3 createBean()方法 

```java
    //根据Bean名和BeanDefinition对象实例化Bean的方法；私有，只供本类内部调用
    //BeanDefinition对象的成员变量type就是Bean的类型（Class格式）
    private Object createBean(String beanName,BeanDefinition beanDefinition){
//        获取Bean的Class格式的类型
        Class clazz = beanDefinition.getType();
        try {
            //1.基于反射创建Bean的实例；
            Object instance = clazz.getConstructor().newInstance();
            //2.依赖注入
            //遍历Bean类Class对象的所有属性；
            for (Field f : clazz.getDeclaredFields()) {
                //找出有@Autowired注解的属性，给这些属性进行填充
                if (f.isAnnotationPresent(Autowired.class)) {
                    //破除 private 修饰符访问限制；这样就可以访问注入的这个依赖里面的私有成员
                    f.setAccessible(true);
                    //给该属性填充属性名对应的Bean对象。
                    // 该属性通过getBean能获得Bean，因为上面构造方法里已经扫描了所有的Bean，并创建了BeanDefinition对象加入到“声明map”里了。
                    //void set(Object obj, Object value)
                    //obj 表示要设置属性值的对象；value 表示要为该成员变量设置的新值。
                    f.set(instance,getBean(f.getName()));
                }
            }

            // 3.Aware回调。如果Bean实例实现了BeanNameAware接口，就调用重写的setter方法，给Bean实例的beanName变量赋值
            if (instance instanceof BeanNameAware) {
                ((BeanNameAware) instance).setBeanName(beanName);
            }

            // 遍历后置处理器列表，执行后置处理器的before方法，在Bean 的初始化方法（如 @PostConstruct 注解的方法）被调用之前被自动调用
            for (BeanPostProcessor beanPostProcessor : beanPostProcessorList) {
                instance = beanPostProcessor.postProcessBeforeInitialization(beanName,instance);
            }

            // 初始化
            if (instance instanceof InitializingBean) {
                ((InitializingBean) instance).afterPropertiesSet();
            }

            //Bean后置处理器接口的after方法，在 Bean 的初始化方法被调用之后被自动调用
            for (BeanPostProcessor beanPostProcessor : beanPostProcessorList) {
                instance = beanPostProcessor.postProcessAfterInitialization(beanName,instance);
            }
            return instance;
        } catch (InstantiationException e) {            //异常处理
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        }
        return null;
    }
```

#### 2.1.4 getBean()方法

```java
//容器类的getBean()方法，根据作用域获取Bean
    public Object getBean(String beanName){
        //从map里获取BeanDefinition对象
        BeanDefinition beanDefinition = beanDefinitionMap.get(beanName);
        if (beanDefinition == null) {
            //如果BeanDefinition对象为空，说明这个bean没有创建成功，抛异常；
            throw new NullPointerException();
        }else{
            //如果BeanDefinition对象不为空，则判断作用域后获取Bean
            String scope = beanDefinition.getScope();
            if ("singleton".equals(scope)) {
                //如果是单例则从单例池根据Bean名取Bean；
                Object bean= singletonObjects.get(beanName);
                if (bean == null) {
                    //如果单例池查到的是null，则新创建Bean，再给单例池赋值
                    bean = createBean(beanName, beanDefinition);
                    singletonObjects.put(beanName,bean);
                }
                //返回Bean
                return bean;
            }else{
                // 多例，每次直接创建新的
                return createBean(beanName, beanDefinition);
            }
        }
    }
```

## 三、完整代码

完整代码地址： https://wwmg.lanzouk.com/ictoK135ye2f