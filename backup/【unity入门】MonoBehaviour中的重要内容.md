# MonoBehaviour中的重要内容
## 获取依附的GameObject信息
### 名字
       print(this.gameObject.name);
### 位置信息
       **位置** print(this.transform.position);
       **角度** print(this.transform.eulerAngles);
       **缩放** print(this.transform.lossyScale);
（this.gameObject.transform和this.transform一样）
### 获取脚本是否激活
     this.enabled = false;
### 得到其他脚本对象的信息
     print(OtherLesson.gameObject.name);
     print(OtherLesson.transform.position);
     ......

## 关于获取脚本
只要能得到场景中其他对象或者其他对象的脚本，就能得到它的所有信息
## 获得自己同个GameObject的不同脚本 
只能得单个，不能同个脚本有多个
获取失败返回空
### 历史替换
     Lesson3_Test t = this.GetComponent("Lesson3_Test") as Lesson3_Test;
     if (t != null)    print(t);
### 通过Type获得
     t = this.GetComponent(typeof(Lesson3_Test)) as Lesson3_Test;
     if (t != null)    print(t);
### 根据泛型获取
     t = this.GetComponent<Lesson3_Test>();
     if (t != null)    print(t);  

### 获得自己多个脚本
一般不会再同个对象中挂几个相同脚本
```c#
     Lesson3[] array = this.GetComponents<Lesson3>();
     print(array.Length);
     List<Lesson3> list = new List<Lesson3>();
     this.GetComponents<Lesson3>(list);
     print(list.Count);
```
  
### 得到子对象的脚本（默认也会找自己身上有没有该脚本）
括号参数默认false 检测gameobject子对象不失活的 true失活也会找
**1.找单个子对象**
```c#
     t = this.GetComponentInChildren<Lesson3_Test>(false);
     print(t);
```
 **2.多个子对象**
```c#
     Lesson3_Test[] arr = this.GetComponentsInChildren<Lesson3_Test>();
     print(arr.Length);
     List<Lesson3_Test> lis = new List<Lesson3_Test>();
     GetComponentsInChildren<Lesson3_Test>(true, lis);
     print(lis.Count);
```
### 得到父对象的脚本(默认找自己的)
括号没有参数，如果父对象失活子对象也失活，就没办法执行脚本
**1.单个父对象**
```c#
     t = this.GetComponentInParent<Lesson3_Test>();
     print(t);
```
**2.多个父对象(所有父类都找)**
```c#
     arr = this.GetComponentsInParent<Lesson3_Test>();
     print(arr.Length);
```
### 尝试获取单个脚本 找到true
正常没找到报空 更安全
```c#
     Lesson3_Test test;
     if(this.TryGetComponent<Lesson3_Test>(out test) {  }
```