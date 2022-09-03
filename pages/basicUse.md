# 基本用法

<div class="rounded-lg shadow">
<div class="flex bg-green-200 rounded-t-lg">
  <div class="w-64 self-center text-center px-3">
    <div class="font-bold text-xl">
      mock() / @Mock
    </div>
  </div>
  <div class="flex-1 bg-green-100 h-full p-3 rounded-tr-lg">

  创建 mock 对象

  <div class="text-sm text-gray-600">
  
  - 可通过  Answer/MockSettings 指定 mock 对象的行为
  - 通过 when()/doXxx() 来指定模拟应该如何表现
  - 可通过自定义 Answer 对 mock 行为进行灵活扩展
  
  </div>
  
  </div>
</div>
<div class="flex bg-blue-200">
  <div class="w-64 self-center text-center px-3">
    <div class="font-bold text-xl">
      spy() / @Spy
    </div>
  </div>
  <div class="flex-1 bg-blue-100 h-full p-3">

  部分 mock，调用真实方法，可以使用 mock 对象的任何方法

  </div>
</div>

<div class="flex bg-red-200">
  <div class="w-64 self-center text-center px-3">
    <div class="font-bold text-xl">
      @InjectMocks
    </div>
  </div>
  <div class="flex-1 bg-red-100 h-full p-3">

  自动注入带有带@Spy 或 @Mock的字段
  
  </div>
</div>

<div class="flex bg-yellow-200 rounded-b-lg">
  <div class="w-64 self-center text-center px-3 rounded-bl-lg">
    <div class="font-bold text-xl">
      verify
    </div>
  </div>
  <div class="flex-1 bg-yellow-100 h-full p-3 rounded-br-lg">

  检查方法是否按某种参数顺序被调用

  <div class="text-sm text-gray-600">
  
  - 可以使用灵活的参数匹配，例如通过 any() 的任何表达式
  - 或者使用 @Captor 来捕获调用的参数
  
  </div>
  
  </div>
</div>
</div>
