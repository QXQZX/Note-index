数组操作

```python
# 创建数组
arr = np.array([
    [[1, 2, 3], [1, 2, 3]],
    [[1, 2, 3], [1, 2, 3]],
    [[1, 2, 3], [1, 2, 3]]
], dtype=int)
print(arr)
```



数组的基本属性

```python
print(type(a))  # numpy.ndarray类型
print(a.shape)  # 3*2*3维
print(a.dtype.name)  # 数据类型
print(a.size)  # 元素个数
print(a.itemsize)  # 每个元素占用的字节
print("维数 ：%d" % a.ndim)  # 维数
```



填充数组

```python
a1 = np.zeros((2, 3, 4), dtype=np.int16)  # 创建2*3*4全1三维数组
a2 = np.ones((2, 3, 4), dtype=np.int16)  # 创建2*3*4全1三维数组

print("zeros\n", a1)
print("ones\n", a2)
# print(np.zeros((2, 3), int), '\n', np.ones((2, 3), int))
```



数组内元素的改查

```python
print("--------改查-------")
a1[0, 2, 3] = 9
print(a1)
print(a1[0, 2, 3])

print("---------运算----------")
print(a2 * 3) # 对应相乘 + - / 同
print(a1 + a2) # 对应加
```

