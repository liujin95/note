# Matplotlib

1. matplotlib简介

   Matplotlib 能够创建多数类型的图表，如条形图，散点图，条形图，饼图，堆叠图，3D 图和地图图表。

   惯例地，我们将pyplot导入为plt，即

   ```python
   import  matplotlib.pyplot  as  plt
   ```

   使用  plt.show()  将图标显示到屏幕上。

2. 绘图基础

   2.1  plot()函数

   >plot(x,y,format_string,**kwargs)是pyplot绘图的基础函数，其中各参数含义如下:
   >
   >* x:X轴数据，列表或数组(单条曲线可选)
   >
   >* y:Y轴数据，列表或数组
   >
   >* format_string:控制曲线的格式字符串，用于填充曲线信息(可选)，包含**颜色，风格，标记**三种字符，含义如下：
   >
   >![image-20210226150833348](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226150833348.png)
   >
   >* **kwargs:更多的曲线参数(x,y,format_string)
   >
   >如下例：
   >
   >```python
   >import matplotlib.pyplot as plt
   >import numpy as np
   >
   >x = np.arange(10)
   >plt.plot(x,x*2,'b-.',x,x*3,'r*',x,x*4,'y-^',x,x*5,'k-.*')  # 1:蓝色实线点标记，2:红色`*`标记，3:黄色虚线上三角标记，4：黑色点画线*标记
   >plt.show()
   >```
   >
   >显示：
   >
   >![image-20210226152425862](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226152425862.png)

   2.2  中文显示

   >`pyplot`标签本身并不支持中文字体，可以通过在label中添加`fontproperties`属性修改字体，`fontsize`设置字体大小，但首先需要保证有对应字体，如果提示没有，则需下载并进行安装。
   >
   >```python
   >plt.xlabel('我是横轴',fontproperties='Simhei',fontsize=10)
   >```

   2.2  文本显示

   >除了绘图之外，我们还需要给图像做一定的说明文字信息，一般包括如下几个文本显示函数：
   >
   >![image-20210226152903664](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226152903664.png)
   >
   >举个详细的例子：
   >
   >```python
   >import numpy as np
   >import matplotlib.pyplot as plt
   >
   >x = np.arange(0,10,0.1)
   >plt.xlabel('我是横轴',fontproperties='Simhei',fontsize=15,color='r')
   >plt.ylabel('我是纵轴',fontproperties='Simhei',fontsize=15,color='b')
   >plt.title('正弦曲线$y=sin(2\pi x)$',fontproperties='Simhei',fontsize=12)
   >plt.text(5,1,'(5,1)',fontsize=12)  # 在(5,1)处添加文本信息
   >plt.annotate('看这里',fontproperties='Simhei',xy=(3,-1),xytext=(4,-1.5),
   >             arrowprops={'facecolor':'k','shrink':0.1,'width':1.5})  # 设置指示箭头
   >plt.ylim(-2,2)  # 设置y轴上下限
   >
   >plt.plot(x,np.sin(2*np.pi*x),'b-.')
   >plt.grid(True)  # 显示网格
   >plt.show()
   >```
   >
   >得到图表：
   >
   >![image-20210226154408423](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226154408423.png)

