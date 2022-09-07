# byte-buddy

<div class="text-xl">
byte-buddy 和 ASM、javassist 一样，都能在运行时动态生产 class 文件
</div>
<div class="text-sm my-3">
以下演示通过这三款字节码工具对 BasicBean 进行 Aop 增强
</div>

```java
public class BasicBean {
    public String sayHello(String name) {
        return "hello " + name;
    }
}
```

<div class="text-sm mt-3">
目标:

<div class="text-xs mt-2">

1. 修改入参: 将 name 变为大写
2. 执行真实调用
3. 对返回值添加: "; 欢迎使用 xxx"

</div>
</div>


<div class="text-sm mt-3">
例子:
</div>

```java
// 对 new BasicBean() 进行 aop 增强
BasicBean aopBean = aop(new BasicBean());
// return "hello THB; 欢迎使用 Mockito"
aopBean.sayHello("thb");
```