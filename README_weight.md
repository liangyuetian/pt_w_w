[布局类Widget](https://flutterchina.club/widgets/layout/)：线性布局Row和Column，流式布局Wrap和Flow，层叠布局Stack和Positioned

拥有单个子元素的布局widget：

    * Container 一个拥有绘制、定位、调整大小的 widget。给 container 设置alignment属性可以撑满宽度。相当于div
    * Padding 一个widget, 会给其子widget添加指定的填充。相当于加一个padding
    * Center 将其子widget居中显示在自身内部的widget。相当于margin: auto auto
    * Align 一个widget，它可以将其子widget对齐，并可以根据子widget的大小自动调整大小。
    * FittedBox 按自己的大小调整其子widget的大小和位置。
    * AspectRatio 一个widget，试图将子widget的大小指定为某个特定的长宽比，
    * ConstrainedBox 对其子项施加附加约束的widget。相当于max-width,max-height,min-width,min-height
    * UnconstrainedBox 与ConstrainedBox相反，是不添加任何约束条件到child上，让child按照其原始的尺寸渲染。
    * Baseline 根据子项的基线对它们的位置进行定位的widget。相当于verticel-align
    * FractionallySizedBox 一个widget，它把它的子项放在可用空间的一小部分。可以设置百分比。相当于：width: 40%
    * IntrinsicHeight 一个widget，它将它的子widget的高度调整其本身实际的高度
    * IntrinsicWidth 一个widget，它将它的子widget的宽度调整其本身实际的宽度
    * LimitedBox 一个当其自身不受约束时才限制其大小的盒子。可以限制最大宽高。相当于max-width,max-height
    * Offstage 一个布局widget，可以控制其子widget的显示和隐藏。相当于display:none,当offstage为true，当前控件不会被绘制在屏幕上，不会响应点击事件，也不会占用空间；另外，当Offstage不可见的时候，如果child有动画，应该手动停掉，Offstage并不会停掉动画。
    * OverflowBox 对其子项施加不同约束的widget，它可能允许子项溢出父级。相当于overflow:visible
    * SizedBox 一个特定大小的盒子。这个widget强制它的孩子有一个特定的宽度和高度。如果宽度或高度为NULL，则此widget将调整自身大小以匹配该维度中的孩子的大小。相当于可以设置宽高，也可以使用Container
    * SizedOverflowBox 一个特定大小的widget，但是会将它的原始约束传递给它的孩子，它可能会溢出。
    * Transform 在绘制子widget之前应用转换的widget。相当于css transform
    * CustomSingleChildLayout 一个自定义的拥有单个子widget的布局widget

拥有多个子元素的布局widget

    * Row 在水平方向上排列子widget的列表。相当于display: flex
    * Column 在垂直方向上排列子widget的列表。相当于display: flex; flex-direction: column
    * Stack 可以允许其子widget简单的堆叠在一起。相当于position: absolute
    * IndexedStack 作用是显示第index个child，继承自Stack
    * GridView GridView在移动端上非常的常见，就是一个滚动的多列列表。
    * Flow
    * Table 为其子widget使用表格布局算法的widget
    * Wrap 可以在水平或垂直方向多行显示其子widget。
    * ListBody 一个widget，它沿着一个给定的轴，顺序排列它的子元素。
    * ListView 可滚动的列表控件。ListView是最常用的滚动widget，它在滚动方向上一个接一个地显示它的孩子。在纵轴上，孩子们被要求填充ListView
    * ListView.builder ListView的标准构造函数会将所有item一次性创建，而ListView.builder会创建滚动到屏幕上显示的item。
    * CustomMultiChildLayout 使用一个委托来对多个孩子进行设置大小和定位的小部件
    * LayoutBuilder 构建一个可以依赖父窗口大小的widget树。函数版，return 一个widget
    
[Flutter widget 目录.](https://flutterchina.club/widgets)

功能性类Weight，类似于css功能:

    * Stack 绝对布局。相当于 position: absolute
    * Positioned Stack 内需要定位的子元素
    * SizedBox 可以设置宽高，相当于：width: 20, height: 50
    * FractionallySizedBox 可以设置宽高相对于父容器的百分比，相当于：width: 20%, height: 50%
    * Wrap 可以折行的盒子
    * SingleChildScrollView 可以让子元素滚动
    * Opacity 让盒子透明
    * PhysicalModel 实现圆角裁剪，相当于 overflow: hidden
    * ClipRRect 实现圆角裁剪，相当于 overflow: hidden
    * DecoratedBox 可以单独设置 decoration 属性


设置盒子百分比：<code>FractionallySizedBox</code>
设置flex布局：<code>Flex</code>
设置flex:1比例：<code>Expanded</code>
设置flex:1比例（只占用指定比例的空间）：<code>Spacer</code>
只有<code>Container</code>才可以设置宽高
margin使用：<code>margin: EdgeInsets.only(bottom: 20)</code>
padding使用：<code>padding: EdgeInsets.only(bottom: 20)</code>


常用的UI组件

    * Tab TabBar和TabBarView和TabController组合使用
    * List ListView 

常用的UI方法
    * Fluttertoast.showToast

大佬博客：

    * https://www.cnblogs.com/holy-loki/tag/Flutter/
    
Key 保证diff算法精确的更新Widget

Key 的种类
    
Localkey

    * ValueKey : ValueKey('String') 使用字符串
    * ObjectKey : ObjectKey(Object) 使用map
    * UniqueKey : UniqueKey() 通过该对象生成一个具有唯一性的 hash 码。
    * PageStorageKey 保持页面的滚动状态
    
    
GlobalKey 
    
GlobalKey 能够跨 Widget 访问状态。
