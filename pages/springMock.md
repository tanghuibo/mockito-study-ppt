---
clicks: 2
---

# @MockBean / @SpyBean

<div v-if="$slidev.nav.clicks === 0" style="padding-top: 1px;">

```java 
@MockBean
UserHelper userHelper;

@SpyBean
ISubtitleService subtitleService;

@Captor
ArgumentCaptor<Subtitle> argumentCaptor;

@Test
public void addSubtitle() {
  // mock 用户身份
  when(userHelper.getUsername()).thenReturn("auto-test");
  // 拦截 db 保存
  doNothing().when(subtitleService).save(any());
  businessService.addSubtitle(2150L, 11001101L, 101073L);
  // 校验 subtitleService.save 是否保存
  verify(subtitleService).save(argumentCaptor.capture());
  // 获取保存时的入参
  Subtitle subtitle = argumentCaptor.getValue();
  // 校验参数是否正确
  assertThat(subtitle.getProjectId(), equalTo(2150L));
  assertThat(subtitle.getVideoId(), equalTo(11001101L));
}
```

</div>

<div v-if="$slidev.nav.clicks > 0" grid="~ cols-2 gap-1">
<div class="col-span-1">


```java {all|1-5|7-8,18-23|19-20|23-24}
@MockBean
UserHelper userHelper;

@SpyBean
ISubtitleService subtitleService;

@Captor
ArgumentCaptor<Subtitle> argumentCaptor;

@Test
public void addSubtitle() {
  // mock 用户身份
  when(userHelper.getUsername()).thenReturn("auto-test");
  // 拦截 db 保存
  doNothing().when(subtitleService).save(any());
  businessService.addSubtitle(2150L, 11001101L, 101073L);
  // 校验 subtitleService.save 是否保存
  verify(subtitleService).save(argumentCaptor.capture());
  // 获取保存时的入参
  Subtitle subtitle = argumentCaptor.getValue();
  // 校验参数是否正确
  assertThat(subtitle.getProjectId(), equalTo(2150L));
  assertThat(subtitle.getVideoId(), equalTo(11001101L));
}
```

</div>
<div v-click="1" class="col-span-1 shadow px-3 my-1 bg-yellow-50 text-gray-800 pt-24">

<div v-click="1">

可以像使用 mock/spy 一样使用 @MockBean/@Spy，@MockBean/@Spy 由 spring-boot-test 提供，已和 spring 依赖注入打通

</div>

<div v-click="2" class="pt-12">

可以通过 ArgumentCaptor 对参数进行拦截，校验参数是否正确

</div>

</div>
</div>