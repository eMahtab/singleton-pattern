# Singleton Pattern


# Implementation 1 : Eager Initialization
```java
public class EagerSingleton {
    private static volatile EagerSingleton instance = new EagerSingleton();
 
    // private constructor
    private EagerSingleton() {
    }
 
    public static EagerSingleton getInstance() {
        return instance;
    }
}
```

**One drawback :** The instance is created irrespective of it is required at runtime or not


