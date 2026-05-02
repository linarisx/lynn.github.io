# 场景异步加载
## 场景同步加载
`SceneManager.LoadScene("GameScene");`
缺点：切换场景是会删除当前场景的所有对象，，并且去加载下一个场景的相关信息
如果当前场景对象过多或者下一个场景对象过多，会耗时卡顿

## 事件回调函数加载
```c#
AsyncOperation ao = SceneManager.LoadSceneAsync("Lesson20_Test");
ao.completed += (a) =>//切场景时被删的对象内存依然存在，相对于事件存了函数引用，在GC时这个事件不会被释放，所以才可以一直监听
{
    print("加载完成");
    //可以自己做地图编辑器，地图编辑器产生的配置文件动态的创建这些资源
};
```

## 协程异步加载（可以在加载中执行一些逻辑）
对象删除/失活，脚本失活协程不会继续执行
只要异步加载成功后面的代码都执行不了
所以要让该对象过场景不被删除
```c#
DontDestroyOnLoad(this.gameObject);
StartCoroutine(LoadScene("Lesson20_Test"));
```
```c#
IEnumerator LoadScene(string name)
{
    AsyncOperation ao = SceneManager.LoadSceneAsync(name);
    print("加载中");
    yield return ao;
    //过场景不被删除才能有下一步
    //加载完执行
    print("加载完");
}
```
```c#
IEnumerator LoadScene(string name)
{
 AsyncOperation ao = SceneManager.LoadSceneAsync(name);
    while (!ao.isDone)//没结束
    {
        print(ao.progress);//打印进度（0~1） 不准确 不常用
        yield return null;
        //做一些进度条
    }
    循环结束，场景加载结束，进度条顶满，隐藏进度条
}
//第二种 自定义进度条规则
yield return ao;
//场景加载结束 进度条20%
//加载怪物 40%
//动态加载 场景模型 100%
//隐藏进度条
```