---
clicks: 5
---

# Spy

<div v-if="$slidev.nav.clicks === 0" style="padding-top: 1px;">

```java
class MockSpyObj {
    public Integer getDouble(Integer item) {
        return 2 * item;
    }
}
// spy 可以传入一个 class， 也可传入一个对象
MockSpyObj spyObj = spy(new MockSpyObj());
// 当 入参小于 5 时均返回 11
doReturn(11).when(spyObj).getDouble(intThat(i -> i < 5));
// 入参为 5 时返回 12
doReturn(12).when(spyObj).getDouble(5);
assertThat(spyObj.getDouble(2), equalTo(11));
assertThat(spyObj.getDouble(5), equalTo(12));
// 未被拦截的调用走真实调用
assertThat(spyObj.getDouble(7), equalTo(14));
// 是否按某种顺序进行调用
InOrder inOrder = inOrder(spyObj);
inOrder.verify(spyObj, times(1)).getDouble(2);
inOrder.verify(spyObj, times(1)).getDouble(5);
inOrder.verify(spyObj, times(1))
  .getDouble(intThat(i -> i == 7));
// 没有多余调用
inOrder.verifyNoMoreInteractions();
```

</div>

<div v-if="$slidev.nav.clicks > 0" grid="~ cols-2 gap-1">
<div class="col-span-1">


```java {all|all|8-11|8-9|16-23|8-9,20-21}
class MockSpyObj {
    public Integer getDouble(Integer item) {
        return 2 * item;
    }
}
// spy 可以传入一个 class， 也可传入一个对象
MockSpyObj spyObj = spy(new MockSpyObj());
// 当 入参小于 5 时均返回 11
doReturn(11).when(spyObj).getDouble(intThat(i -> i < 5));
// 入参为 5 时返回 12
doReturn(12).when(spyObj).getDouble(5);
assertThat(spyObj.getDouble(2), equalTo(11));
assertThat(spyObj.getDouble(5), equalTo(12));
// 未被拦截的调用走真实调用
assertThat(spyObj.getDouble(7), equalTo(14));
// 是否按某种顺序进行调用
InOrder inOrder = inOrder(spyObj);
inOrder.verify(spyObj, times(1)).getDouble(2);
inOrder.verify(spyObj, times(1)).getDouble(5);
inOrder.verify(spyObj, times(1))
  .getDouble(intThat(i -> i == 7));
// 没有多余调用
inOrder.verifyNoMoreInteractions();
```

</div>
<div v-click="1" class="col-span-1 shadow px-3 my-1 bg-yellow-50 text-gray-800 pt-2">
<div v-click="1">

spy 对象默认会执行真实的方法。

</div>

<div v-click="2" class="pt-1">

指定行为时支持根据条件指定，未指定的行为走真实调用

</div>

<div v-click="3" class="pt-1">

mock / spy 均支持 doXXX().when() 和 when().doXXX()，使用 doXXX.when() 可以**避免真实调用**

</div>

<div v-click="4" class="pt-1">

通过 inOrder 可以验证 mock / spy 对象是否按某种顺序执行

</div>

<div v-click="5" class="pt-1">

intThat 来自于 ArgumentMatchers.intThat, 产生 ArgumentMatcher 对象，ArgumentMatcher 不仅可以**对入参进行灵活的匹配**，也可在**校验流程中使用**

</div>
</div>
</div>


<style>
  
.my-table th {
    display: none;
}

.my-table td {
  padding-top: 6px;
  padding-bottom: 6px;
}

</style>
