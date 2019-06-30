# CSS的flex布局看完这篇你就懂了

我们之前已经学过一些布局模型，比如说浮动，绝对定位等等，但是这些布局方式一是不够简洁，而是使用的范围确实是太窄了。

flex模型拥有比较多的属性，来设置多样的布局方式，接下来我们就详细介绍各种属性对布局的改变，最后再对属性做一个汇总

先看一下flex的基本模型，如下图所示：

![](https://img-blog.csdn.net/20180812130511152?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

container父容器里有三个子元素flex-item。当给父容器设置display:flex;直接子元素就有布局模型了，上图中还有主轴和纵轴分别是布局的一个方向，后面的属性会详细说到。

接下来就先从flex-container属性开始介绍

## 1.flex-container

### **1.1 flex-direction(主轴方向)**

​     **flex-direction:row;**   （布局为一行，从start开始排）

![img](https://img-blog.csdn.net/201808121322217?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**flex-direction:row-reverse;**    (布局为一行，从end开始排)

![img](https://img-blog.csdn.net/20180812132312292?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**flex-direction:column;**    (布局为一列，从start开始排)

![img](https://img-blog.csdn.net/20180812132643507?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**flex-direction:column-reverse;**   (布局为一列，从end开始排)

![img](https://img-blog.csdn.net/20180812132829702?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 

## 1.2  flex-wrap(一条轴线排不下如何换行)

flex-wrap：nowrap; (不换行，在一行显示，即使子元素的宽度或者高度大于父元素的宽度或者高度，也在一行显示)

![img](https://img-blog.csdn.net/2018081213341664?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**flex-wrap:wrap; (内容超过后换行)**

![img](https://img-blog.csdn.net/2018081213354031?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**flex-wrap:wrap-reverse; (换行后有两条轴线，reverse就是把轴线排列的顺序倒置过来)**

![img](https://img-blog.csdn.net/20180812133752554?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **1.3 justify-content （主轴对齐方式）**

**justify-content:flex-start; (start侧对齐，左对齐)**

![img](https://img-blog.csdn.net/20180812134126868?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**justify-content:flex-end;   (end侧对齐，右对齐)**

![img](https://img-blog.csdn.net/20180812134637582?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**justify-content:center  （中心对齐）**

![img](https://img-blog.csdn.net/20180812134706205?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**justify-content:space-between；（左右两侧没有间距，中间间距相同）**

![img](https://img-blog.csdn.net/20180812134932932?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**justify-content:space-around；    （左右两侧的间距为中间间距的一半）**

![img](https://img-blog.csdn.net/2018081213495396?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **1.4  align-items（交叉轴对齐方式）**

**align-items:stretch;   (拉伸)**

![img](https://img-blog.csdn.net/20180812135359262?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-items:flex-start;   （start侧开始，上对齐）**

![img](https://img-blog.csdn.net/20180812135544490?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-items:flex-end;    （end侧开始，下对齐）**

![img](https://img-blog.csdn.net/20180812135602317?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-items:center;         (中心对齐)**

![img](https://img-blog.csdn.net/20180812135616569?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-items:baseline;   （基线对齐）**

![img](https://img-blog.csdn.net/20180812135632904?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **1.5 align-content  （多根轴线对齐方式）**

**align-content :stretch;   (拉伸)**

![img](https://img-blog.csdn.net/201808121401521?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-content :flex-start;   (start侧开始，上对齐)**

![img](https://img-blog.csdn.net/20180812140207155?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-content :flex-end;   （end侧开始，下对齐）**

![img](https://img-blog.csdn.net/20180812140222896?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-content :center;       (中心对齐)**

![img](https://img-blog.csdn.net/20180812140235334?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-content:space-between;  （上下没有间距，中间各子元素间距相同）**
![img](https://img-blog.csdn.net/20180812140252361?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**align-content:space-around;     (上下间距之和等于中间各个间距)**

![img](https://img-blog.csdn.net/20180812140306635?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 

## 2.flex-item相关属性

flex-item中的5个属性分别是order, flex-grow, flex-shrink, flex-basis, flex-self (分别对应下面的0,0,1,auto,auto初始顺序是123)

![img](https://img-blog.csdn.net/20180812141541391?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **2.1  order(排列顺序)**

![img](https://img-blog.csdn.net/2018081214172579?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **2.2 flex-grow（放大比例，剩余空间怎么分配,如下图所示，剩余空间的分配比例是1:2:1）**

![img](https://img-blog.csdn.net/20180812142455936?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 2.3 flex-shrink （缩小比例，超出空间怎么压缩）

![img](https://img-blog.csdn.net/20180812194518393?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **2.4 flex-basis  (item所占主轴空间，优先级高于width)**

![img](https://img-blog.csdn.net/20180812194551661?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### **2.5  align-self  (对齐方式，取值和align相同，覆盖align-items)**

![img](https://img-blog.csdn.net/20180812194628761?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FsbGVueWh5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 

## 3.属性总结

flex-container的属性有flex-direction,  flex-wrap,  justify-content,  align-items,  align-content

fl**ex-direction(主轴方向):**  1) row（布局为一行，从start开始排）

​                                        2) row-reverse(布局为一行，从end开始排)

​                                        3) column(布局为一列，从start开始排)

​                                        4) column-reverse(布局为一列，从end开始排)

**flex-wrap(一条轴线排不下如何换行)：**1) nowarp (不换行，在一行显示)

​                                                            2) wrap(内容超过后换行)

​                                                            3) warp-reverse(换行后有两条轴线，reverse就是把轴线排列的顺序倒置过来)

**justify-content(主轴对齐方式)：**1) flex-start (start侧对齐，左对齐)

​                                                  2) flex-end(end侧对齐，右对齐)

​                                                  3) center(中心对齐)

​                                                  4) space-between(左右两侧没有间距，中间间距相同)

​                                                  5) justify-content:space-around（左右两侧的间距为中间间距的一半）

**align-items(交叉轴对齐方式)：**  1）align-items:stretch;   (拉伸)

​                                                  2）align-items:flex-start（start侧开始，上对齐）

​                                                  3）align-items:flex-end（end侧开始，下对齐）

​                                                  4）align-content :center (中心对齐)

​                                                  5）align-items:baseline（基线对齐）

**align-content(多根轴线对齐方式)：**  1）align-content :stretch  (拉伸)

​                                                       2）align-content :flex-start  (start侧开始，上对齐)

​                                                       3）align-content :flex-end（end侧开始，下对齐）

​                                                       4）align-content :center  (中心对齐)

​                                                       5）align-content:space-between（上下没有间距，中间各子元素间距相同）

​                                                       6）align-content:space-around  (上下间距之和等于中间各个间距)

flex-item相关属性有order，flex-grow，flex-shrink，lex-basis，align-self

**order(排列顺序)**

**flex-grow（放大比例，剩余空间怎么分配,如下图所示，剩余空间的分配比例是1:2:1）**

**flex-shrink （缩小比例，超出空间怎么压缩）**

**flex-basis  (item所占主轴空间，优先级高于width)**

**align-self  (对齐方式，覆盖align-items)**

 

只要搞懂每个属性的功能，自己在调试演示一下，flex布局应该没有什么问题！！

调试的网站推荐  [CSS的flex布局调试](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/)

这些属性综合起来，真的是可以做出超级多的布局！！