# 最小单位GameObject
## GameObject的成员变量
### 名字
`print(this.gameObject.name);`
### 改名
this.gameObject.name = "Lesson4新改的名字";
`print(this.gameObject.name);`
### 是否激活
`print(this.gameObject.activeSelf);`
### 是否静态
`print(this.gameObject.isStatic);`
### 层级layer
`print(this.gameObject.layer);`
### 标签tag
`print(this.gameObject.tag);`

```c#
print(this.transform.position);
print(this.gameObject.transform.rotation);
```
this.gameObject.transform == this.transform

# GameObject的静态方法
## 创建几何体
```c#
GameObject obj = GameObject.CreatePrimitive(PrimitiveType.Cube);
obj.name = "小林的正方体";
```
可以通过obj.GetComponent获取正方体的脚本信息

## 查找场景中的一个对象(效率低，会遍历所有场景)
都没办法找到失活的对象
如果有同名的无法找到指定的对象，只能随机找
### 根据名字查找
```c#
GameObject obj2 = GameObject.Find("小林的正方体");
if (obj2 != null)
{
    print("找到了" + obj2.name);
}
else
{
    print("没找到");
}
```
### 通过Tag来查找对象
如果有两个对象都是Player标签，无法找到指定的对象，只能随机找
```c#
GameObject obj3 = GameObject.FindWithTag("Player");
//GameObject.FindGameObjectsWithTag("Player"); //跟上面的一模一样
if (obj3 != null)
{
    print("找到了palyer标签的" + obj3.name);
}
else
{
    print("没找到");
}
```
### 查找多个对象 只能通过Tag
只能找到激活对象
```c#
GameObject[] objs = GameObject.FindGameObjectsWithTag("Player");
print("找到tag为Palyer的对象个数" + objs.Length);
```
Unity中的Object是Unity自定义类,也是继承万物之父object，命名空间UnityEngine
万物之父object，命名空间system

### 找到场景中的脚本
先遍历了对象再从各个对象中找有没有这个脚本，效率低
```c#
Lesson4 o = GameObject.FindObjectOfType<Lesson4>();
print(o.gameObject.name);
```

## 克隆对象
对象继承MonoBehaviour，不用写GameObject，这个方法在Object里
`GameObject obj5 = GameObject.Instantiate(myObject);`
之后再来操作这个克隆对象

## 删除对象 
继承MonoBehaviour，不用写GameObject，这个方法在Object里
先打一个删除标签，下一帧才删除，避免卡顿
`GameObject.Destroy(deleteObj);`
延迟五秒删除
`GameObject.Destroy(obj5, 5);`
删除自己这个脚本
`GameObject.Destroy(this);`
马上在这一帧就删除了
`GameObject.DestroyImmediate();`


### 过场景不被删除
默认切换场景删除场景中的对象
一般情况下是自己这个对象
继承MonoBehaviour，不用写GameObject，这个方法在Object里
`GameObject.DontDestroyOnLoad(this.gameObject);`

# GameObject的成员方法
## 创建空物体
```c#
GameObject obj6 = new GameObject();
GameObject obj7 = new GameObject("小林创建的空物体的名字");
GameObject obj8 = new GameObject("小林创建的空物体，顺便加了俩脚本", typeof(Lesson2), typeof(Lesson3));
```

## 为对象添加脚本
```c#
Lesson2 les1 = obj6.AddComponent(typeof(Lesson2)) as Lesson2;
Lesson2 les2 = obj6.AddComponent<Lesson2>();
```
//之后再进行一些处理

## 得到脚本的方法，和之前继承mono的一样

## 标签比较
```c#
if (this.gameObject.CompareTag("Player"))
{
    print("对象的标签是 Player");
}
if (this.gameObject.tag =="Player")
{
    print("对象的标签是 Player");
}
```

## 让对象失活
```c#
obj6.SetActive(false);
obj7.SetActive(false);
obj8.SetActive(false);
```

## 执行自己身上所有脚本的该方法
### 效率低每个脚本都找 广播行为
`this.gameObject.SendMessage("TestFun");`
### 让自己和自己的子对象执行
`this.gameObject.BroadcastMessage("函数名");`
### 让自己和自己的父对象执行
`this.gameObject.SendMessageUpwards("函数名");`