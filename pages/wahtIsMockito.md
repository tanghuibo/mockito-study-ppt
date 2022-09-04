---
clicks: 3
---

# Mockito 是啥?

<div v-if="$slidev.nav.clicks === 0" grid="~ cols-7 gap-1 mt-36">
  <div class="col-span-3 rounded-tl-lg">
  <img style="position: absolute; left: 250px; top: 160px;" src="/image/mockito-image.png" class="rounded-tl-lg" />
  </div>
</div>


<div v-if="$slidev.nav.clicks > 0" class="bg-green-200 rounded-lg shadow">
<div grid="~ cols-7 gap-1 mt-36">
  <div class="col-span-3 bg-green-100 rounded-tl-lg">
  <img v-motion
  :initial="{ x: 200, y: 80 }"
  :enter="{ x: 0, y: 0, transition: {duration: 600} }" src="/image/mockito-image.png" class="rounded-tl-lg" />

  </div>
  <div class="col-span-4 self-center p-1">

  <div class="font-bold text-center text-gray-800">
      Mockito 是一种 Java Mock 框架，主要用来做 Mock 测试
  </div>  
  <div class="card-right text-gray-700 text-basic">

  它可以**模拟任何对象、模拟方法的返回值、模拟抛出异常**等等
  
  同时也会**记录调用这些模拟方法的参数、调用顺序**，从而可以校验出这个 Mock 对象**是否有被正确的顺序调用，以及按照期望的参数被调用**
  </div>
  </div>
</div>

<div v-if="$slidev.nav.clicks > 1" class="text-baisc text-gray-600 bg-green-50 p-6 pb-1 rounded-b-lg">
Mockito 可以在单元测试中模拟一个 Service 返回的数据，而不会真正去调用该 Service，通过模拟一个假的 Service 对象，来快速的测试当前想要测试的类。

目前在 Java 中主流的 Mock 测试工具有 Mockito、JMock、EasyMock等等，而 SpringBoot 目前默认的测试框架是 Mockito 框架。
</div>
</div>

<div v-click="3" class="bg-gradient-to-br from-green-100 to-green-400 mt-6 p-6 inline-block font-bold rounded-lg text-gray-600 float-right shadow-lg">
一起来一杯 Mockito?
</div>

<style>
.card-right p:last-child {
  margin-bottom: 0px !important;
  padding-bottom: 0px !important;
}
</style>