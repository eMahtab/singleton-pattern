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

## Implementation 2 :
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

