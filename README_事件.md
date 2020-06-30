[大佬博客](https://www.cnblogs.com/lxlx1798/p/11097012.html)

Flutter中的手势系统分为二层：

* 第一层是触摸原事件（指针）
    * PointerDownEvent：用户与屏幕接触产生了联系
    * PointerMoveEvent：手指已从屏幕上的一个位置移动到另一个位置
    * PointMoveEvent：指针停止接触屏幕
    * PointerUpEvent：用户已停止接触屏幕
    * PointerCanceEvent：此指针的输入不再指向此应用程序

* 第二层是手势事件（轻击，拖动，缩放）
    * 自带交互的控件监听
        * RaisedButton、
        * IconButton、
        * OutlineButton、
        * Checkbox、
        * SnackBar、
        * Switch等　　　　
        * 用GestureDelector进行手势检测
        * 用Dismissible实现滑动删除　　　　


GestureDetector支持的手势

```dart
GestureDetector({
    Key key,
    this.child,
    this.onTapDown,//按下，每次和屏幕交互都会调用
    this.onTapUp,//抬起，停止触摸时调用
    this.onTap,//点击，短暂触摸屏幕时调用
    this.onTapCancel,//取消 触发了onTapDown，但没有完成onTap
    this.onDoubleTap,//双击，短时间内触摸屏幕两次
    this.onLongPress,//长按，触摸时间超过500ms触发
    this.onLongPressUp,//长按松开
    this.onVerticalDragDown,//触摸点开始和屏幕交互，同时竖直拖动按下
    this.onVerticalDragStart,//触摸点开始在竖直方向拖动开始
    this.onVerticalDragUpdate,//触摸点每次位置改变时，竖直拖动更新
    this.onVerticalDragEnd,//竖直拖动结束
    this.onVerticalDragCancel,//竖直拖动取消
    this.onHorizontalDragDown,//触摸点开始跟屏幕交互，并水平拖动
    this.onHorizontalDragStart,//水平拖动开始，触摸点开始在水平方向移动
    this.onHorizontalDragUpdate,//水平拖动更新，触摸点更新
    this.onHorizontalDragEnd,//水平拖动结束触发
    this.onHorizontalDragCancel,//水平拖动取消 onHorizontalDragDown没有成功触发
    //onPan可以取代onVerticalDrag或者onHorizontalDrag，三者不能并存
    this.onPanDown,//触摸点开始跟屏幕交互时触发
    this.onPanStart,//触摸点开始移动时触发
    this.onPanUpdate,//屏幕上的触摸点位置每次改变时，都会触发这个回调
    this.onPanEnd,//pan操作完成时触发
    this.onPanCancel,//pan操作取消
    //onScale可以取代onVerticalDrag或者onHorizontalDrag，三者不能并存，不能与onPan并存
    this.onScaleStart,//触摸点开始跟屏幕交互时触发，同时会建立一个焦点为1.0
    this.onScaleUpdate,//跟屏幕交互时触发，同时会标示一个新的焦点
    this.onScaleEnd,//触摸点不再跟屏幕交互，标示这个scale手势完成
    this.behavior,
    this.excludeFromSemantics = false
});
```

Dismissible 滑动删除 组件
```dart

/**
 *  滑动删除
 *
 * const Dismissible({
    @required Key key,//
    @required this.child,//
    this.background,//滑动时组件下一层显示的内容，没有设置secondaryBackground时，从右往左或者从左往右滑动都显示该内容，设置了secondaryBackground后，从左往右滑动显示该内容，从右往左滑动显示secondaryBackground的内容
    //secondaryBackground不能单独设置，只能在已经设置了background后才能设置，从右往左滑动时显示
    this.secondaryBackground,//
    this.onResize,//组件大小改变时回调
    this.onDismissed,//组件消失后回调
    this.direction = DismissDirection.horizontal,//
    this.resizeDuration = const Duration(milliseconds: 300),//组件大小改变的时长
    this.dismissThresholds = const <DismissDirection, double>{},//
    this.movementDuration = const Duration(milliseconds: 200),//组件消失的时长
    this.crossAxisEndOffset = 0.0,//
    })
 */

```

原始指针事件

在移动端，各个平台或UI系统的原始指针事件模型基本都是一致，即：一次完整的事件分为三个阶段：手指按下、手指移动、和手指抬起，而更高级别的手势（如点击、双击、拖动等）都是基于这些原始事件的。

响应流程
　当指针按下时，Flutter会对应用程序执行命中测试(Hit Test)，以确定指针与屏幕接触的位置存在哪些widget， 指针按下事件（以及该指针的后续事件）然后被分发到由命中测试发现的最内部的widget，然后从那里开始，事件会在widget树中向上冒泡，这些事件会从最内部的widget被分发到widget根的路径上的所有Widget，这和Web开发中浏览器的事件冒泡机制相似， 但是Flutter中没有机制取消或停止冒泡过程，而浏览器的冒泡是可以停止的。
   注意，只有通过命中测试的Widget才能触发事件。
事件监听
     Flutter中可以使用Listener widget来监听原始触摸事件，它也是一个功能性widget。

```dart
Listener({
  Key key,
  this.onPointerDown, //手指按下回调
  this.onPointerMove, //手指移动回调
  this.onPointerUp,//手指抬起回调
  this.onPointerCancel,//触摸事件取消回调
  this.behavior = HitTestBehavior.deferToChild, //在命中测试期间如何表现
  Widget child
});
```

## behavior属性　　　　　　　　
我们重点来介绍一下，它决定子Widget如何响应命中测试，它的值类型为HitTestBehavior，这是一个枚举类，有三个枚举值：

* deferToChild：子widget会一个接一个的进行命中测试，如果子Widget中有测试通过的，则当前Widget通过，这就意味着，如果指针事件作用于子Widget上时，其父(祖先)Widget也肯定可以收到该事件。

* opaque：在命中测试时，将当前Widget当成不透明处理(即使本身是透明的)，最终的效果相当于当前Widget的整个区域都是点击区域。

* translucent 在背景是透明的区域可以点击到元素下方的盒子，即 点透

忽略PointerEvent

假如我们不想让某个子树响应PointerEvent的话，
我们可以使用IgnorePointer和AbsorbPointer，
这两个Widget都能阻止子树接收指针事件，
不同之处在于AbsorbPointer本身会参与命中测试，
而IgnorePointer本身不会参与，
这就意味着AbsorbPointer本身是可以接收指针事件的(但其子树不行)，而IgnorePointer不可以。