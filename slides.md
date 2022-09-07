---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
selectable: true
# show line numbers in code blocks
lineNumbers: true
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

# Mockito 学习分享

<div class="mt-6 text-gray-400">
分享者: 唐汇波
</div>

---
src: ./pages/wahtIsMockito.md
---


---
src: ./pages/basicUse.md
---

---
layout: center
class: text-center
---

# 代码演示

通过一些简单的用例带大家快速入门 Mockito

---
src: ./pages/mockBasicUse.md
---

---
src: ./pages/spyBasicUse.md
---

---
layout: center
class: text-center
---

# mockito 支持 mock 静态方法 和 final 修饰的方法

需要导入 `mockito-inline` 进行支持

---
src: ./pages/mockStatic.md
---

---
layout: center
class: text-center
---

# mockito 不支持 mock 被 private 修饰的方法

需要 mock 私有方法可以使用替代品 powerMock


---
layout: center
class: text-center
---

# 在 SpringBoot 中使用

真实项目中有很多外部依赖和条件在单元测试中很难满足，spring 官方通过集成 Mockito，提供 @MockBean/@Spy 等注解帮助我们对数据进行 mock

---
src: ./pages/springMock.md
---

---
layout: center
class: text-center
---

# 本地无法启动项目？启动很慢？外部依赖很少？

<div class="mt-6 text-gray-500 text-xl" v-click="1">
试试 @InjectMocks
</div>


---
src: ./pages/injectMocks.md
---


---
src: ./pages/deep.md
---

---
src: ./pages/objenesis.md
---

---
src: ./pages/asmUtil.md
---


---
src: ./pages/cgLib.md
---

---
src: ./pages/javassist.md
---

---
src: ./pages/javassistBadCase.md
---

---
src: ./pages/bytebuddy.md
---