# javassist

<div class="mb-2">
javassist 中可以使用字符串生成代码，适合运维时，如 arthas
</div>

```java
BasicBean aop(BasicBean realBean) throws Exception {
    ClassPool pool = ClassPool.getDefault();
    // 设置类名
    CtClass cc = pool.makeClass("io.github.tanghuibo.mockitostudy.aop.BasicBean$proxy");
    // 设置父类
    cc.setSuperclass(pool.getCtClass("io.github.tanghuibo.mockitostudy.aop.BasicBean"));
    // 设置字段, 用于存放被代理类
    cc.addField(CtField.make("public io.github.tanghuibo.mockitostudy.aop.BasicBean targetBean$1;", cc));
    // 设置方法
    CtMethod sayHello =  CtMethod.make("public String sayHello(String name) {\n" +
        "    return targetBean$1.sayHello(name.toUpperCase()) + \"; 欢迎使用 javassist\";\n" +
        "}", cc);
    cc.addMethod(sayHello);
    BasicBean proxyBean = (BasicBean)ObjenesisHelper.newInstance(cc.toClass());
    // 注入代理类
    proxyBean.getClass().getField("targetBean$1").set(proxyBean, realBean);
    return proxyBean;
}
BasicBean proxyBean = aop(new BasicBean());
assertThat(proxyBean.sayHello("thb"), equalTo("hello THB; 欢迎使用 javassist"));
```