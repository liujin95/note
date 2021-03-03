# pandas

1. 数据结构

   pandas常用数据结构有：Series、DataFrame两种。Panel很少使用。

   Series:

   >表示一维数据，可以简单理解为一个向量，但是不同于向量的是，Series会自动为这一维数据创建行索引。数据采取各种形式，如：`ndarray`，`list`，`constants`
   >
   >```python
   >import pandas as pd
   >obj = pd.Series(['1','2','3','4'])
   >```
   >
   >![image-20210227100022279](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227100022279.png)

   DataFrame：

   >dataframe是一种表格型的数据结构，既有行索引index，也有列索引columns。其实可以简单把dataframe理解为一张数据表。
   >
   >```python
   >import pandas as pd
   >#方法一 字典生成
   >d = {'col1': [1, 2], 'col2': [3, 4]}
   >df = pd.DataFrame(data=d)
   >#方法二 文件生成
   >df = pd.read_excel("demo.xlsx")
   >#方法三 创建一个空DataFrame
   >df = pd.DataFrame(columns=["name","age","gender"])
   >```
   >
   >![image-20210227105959844](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227105959844.png)
   >
   >![image-20210227110045227](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227110045227.png)

2. 导入excel数据

   ![image-20210227110629581](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227110629581.png)

   * ```python
     import pandas as pd
     df = pd.read_excel("g:\\python\\sample\\pandas\\10.xlsx")
     ```

   * ```python
     import pandas as pd
     excelFile = pd.ExcelFile("g:\\python\\sample\\pandas\\10.xlsx")
     # 此方法 多用于从一个Excel文件 中获取多个sheet操作 较为方便，只需要修改sheet_name 
     df = pd.read(excelFile,sheet_name="sheet1")
     #sheetList = excelFile.sheet_names 获取当前excel文件里的sheet 名 列表。["sheet1","sheet2"]
     ```

3. 输出excel列表

   ![image-20210227111545799](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227111545799.png)

   * 方法一

     ```python
     import pandas as pd
     # 将df 的数据生成一个excel文件，默认sheet_name为sheet1,也可以根据需要自定义。
     df = DataFrame({"name":["小张","小李"],"age":[18,20]}
     df.to_excle(file_path) #file_path 文件存放路径+文件名
     ```

   * 方法二：一个表中要生成多个sheet时使用

     ```python
     import pandas as pd
     
     df1 = DataFrame({"name":["小张","小李"],"age":[18,20]}
     df2 = DataFrame({"goods_name":["土豆","茄子"],"price":[1.3,3,5]})
     
     excelWriter = pd.ExcelWriter(filePath) #file_path 文件存放路径+文件名
     df1.to_excel(excelWriter,sheet_name="用户信息"）#生成一个用户信息sheet
     df2.to_excel(excelWriter,sheet_name="商品信息") #生成一个商品信息sheet 
     
     excelWrite.save()
     excelWrite.close()
     ```

