# numpy

1. axis = 0 代表对竖直方向操作；

   axis = 1 代表对水平方向操作；
   
2. numpy  ndarray结构

   ```python
   numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
   ```

    ![image-20210205163521239](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210205163521239.png)

   array([1,2,3],[4,5,6])错误

   array([[1,2,3],[4,5,6]])正确

3. 数组属性

   ![image-20210204160618295](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210204160618295.png)

   ndarray.ndim用于返回数组的维数，等于秩；

   ndarray.shape表示数组的维度，返回一个元组。

   > a=numpy.array([[1,2,3,],[4,5,6]])
   >
   > print(a.shape)
   >
   > 输出：(2，3)     <!--2行3列-->
   >
   > 可以用来调整数组大小:
   >
   > a=numpy.array([[1,2,3,],[4,5,6]])
   >
   > a.shape=(3,2) <!--=很重要，不能丢掉-->
   >
   > print(a)
   >
   > 输出：[[1 2]
   >
   > ​			[3 4]
   >
   > ​			[5 6]]

4. 创建数组

   >1. numpy.empty 方法用来创建一个指定形状（shape）、数据类型（dtype）且未初始化的数组
   >
   >   ```
   >   numpy.empty(shape, dtype = float, order = 'C')
   >   ```
   >
   >   order有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。
   >
   >2. numpy.zeros() 创建指定大小的数组，数组元素以 0 来填充：
   >
   >3. numpy.ones()  创建指定形状的数组，数组元素以 1 来填充：
   >
   >4. 从已有的数组中创建数组
   >
   >   >* numpy.asarray 类似 numpy.array，  numpy.asarray(a, dtype = None, order = None)
   >   >
   >   >* numpy.asarray可以将**列表**、**元组**、**元组列表**转换为ndarray
   >   >
   >   >  ```python
   >   >  import numpy as np
   >   >  a=[1,2,3,4,5,6]
   >   >  b=np.asarray(a)
   >   >  print(b.shape)
   >   >  c=b.reshape(2,3)
   >   >  print(c)
   >   >  ```
   >   >
   >   >  输出：
   >   >
   >   >  ```
   >   >  (6,)
   >   >  [[1 2 3]
   >   >   [4 5 6]]
   >   >  ```
   >   >
   >   >  tip:下面这种情况会报错：'list' object has no attribute 'shape'。通过numpy.asaary转换则正常
   >   >
   >   >  ```
   >   >  import numpy as np
   >   >  a=[1,2,3,4,5,6]
   >   >  print(a.shape)
   >   >  ```
   >
   >5. 从数值范围创建数组
   >
   >   >```
   >   >numpy.arange(start, stop, step, dtype)
   >   >```
   >   >
   >   >![image-20210205175132063](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210205175132063.png)
   >   >
   >   >```
   >   >import numpy as np
   >   >x = np.arange(10,20,2)  
   >   >print (x)
   >   >```
   >   >
   >   >输出：
   >   >
   >   >```
   >   >[10  12  14  16  18]
   >   >```
   >   >
   >   >tip:numpy.linspace 、numpy.logspace 可以建立等差、等比数列，此处不做赘述。

5. 切片和索引

   ndarray对象的内容可以通过索引或切片来访问和修改。ndarray 数组可以基于 0 - n 的下标进行索引，切片对象可以通过内置的 slice 函数，并设置 start, stop 及 step 参数进行，从原数组中切割出一个新数组。*也可以通过冒号分隔切片参数 **start:stop:step** 来进行切片操作*

   ```python
   import numpy as np
   a = np.arange(10)
   s = slice(2,7,2) # 从索引 2 开始到索引 7 停止，间隔为2
   print (a[s])
   
   import numpy as np
   a = np.arange(10)  
   b = a[2:7:2]   # 从索引 2 开始到索引 7 停止，间隔为 2
   print(b)
   ```

   输出：

   ```
   [2  4  6]
   ```

   冒号 **:** 的解释：如果只放置一个参数，如 **[2]**，将返回与该索引相对应的单个元素。如果为 **[2:]**，表示从该索引开始以后的所有项都将被提取。如果使用了两个参数，如 **[2:7]**，那么则提取两个索引(不包括停止索引)之间的项

   ```python
   import numpy as np
   a = np.arange(10)
   print(a[2:])
   ```

   输出结果：

   ```
   [2  3  4  5  6  7  8  9]
   ```

