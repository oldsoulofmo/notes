IoC (Inversion of Control) : The approach of outsourcing the construction and management of objects. 

Spring container works as an object factory linked to a configuration that creates wanted objects. 

## Qualifiers 

If there are many beans then `@autowired` alone is not enough, `@Qualifier` is useful here to specify which bean we want to inject. 

```java
@Autowired  
public DemoRestController(@Qualifier("footballCoach") Coach coach) {  
   myCoach = coach;  
}
```

In this example I had many beans : 

- `FootballCoach`.
- `CricketCoach`.

In the qualifier I must specify the bean's ID but starting with a lower case `footballCoach`.

## Primary 

Instead of specifying each bean by it's name (bean's ID) we can specify which bean should be the primary and then `autowired` will implement only the primary one. 

> Using multiple primary beans will cause an erro.

Mixing `@Primary` and `@Qualifier` will lead to the qualifier being prioritized. 

> Qualifier allows me to be more specific on which bean I want.

- Qualifier is more specific.
- Qualifier has higher priority.

## Lazy initialization 

By default when the application starts are beans are initialized. 
Spring will create an instance of each and make them available.

Instead of creating all beans upfront, we can specify lazy initialization. 

A bean will be initialized when : 

- It is needed for dependency injection.
- It is explicitly requested. 

> I must use the `@Lazy` annotation to a given class.

What Lazy initialization mean is telling spring to initialize (create) a bean only if needed for dependency injection, if not then it will not be created. 

To configure other beans for lazy initialization I must add the `@Lazy` to every class, but I can also use a global configuration if there are a lot of classes. I do that using a configuration in the application properties. 

```java
spring.main.lazy-initialization=true
```

This means all beans are lazy : not created until needed, including the   `DemoController`. 

Once I access the REST endpoint `/dailyworkout`, spring will determine dependencies for `DemoController`.

For dependency resolution, spring will create an instance of `cricketCoach` first then it will create an instance of `DemoController` and inject the `cricketCoach`.

==Disadvantages :== 

- In web related components, `@RestController` will not be created until requested.
- May not discover configuration issues until too late.
- Need to make sure I have enough memory for all beans once created.

> Lazy initialization is disabled by default. 

To sum it up, lazy initialization is all about injecting dependencies only when needed and spring actually creates the instance of the bean first then it creates an instance of the controller. 

## Bean scopes 

- The lifecycle of a bean.
- How long does a bean lives ? 
- How many instances are created ? 
- How is a bean shared ? 

>Default scope is singleton. 

>Spring container creates only one instance of the bean by default.


> [!NOTE] Singleton
> It is cached in memory, all dependency injections for the bean will reference the same bean. 

Singleton : Creates a single shared instance of the bean. _(Default scope)_
Prototype : Creates a new bean instance for each container request. 
Request : Scope to an HTTP web request. _(Only used for web apps)_
Session : Scope to an HTPP web session. _(Only used for web apps)_
Application : Scoped to a web app ServletContext. _(Only used for web apps)_
Websocket : Scoped to a web socket. _(Only used for web apps)_

![[Drawing 2025-02-25 20.22.41.excalidraw.svg]]

To create a prototype scoped bean : 

```java
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
```

![[Drawing 2025-02-25 20.40.09.excalidraw.svg]]

In this example I'm only using things by default which means that the scope by default here is singleton : both injections are pointing to the same bean which is the `CricketCoach`.

```java
@RestController  
public class DemoRestController {  
  
    private Coach myCoach;  
    private Coach TheOtherCoach;  
  
    public DemoRestController(  
            @Qualifier("cricketCoach") Coach coach,  
            @Qualifier("cricketCoach") Coach theOtherCoach  
    )  
        { 
         
       myCoach = coach;  
       TheOtherCoach = theOtherCoach;  
       
    }  
  
    @GetMapping("/dailyworkout")  
    public String getDailyWorkOut() {  
        return myCoach.getDailyWorkOut();  
    } 
     
    @GetMapping("/check")  
    public String getCheck() {  
        return "theOtherCoach == coach : " + (TheOtherCoach == myCoach);  
    }  
}
```

In here, `myCoach` and `TheOtherCoach` are both beans, in the end I did compare the beans and they both point to the same reference. 

Now I am using the prototype scope :

```java
@Component  
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)  
public class CricketCoach implements Coach {  
  
    public CricketCoach() {  
        System.out.println("The constructor : " + getClass().getSimpleName());  
    }  
  
    @Override  
    public String getDailyWorkOut() {  
        return "Practice chi haja for 10 minutes";  
    }  
}
```

The `getCheck` method will return false because each injection here will create a new instance object and each bean : `myCoach` and `TheOtherCoach` will point to one of these two different objects. 

## Bean lifecycle methods 

The bean lifecycle by order : 

- Container starts. 
- Bean instantiated. 
- Dependencies injected.
- Internal spring processing. _(5)_
- My custom init method.
- Bean ready for use. 
  
When container shutdown : 

- My custom destroy method.
- Stop. 

==Important notes about the bean lifecycle methods/hooks :== 

- I can add custom code during bean initialization :
  - Call custom business logic methods.
  - Set up handles to resources (db, sockets, files, etc).

The same thing applies during bean destruction.

`@PostConstruct` for the init method configuration. 
`@PreDestroy` for the destroy method configuration.

After the step 5, the custom init method will be executed and then I had the printed stuff happened ... 

After stoping the application, the `onDestroy` method was executed and I had the desired printed line.

```java
// init method  
@PostConstruct  
public void onStart() {  
    System.out.println("stuff happened at the init time " + getClass().getSimpleName());  
}  
  
// destroy method  
@PreDestroy  
public void onDestroy() {  
    System.out.println("stuff happened at destroy time " + getClass().getSimpleName());  
}
```


> [!NOTE] Prototype scope and the destroy lifecycle method
> For prototype scoped beans, spring does not call the destroy method. 
> Spring does not control the whole lifecycle of a scoped prototype bean, the client code must clean up prototype scoped objects and release expensive resources that the prototype bean is holding.

## Configure a bean with java

- Create a `@Configuration` class.
- Define the `@Bean` method to configure the bean.
- Inject the bean into the controller.

<mark style="background: #FFF3A3A6;">Why a spring bean annotation ? </mark>

The idea is to make an existing third-party library class available for the spring framework. 

I may not have the access to the source code of a third-party class but I would however want to use the third-party class as a spring bean.


> `@Bean` use case : Take an existing third-party class and expose it as a spring bean.

I can give a custom ID to my bean : 

```java
@Configuration  
public class SportConfig {  
    @Bean("aquatic")  
    public Coach swimCoach() {  
        return new SwimCoach();  
    }  
}
```





