我们对一个算法进行评价，一般有 2 个重要依据-时间复杂度和空间复杂度。

## 2.1. 时间复杂度

| 名称 | 运行时间 T(n) | 时间举例 | 算法举例 |
| :--: | :-----------: | :------: | :------: |
| 常数 |     O(1)      |    3     |    -     |
| 线性 |     O(n)      |    n     | 操作数组 |
| 平方 |     O(n2)     |    n2    | 冒泡排序 |
| 对数 |   O(log(n))   |  log(n)  | 二分搜索 |

1. O(1)

算法所执行的时间不会随着 n 的大小变化,不管 O(几)，我们都称为 O(1)。

```js
const a = 1
```

2. O(n)

下面的 for 循环，会执行 N 次,不管 N 是几；都称做 O(n)。

```js
for (let i = 0; i < n; i++) {}
```

3. O(n2)

2 次循环，内层循环会执行 n\*n 次；也就是 n2，随着 n 的增大，复杂度会随着 n 的增大，复杂度会随着平方级增加。

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; i++) {}
}
```

4. O(log(n)) 对数复杂度

高中数学知识， y = loga x 叫做对数函数，a 是对数；y 就是以 a 为底 x 的对数。

```js
for (leti = 1; i <= n; i *= 2) {
  console.log(i)
}
```

我们可以看出，这个算法对元素进行跳跃式输出；就是数组从下标开始，每次都会乘以 2，直到 i 小于 n 的时候结束循环。

1\*2 -> 2\*2 -> 4\*2 -> 8\*2 ....

2^1 -> 2^2 -> 2^3 -> 2^4 ....

假设 i 在 i=i\*2 的规则递增了 x 次之后，i<=n 开始不成立；那么我们可以推算出下面一个数学方程式:

```js
2^x >= n
```

x 解出来，就是大于等于以 2 为底 n 的对数

```js
x>= log2 n
```

如果把上面的 i _= 2 改为 i _= 3 ，那么这段代码的时间复杂度就是 log3 n 。

注意涉及到对数的时间复杂度，底数和系数都是要被简化掉的。那么这里的 O(n) 就可以表示为：

```js
O(log(n))
```