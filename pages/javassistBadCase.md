# javassist

<div>
javassist 通过 继承 + getMethod 实际拿到的时父类的方法，对其修改可能会影响到父类
</div>

```java
ClassPool pool = ClassPool.getDefault();
// 设置类名
CtClass cc = pool.makeClass("io.github.tanghuibo.mockitostudy.aop.BasicBean$proxy");
// 设置父类
cc.setSuperclass(pool.getCtClass("io.github.tanghuibo.mockitostudy.aop.BasicBean"));
// 通过 getMethod 实际拿到的是父类的 CtMethod
CtMethod sayHello = cc.getMethod("sayHello", "(Ljava/lang/String;)Ljava/lang/String;");
// 对父类的 CtMethod 修改会影响到父类
sayHello.insertBefore("$1 = $1.toUpperCase();");
sayHello.insertAfter("$_ = $_ + \"; 欢迎使用 javassist\";");
pool.getCtClass("io.github.tanghuibo.mockitostudy.aop.BasicBean").toClass();
BasicBean realBean = new BasicBean();
assertThat(realBean.sayHello("thb"), equalTo("hello THB; 欢迎使用 javassist"));
```