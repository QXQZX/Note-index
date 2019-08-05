TensorFlow  是一种声明式数据编程 抽象



1.tensorflow的运算实质

​      tf = tensor + 计算图

2.tensor张量     某种相同数据类型的多维数组 

```python
tf.constant()  # 常量  不可改变的
tf.placeholder() # 占位符
tf.Variable(<initial-vlaue>, name=<optional-name>) # 变量

# -----------------------------------------------
data1 = tf.constant(2.5, dtype=tf.float64)  # 常量
data2 = tf.Variable(10, name='var')  # 变量

print(data1)
print(data2)
# 打印常量
sess = tf.Session()
print(sess.run(data1))

# 初始化变量  并打印变量
init = tf.global_variables_initializer()
sess.run(init)
print(sess.run(data2))
```

通过tf.Variable()创建的变量 和 张量一样，可以作为操作的输入和输出，不同之处在于：

* 张量的声明周期通常随依赖的计算完成而结束，内存也随之释放。

* 常量则常驻内存，在每一步训练时不断更新其值，以实现模型参数的更新。



张量是一种数据实体，几何代数中定义的张量是基于向量和矩阵的推广，通俗一点理解的话，我们可以将标量视为零阶张量，矢量视为一阶张量，那么矩阵就是二阶张量。数据立体是三阶张量。



啰嗦一下

如果一个物理量，在物体的某个位置上只是一个单值，那么就是普通的标量，比如密度。如果它在同一个位置、从不同的方向上看，有不同的值，而且这个数恰好可以用矩阵乘观察方向来算出来，就是张量。

> 张量的理解：**张量是有大小和多个方向的量。**这里的方向就是指张量的阶数。
>  空间维度n：一般我们使用3维空间，也可以是4维及以上维度。
>  张量阶数m：在固定的3维度空间再谈张量的阶数，阶数小于等于维数，即m<=n。
>  **下面区分这个量：张量的阶数（张量的方向数）和所在空间的维数（所在空间的方向数）的区别**
>  在二维空间里，二维二阶张量（平面应力张量）的每个方向都可以用二维空间两个方向表示。（区分2阶张量的2个方向，和二维空间的两个方向x，y）所以共有2^2=4个方向。
>  在三维空间里，三维二阶张量（空间应力张量）的每个方向都可以用三维空间三个方向表示。（区分2阶张量的2个方向，和三维空间的三个方向x，y、z）所以共有3^2=9个方向。





3.Op  操作   Graphs   计算图

session   所有的计算图放在session中执行



4.矩阵基础

```python
import tensorflow as tf

data1 = tf.constant([[1, 2], [3, 4], [5, 6]])
# data1 = tf.placeholder(tf.float32)
# data2 = tf.placeholder(tf.float32)
# dataAdd = tf.add(data1, data2)

with tf.Session() as sess:
    print(sess.run(data1))  # 打印整体
    print(sess.run(data1[0]))  # 打印行
    print(sess.run(data1[:, 0]))  # 打印列
    print(sess.run(data1[0, 0]))  # 打印某行某列的元素
    # print(sess.run(dataAdd, feed_dict={data1: 6, data2: 2}))
print("end!!")
```

矩阵的运算

```python
import tensorflow as tf

data1 = tf.constant([[1, 2, 1], [3, 4, 1], [5, 6, 1]])
data2 = tf.constant([[1, 1, 1], [1, 1, 1], [1, 1, 1]])
dataMul = tf.matmul(data1, data2) # 矩阵乘法
dataAdd = tf.add(data1, data2) # 矩阵加法

with tf.Session() as sess:
    print("--------------")
    print(sess.run(dataAdd))
    print(sess.run(dataMul))
    print(sess.run(tf.multiply(data1, data2))) # 对应位置元素相乘
    print(sess.run([dataAdd, dataMul]))
print("end!!")

```

矩阵的填充

````python
import tensorflow as tf

mat1 = tf.zeros([2, 3])  # all 0
mat2 = tf.ones([2, 3])  # all 1
mat3 = tf.fill([3, 2], 88)  # all 88
mat4 = tf.zeros_like(mat3)  # 以mat3为模板 填充0的矩阵
mat5 = tf.linspace(0.0, 1, 10)  # 0-1之间  均分的矩阵
mat6 = tf.random_uniform([2, 3], -1, 2)  # 2x3 的 -1 -- 2之间随机数的 矩阵

with tf.Session() as sess:
    print(sess.run(mat1))
    print(sess.run(mat2))
    print(sess.run(mat3))
    print(sess.run(mat4))
    print(sess.run(mat5))
    print(sess.run(mat6))

print("end!!")

````