3. 常用图表绘制：

   3.1  直方图：适用数值对比。

   *函数定义*

   > `plt.hist(x,bins,color)`
   >
   > x : (n,) array or sequence of (n,) arrays
   >
   > 这个参数是指定每个bin(箱子)分布的数据,对应x轴
   >
   > bins : integer or array_like, optional
   >
   > 这个参数指定bin(箱子)的个数,也就是总共有几条条状图

   *代码及效果*

   >```python
   >import matplotlib.pyplot as plt
   >import numpy as np
   >
   >x = np.random.randint(0,50,50)  
   >bins = np.arange(0,51,10)  # 设置直方图分布区间[0-50],10为间距
   >
   >plt.hist(x,bins,color="darkgreen")
   >plt.title('学生成绩分布图',fontproperties='SimHei', fontsize=15)
   >plt.xlabel('成绩',fontproperties='SimHei', fontsize=15)
   >plt.ylabel('人数',fontproperties='SimHei', fontsize=15)
   >plt.xlim(-10,60)  # 设置x轴区间范围，空出一些
   >
   >plt.show()
   >```
   >
   >效果图：
   >
   >![image-20210226155233358](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226155233358.png)
   >
   >* 正态分布直方图
   >
   >  ```python
   >  import numpy as np
   >  import matplotlib.pyplot as plt
   >  
   >  # Fixing random state for reproducibility
   >  np.random.seed(20200306)
   >  
   >  mu, sigma = 50, 20  # 均值和方差
   >  x = mu + sigma * np.random.randn(10000)
   >  
   >  # the histogram of the data
   >  plt.hist(x, 50, density=True, facecolor='g', alpha=0.75)
   >  
   >  plt.xlabel('Smarts')
   >  plt.ylabel('Probability')
   >  plt.title('Histogram of IQ')
   >  plt.text(25, .023, r'$\mu=50,\ \sigma=20$')
   >  plt.xlim(-40, 160)
   >  plt.ylim(0, 0.03)
   >  plt.grid(True)
   >  plt.show()
   >  
   >  ```
   >
   >  效果图：
   >
   >  ![image-20210226162835792](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226162835792.png)

   3.2  饼状图:使用比例区分

   *函数定义*

   >Matplotlib中绘制饼图的函数是`plt.pie()`,完整的函数定义和参数如下：
   >
   >```python
   >def pie(x, explode=None, labels=None, colors=None, autopct=None,
   >pctdistance=0.6, shadow=False, labeldistance=1.1, startangle=None,
   >radius=None, counterclock=True, wedgeprops=None, textprops=None,
   >center=(0, 0), frame=False, rotatelabels=False, hold=None, data=None)
   >```
   >
   >![image-20210226163343557](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226163343557.png)

   *代码及效果*

   >```python
   >import matplotlib.pyplot as plt
   >
   >plt.rcParams['font.sans-serif'] = ['SimHei'] 
   >labels = ('语文','数学','英语','物理')
   >x = [20,30,25,25]  # 按100比例分配
   >explode = (0.2,0.1,0,0)  # 距离中心距离
   >
   >plt.pie(x,explode=explode,labels=labels,autopct='%.2f%%',  # 添加了百分号
   >shadow = False, startangle=45)
   >
   >#添加图例
   >plt.axis('equal')  # 摆正
   >plt.legend(loc="upper right", fontsize = 15, bbox_to_anchor=(1.1,1.2),borderaxespad=0.3)  
   ># loc :  'upper right' 位于右上角
   ># bbox_to_anchor: 上边距
   ># borderaxespad: 图例的内边距
   >plt.show()
   >```
   >
   >效果图：
   >
   >![image-20210226163826155](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226163826155.png)

   3.3  散点图：适用数据点分布

   散点图本身也是数据点的集合，因此可以采用`plot`函数或`plt.scatter`实现。当散点图中可能有两类或以上不同类型的点，我们需要绘制出来并进行标注对比，这时候采用`plt.scatter()`函数更方便。

   *`plt.scatter()`函数定义*

   >```python
   >def scatter(x, y, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None,
   >alpha=None, linewidths=None, verts=None, edgecolors=None, hold=None, data=None, **kwargs)
   >```
   >
   >![image-20210226164402495](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226164402495.png)

   *代码及效果*

   >**scatter()实现**
   >
   >```python
   >import matplotlib.pyplot as plt
   >import numpy as np
   >
   >x = np.random.randn(100)
   >y = np.random.randn(100)
   >
   >plt.scatter(x,y, alpha=0.4)
   >plt.title('plt.scatter')
   >
   >plt.show()
   >```
   >
   >效果图：
   >
   >![image-20210226164926132](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226164926132.png)
   >
   >当有多个点集并进行对比时：
   >
   >```python
   >import matplotlib.pyplot as plt
   >import numpy as np
   >
   >x = np.random.randn(100)
   >y = np.random.randn(100)
   >colors = np.random.rand(100) 
   >
   >plt.scatter(x,y,c = colors, alpha=0.4)
   >plt.title('plt.scatter')
   >plt.colorbar()
   >
   >plt.show()
   >```
   >
   >效果图：
   >
   >![image-20210226165205928](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226165205928.png)
   >
   >**plot实现**
   >
   >```python
   >import matplotlib.pyplot as plt
   >import numpy as np
   >
   >plt.plot(np.random.randint(0,100,50),np.random.randint(0,100,50),'o')
   >plt.title('Scatter')
   >
   >plt.show()
   >```
   >
   >效果图：
   >
   >![image-20210226164608717](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210226164608717.png)

   

