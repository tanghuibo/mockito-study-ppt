---
clicks: 3
---

# @MockBean / @SpyBean

<div v-if="$slidev.nav.clicks === 0" style="padding-top: 1px;">

```java 
@MockBean
UserHelper userHelper;

@SpyBean
ITranslateProjectVideoSubtitleService subtitleService;

@Captor
ArgumentCaptor<TranslateProjectVideoSubtitle> argumentCaptor;

@Test
public void addProjectVideoSubtitle() {
    // mock 用户身份
    when(userHelper.getUsername()).thenReturn("thb-test");
    // 拦截 db 保存
    doNothing().when(subtitleService).save(any());
    businessService.addProjectVideoSubtitle(2150L, 1100001101L, 1010007993L);
    // 校验 subtitleService.save 是否保存
    verify(subtitleService).save(argumentCaptor.capture());
    // 获取保存时的入参
    TranslateProjectVideoSubtitle subtitle = argumentCaptor.getValue();
    // 校验参数是否正确
    assertThat(subtitle.getTranslateProjectId(), equalTo(2150));
    assertThat(subtitle.getVideoId(), equalTo(1100001101L));
}
```

</div>

<div v-if="$slidev.nav.clicks > 0" grid="~ cols-2 gap-1">
<div class="col-span-1">


```java {all|all|1-5|7-8,18-23|19-20|23-24}
@MockBean
UserHelper userHelper;

@SpyBean
ITranslateProjectVideoSubtitleService subtitleService;

@Captor
ArgumentCaptor<TranslateProjectVideoSubtitle> argumentCaptor;

@Test
public void addProjectVideoSubtitle() {
    // mock 用户身份
    when(userHelper.getUsername()).thenReturn("thb-test");
    // 拦截 db 保存
    doNothing().when(subtitleService).save(any());
    businessService.addProjectVideoSubtitle(2150L, 1100001101L, 1010007993L);
    // 校验 subtitleService.save 是否保存
    verify(subtitleService).save(argumentCaptor.capture());
    // 获取保存时的入参
    TranslateProjectVideoSubtitle subtitle = argumentCaptor.getValue();
    // 校验参数是否正确
    assertThat(subtitle.getTranslateProjectId(), equalTo(2150));
    assertThat(subtitle.getVideoId(), equalTo(1100001101L));
}
```

</div>
<div v-click="1" class="col-span-1 shadow px-3 my-1 bg-yellow-50 text-gray-800 pt-8">
<div v-click="1">

在真实项目中有很多外部依赖和条件在单元测试中很难满足，spring 官方通过集成 Mockito，提供 @MockBean/@Spy 等注解帮助我们对数据进行 mock

</div>

<div v-click="2" class="pt-6">

可以像使用 mock/spy 一样使用 @MockBean/@Spy，@MockBean/@Spy 由 spring-boot-test 提供，已和 spring 依赖注入打通

</div>

<div v-click="3" class="pt-6">

可以通过 ArgumentCaptor 对参数进行拦截，校验参数是否正确

</div>

</div>
</div>