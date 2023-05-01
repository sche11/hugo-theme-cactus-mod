> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [mp.weixin.qq.com](https://mp.weixin.qq.com/s?__biz=MzI4NDQ4NjU0MA==&mid=2247819262&idx=4&sn=ff57a3477e21ea629192b1cb22f26d3c&chksm=ebf4e11ddc83680b2d40c33be4898b833d2af26624bf6df7f7f17498246442e481671f872fd7&mpshare=1&scene=1&srcid=0430KavA9cnUgKY31UYxcBw1&sharer_sharetime=1682819695809&sharer_shareid=63953633c6a3464dbfffb64fecf004f0#rd)

**导读** 

Origin 是每一位科研工作者最常用的数据绘图软件之一，具备统计、峰值分析和曲线拟合等分析功能，可以绘制出二维和三维图形。

一、绘制线 (Line) 图

二、绘制误差棒图

三、绘制散点图

四、绘制垂线图

五、绘制气泡图

六、绘制彩色点图

七、绘制彩色气泡图

八、绘制点线图

九、绘制柱形图

十、绘制条形图

十一、绘制浮动柱形图

十二、绘制浮动条形图

十三、绘制饼图

十四、绘制 Y 轴错位堆垒曲线图

十五、绘制二维瀑布图

十六、绘制面积图

十七、绘制堆垒面积图

十八、绘制填充面积图

十九、绘制局部放大图

二十、绘制含数据标签图

**一、绘制线图**

**示例准备：**导入 Graphing 文件夹中的 AXES.OAT 文件数据。

① 选中 B 列。

② 单击菜单命令【Plot】→【Line】→【Line】或 2D Graphs 工具栏的【Line】。

**2D Graphs 工具栏：**

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVPcvTGPdSoBdwickYrksARv3rQPYzCvViatKTxib7cfYfcCfVmV2K8kibXQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**如下图所示：**

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVKAz63SQNpTHd9P9z2oXIcrYFOCKdYUQpxwpCXCxEqAgrkURPLgGmYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**二、绘制误差棒图形**

在 Book1 数据空白处，单击右键，选择 “Add New Column”，增加 2 列新的数据单元格 “C（Y）” 和 “D（Y）” 两列数据。

**如下图所示：**  

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV1iaYF08TSlkVYulSxQFialwibU15nib9Yh0jnM76tuDC1yzQHZ0xRWRYjA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVLAsUbBqXibpxAvUD9pPE7YSL9EYZrntWX5dP93Rgrib6SH1ujjvibicYpQ/640?wx_fmt=jpeg)

将计算得到的 X 轴数据，平均值，2 列标准偏差分别输入 origin 的 Book1 数据表中，然后选中标准偏差所在列的数据，右键单击，选择”set as“，将 “C（Y）列数据设置为 “ Xerror”，将 “D（Y）列数据设置为 “ Y error ” 将如下图所示：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV1yF4LhKMP7V9ibRSf7dxlgB8qQF4eLNLp1SoVkyOKdvntpgqf2JVyXQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVS5pfXxRrQIjtY4Rh4jZ2EW0UwlPxspadyGAGGqUhfy5JyoycopDLibA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV58ZeqhtiaUtzqZic4TB2pjIFqnuWONfUibficCdB5sgMWxYnyuZLCfDZ3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**三、绘制散点图**

选中数据，点击点击 “Plot”——“Symbol”。或者直接点击下面的工具栏选项。

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVBkuxFgib3kqvjLYT82DZqkIibtkxLFtzJJMVAicmyibibP86eZfjoiaqebPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)  

**各个选项的意思：**Scatter (散点图); Scatter Central (中心散点图); Y Error (Y 误差); XY Error (XY 误差) Vertical Drop Line (垂线)；Bubble (气泡)；Color Mapped (彩标)；Bubble + CM (气泡 + 彩标) 。

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVhYVuX3ibdngJEoQ3ecFtmu8rzZRm4cdmuLj9s6wfDibph7OdqXHvx8Xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

① 选择 Scatter，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVmQXW1qVrQRvJQmq6bR1ibl4Yjpq8KwEToN9iaOSJppVqQYK72aAyApOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

② 选择 Scatter Central，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVF7OBkic4VS807FkQqlPTuPRfNsACRwxAKQZbQ3r6AFHibZ96v2E0L7nQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

③ 选择 Vertical Drop Line ，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVFoqUz0ZzxfvuSwpIibwZRXdo7ydAWLiaAv1E5WrS8BDcqZK5vmM6HCdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

④ 选择 Bubble ，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVpnKcVtjicdgFDU5KL6vdCuDMysU92L3zHUCYfcdPJz5SbEgVdOEbJMg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

⑤ 选择 Color Mapped ，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVfoicOzjdbDnA9GQFbOX6Ok6Bsu7Bdzksj0zRnwvxcIck8SFcibr20dvA/640?wx_fmt=png)

⑥ 选择 Bubble + CM，做出的图形如下：

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVLiaTMguPsbLYzmNk8ZLrHkP4LXND8kjJnsQatkUREuSy2g22k4atvrA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**四、绘制垂线图**

