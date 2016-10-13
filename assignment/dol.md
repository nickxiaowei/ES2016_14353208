## DOL ##

### 改完的*.dot截图 ###

* **example2.dot**

![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/lab3_picture1.jpg)

* **example1.dot**

![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/lab3_picture2.png)


### 具体如何修改的解释 ###

* **example2**
目的：修改example2，让3个square模块变成2个
方法：修改xml中的iterator：
将原本的：

   >  ＜variable value="3" name="N"/ ＞

   将迭代次数N的value从3改成2：

   >  ＜variable value="2" name="N"/ ＞
  
   修改完之后，运行example2：
   
   ![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/lab3_picture3.png)

   可以看到，运行结果从i的八次方变成了i的四次方。


* **example1**
目的：修改example1，使其输出3次方数
方法：修改squre.c处理函数，原本读入输入端信号i后对i做了平方：

   ```
if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
   ```

   改成3次方即可：

   ```
if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
   ```

   修改完之后，运行example1：

   ![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/lab3_picture4.png)

   可以看到，运行结果从i的平方变成了i的三次方。

### 实验感想 ###
这次的实验可能是因为是第一次实验吧，所以很简单，第一个任务只要改一个数字第二个任务也只是加了个*i,没有什么难度，希望以后的实验也这么简单就好了。