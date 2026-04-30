# Mathf
## 基础常见使用
### 绝对值
`print(Mathf.Abs(-1));`

### 向上取整
`print(Mathf.CeilToInt(1.3f));`

### 向下取整
`print((int)1.3f);`
`print(Mathf.FloorToInt(1.3f));`

### clamp 夹紧 
比最小还小就输出最小，比最大还大就输出最大，其他就是正常值
（值，最小值，最大值）
`print(Mathf.Clamp(10, 11, 20));`

### 最大值
`print(Mathf.Max(12, 6, 5));`
### 最小值
`print(Mathf.Min(13, 7, 4));`

### 四舍五入
`print(Mathf.RoundToInt(1.3f));`
`print(Mathf.RoundToInt(1.6f));`

### 平方根，开根号
开不出整数会自动算小数
`print(Mathf.Sqrt(64));`
`print(Mathf.Sqrt(10));`

### 判断是否是2的次方
返回true/false
`print(Mathf.IsPowerOfTwo(10));`

### 判断正负数
正数返回1，负数返回-1
`print(Mathf.Sign(10));`
`print(Mathf.Sign(-10));`

## 线性差值的运算
Lerp 线性插值运算 一直计算
result = Mathf.Lerp(start, end, t);
result = start + (end - start) * t
t为插值系数（0~1）

```c#
float start = 0;
float result = 0;
float time = 0;
void Update()
{   
   start = Mathf.Lerp(start, 10, Time.deltaTime);//一直趋近10，start变大

   time += Time.deltaTime;
   result = Mathf.Lerp(start, 10, time);//一直匀速上涨到10，因为t一直变大
}
```
### 其他
如果使用匀速移动到目标点，需要一直更新开始位置、目标位置、时间