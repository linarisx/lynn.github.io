# Transform父子关系
## 获取父对象
获取父对象
`print(this.transform.parent.name);`
移除父对象
`this.transform.parent = null;`
更换父对象 不用置空也可以更换父对象
`this.transform.parent = GameObject.Find("Father2").transform;`

通过API
移除父对象
`this.transform.SetParent(null);`
设置父对象
`this.transform.SetParent(GameObject.Find("Father2").transform);`

**参数一：父对象
参数二：是否保留世界坐标**
true: 和原本位置一样 并且还是会和父对象进行参考计算, 缩放位置会随父对象变化
false: 不再和父对象进行计算了，世界坐标是啥样的进来也是啥样的，参考对象变成父对象，该物体可能会放大缩小或者位置发生改变
`this.transform.SetParent(GameObject.Find("Father3").transform, false);`


## 抛妻弃子
断绝父子关系 没办法断绝子孙关系
`this.transform.DetachChildren();`

## 获取子对象
找子对象
按名字查找
失活的也可以找到 GameObject的不能找到失活的
`print(this.transform.Find("Cube (1)").name);`
只能找儿子不能找孙子
`print(this.transform.Find("GameObject").name);`

遍历儿子
获得儿子的数量(包括失活的儿子，不包括孙子)
`print(this.transform.childCount);`
通过索引获得儿子 返回值transform可以得到位置信息
this.transform.GetChild(0);//溢出报错
```
for (int i = 0; i < this.transform.childCount; i++)
{
    print(this.transform.GetChild(i).name);
}
```

## 儿子的操作
判断父对象是谁
判断Son是不是我的儿子
失活的也可以
### 一个对象判断自己是不是另一个对象的儿子
```
if (son.IsChildOf(this.transform))
{
    print(son + "是我的儿子");
}
```

### 得到自己作为的编号
`print(son.GetSiblingIndex());`
### 把自己设置成第一个儿子
`son.SetAsFirstSibling();`
###把自己设置成最后一个儿子
`son.SetAsLastSibling();`
### 把自己设置成指定儿子
```
son.SetSiblingIndex(15);//就算填的溢出也不报错 会变成最后一个编号
son.SetSiblingIndex(-1);//超出范围都是最后一个编号
```