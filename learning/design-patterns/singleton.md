# Singleton


```java
public class StaticSingleton {
  public int someValue;
  private StaticSingleton() {
    someValue = 10;
  }
  public static StaticSingleton instance = new StaticSingleton();
}

```