**示例准备：**导入 Graphing 文件夹中的 AXES .DAT 文件数据。

① 选中 B 列。

② 单击菜单命令【Plot】→【Symbol】→【Vertical Drop Line】或 2D Graphs 工具栏【Vertical Drop Line】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVkCraBXytHXbnKibXPKwOy9SiaV9eYq1IoWFEULmMGAhw4KhNy2LLuKkA/640?wx_fmt=jpeg)

**五、绘制气泡图**

**数据要求：**用于作图的数据包含两个数值型 Y 列 (第 1 个 Y 列设定气泡纵向位置，第 2 个 Y 列用于设定气泡的大小)。

**示例准备：**导入 Curve Fitting 文件中的 Gaussian.dat 文件数据。

① 选中 B、C 两列。

② 单击菜单命令【Plot】→【Symbol】→【Bubble】或 2D Graphs 工具栏上的【Bubble】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVbnDLh3VubNLYHkCJ9EROMaruDDPZgjgxxvqNS2EMoibt51OiaDiaInEicQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**六、绘制彩色点图**

**数据要求：**用于作图的数据包含两个数值型 Y 列 (第 1 个 Y 列设定点的纵向位置，第 2 个 Y 列用于设定点的颜色)。

**示例准备：**导入 Curve Fitting 文件中的 Gaussian.dat 文件数据。

① 选中 B、C 两列。

② 单击菜单命令【Plot】→【Symbol】→【Color Mapped】或 2D Graphs 工具栏上的【Color Map】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVBWFwvX7WGKava1yhR0uxG8iakV59QLAZDljnyTkdD4dibmp7RHMnHSvQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**七、绘制彩色气泡图**

**数据要求：**用于作图的数据包含两个数值型 Y 列 (第 1 个 Y 列设定气泡的纵向位置，第 2 个 Y 列用于设定气泡的大小和颜色)。

**示例准备：**导入 Curve Fitting 文件中的 Gaussian.dat 文件数据。

① 选中 B、C 两列。

② 单击菜单命令【Plot】→【Symbol】→【Bubble+Color Mapped】或 2D Graphs 工具栏上的【Bubble+Color Mapped】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV1tBPHRicDhpVCEKaPnvJreejEmFrvmEa9gn8jFnKCTu7msQnSrtBAKg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**八、绘制点线图**

**数据要求：**用于作图的数据包含一个或多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 AXES.DAT 文件数据。

① 选中 B 列。

②单击菜单命令【Plot】→【Line+Symbol】→【Line+Symbol】或 2D Graphs 工具栏上的 Line+Symbol】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrT7uA1ia1SJ9LhiamzE4UKBKYHk1sSxXXeCYwAyAUEngH0ty0oafqwfAg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**九、绘制柱形图**

**数据要求：**用于作图的数据为数值型可包含一个或多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 AXES.DAT 文件数据。

① 选中 B 列。

②单击菜单命令【Plot】→【Column/Bar/Pie】→【Column】或 2D Graphs 工具栏的【Column】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrfOvtgickUbLCDv7yxyw7bn4fFuJPdmYHjzMBNwmzsQXziaaQIUKpI5ZA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十、绘制条形图**

**数据要求：**用于作图的数据为数值型可包含一个或多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 AXES.DAT 文件数据。

① 选中 B 列。

② 单击菜单命令【Plot】→【Column/Bar/Pie】→【Bar】或 2D Graphs 工具栏的【Bar】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVuiaD9CMklVGNPaiazdtvp4xu8uVPnbyWId6tajI3thiaF3R2fZMcpbo6g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十一、绘制浮动柱形图**

**数据要求：**用于作图的数据为数值型且包含多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 Group . DAT 文件数据。

① 选中所有的 Y 列。

② 单击菜单命令【Plot】→【Column/Bar/Pie】→【Floating Column】或 2D Graphs 工具栏的【Floating Column】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgruUwhHiaCUqHCycsVEiaxeOuInPrpRO5yHR1GIBibAR3SlqNfzViaibYNhhw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十二、绘制浮动条形图**

**数据要求：**用于作图的数据为数值型且包含多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 Group . DAT 文件数据。

① 选中所有的 Y 列。

② 单击菜单命令【Plot】→【Column/Bar/Pie】→【Floating Bar】或 2D Graphs 工具栏的【Floating Column】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrcagKasjPDZL9068n1wd2etMrtVJRyy8JDI3VnPhL6c8Z9V2mZE2D1g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十三、绘制饼图**

**数据要求：**用于作图的数据为数值型且包含多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 3D Pie Chart . dat 文件数据。

① 选中所有的 B 列。

② 单击菜单命令【Plot】→【Column/Bar/Pie】→【3D Color Pie Chart】。

