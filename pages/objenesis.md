# objenesis

<div class="mb-2">
一个很小的 java 库，主要功能是通过一些 unsafe 的方法(根据不同的 jvm 虚拟机有不同的实现)，在不调用构造方法的情况下直接生成对象，在 spring-aop 和 mock 中经常被使用。
</div>

```java
 public static <T> T newInstance(Class<T> clazz) {
    //...
 }
```