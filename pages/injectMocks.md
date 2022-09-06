# @InjectMocks / @Mock / @Spy


@InjectMocks 由 Mockito 提供，被测试类需要使用 @InjectMocks，只能对字段进行注入，需要配合 Mockito.openMocks 使用，不依赖 Spring，启动速度很快。



```java 
@InjectMocks
SubtitleBusinessService businessService;

@Spy
TranslateTaskService taskService;

@Mock
VideoService videoService;

@Test
public void addSubtitle() {
    // 激活注解
    openMocks(this);
    doNothing().when(taskService).check();
    when(videoService.getById(101073L)).thenReturn(new Video());
    businessService.addSubtitle(2150L, 11001101L, 101073L);
}
```