![](https://mmbiz.qpic.cn/mmbiz_png/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV8LcHF0scZWsIiaMY8uibsicOqWdvH2ic5SKQPvRg6NjtDptC81Baeeia15A/640?wx_fmt=png)

**十四、绘制 Y 轴错位堆垒曲线图**

Y 轴错位堆垒曲线图将多条曲线在单个图层上从上到下堆垒并将其纵轴 (y 轴) 做适当的错位, 特别适合绘制多条包含多个峰的曲线图形。  

**数据要求：**包含多个数值型 Y 列。

**示例准备：**导入 Curve fitting 文件夹中的 Multiple Peaks.dat

① 选中所有的 Y 列。

② 单击菜单命令【Plot】→【Multi-Curve】→【Stack Lines by Y Offsets】或 2D Graphs 工具栏的【Stack Lines by Y Offsets】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhViclJfrIZicQv25Nb4gWric3mJ6GXm8HFpoYNEiasSndHJfD0mZrwDuFK2Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

本例如果绘制线图，则结果如下图所示：

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVQz7rO1DjKtFNiaWzSgexzuZd0WMicsszae4giaQIVy8f9R5rU8SW5VzsA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十五、绘制二维瀑布 (Waterfall) 图**

二维瀑布图将多条曲线在单个图层上按前后顺序排列并将它们向右上方做适当的错位，以便清晰地显示各曲线细微差别，特别适合绘制多条包含多个峰又极其相似的曲线图形。

**数据要求：**包含多个数值型 Y 列。

**示例准备：**导入 Graphing 文件夹中 Waterfall.dat 文件数据。

① 选中前 6 个 Y 列 (也可以选中所有 Y 列，这里只是为了更清晰显示)。

②单击菜单命令【Plot】→【Multi- Curve】→【Waterfall】或 2D Graphs 工具栏的【Waterfall】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVuVavZzOV19H11KZSGoMhgib6aibJiceGlHIfAGSkswjuBA89BeTLOjpBw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十六、绘制面积图**

**数据要求：**用于作图的数据包含一个或多个数值型 Y 列。

**示例准备：**导入 Graphing 文件夹中的 AXES.DAT 文件数据。

① 选中所有的 Y 列。

② 单击菜单命令【Plot】→【Area】→【Area】或 2D Graphs 工具栏【Area】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV5FKYCAjgz1oee0cHJn0lqngaxf1XR99HarXRBAiawglyzib8xVoIxTZQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十七、绘制堆垒面积 (Stock Area) 图**

**数据要求：**用于作图的数据为数值型且包含多个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 Group.dat 文件数据。

① 选中所有的 Y 列。

② 单击菜单命令

【Plot】→【Area】→【Stock Area】或 2D Graphs 工具栏的【Stock Area】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrZdyxR7w7JVTZVDNBQAcR6zeC4wzHTpGpEI2sgRzPIic2kBIpb0lDibQg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**十八、绘制填充面积 (Fill Area) 图**

**数据要求：**用于作图的数据为数值型且包含 2 个 Y 列。

**示例准备：**导入 Graphing 文件夹中的 Group.dat 文件数据。

① 选中 2 个的 Y 列。

② 单击菜单命令【Plot】→【Area】→【Fill Area】或 2D Graphs 工具栏的【Fill Area】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrzZWuqIJhDYPLFGRAMx8ptyrD5ibFf5niaoBqOe6yQzLQiaH85NM3zaw7w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

（特殊二维图形绘制）

**十九、绘制局部放大（Zoom）图**

**数据要求：**用于作图的数据包含一个或多个相同因变量的 Y 列。

**示例准备：**导入 Spectroscopy 文件夹中的 Peaks with Base.dat 文件数据。

① 选中 B 列。

② 单击菜单命令【Plot】→【Specialized】→【Zoom】或 2D Graphs 工具栏上的【Zoom】按钮，初步绘制结果如图所示。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgreia6Op8sGIX3Pd9lgLecjKedPMPoScibFPJH7R82X1QHJibvCiaBPl1Wicw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaEWhnIhkE0MZwrxoOlTCKgrEGJsibiaeEylU7FVVM5D2Cd1tuOicaSCVYvESc18OJnY0AKW6jEibFoiapQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

③ 将图层 1 中的放大区域选取框拖动到要放大的区域。

④ 单击放大区域选取框，通过 8 个黑色控制柄可以调整选取框的大小。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhVspeSxl9AE31hhUhWhDPBvXiabK86OPxUwlB3nGNliaVvSC4sbEicCOybQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

（含标签、误差棒图形绘制）

**二十、绘制含数据标签（Label）图**

如果需要在图形数据上加注标签 (如数据或其他标识等)，则需要绘制含数据标签图形。  

**数据要求：**用于作图的数据包含 Y 列和标签列。

**示例准备：**

① 导入 Graphing 文件夹中的 3D Pie Chart.dat 文件数据。

② 添加一个列，然后将 B 列数据复制到 C 列。

**绘图步骤：**

① 选中 C 列将其设置为标签列。

② 选中 B、C 两列，然后单击菜单命令【Plot】→【Column/Bar/Pie】→【Bar】或 2D Graphs 工具栏上的【Bar】按钮。

![](https://mmbiz.qpic.cn/mmbiz_jpg/1CrGx3vzAaHYwUq6QR0VZvOsR5BzYGhV48e9NeiangGvYicbsTxEvBBFLss6Wor4ZGYEfLlGEuDFy51VYibSntBbg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)