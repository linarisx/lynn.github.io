# Resources的同步与异步加载
多个resources是可以的，打包时自动合并成一个
## 同步加载
### 同步加载的不同方式
`Object obj = Resources.Load("Cube");`
`TextAsset ta = Resources.Load<TextAsset>("TextAsset/Test");`
`AudioClip ad = Resources.Load("Audio/LaserShoot") as AudioClip;`
`Sprite tx =  Resources.Load("Texture/2026_4.9", typeof(Sprite)) as Sprite;`

### 支持格式

1. 预设体对象-GameObject
2. 音效文件-AudioClip
3. 文本文件-TextAsset
4. 图片文件-Texture

### 文本类型
```c#
TextAsset ta = Resources.Load<TextAsset>("TextAsset/Test");
print(ta.text);
print(ta.bytes);//字节数据组
```

### 音效文件
```c#
AudioClip ad = Resources.Load("Audio/LaserShoot") as AudioClip;
audioS.clip = ad;
audioS.Play();
```

### 加载同名的所有资源
```c#
Object[] objs = Resources.LoadAll("Texture/Test");
foreach(Object item in objs)
{
    if(item is Sprite)
    {

    }
    else if(item is TextAsset)
    {

    }
}
```
## 异步加载
### 解决的问题
硬盘把数据读取到内存中是需要计算的，如果加载的资源过大会导致卡顿
一步加载中，通过后台新开线程同步加载，解决卡顿

## 通过后台线程异步加载
ResourceRequest的父类有个监听事件
```c#
ResourceRequest rq = Resources.LoadAsync<Texture>("Texture/2026_4.9");
rq.completed += IsOver;//如果加载完成，就在内部invoke执行isOver
//rq.asset 一定要加载完才使用不要在这里！
print(Time.frameCount);//帧

void IsOver(AsyncOperation ac)
{
    print("加载完成");
    tex  = (ac as ResourceRequest).asset as Texture;
    print(Time.frameCount);//帧
}
```
## 通过协程异步加载
```c#
StartCoroutine(Load());
IEnumerator Load()
{
   ResourceRequest rq = Resources.LoadAsync<Texture>("Texture/2026_4.9");
   print(Time.frameCount);
   yield return rq;//unity自己会判断rq是在异步加载  WaitForSeconds基类和ResourceRequest基类的基类是一样的

   //自己判断如果加载完就执行后面的内容
   tex = rq.asset as Texture;
   print(Time.frameCount);//至少一帧才能使用资源  
}
```
```c#
IEnumerator Load()
{
   ResourceRequest rq = Resources.LoadAsync<Texture>("Texture/2026_4.9");
   while (!rq.isDone)//没有加载完毕进入循环
     {
         print(rq.progress);//加载进度0~1
         yield return null;//下一帧执行
     }
     tex = rq.asset as Texture;//加载结束再使用来绘制
}
```