# cgLib

spring aop 的依赖，背后使用 ASM 生成字节码，利用 fastClass 规避放射调用的开销

```java
BasicBean aop(BasicBean realBean) {
    Enhancer enhancer = new Enhancer();
    enhancer.setSuperclass(BasicBean.class);
    MethodInterceptor callback = (proxyObj, method, objects, methodProxy) -> {
        // 修改入参
        objects[0] = objects[0].toString().toUpperCase();
        // 真实调用，此处使用 fastClass 技术，不走反射
        Object result = methodProxy.invoke(realBean, objects);
        // 修改返回值
        return result + "; 欢迎使用 cgLib";
    };
    enhancer.setCallbackTypes(new Class[] { MethodInterceptor.class });
    // 多个 CallbackType 时设置，返回值代表 method 由第几个callbackType 处理
    // enhancer.setCallbackFilter(method -> 0);
    BasicBean proxyBean = ObjenesisHelper.newInstance(enhancer.createClass());
    // 生成代理对象后可动态设置 callback
    ((Factory) proxyBean).setCallbacks(new Callback[] { callback });
    return proxyBean;
}
BasicBean proxyBean = aop(new BasicBean());
assertThat(proxyBean.sayHello("thb"), equalTo("hello THB; 欢迎使用 cgLib"));
```