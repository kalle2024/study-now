# SpringBoot核心源码
## 1.1 流程入口
```java
SpringApplication.run(DemoApplication.class, args);
```
```java
return new SpringApplication(primarySources).run(args);
```
> 主要方法
```text
(1) WebApplicationType.deduceFromClasspath()                    : 判断当前Spring工程的类型: REACTIVE | NONE | SERVLET
(2) private List<ApplicationContextInitializer<?>> initializers : 初始化器
(3) private List<ApplicationListener<?>>           listeners    : 监听器
```
```java
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
    this.resourceLoader = resourceLoader;
    Assert.notNull(primarySources, "PrimarySources must not be null");
    // 将primarySources数组包装成List，然后再包装成LinkedHashSet
    this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
    // 判断当前Spring工程的类型：REACTIVE, NONE, SERVLET
    // 最终this.webApplicationType = SERVLET
    this.webApplicationType = WebApplicationType.deduceFromClasspath();
    this.bootstrapRegistryInitializers = new ArrayList<>(
            getSpringFactoriesInstances(BootstrapRegistryInitializer.class));
    setInitializers((Collection) getSpringFactoriesInstances(ApplicationContextInitializer.class));
    setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
    this.mainApplicationClass = deduceMainApplicationClass();
}
```

## 1.2 初始化器 ApplicationContextInitializer
> 在Spring容器执行`refresh()`方法之前，通过context进行一些操作<br>
> `run()` -> `prepareContext()` -> `applyInitializers()`

(1) 类声明
```java
@FunctionalInterface
public interface ApplicationContextInitializer<C extends ConfigurableApplicationContext> {

	/**
	 * Initialize the given application context.
	 * @param applicationContext the application to configure
	 */
	void initialize(C applicationContext);
}
```