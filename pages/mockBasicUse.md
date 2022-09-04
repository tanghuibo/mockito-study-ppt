---
clicks: 3
---

# Mock

<div v-if="$slidev.nav.clicks === 0" style="padding-top: 1px;">

```java
// mock 一个 random
Random random = mock(Random.class);
// 设定 nextInt 第一次返回 10, 第二次返回 11
when(random.nextInt()).thenReturn(10, 11);
// 验证第一次返回 10
assertThat(random.nextInt(), equalTo(10));
// 验证第二次返回 11
assertThat(random.nextInt(), equalTo(11));
// 未指定行为的方法不会调用真实方法，直接返回默认值
assertThat(random.nextLong(), equalTo(0L));
// 验证 nextInt 被执行了两次
verify(random, times(2)).nextInt();
```

</div>

<div v-if="$slidev.nav.clicks > 0" grid="~ cols-2 gap-1">
<div class="col-span-1">


```java {all|9-10|1-2}
// mock 一个 random
Random random = mock(Random.class);
// 设定 nextInt 第一次返回 10, 第二次返回 11
when(random.nextInt()).thenReturn(10, 11);
// 验证第一次返回 10
assertThat(random.nextInt(), equalTo(10));
// 验证第二次返回 11
assertThat(random.nextInt(), equalTo(11));
// 未指定行为的方法不会调用真实方法，直接返回默认值
assertThat(random.nextLong(), equalTo(0L));
// 验证 nextInt 被执行了两次
verify(random, times(2)).nextInt();
```

</div>
<div v-click="1" class="col-span-1 shadow px-3 my-1 bg-yellow-50 text-gray-800 pt-6">
<div v-click="1">

mock 对象默认不会执行真实的方法。

</div>

<div v-click="2" class="py-2">

如果不指定 mock 对象的行为，默认会根据方法返回值类型返回默认值或 null。

</div>

<div v-click="3">

可通过 mock 方法的第二个值指定 mock 默认行为。

</div>
</div>
</div>

<div class="text-sm text-center my-table" v-click="3">

|||
|---|---|
|RETURNS_DEFAULTS|默认行为，返回 0, false ... 或 null|
|RETURNS_SMART_NULLS|返回非 null 的值，但不能继续调用其方法|
|RETURNS_MOCKS|返回一个 mock 的值|
|RETURNS_DEEP_STUBS|返回一个 mock 的值，返回值的返回值还是 mock 的值|
|RETURNS_SELF|返回自身，用于 builder 模式|
|CALLS_REAL_METHODS|调用真实方法|

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
