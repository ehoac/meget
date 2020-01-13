# wxPython

### wx.Frame 常用样式
* wx.CAPTION 在框架上增加一个标题栏， 它显示该框架的标题属性
* wx.CLOSE_BOX 指示系统在框架的标题栏上显示一个关闭框，使用系统默认的位置和样式。
* wx.DEFAULT_FRAME_STYLE 默认样式
* wx.FRAME_SHAPED：用这个样式创建的框架可以使用SetShape()方法去创建一个 非矩形的窗口。 
* wx.FRAME_TOOL_WINDOW：通过给框架一个比正常更小的标题栏，使框架看起 来像一个工具框窗口。在Windows下，使用这个样式创建的框架不会出现在显示所 有打开窗口的任务栏上。 
* wx.MAXIMIZE_BOX：指示系统在框架的标题栏上显示一个最大化框，使用系统默认 的位置和样式。 
* wx.MINIMIZE_BOX：指示系统在框架的标题栏上显示一个最小化框，使用系统默认 的位置和样式。 
* wx.RESIZE_BORDER：给框架增加一个可以改变尺寸的边框。 wx.SIMPLE_BORDER：没有装饰的边框。不能工作在所有平台上。 
* wx.SYSTEM_MENU：增加系统菜单（带有关闭、移动、改变尺寸等功能）和关闭 框到这个窗口。在系统菜单中的改变尺寸和关闭功能的有效性依赖于wx.MAXIMIZE_BOX, wx.MINIMIZE_BOX和wx.CLOSE_BOX样式是否被应用。

### wx 事件术语
* 事件event 在你的应用程序期间发生的事情，它要求有一个响应
* 事件对象(event object)：在wxPython中，它具体代表一个事件，其中包括了事件的 数据等属性。它是类wx.Event或其子类的实例，子类如wx.CommandEvent和 wx.MouseEvent。 
* 事件类型(event type)：：wxPython分配给每个事件对象的一个整数ID。事件类型给出 了关于该事件本身更多的信息。例如，wx.MouseEvent的事件类型标识了该事件是 一个鼠标单击还是一个鼠标移动。
* 事件源(event source)：任何wxPython对象都能产生事件。例如按钮、菜单、列表框 和任何别的窗口部件。
* 事件驱动(event-driven)：一个程序结构，它的大部分时间花在等待或响应事件上。 
* 事件队列(event queue)：已发生的但未处理的事件的一个列表
* 事件处理器(event handler)：响应事件时所调用的函数或方法。也称作处理器函数或 处理器方法。
* 事件绑定器(event binder)：一个封装了特定窗口部件，特定事件类型和一个事件处 理器的wxPython对象。为了被调用，所有事件处理器必须用一个事件绑定器注册
* wx.EvtHandler：一个wxPython类，它允许它的实例在一个特定类型，一个事件源， 和一个事件处理器之间创建绑定。注意，这个类与先前定义的事件处理函数或方法不 是同一个东西。

###  重构的一些重要原则
* 不要重复：你应该避免有多个相同功能的段。当这个功能需要改变时，这维护起来会 很头痛
* 一次做一件事情：一个方法应该并且只做一件事情。各自的事件应该在各自的方法中。方法应该保持短小
* 嵌套的层数要少：尽量使嵌套代码不多于2或3层。对于一个单独的方法，深的嵌套 也是一个好的选择。
* 避免字面意义上的字符串和数字：字面意义上的字符串和数字应使其出现在代码中的次数最小化。一个好的方法是，把它们从你的代码的主要部分中分离出来，并存储于一个列表或字典中。

### 标准MVC体系的组成
* Model：包含业务逻辑,包含所有由系统处理的数据。它包括一个针对外部存储（如一个数据库）的接口。通常模型(model)只暴露一个公共的API给其它的组分。 
* View：包含显示代码。这个窗口部件实际用于放置用户在视图中的信息。在 wxPython中，处于wx.Window层级中的所有的东西都是视图(view)子系统的一部分。
* Controller：包含交互逻辑。该代码接受用户事件并确保它们被系统处理。在 wxPython中，这个子系统由wx.EvtHandler层级所代表。

### 设备上下文 （wx.DC的子类）
1. wx.BufferedDC：用于缓存一套绘画命令，直到命令完整并准备在屏幕上绘画。这防 止了显示中不必要的闪烁。
2. wx.BufferedPaintDC：和wx.BufferedDC一样，但是只能用在一个wx.PaintEvent的处 理中。仅临时创建该类的实例。
3. wx.ClientDC：用于在一个窗口对象上绘画。当你想在窗口部件的主区域上（不包括 边框或别的装饰）绘画时使用它。主区域有时也称为客户区。wx.ClientDC类也应临 时创建。该类仅适用于wx.PaintEvent的处理之外。 wx.MemoryDC：用于绘制图形到内存中的一个位图中，此时不被显示。然后你可以 选择该位图，并使用wx.DC.Blit()方法来把这个位图绘画到一个窗口中。
4. wx.MetaﬁleDC：在Windows操作系统上，wx.MetaﬁleDC使你能够去创建标准窗口图 元文件数据。
5. wx.PaintDC：等同于wx.ClientDC，除了它仅用于一个wx.PaintEvent的处理中。仅 临时创建该类的实例。
6. wx.PostScriptDC：用于写压缩的PostScript文件。 wx.PrinterDC：用于Windows操作系统上，写到打印机。 wx.ScreenDC：用于直接在屏幕上绘画，在任何被显示的窗口的顶部或外部。该类 只应该被临时创建。
7. wx.WindowDC：用于在一个窗口对象的整个区域上绘画，包括边框以及那些没有被 包括在客户区域中的装饰。非Windows系统可能不支持该类

