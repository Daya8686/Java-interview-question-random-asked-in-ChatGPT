# Bean Creation Process Deep Dive?

# Bean Creation Deep Dive

How bean creation works internally with a deep dive and different ways of doing the PostConstruct and PreDestroy, i.e., executing a method that is executed when constructor initialization completes and executing a method before bean destruction. 

## When does a bean get destroyed?
**Answer:** When the IOC container gets closed (destroyed).

## Three ways to manage PostConstruct and PreDestroy
**First, add the `javax` dependency in `pom.xml`.**

1. We can use `@PostConstruct` for the initialization of values after the constructor and `@PreDestroy` at the time when the IOC container gets destroyed as there are different ways the container can be destroyed. These annotations are Java-specific, meaning they are defined by Java in the `javax` package.

2. Using `InitializingBean`, a functional interface provided by Spring for executing a method after constructor initialization completes, we need to override a method from the `InitializingBean` interface, i.e., `afterPropertiesSet()`. For performing the destruction process before bean destruction, we need to use the `DisposableBean` interface, which has only one abstract method in it. Despite not being annotated with `@FunctionalInterface`, the method name is `destroy()`, which acts like `@PreDestroy` but is provided by Spring, not Java, so it is tightly coupled with the framework, and we should avoid using this.

3. With the Configuration class with methods annotated with `@Bean`, the `@Bean` has a new method by which we can execute code after the constructor and before the destruction of the bean. We need to write a method in the class for which we are saying this bean is managed by Spring. The class bean is created in the Configuration class, and we need to write like this at the time of bean creation: `@Bean(initMethod ="MethodName that is going to execute after the constructor")`. This works like `@PostConstruct`, and for destroying, we need to write `@Bean(destroyMethod="MethodName that is going to execute before destroy")`, which acts like `@PreDestroy`.

## How does the bean get destroyed?
**Answer:** When the IOC container gets closed or destroyed.

## How does the IOC container get destroyed?
If we are creating a standalone application, we need to handle it. When creating a web project, this is managed by Spring.

## How to destroy or close the container manually?
We have three different methods:

1. Use the `close()` method of the `AnnotationConfigApplicationContext` class: `context.close()`. 
   - **Note:** Not recommended because when an exception occurs, it will not execute.

2. Use the `registerShutdownHook()` method.
   - **Recommended:** It will execute when the JVM shuts down; even if an exception occurs, when the JVM shuts down, this will also shut down.

3. Using `try-with-resources` as its interface inherits `AutoCloseable`.

#### Main class
```java
public class App 
{
	
    public static void main( String[] args )
    {
    	AnnotationConfigApplicationContext context= new AnnotationConfigApplicationContext(AppConfig.class);
       Teacher teacher = context.getBean(Teacher.class);
       teacher.teachingSubjects();
       
       context.registerShutdownHook(); //To destory Container
    }

```

#### AppConfig class
```java
@Configuration
@ComponentScan
public class AppConfig {
	
	//METHOD 3
	@Bean(initMethod = "initilzationMethod", destroyMethod = "destroyMethod")
	public Teacher teacher() {
		return new Teacher();
	}

}
```

#### Teacher Class(Logic class)
```java

@Component
public class Teacher implements InitializingBean, DisposableBean  //METHOD 2
{
	
	private List<String> subjects;
	
	public Teacher() {
		System.out.println("Constructor executing...");
	}
	
	@PostConstruct //This call after constructor class happends //METHOD 1
	public void init() {
		System.out.println("Initialization is done with @postConstruct");
		subjects=new ArrayList<>();
		subjects.add("Maths");
		subjects.add("science");
	}

	public void teachingSubjects() {
		System.out.println("----Method call like API call ---- Start");
		for(String sub: subjects) {
			
			System.out.println("teacher teaches: "+sub);
			
		}
		System.out.println("----Method call like API call ---- End");
	}
	
	public void initilzationMethod() { //METHOD 3
		System.out.println("Initialization is done with @Bean(InitMethod=) ");
		subjects=new ArrayList<>();
		subjects.add("Maths");
		subjects.add("science");
	}

@Override //METHOD 2
public void afterPropertiesSet() throws Exception {
	System.out.println("Initialization is done with Spring provide interface InitializingBean");
	subjects=new ArrayList<>();
	subjects.add("Maths");
	subjects.add("science");
	
}
	@PreDestroy
	public void destroyMeth() { //Method 1
		System.out.println("Cleaning resource!!! with @preDestory");
	}
	
	@Override
	public void destroy() throws Exception { // method 2 
		
		System.out.println("Cleaning resource!!! with DisposableBean interface");
	}
	
	public void destroyMethod() { // method 3
		System.out.println("Cleaning resource!!! with method 3 with @Bean");
	}

	

}

```
### Priority of execution when all are executed
```ruby
1st @preConstruct 
2nd Spring InitializingBean interface method
3rd @Bean methods @Bean(initMethod="")
------------------------------------------
Output:--
Constructor executing...
Initialization is done with @postConstruct
Initialization is done with Spring provide interface InitializingBean
Initialization is done with @Bean(InitMethod=) 
----Method call like API call ---- Start
teacher teaches: Maths
teacher teaches: science
----Method call like API call ---- End
Cleaning resource!!!

```
