# GitLab

1. **Git、Github、Gitlab与Gitee之间的关系**

>  Git    是一种版本控制系统，是一个命令，是一种工具，有点像cmd(命令行工具)。
>
> Github  是一个基于git实现在线代码托管的仓库，向互联网开放，企业版要收钱。
>
> Gitee   即码云，是 oschina 免费给企业用的，不用自己搭建环境，可以建立自己的私有仓库。
>
> Gitlab  是一个基于Git实现的在线代码仓库托管软件，你可以用gitlab自己搭建一个类似于Github一样的系统，一般用于在企业内搭建git私服，要自己搭环境。
>
> Git-ce  是社区版，gitlab-ee是企业版，收费的。  

2. **注册**

   ![image-20210129181147097](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210129181147097.png)

3. **git命令**

   ![image-20210129193512086](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210129193512086.png)

*创建仓库命令*

>git init : 初始化仓库
>
>git clone : 拷贝一份远程仓库，即下载一个项目

*提交与修改*

> git add :添加文件到仓库
>
> git commit : 提交，将暂存区内容添加到仓库中

*远程操作*

> git remote : 远程仓库操作
>
> git fetch : 从远程获取代码库
>
> git pull :下载远程代码并合并
>
> git push : 上传远程代码并合并

*分支管理*

>git branch : 创建分支
>
>git checkout : 切换分支

4. **项目的上传、下载**

   * 上传：创建新项目添加新文件

     ![](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210225175413381.png)

     点击上传按钮（也可以创建文件夹等）

     ![image-20210225175602486](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210225175602486.png)

     文件上传成功

     ![image-20210225175656371](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210225175656371.png)

   * 下载：打开项目，点击下载按钮即可

     ![image-20210225180451007](C:\Users\智萍\AppData\Roaming\Typora\typora-user-images\image-20210225180451007.png)

     也可以点击复制按钮，直接复制源代码

     ```python
     import torch
     
     # batch_n表示一个批次输入数据的数量；同时。每个数据包含有数据特征input_data个
     # hidden_layer用于定义经过隐藏层后保留的数据特征个数，本网络只有一层隐藏层。output_data是输出的数据
     batch_n=100
     hidden_layer=100
     input_data=1000
     output_data=10
     
     #初始化权重
     x=torch.randn(batch_n,input_data)
     y=torch.randn(batch_n,output_data)
     
     w1=torch.randn(input_data,hidden_layer)
     w2=torch.randn(hidden_layer,output_data)
     
     #明确训练次数和学习效率
     epoch_n=20
     lenrning_rate=1e-6
     
     #梯度下降优化神经网络
     for epoch in range(epoch_n):
         h1=x.mm(w1)  #100*1000
         h1=h1.clamp(min=0)
         y_pred=h1.mm(w2)  #100*10
     
         loss=(y_pred-y).pow(2).sum()
         print("Epoch:{},loss:{:.4f}".format(epoch,loss))
     
         gray_y_pred=2*(y_pred-y)
         gray_w2=h1.t().mm(gray_y_pred)
     
         gray_h=gray_y_pred.clone()
         gray_h=gray_h.mm(w2.t())
         gray_h.clamp_(min=0)
         gray_w1=x.t().mm(gray_h)
     
         w1-=lenrning_rate*gray_w1
         w2-=lenrning_rate*gray_w2
     ```