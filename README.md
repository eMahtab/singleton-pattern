# Singleton Pattern


## Implementation 1 : Eager Initialization
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

## Implementation 2 : Lazy Initialization : Double checked locking
```java
public class LazySingleton {
    private static volatile LazySingleton instance = null;
 
    // private constructor
    private LazySingleton() {
    }
 
    public static LazySingleton getInstance() {
        if (instance == null) {
            synchronized (LazySingleton.class) {
                // Double check
                if (instance == null) {
                    instance = new LazySingleton();
                }
            }
        }
        return instance;
    }
}
```

## Implementation 3 : Lazy Initialization : Nested Inner class (Bill Pugh Approach)
```java
public class BillPughSingleton {
    private BillPughSingleton() {
    }
 
    private static class LazyHolder {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }
 
    public static BillPughSingleton getInstance() {
        return LazyHolder.INSTANCE;
    }
}
```
#### Bill Pugh approach ensures we create only one singleton and its thread safe without using volatile and synchronized.

Because the first time getInstance() is called, the JVM will hold the holder class. If another thread calls getInstance() concurrently, the JVM won't load the holder class a second time: it will wait for the first thread to have completed the class loading, and at the end of the loading and initialization of the holder class, both thread will see the holder class properly initialized and thus containing the unique singleton instance.



# References :
https://howtodoinjava.com/design-patterns/creational/singleton-design-pattern-in-java
