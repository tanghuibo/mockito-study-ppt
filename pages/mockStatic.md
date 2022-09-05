---
clicks: 4
---

# mock 静态方法

<div v-if="$slidev.nav.clicks === 0" style="padding-top: 1px;">

```java 
class MockStaticObj {
    public static Integer getDouble(Integer item) {
        return 2 * item;
    }
}
// mock 静态方法
MockedStatic<MockStaticObj> mockMockedStatic = mockStatic(MockStaticObj.class);
// 小于 0 时返回 -2 * 入参
mockMockedStatic.when(() -> MockStaticObj.getDouble(ArgumentMatchers.intThat(i -> i < 0)))
        .thenAnswer(invocationOnMock -> -2 * (Integer) invocationOnMock.getArgument(0));
// 大于 3 时返回值不能超过 10
mockMockedStatic.when(() -> MockStaticObj.getDouble(ArgumentMatchers.intThat(i -> i > 3)))
        .thenAnswer(invocationOnMock -> Math.min(10, (Integer) invocationOnMock.callRealMethod()));
// 2 执行真实调用
mockMockedStatic.when(() -> MockStaticObj.getDouble(2)).thenAnswer(Answers.CALLS_REAL_METHODS);

assertThat(MockStaticObj.getDouble(-3), equalTo(6));
assertThat(MockStaticObj.getDouble(2), equalTo(4));
// mock 静态方法默认使用 Answers.RETURNS_DEFAULTS
assertThat(MockStaticObj.getDouble(3), equalTo(0));
assertThat(MockStaticObj.getDouble(4), equalTo(8));
assertThat(MockStaticObj.getDouble(6), equalTo(10));
// 恢复原有的状态
mockMockedStatic.reset();
```

</div>

<div v-if="$slidev.nav.clicks > 0" grid="~ cols-2 gap-1">
<div class="col-span-1">


```java {all|all|all|19-20|23-24}
class MockStaticObj {
    public static Integer getDouble(Integer item) {
        return 2 * item;
    }
}
// mock 静态方法
MockedStatic<MockStaticObj> mockMockedStatic = mockStatic(MockStaticObj.class);
// 小于 0 时返回 -2 * 入参
mockMockedStatic.when(() -> MockStaticObj.getDouble(ArgumentMatchers.intThat(i -> i < 0)))
        .thenAnswer(invocationOnMock -> -2 * (Integer) invocationOnMock.getArgument(0));
// 大于 3 时返回值不能超过 10
mockMockedStatic.when(() -> MockStaticObj.getDouble(ArgumentMatchers.intThat(i -> i > 3)))
        .thenAnswer(invocationOnMock -> Math.min(10, (Integer) invocationOnMock.callRealMethod()));
// 2 执行真实调用
mockMockedStatic.when(() -> MockStaticObj.getDouble(2)).thenAnswer(Answers.CALLS_REAL_METHODS);

assertThat(MockStaticObj.getDouble(-3), equalTo(6));
assertThat(MockStaticObj.getDouble(2), equalTo(4));
// mock 静态方法默认使用 Answers.RETURNS_DEFAULTS
assertThat(MockStaticObj.getDouble(3), equalTo(0));
assertThat(MockStaticObj.getDouble(4), equalTo(8));
assertThat(MockStaticObj.getDouble(6), equalTo(10));
// 恢复原有的状态
mockMockedStatic.reset();
```

</div>
<div v-click="1" class="col-span-1 shadow px-3 my-1 bg-yellow-50 text-gray-800 pt-6">
<div v-click="1">

mockito 支持 mock 静态方法 和 final 修饰的方法，需要导入 `mockito-inline` 进行支持

</div>

<div v-click="2" class="pt-2">

mockito 不支持 mock 被 private 修饰的方法，需要 mock 私有方法可以使用替代品 powerMock

</div>

<div v-click="3" class="pt-2">

mock 静态方法默认使用 Answers.RETURNS_DEFAULTS，**对所有静态方法生效，对非静态方法不生效**

</div>

<div v-click="4" class="pt-2">

mock 结束后需要对 mock 进行 reset，否则**影响将会一直持续**

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