6. 广播（Broadcast)

   广播(Broadcast)是 numpy 对不同形状(shape)的数组进行数值计算的方式， 对数组的算术运算通常在相应的元素上进行。如果两个数组 a 和 b 形状相同，即满足 **a.shape == b.shape**，那么 a*b 的结果就是 a 与 b 数组对应位相乘。这要求维数相同，且各维度的长度相同。例如：

   ```python
   import numpy as np 
   a = np.array([1,2,3,4]) 
   b = np.array([10,20,30,40]) 
   c = a * b 
   print (c)
   ```

   输出结果为：

   ```
   [ 10  40  90 160]
   ```

   * 当运算中的 2 个数组的形状不同时，numpy 将自动触发广播机制。如：

     ```python
     import numpy as np 
      
     a = np.array([[ 0, 0, 0],
                [10,10,10],
                [20,20,20],
                [30,30,30]])
     b = np.array([1,2,3])
     print(a + b)
     ```

     a,b兼容过程：

     ![image-20210207194613031](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210207194613031.png)

     输出结果：

     ```
     [[ 1  2  3]
      [11 12 13]
      [21 22 23]
      [31 32 33]]
     ```

7. 迭代数组

   numpy.nditer（） 提供了一种灵活访问一个或者多个数组元素的方式。还可以控制便利的顺序，如for x in np.nditer(a, order='C'):`C order，即是行序优先。

   ```python
   import numpy as np 
    
   a = np.arange(0,60,5) 
   a = a.reshape(3,4)  
   print ('原始数组是：')
   print (a)
   print ('\n')
   print ('以 C 风格顺序排序：')
   for x in np.nditer(a, order =  'C'):  
       print (x, end=", " )
   print ('\n')
   print ('以 F 风格顺序排序：')
   for x in np.nditer(a, order =  'F'):  
       print (x, end=", " )
   ```

   输出结果：

   ```
   原始数组是：
   [[ 0  5 10 15]
    [20 25 30 35]
    [40 45 50 55]]
   
   以 C 风格顺序排序：
   0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 
   
   以 F 风格顺序排序：
   0, 20, 40, 5, 25, 45, 10, 30, 50, 15, 35, 55,
   ```

   * 修改数组中元素的值

     nditer 对象有另一个可选参数 op_flags。 默认情况下，nditer 将视待迭代遍历的数组为只读对象（read-only），为了在遍历数组的同时，实现对数组元素值得修改，必须指定 read-write 或者 write-only 的模式。

     ```python
     import numpy as np
      
     a = np.arange(0,60,5) 
     a = a.reshape(3,4)  
     print ('原始数组是：')
     print (a)
     print ('\n')
     for x in np.nditer(a, op_flags=['readwrite']): 
         x[...]=2*x 
     print ('修改后的数组是：')
     print (a)
     ```

     输出结果：

     ````
     原始数组是：
     [[ 0  5 10 15]
      [20 25 30 35]
      [40 45 50 55]]
     
     修改后的数组是：
     [[  0  10  20  30]
      [ 40  50  60  70]
      [ 80  90 100 110]]
     ````

8. 数组操作

   * 修改数组形状：numpy.reshape 函数可以在不改变数据的条件下修改形状，格式如下： numpy.reshape(arr, newshape, order='C')

   * 翻转数组：numpy.transpose 函数用于对换数组的维度，格式如下：

     ```
     numpy.transpose(arr, axes)
     ```

     与数组转置相同（a.T）

   * 连接数组：numpy.concatenate

     numpy.concatenate 函数用于沿指定轴连接相同形状的两个或多个数组，格式如下：

     ```
     numpy.concatenate((a1, a2, ...), axis)
     ```

     ```python
     import numpy as np
      
     a = np.array([[1,2],[3,4]])
      
     print ('第一个数组：')
     print (a)
     print ('\n')
     b = np.array([[5,6],[7,8]])
      
     print ('第二个数组：')
     print (b)
     print ('\n')
     # 两个数组的维度相同
      
     print ('沿轴 0 连接两个数组：')
     print (np.concatenate((a,b)))
     print ('\n')
      
     print ('沿轴 1 连接两个数组：')
     print (np.concatenate((a,b),axis = 1))
     ```

     输出结果为：

     ```
     第一个数组：
     [[1 2]
      [3 4]]
     
     第二个数组：
     [[5 6]
      [7 8]]
     
     沿轴 0 连接两个数组：
     [[1 2]
      [3 4]
      [5 6]
      [7 8]]
     
     沿轴 1 连接两个数组：
     [[1 2 5 6]
      [3 4 7 8]]
     ```

   * 分割数组：numpy.split(arr, indices_or_sections, axis)函数沿特定的轴将数组分割为子数组。其中， indices_or_sections：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置。

   * 数组元素的添加与删除

     ![image-20210224172325573](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210224172325573.png)

9. 位运算

   ![image-20210224172605240](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210224172605240.png)

10. 数学函数：包括三角函数，算术运算的函数，复数处理函数等。
    * numpy.around() 函数返回指定数字的四舍五入值。
    * numpy.floor() 返回小于或者等于指定表达式的最大整数，即向下取整。
    * numpy.ceil() 返回大于或者等于指定表达式的最小整数，即向上取整。

11. 算术函数：加减乘除: **add()**，**subtract()**，**multiply()** 和 **divide()**，还有
    * numpy.reciprocal() 取倒
    * numpy.power() 函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组中相应元素的幂。
    * numpy.mod() 计算输入数组中相应元素的相除后的余数。

12. 统计函数：

    * numpy.amin(arr,axis) 、numpy.amax() 用于计算数组中的元素沿指定轴的最小值、最大值。
    * numpy.ptp(arr,axis)函数计算数组中元素最大值与最小值的差（最大值 - 最小值）
    * numpy.median() 函数用于计算数组 a 中元素的中位数（中值）
    * numpy.mean() 函数返回数组中元素的算术平均值。
    * numpy.average() 函数根据在另一个数组中给出的各自的权重计算数组中元素的加权平均值。
    * 标准差：np.std([1,2,3,4])
    * 方差：np.var([1,2,3,4])

13. 排序、条件筛选

    ![image-20210224181041539](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210224181041539.png)

    * numpy.sort(a, axis, kind, order ）函数返回输入数组的排序副本。其中，kind: 默认为'quicksort'（快速排序）；order:如果数组包含字段，则是要排序的字段。

14. 副本和视图

    **视图一般发生在：**

    - 1、numpy 的切片操作返回原数据的视图。
    - 2、调用 ndarray 的 view() 函数产生一个视图。

    **副本一般发生在：**

    - Python 序列的切片操作，调用deepCopy()函数。
    - 调用 ndarray 的 copy() 函数产生一个副本。

15. 矩阵库（Matrix）

    NumPy 中包含了一个矩阵库 numpy.matlib，该模块中的函数返回的是一个矩阵，而不是 ndarray 对象。

16. 线性代数

    NumPy 提供了线性代数函数库 **linalg**，该库包含了线性代数所需的所有功能

    ![image-20210224184303139](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210224184303139.png)

17. IO

    Numpy 为ndarray引入一个简单的文件格式：npy，读写磁盘上的文本数据或二进制数据。常用的 IO 函数有：

    - load() 和 save() 函数是读写文件数组数据的两个主要函数，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npy 的文件中。

      ```
      numpy.save(file, arr)
      ```

      ```python
      import numpy as np 
       
      a = np.array([1,2,3,4,5]) 
       
      # 保存到 outfile.npy 文件上
      np.save('outfile.npy',a) 
       
      # 保存到 outfile2.npy 文件上，如果文件路径末尾没有扩展名 .npy，该扩展名会被自动加上
      np.save('outfile2',a)
      ```

      

    - savez() 函数用于将多个数组写入文件，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npz 的文件中。如上
    - loadtxt() 和 savetxt() 函数处理正常的文本文件(.txt 等)

18. Matplotlib

    Matplotlib 是 Python 的绘图库。 它可与 NumPy 一起使用，提供了一种有效的 MatLab 开源替代方案。 它也可以和图形工具包一起使用，如 PyQt 和 wxPython。

    ```python
    import numpy as np 
    from matplotlib import pyplot as plt 
     
    x = np.arange(1,11) 
    y =  2  * x +  5 
    plt.title("Matplotlib demo") 
    plt.xlabel("x axis caption") 
    plt.ylabel("y axis caption") 
    plt.plot(x,y) 
    plt.show()
    ```

    其中，np.arange() 函数创建 x 轴上的值。y 轴上的对应值存储在另一个数组对象 y 中。 这些值使用 matplotlib 软件包的 pyplot 子模块的 plot() 函数绘制，图形由 show() 函数显示。

    ![image-20210224191402535](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210224191402535.png)

还可以通过库里的函数画出点图，正弦波、直方图等等。