4. 数据概览

   DataFrame提供了两个好用的数据概览函数

   * info()  :展示数据概要信息

     ```python
     import pandas as pd
     df = pd.read_excel("C:\\Users\\智萍\\Desktop\\附件3：2021年学生拟发展对象登记表.xls")
     print(df.info())
     ```

     ![image-20210227113047442](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227113047442.png)

   * describe()  :展示统计信息（包括数据量、均值、方差、min、max等）

     ```python
     import pandas as pd
     
     df = pd.read_excel("C:\\Users\\智萍\\Desktop\\附件3：2021年学生拟发展对象登记表.xls")
     print(df.describe())
     print(df.describe(include="all"))
     ```

     ![image-20210227113446993](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210227113446993.png)输出结果为：(第一个输出为不带参数的结果，第二是加入参数include="all"的结果，可对比查看区别。

5. 数据清洗

   ![image-20210228141859791](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228141859791.png)

   * dropna()

     >![image-20210228141946623](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228141946623.png)
     >
     >```python
     >import pandas as pd
     >import numpy as np
     >
     >df = pd.DataFrame({"name": ['Alfred', 'Batman', 'Catwoman'],"toy": [np.nan, 'Batmobile', 'Bullwhip'],"born": [pd.NaT, pd.Timestamp("1940-04-25"),pd.NaT]})
     >
     >print "当前数据"
     >print df
     >print "删除含有NA值的行"
     >print df.dropna()
     >print "删除含有NA值的列"
     >print df.dropna(axis=1)
     >print "删除所有例都含有NA值的行"
     >print df.dropna(how='all')
     >print "删除含有2个NA值的行"
     >print df.dropna(thresh=2)
     >print "删除列['name', 'born']的行"
     >print df.dropna(subset=['name', 'born'])
     >```
     >
     >输出结果：
     >
     >![image-20210228142529022](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228142529022.png)

   * replace()

     >![image-20210228142625962](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228142625962.png)code:
     >
     >```python
     >#--coding:GBK
     >import pandas as pd
     >df = pd.DataFrame({'A': [0, 1, 2, 3, 4],
     >                   'B': [5, 6, 7, 8, 9],
     >                   'C': ['a', 'b', 'c', 'd', 'e']})
     >print "原始数据为"
     >print df
     >print "将数据中的0替换为5"
     >print df.replace(0, 5)
     >print "将数据中的0，1，2，3 替换为4"
     >print df.replace([0, 1, 2, 3], 4)
     >print "将数据中的0，1，2，3 替换为 4,3,2,1"
     >print df.replace([0, 1, 2, 3], [4, 3, 2, 1])
     >print "将数据中的 0替换为10，1替换为100"
     >print df.replace({0: 10, 1: 100})
     >print "将A列的0，B列的5替换为100"
     >print df.replace({'A': 0, 'B': 5}, 100)
     >print "将A列中的0，替换为100，4替换为400"
     >print df.replace({'A': {0: 100, 4: 400}})
     >```

   * apply()

     >![image-20210228143050164](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228143050164.png)
     >
     >code:
     >
     >```python
     >import pandas as pd
     >import numpy as np
     >
     >print df
     >print "函数执行结果"
     >print df.apply(np.sqrt)
     >```

   * fillna()

     >code:
     >
     >```
     >import pandas as pd
     >import numpy as np
     >df = pd.DataFrame([[np.nan, 2, np.nan, 0],
     >                   [3, 4, np.nan, 1],
     >                   [np.nan, np.nan, np.nan, 5],
     >                   [np.nan, 3, np.nan, 4]],
     >                  columns=list('ABCD'))
     >print "原始数据"
     >print df
     >print "将nan数据替换为0"
     >print df.fillna(0)
     >print "将A列的nan替换为0，B列替换为1，C列替换为2，D列替换为3"
     >print df.fillna(value={'A': 0, 'B': 1, 'C': 2, 'D': 3})
     >```
     >
     >![image-20210228143528691](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228143528691.png)

6. 数据选择

   * ![image-20210228143755963](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228143755963.png)

   >例如在下表中获取指定的信息：
   >
   >![image-20210228143842695](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228143842695.png)code:
   >
   >```python
   >import pandas as pd
   >
   >#设置第一行，第0列（餐厅名称） 分别为列索引和行索引
   >df = pd.read_excel("g:\python\sample\pandas\8.xlsx",header=1,index_col=0) 
   >#通过行索引【食膳美】的信息
   >print df.loc[u"食美"]
   >#获取【食膳美】餐厅的 u'排餐次数', u'排餐总量'信息
   >print df.loc[u"食美",[u'排餐次数', u'排餐总量']]
   >#获取列【u'排餐总量'】的所有信息
   >print df.loc[:,u'排餐总量']
   >#查看餐厅【食膳美，渝是乎】的排餐总量信息
   >print df.loc[[u"食美",u"乎家"],[u'排餐总量',u'平均每日排餐数']]
   >
   >```
   >
   >```python
   >import pandas as pd
   >
   >#设置第一行，第0列（餐厅名称） 分别为列索引和行索引
   >df = pd.read_excel("g:\python\sample\pandas\8.xlsx",header=1,index_col=0)
   >#通过行索引【食膳美】的信息
   >print df.iloc[8]
   >#获取【食膳美】餐厅的 u'排餐次数', u'排餐总量'信息
   >print df.iloc[8,[2, 3]]
   >#获取列【u'排餐总量'】的所有信息
   >print df.iloc[:,2]
   >#查看餐厅【食膳美，渝是乎】的排餐总量信息
   >print df.iloc[[8,9],[2,3]]
   >```

   * 2.根据条件查询数据

   >![image-20210228144205699](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144205699.png)code:
   >
   >```python
   >#--coding:GBK
   >import pandas as pd
   >
   >#设置第一行，第0列（餐厅名称） 分别为列索引和行索引
   >df = pd.read_excel("g:\python\sample\pandas\8.xlsx",header=1,index_col=0) 
   ># 此处用 &（并且）|（或者）！（取反） 进行逻辑运算
   >dfResult = df[(df[u"排餐总量"]>500) & (df[u"餐厅类别"].isin([u'中式炒菜']))]
   >print dfResult
   >```

8. 数据排序

   ![image-20210228144330739](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144330739.png)

   ```python
   import pandas as pd
   df = pd.read_excel("g:\python\sample\pandas\8.xlsx",header=1)
   
   dfSort = df.sort_values(by=[u"排餐总量"],ascending=False)
   #排餐前3家店
   print dfSort.head(3)
   #排餐后3家店
   print dfSort.tail(3)
   ```

9. 数据分组

   ![image-20210228144506040](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144506040.png)

   比如下例：

   ```python
   import pandas as pd
   
   #读取Excel成绩单数据
   df = pd.read_excel("g:\python\sample\pandas\8.xlsx",sheet_name="Sheet2")
   
   #根据姓名字进行成绩汇总
   #方式一
   dfsum1 = df.groupby(by=[u"姓名"]).sum()
   #输出汇总结果
   print dfsum1
   # 方式二 通过agg函数 
   dfsum2 = df.groupby(by=[u"姓名"]).agg({u"分数":sum})
   print dfsum2
   #agg() 可以指定进行运算的字段名，且可以对一个字段同时进行多个运算。
   #统计 考生的总成绩，最高分、最低分
   print df.groupby(by=[u"姓名"]).agg({u"分数":[sum,max,min]})
   ```

   ![image-20210228144636573](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144636573.png)

   agg支持一列多种运算，同时也可以支持多列实现不同的运算。`agg({col:max,col2:sum,col3:[sum,min,max]})`

10. 数据透视

    ![image-20210228144911535](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144911535.png)

    如下例：

    ![image-20210228144949726](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228144949726.png)

    ```python
    #--coding:GBK
    import pandas as pd
    
    df = pd.read_excel("G:\python\sample\pandas\pivot_data.xlsx",header=1)
    #分析不同车型在1，2月的销售性况以及各车型1月份，2月份的销售总量
    pivData=pd.pivot_table(df,index="car_name",columns=["month"],values=["sales_performance"],aggfunc="sum",margins=True)
    
    pivData.to_excel("G:\pivData.xlsx")
    ```

11. 数据合并

    * 数据的合并在pandas中分为横向合并与纵向合并。
      横向合并用merge()函数 等同于Excel的vlookup,SQL的join
      纵向合并用concat()函数，将多个数据纵向合并到一起。

    * ![image-20210228145157655](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145157655.png)

      >如下例：一个用户数据表，一个订单数据表。将两个表进行合并为一张新含有用户信息及订单信息的新表
      >
      >![image-20210228145255793](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145255793.png)
      >
      >code:
      >
      >```python
      >import pandas as pd
      >
      >dfUser = pd.read_excel("G:\python\sample\pandas\user.xlsx")
      >dfOrder = pd.read_excel("G:\python\sample\pandas\order.xlsx")
      >dfNew = pd.merge(dfuser,dfOrder)
      >dfNew.to_excel("G:\python\sample\pandas\user-order.xlsx")
      >```
      >
      >print：
      >
      >![image-20210228145422321](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145422321.png)
      >
      >只将 用户名、商品名称、商品价格 列进行合并:
      >
      >`dfNew = pd.merge(dfUser[[u"用户ID",u"用户名"]],dfOrder[[u"商品名称",u"商品价格",u"用户ID"]])`

    * ![image-20210228145643193](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145643193.png)

      比如将两个表的数据合在一起：

      ![image-20210228145848750](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145848750.png)

      code:

      ```python
      import pandas as pd
      
      df2018 = pd.read_excel("G:\\python\\sample\\pandas\\2018.xlsx")
      df2019 = pd.read_excel("G:\\python\\sample\\pandas\\2019.xlsx")
      dfnew =pd.concat([df2018,df2019],ignore_index=True)
      
      dfnew.to_excel("G:\\python\\sample\\pandas\\20189.xlsx")
      
      ```

      print:

      ![image-20210228145927366](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145927366.png)

12. 数据可视化

    ![image-20210228145958398](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228145958398.png)

    案例：分析某网站的用户注册趋势

    ![image-20210228150035873](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228150035873.png)

    code:

    ```python
    #--coding:GBK
    import pandas as pd
    import matplotlib.pyplot as plt
    
    df = pd.read_excel("G:\\python\\sample\\pandas\\userRe.xlsx")
    print df
    #解决中文乱码问题
    plt.rcParams['font.sans-serif']=['SimHei']
    #设置图表类型为柱图，横轴为日期，图表标题
    df.plot(kind="bar",title=u"用户注册分析",x=u"日期")
    plt.show()#显示图表
    ```

    print:

    ![image-20210228150143743](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210228150143743.png)

