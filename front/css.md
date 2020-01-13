# 常用样式

### 垂直居中
1.
```
selector: {
  display: inline-block;
  vertical-align: middle;
}
```
2.
```
parent: {
  display: flex;
}

children: {
  align-self: center;
}
```
3.
```
parent: {
  height: 300px;
}

children: {
  line-height: 300px;
}
```

### css 书写规范
#### 书写顺序
1. Positioning Model 布局方式、位置，相关属性包括：position, top, z-index, display, float等
2. Box Model 盒模型，相关属性包括：width, height, padding, margin, border, overflow等
3. Typographic 文本排版，相关属性包括：font, line-height, letter-spacing, color- text-align等
4. Visual 视觉外观，相关属性包括：color, background, list-style, transform, animation等

#### 书写规范
1. 使用CSS缩写属性 CSS有些属性是可以缩写的，比如padding,margin,font等等，这样精简代码同时又能提高用户的阅读体验。可缩写的属性中，如果属性值只有1个或2个，那应该分开写；如果大于2个，应该合并写在一起。这样就可以使其编译的时间最优化。
2. 去掉小数点前的“0”和0后面的单位，如：0px -> 0
3. 16进制颜色代码缩写

#### 命名规则
1. 分类式命名法
  * 布局（grid）（.g-）：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等！
  * 模块（module）（.m-）：通常是一个语义化的可以重复使用的较大的整体！比如导航、登录、注册等
  * 元件（unit）（.u-）：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块中！比如按钮、输 入框、loading等！
  * 功能（function）（.f-）：为方便一些常用样式的使用，我们将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等！不可滥用！
  * 状态（.z-）：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现（.u-ipt.z-dis{}，.m-list li.z-sel{}）
  * javascript(.j-)：.j-将被专用于JS获取节点，请勿使用.j-定义样式
2. 不要使用 " _ " 下划线来命名css
3. id采用驼峰式命名(不要乱用id)
4. scss中的变量、函数、混合、placeholder采用驼峰式命名
5. 相同语义的不同类命名方法：直接加数字或字母区分即可（如：.m-list、.m-list2、.m-list3等，都是列表模块，但是是完全不一样的模块）。其他举例：.f-fw0、.f-fw1、.s-fc0、.s-fc1、.m-logo2、.m-logo3、u-btn、u-btn2等等。
6. 命名方式(BEM)：类-体（例：g-head）、类-体-修饰符（例：u-btn-active）
7. 后代选择器：体-修饰符即可（例：.m-page .cut{}）注：后代选择器不要在页面布局中使用，因为污染的可能性较大；
8. 简写命名

#### 举例
```
 /* 这是某个模块 */
.m-nav{}/* 模块容器 */
.m-nav li,.m-nav a{}/* 先共性  优化组合 */
.m-nav li{}/* 后个性  语义化标签选择器 */
.m-nav a{}/* 后个性中的共性 按结构顺序 */
.m-nav a.a1{}/* 后个性中的个性 */
.m-nav a.a2{}/* 后个性中的个性 */
.m-nav .z-crt a{}/* 交互状态变化 */
.m-nav .z-crt a.a1{}
.m-nav .z-crt a.a2{}
.m-nav .btn{}/* 典型后代选择器 */
.m-nav .btn-1{}/* 典型后代选择器扩展 */
.m-nav .btn-dis{}/* 典型后代选择器扩展（状态） */
.m-nav .btn.z-dis{}/* 作用同上，请二选一（如果可以不兼容IE6时使用） */
.m-nav .m-sch{}/* 控制内部其他模块位置 */
.m-nav .u-sel{}/* 控制内部其他元件位置 */
.m-nav-1{}/* 模块扩展 */
.m-nav-1 li{}
.m-nav-dis{}/* 模块扩展（状态） */
.m-nav.z-dis{}/* 作用同上，请二选一（如果可以不兼容IE6时使用） */
```

1. 布局(.g-)
|语义|命名|简写|
|--|--|--|
|文档|doc|doc|
|头部|head|hd|
|主体|body|bd|
|尾部|foot|ft|
|主栏|main|mn|
|主栏子容器|mainc|mnc|
|侧栏|side|sd|
|侧栏子容器|sidec|sdc|
|盒容器|wrap/box|wrap/box|
2. 模块（.m-）、元件（.u-）
|语义|命名|简写|
|--|--|--|
|导航|nav|nav|
|子导航|subnav|snav|
|面包屑|crumb|crm|
|菜单|menu|menu|
|选项卡|tab|tab|
|标题区|head/title|hd/tt|
|内容区|body/content|bd/ct|
|列表|list|lst|
|表格|table|tb|
|表单|form|fm|
|热点|hot|hot|
|排行|top|top|
|登录|login|log|
|标志|logo|logo|
|广告|advertise|ad|
|搜索|search|sch|
|幻灯|slide|sld|
|提示|tips|tips|
|帮助|help|help|
|新闻|news|news|
|下载|download|dld|
|注册|regist|reg|
|投票|vote|vote|
|版权|vcopyright|cprt|
|结果|result|rst|
|标题|title|tt|
|按钮|button|btn|
|输入|input|ipt|
3. 功能（.f-）
|语义|命名|简写|
|--|--|--|
|清除浮动|clearboth|cb|
|左浮动|floatleft|fl|
|内联|inlineblock|ib|
|文本居中|textaligncenter|tac|
|垂直居中|verticalalignmiddle|vam|
|溢出隐藏|overflowhidden|oh|
|完全消失|displaynone|dn|
|字体大小|fontsize|fz|
|字体粗细|fontweight|fs|
4. 皮肤（.s-）
|语义|命名|简写|
|--|--|--|
|字体颜色|fontcolor|fc|
|背景颜色|backgroundcolor|bgc|
|边框颜色|bordercolor|bdc|
5. 状态(.z-)
|语义|命名|简写|
|--|--|--|
|选中|selected|sel|
|当前|curren|crt|
|显示|show|show|
|隐藏|hide|hide|
|打开|open|open|
|关闭|close|close
|出错|error|err|
|不可用|disabled|dis|