# byte-buddy

<div class="mb-2">
接口相对比较干净，写出来的代码比较好维护，比 cgLib 更灵活，但性能调优困难(相对于ASM)
</div>

```java
class MethodInterceptor {
    @RuntimeType
    public static Object around(@Argument(0) String name, @This Object proxyObj, @SuperMethod Method method) throws Exception {
        return method.invoke(((AopBeanInterface) proxyObj).getTarget(), name.toUpperCase()) + "; 欢迎使用 bytebuddy";
    }
}

interface AopBeanInterface { 
    Object getTarget(); 
}

BasicBean aop(BasicBean realBean) {
    Class<? extends BasicBean> clazz = new ByteBuddy()
            .subclass(BasicBean.class)
            .implement(AopBeanInterface.class)
            .method(ElementMatchers.named("getTarget")).intercept(FixedValue.value(realBean))
            .method(ElementMatchers.named("sayHello")).intercept(MethodDelegation.to(MethodInterceptor.class))
            .make().load(BasicTest.class.getClassLoader()).getLoaded();
    return ObjenesisHelper.newInstance(clazz);
}
BasicBean proxyBean = aop(new BasicBean());
assertThat(proxyBean.sayHello("thb"), equalTo("hello THB; 欢迎使用 bytebuddy"));
```