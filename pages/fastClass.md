# cgLib FastClass

<div style="transform-origin: top left; scale: 0.75">
<div class="flex gap-x-3">

<div>

```java
class BasicBeanProxy extends BasicBean {
    Method method = BasicBean.class.getMethod("sayHello", String.class);
    MethodProxy methodProxy =  MethodProxy.create(fastClass, proxyFastClass, "sayHello", "CGLIB$sayHello$0");
    MethodInterceptor methodInterceptor; // 用户写的拦截逻辑
    final String CGLIB$sayHello$0(String name) {  //sayHello 变基
        return super.sayHello(name);
    }
    @Override
    public final String sayHello(String arg0) {
        return methodInterceptor.intercept(this, method, new Object[]{ arg0 }, methodProxy);
    }
}
```

</div>

<div class="bg-yellow-50 shadow">

<div class="ml-6" style="width: 316px;">
<div class="pt-6">
动态生产 3 个 class: 
</div>

<div class="ml-6">

- BasicBeanProxy
- BasicBeanProxyFastClass
- BasicBeanFastClass

</div>

中间通过 MethodProxy 进行连接
</div>
</div>

</div>

<div class="flex gap-x-3">
<div>

```java
class BasicBeanFastClass extends FastClass {
    @Override
    public int getIndex(String methodName) {
        int hashCode = methodName.hashCode();
        if(hashCode == 0x1231232) {
            if(methodName.equals("sayHello")) { return 1; }
        }
        return 0;
    }

    @Override
    public Object invoke(int methodIndex, Object o, Object[] args) {
        switch (methodIndex) {
            case 1:
                return ((BasicBean) o).sayHello(((String) args[1]));
        }
        return null;
    }
} //  省略 class BasicBeanProxyFastClass extends FastClass
```

</div>

<div>

```java
 class MethodProxy {
    private FastClass fastClass, proxyFastClass;
    private Integer methodIndex, proxyMethodIndex;
    public static MethodProxy create(FastClass fastClass, FastClass proxyFastClass,
                                        String methodName, String proxyMethodName) {
        MethodProxy methodProxy = new MethodProxy();
        methodProxy.fastClass = fastClass;
        methodProxy.proxyFastClass = proxyFastClass;
        methodProxy.methodIndex = proxyFastClass.getIndex(methodName);
        methodProxy.proxyMethodIndex = proxyFastClass.getIndex(proxyMethodName);
        return methodProxy;
    }
    public Object invoke(Object obj, Object[] args) throws Throwable {
        return fastClass.invoke(methodIndex, obj, args);
    }
    public Object invokeSuper(Object obj, Object[] args) throws Throwable {
        return proxyFastClass.invoke(proxyMethodIndex, obj, args);
    }
}
```

</div>

</div>
</div>
