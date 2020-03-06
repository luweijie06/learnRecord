

processon类图

> https://www.processon.com/view/link/5e61df20e4b03ecc7523f02e

![mark](http://q66uz2l8w.bkt.clouddn.com/picture/20200306/OxucxEAcnAu1.png?imageslim)

### 	SpringBean的生命周期执行过程描述：

1. 根据配置情况调用Bean构造方法或工厂方法实例化Bean
2. 利用依赖注入完成Bean中所有属性值的配置注入
3. 如果Bean实现了`BeanNameAware`接口， 则Spring调用Bean的`setBeanName`()方法传入当前Bean的id值
4. 如果Bean实现了`BeanFactoryAware`接口，则spring调用`setBeanName`()方法传入当前的工厂实例引用
5. 如果Bean实现了`ApplicationContextAware`接口，则Spring调用`setApplicationContext`()方法传入当前ApplicationContext实例的引用
6. 如果`BeanPostProcessor` 和Bean 关联， 则Spring 将调用该接口的预初始化方法`postProcessBeforeInItoalzation`()对Bean进行加工操作，spring的aop就是利用它实现的
7. 如果Bean实现了`lnitializingBean`接口，则Spring将调用`afterPropertiesSet`()方法
8. 如果在配置文件中通过init-method属性指定了初始化方法，则调用该初始化方法
9. 如果 `BeanPostProcessor` 和 Bean 关联，则 Spring 将调用该接口的初始化方法 postProcessAfterInitialization()。此时，Bean 已经可以被应用系统使用了
10. 如果在 `<bean>` 中指定了该 Bean 的作用范围为 `scope="singleton"`，则将该 Bean 放入 Spring IoC 的缓存池中，将触发 Spring 对该 Bean 的生命周期管理；如果在 `<bean>` 中指定了该 Bean 的作用范围为 `scope="prototype"`，则将该 Bean 交给调用者，调用者管理该 Bean 的生命周期，**Spring 不再管理该 Bean**。
11. 如果 Bean 实现了 DisposableBean 接口，则 Spring 会调用 destory() 方法将 Spring 中的 Bean 销毁；如果在配置文件中通过 destory-method 属性指定了 Bean 的销毁方法，则 Spring 将调用该方法对 Bean 进行销毁。

**二、Bean接口方法的分类**

​     1、Bean自身的方法：包括了Bean本身调用的方法和通过配置文件中<bean>的init-method和destroy-method指定的方法

​      2、Bean级生命周期接口方法：这个包括了`BeanNameAware`、`BeanFactoryAware`、`InitializingBean`和`DiposableBean`这些接口的方法

​		3、容器级生命周期接口方法：这个包括了`InstantiationAwareBeanPostProcessor` 和 `BeanPostProcessor` 这两个接口实现，一般称它们的实现类为“后处理器”。

​		4.工厂后处理器接口方法：这个包括了`AspectJWeavingEnabler`, `ConfigurationClassPostProcessor`, `CustomAutowireConfigurer`等等非常有用的工厂后处理器　　接口的方法。工厂后处理器也是容器级的。在应用上下文装配配置文件之后立即调用。



## 