###  wx.DC的常用方法 
1. Blit(xdest, ydest, width,height, source, xsrc,ysrc)：从源设备上下文复制块到调用该 方法的设备上下文。参数xdest, ydest是复制到目标上下文的起始点。接下来的两个 参数指定了要复制的区域的宽度和高度。source是源设备上下文，xsrc,ysrc是源设备 上下文中开始复制的起点。还有一些可选的参数来指定逻辑叠加功能和掩码。
2. Clear()：通过使用当前的背景刷来清除设备上下文。 DrawArc(x1, y1, x2, y2,xc, yc)：使用起点(x1, y1)和终点(x2, y2)画一个圆弧。 (xc, yc)是圆弧的中心。圆弧使用当前的画刷填充。这个函数按逆时针画。这也有一 个相关的方法DrawEllipticalArc()。     DrawBitmap(bitmap, x,y, transparent)：绘制一个wx.Bitmap对象，起点为(x, y)。如 果transparent为真，所复制的位图将是透明的。
3. DrawCircle(x, y, radius) DrawCircle(point, radius)：按给定的中心点和半径画圆。这也有一个相关的方法 DrawEllipse。 DrawIcon(icon, x, y)：绘制一个wx.Icon对象到上下文，起点是(x, y)。 DrawLine(x1, y1, x2, y2)：从点(x1, y1)到(x2, y2)画一条线。这有一个相关的方法 DrawLines()，该方法要wx.Point对象的一个Python列表为参数，并将其中的点连接 起来。
4. DrawPolygon(points)：按给定的wx.Point对象的一个Python列表绘制一个多边形。 与DrawLines()不同的是，它的终点和起点相连。多边形使用当前的画刷来填充。这 有一些可选的参数来设置x和y的偏移以及填充样式。 DrawRectangle(x, y,width, height)：绘制一个矩形，它的左上角是(x, y)，其宽和高 是width和height    
。
5. DrawText(text, x, y)：从点(x, y)开始绘制给定的字符串，使用当前的字体。相关函数 包括DrawRotatedText()和GetTextExtent()。文本项有前景色和背景色属性。 FloodFill(x, y, color,style)：从点(x, y)执行一个区域填充，使用当前画刷的颜色。参 数style是可选的。style的默认值是wx.FLOOD_SURFACE，它表示当填充碰到另一 颜色时停止。另一值wx.FLOOD_BORDER表示参数color是填充的边界，当填充碰到 该颜色的代表的边界时停止。
6. GetBackground() SetBackground(brush)：背景画刷是一个wx.Brush对象，当Clear()方法被调用时使 用。
7. GetBrush() SetBrush(brush)：画刷是一个wx.Brush对象并且用于填充任何绘制在设备上下文上 的形状。
8. GetFont() SetFont(font)：字体(font)是一个wx.Font对象，被用于所有的文本绘制操作。 GetPen() SetPen(pen)：画笔(pen)是一个wx.Pen对象，被用于所有绘制线条的操作。 GetPixel(x, y)：返回一个关于点(x, y)的像素的一个wx.Colour对象。 GetSize() 148 / 565
9. GetSizeTuple()：以一个wx.Size对象或一个Python元组的形式返回设备上下文的像 素尺寸。

### wx.StatusBar的方法 
1. GetFieldsCount() SetFieldsCount(count)：得到或设置状态栏中域的数量。 GetStatusText(ﬁeld=0)
2. SetStatusText(text, ﬁeld=0)：得到或设置指定域中的文本。0是默认值，代表最左端 的域。
3. PopStatusText(ﬁeld=0)：弹出堆栈中的文本到指定域中，以改变域中的文本为弹出 值。
4. PushStatusText(text, ﬁeld=0)：改变指定的域中的文本为给定的文本，并将改变前的 文本压入堆栈的顶部。
5. SetStatusWidths(widths)：指定各状态域的宽度。widths是一个整数的Python列表

### 最常用的wxPython的sizer 
1. wx.BoxSizer：在一条线上布局子窗口部件。wx.BoxSizer的布局方向可以是水平或坚 直的，并且可以在水平或坚直方向上包含子sizer以创建复杂的布局。在项目被添加 时传递给sizer的参数控制子窗口部件如何根据box的主体或垂直轴线作相应的尺寸调 整。
2. wx.FlexGridSizer：一个固定的二维网格，它与wx.GridSizer的区别是，行和列根据 所在行或列的最大元素分别被设置。
3. wx.GridSizer：一个固定的二维网格，其中的每个元素都有相同的尺寸。当创建一个 grid sizer时，你要么固定行的数量，要么固定列的数量。项目被从左到右的添加， 直到一行被填满，然后从下一行开始。
4. wx.GridBagSizer：一个固定的二维网格，基于wx.FlexGridSizer。允许项目被放置在 网格上的特定点，也允许项目跨越多和网格区域。
5. wx.StaticBoxSizer：等同于wx.BoxSizer，只是在box周围多了一个附加的边框（有 一个可选的标签）。


